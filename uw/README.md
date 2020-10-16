## Alignment 1

### Info

- **Extracted:** Niche University of Washington (https://www.niche.com/colleges/university-of-washington/)
- **Existing Schema:** http://mappings.dbpedia.org/server/ontology/classes/University
- **Existing Data:** DBPedia (http://dbpedia.org/page/University_of_Washington)

### Details

1. Values that match a property in the existing data

   - Exact
     - `rdfs:label`
     - `dbo:city`
   - Similar
     - `dbo:athletics`
       - Niche: "NCAA Division I-FBS"
       - DBPedia: "dbr:NCAA_Division_1"
     - `dbo:numberOfUndergraduateStudents`
       - Niche: 29496 full-time + 2603 part-time
       - DBPedia: 31099
   - Source-dependent semantics/data
     - `abstract`
     - Niche's ratings for different criteria

2. Values with attributes in the schema, but not in existing data

   - `address`

3. Semantics unaccounted for in the schema

   - "4 year"
   - `website`/`homepage`
   - "Athletic Conference"
   - "Branch Campuses"
   - Admissions related: "Acceptance Rate", "Application Deadline", "SAT Range",
     "ACT Range", "Application Fee", "SAT/ACT", "High School GPA", "Early Decision/
     Early Action", "Application Website", "Students also applied to ..."
   - Finances related: "Net Price", "Average Total Aid Awarded",
     "Students Receiving Financial Aid"
   - "Student Faculty Ratio"
   - Degree Programs: "Evening Degree Programs", online degree info, most popular
     majors
   - Student body stats: "Undergrads Over 25", "Pell Grant", "Varsity Athletes"
   - Employment related: "Median Earnings 6 Years After Graduation", "Employed
     2 Years After Graduation"
   - "Graduation Rate"
