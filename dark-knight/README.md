## Alignment 1

### Info

- **Extracted:** IMDB Dark Knight (https://www.imdb.com/title/tt0468569/?ref_=nv_sr_srsg_0)
- **Existing Schema:** https://schema.org/Movie
- **Existing Data:** Rotten Tomatoes' (RT) Dark Knight schema.org markup

### Details

1. Values that match a property in the existing data

   - Exact
     - `name`
     - `contentRating`
     - `director`
     - `author`
   - Similar
     - `productionCompany`
       - IMDB: "Warner Bros.", "Legendary Entertainment"
       - RT: "Warner Bros. Pictures/Legendary"
     - `actors`
       - IMDB: doesn't display all actors on main page
     - `characters`; some exactly match, some discrepancies, e.g.:
       - IMDB: "Bruce Wayne"; RT: "Batman/Bruce Wayne"
       - IMDB: "Joker"; RT: "The Joker"
       - IMDB: "Rachel"; RT: "Rachel Dawes"
   - Source-dependent semantics/data
     - `rating`
       - IMDB: out of 10.0
       - Rotten Tomatoes: out of 100
     - `genre`
       - IMDB: Action, Crime, Drama, Thriller
       - RT: Action & Adventure, Drama, Science Fiction & Fantasy
     - `abstract`
     - `reviews`

2. Values with attributes in the schema, but not in existing data

   - `duration`
     - IMDB: "2h 32min", "152 min"
   - `datePublished`
     - IMDB: 18 July 2008
     - RT: `null`
   - `releasedEvent`
     - IMDB: 18 July 2008, USA
   - `keywords`
     - IMDB: "dc comics, joker, psychopath, clown, criminal mastermind"
   - `inLanguage`
   - `alternateName` and/or `alternativeHeadline`
     - IMDB: "Batman Begins 2"
   - `locationCreated`
     - IMDB: "Times Square", "Causeway Bay", "Hong Kong"

3. Semantics unaccounted for in the schema

   - `author`: whether author wrote story or screenplay or both
   - `actor` + `character`: pairing of which actor played which character
   - Taglines
   - Storyline: Possibly mapped to `abstract`?
   - Financials: Budget, Box Office Gross
   - Technicals: Sound Mix, Color, Aspect Ratio

## Alignment 2

### Info

- **Extracted:** IMDB Dark Knight (https://www.imdb.com/title/tt0468569/?ref_=nv_sr_srsg_0)
- **Existing Schema:** http://mappings.dbpedia.org/server/ontology/classes/Film
- **Existing Data:** http://dbpedia.org/page/The_Dark_Knight_(film)

### Details

1. Values that match a property in the existing data

   - Exact
     - `dbo:Work/runtime`
     - `dbo:director`
   - Similar
     - `dbo:budget`
       - IMDB: \$185,000,000
       - DBPedia: 1.85E8
     - `dbo:gross`
       - IMDB: \$1,005,456,758
       - DBPedia: 1.005E9
     - `dbo:runtime` (distinct from `dbo:Work/runtime`)
       - IMDB: 2h 32min, 152 min
       - DBPedia: 9120 (in seconds)
   - Source-dependent semantics/data
     - `abstract`

2. Values with attributes in the schema, but not in existing data

   - `owl:Thing/releaseDate`
   - `dbo:Work/releaseLocation`
   - `owl:Thing/genre`
   - `writer`
   - `starring`
   - `originalLanguage`
   - `alternativeTitle`
   - `filmColourType`

3. Semantics unaccounted for in the schema

   - `owl:Thing/releaseDate` + `dbo:Work/releaseLocation`: pairing
   - `writer`: whether author wrote story or screenplay or both
   - Character roles
   - Plot Keywords
   - MPAA rating
   - Reviews
   - Alternate languages
   - Time/location-specific financials: Opening Weekend, Gross USA
   - Technicals: Sound Mix, Aspect Ratio
