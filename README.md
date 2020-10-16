# Ontology Alignment Testing

## Challenges

### Topic/Root Entity

1. **Entity Class**: The user can either manually select that the topic entity
   of the pages are `Movie` or `Film` by searching for it in the ontology schema,
   or the system can attempt to automatically infer it via distant supervision with
   existing overlapping data.
2. **Entity Linking**: After we establish the topic entity class, individual
   entities in the extracted data need to be matched with existing data:

   - For example, the entity label may be `The Dark Knight`, but the existing
     ontology data may have the label `The Dark Knight (film)`. Another example
     is `A Star is Born`, for which there is a 1976 and 2018 version.

### Related Entities

For entities and literal values `E_R` that are properties of the topic entity `E_T`,
such that `(E_T, R, E_R)` or `(E_R, R, E_T)` are triples for some relation `R`, the
goal is to either match `E_R` to existing entities in the KB or to create new
ones, and to match `R` to existing relations in the KB or create new ones if
needed.

There are a few cases to consider:

1. **Existing/extracted data matches**: The extracted data (roughly) matches the
   triple already in the KB. It may be possible in these cases to detect the relation
   `R` automatically using the similarity between the existing and extracted
   data, as well as by comparing the extracted page "relation labels" (if they
   exist) to the schema. There are many cases where values don't exactly match,
   with no simple automatic solution:

   - _Naming discrepancies_: IMDB lists the production company of `The Dark Knight`
     as the array `["Warner Bros.", "Legendary Entertainment"]`, while RT uses the
     string `Warner Bros. Pictures/Legendary`. Similarly, IMDB lists Christian Bale's
     character as `Bruce Wayne`, while RT lists it as `Batman/Bruce Wayne`.

   - _Unit differences_: IMDB lists the runtime in two formats: `2h 32min` and
     `152 min`, whereas DBPedia has two relations for runtime - one in minutes:
     `152`, and the other in seconds: `9120`.

   - _Precision differences_: The gross box office is listed precisely as
     `$1,005,456,758` for IMDB while DBPedia lists it as `1.85E8`.

2. **Extracted values not in KB**: These are cases where the extracted `E_R`
   values have corresponding attributes in the existing schema, but the existing
   KB does not contain `E_R`.

   - If the data exists in the KB for _other_ entities, one possibility is to
     use the global similarity of the extracted values to the existing values
     to infer `R` even for pages that there is no existing data for.

   - If we can guess the class of `E_R`, we can narrow the options of `R` from
     the existing schema and present them to the user.

   - If "relation labels" exist from the extracted data, we can also use the
     similarity to relations in the schema to rank `R` candidates.

   - Even with all these heuristics, the user will likely need to be consulted.

3. **Source-specific semantics/data**: In some cases, the existing data and new
   data come from different sources and each must be independently preserved.

   - _Source-specific semantics_: IMDb and RT use different taxonomies for
     `genre`. For example, one lists `Action` and `Thriller`, the other lists
     `Action & Adventure`, and we should keep both as they are don't necessarily
     mean the same thing. Another example is the rating system, which is out of
     10.0 for IMDb but out of 100 (and aggregated from critics) for RT.

   - _Source-specific data_: We should not attempt to merge and match a review
     on IMDb with a review on RT. They are distinct by nature.

   - Another dimension to consider could be time - the same source might report
     two different values depending on extraction time - such as Amazon product
     prices.

   - There is no way to automatically detect such situations, unless metadata
     indicates so (e.g. mark such relations in the schema as source-specific).

4. **Missing semantics in the schema**: The user/system must realize when
   the schema doesn't account for the data.

   - Is there a way to identify this automatically?

   - _Complete miss_: Need to add new relation to schema.

   - _Partial miss_: An example is where the IMDb website pairs an actor and
     character, a release date with release location, and a writer with the
     content they contributed. There are a few sub-cases for this:

     - Both relations exist in the schema, but the pairing relationship does
       not. (How does this generalize when n >= 2?)
     - Only one of the relations currently exist in the schema.
