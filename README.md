# Ontology Alignment Testing

## Challenges

### Topic/Root Entity

1. **Entity Type**: The user can either manually select that the topic entity
   of the pages are `Movie` or `Film` by searching for it in the ontology schema,
   or the system can attempt to automatically infer it via distant supervision with
   existing overlapping data.
2. **Entity Linking**: If the entity label is `The Dark Knight` but the
   existing ontology data has the label `The Dark Knight (film)`, how do we link
   the two? Moreover, how do we decide that an entity doesn't exist in the KB and
   we should create a new one?

### Related Entities

For entities and literal values `E_R` that are properties of the topic entity `E_T`,
such that `(E_T, R, E_R)` or `(E_R, R, E_T)` are triples for some relation `R`, the
goal is to either match `E_R` to existing entities in the KB or to create new
ones, and to match `R` to existing relations in the KB or create new ones if
needed.

There are a few cases to consider:

1. **Existing/extracted data matches**: The extracted data matches the triple
   already in the KB. It may be possible in this case (and the next), to detect the
   relation R automatically using the similarity between the existing and extracted
   data, as well as by comparing the extracted page "relation labels" (if they
   exist) to the schema.

   - **Value/Entity Linking**: IMDB may list the production company as an
     array: `["Warner Bros.", "Legendary Entertainment"]`, while the existing data
     lists a single value: `Warner Bros. Pictures/Legendary`. We can either leave
     both entities separately, or attempt to resolve to a common representation.
     Another example is the character played by Christian Bale in The Dark Knight,
     which is listed as `Bruce Wayne` on IMDB but `Batman/Bruce Wayne` elsewhere.

2. **Extracted values not in KB**: These are cases where the extracted values
   have corresponding attributes in the existing schema, but the existing KB does
   not contain the actual data. If the data exists in the KB for _other_ entities,
   one possibility is to use the global similarity of the extracted values to the
   existing values and infer even for pages that there is no existing data for.
   Otherwise, the closest we can get is to attempt some type inference using some
   heuristics and suggest them to the user who makes the final decision.
3. **Source-dependent semantics/data**: In some cases, the existing data and
   new data come from different sources and each must be independently preserved.
   For example, we should make no effort to resolve/match ratings or user reviews
   on IMDb and Rotten Tomatoes, as they are meant to be separate sources. The two
   sources may also use different taxonomies for `genre`, and have different
   movie summaries that are all equally valid. Perhaps this is a meta-property of
   relations/properties on the schema.
4. **Missing semantics in the schema**: In these cases, first, the user/system
   must realize the schema doesn't account for the data. Then, new relations
   need to be added to the schema, or existing ones need to be modified. There
   are some different "transformation" cases that need to be accounted for when
   modifying.
