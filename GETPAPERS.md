# specs for `getpapers`

Initially ONLY used for `crossref` and `epmc`. Other APIs (including EPMC) are much or and rarer.

## arguments

```
  -h, --help              output usage information                  NO
  -V, --version           output the version number                 NO
  -q, --query <query>     Search query (required for EPMC)          EMPC or CROSSREF
  -o, --outdir <path>     Output directory (required - will be created if not found)   MANDATORY == CPROJECT
  --api <name>            API to search [arxiv, eupmc, ieee] (default: eupmc)  REQUIRED FOR CROSSREF; DEFAULTS TO EPMC
  -x, --xml               Download fulltext XMLs if available       EPMC (possibly for QUICKSCRAPE on CROSSREF)
  -p, --pdf               Download fulltext PDFs if available       EPMC (possibly for QUICKSCRAPE on CROSSREF)
  -s, --supp              Download supplementary files if available EPMC (possibly for QUICKSCRAPE on CROSSREF)
  -l, --loglevel <level>  amount of information to log (silent, verbose, info*, data, warn, error, or debug) NO
  -a, --all               search all papers, not just open access   EPMC (CROSSREF does this by default)
  --filter                construct CROSSREF query - NOT for EPMC
```
## crossref

The `crossref` api is at :
https://github.com/CrossRef/rest-api-doc/blob/master/rest_api.md
Relatively stable for 2.5 months. Will refer to this doc in the discussion (by named sections).

There is much of this that we do not currently use (or use rarely). 

### works
`/works` (i.e. articles, etc.) will be the only type supported.

**Combining resource components** is not supported in the GUI.

**Parameters** only supports `filter` 

**Field Queries** not supported

** Sorting** not supported

**Facet Counts** not supported

**Filters** are supported, see section

**Dot filters** not used.


### filters

**prefix** and **member** represent publishers and might become useful when backed by a list of common values.

**from-pub-date** and **until-pub-date** . ideally this should be set with calendar pulldowns and check that `until` is not ealiers than `from`

**issn** very useful and should be repeatable. Backed by list of common journals (especially for subject-related queries).

### rows, offset, cursors, sample

Not used.

## EPMC

The EPMC API is at: 
https://europepmc.org/RestfulWebService
Most of the functionality we require is already in `getpapers`

see https://europepmc.org/advancesearch for compound queries.
It has fields:
 * Journal (with autocomplete for most relevant)
 * Author
 * Date (from to) with electronic/inPrint/embargo
 * Volume, Issue, first page 
 * Title
 * Bibliographic field (Abstract, affiliation ... Year (26 fields)
 * funder
 * open acccess
 * publication type (includes journal article)
 * license
 * sections (17 types)
 * data
 * external links
 
 Of these the only ones we need are Journal, Date, ?title?, open access, 
 
Most of the emphasis here is on building queries
```
query=sodium chloride
```
```
http://www.ebi.ac.uk/europepmc/webservices/rest/profile?query=human%20malaria
or
http://www.ebi.ac.uk/europepmc/webservices/rest/profile?query="human malaria"
```
More advanced:
```
(JOURNAL:"Proceedings of the Royal Society of London. Series B, Biological sciences") AND malaria

%28JOURNAL:%22Nature+chemistry%22+OR+JOURNAL:%22Molecules+%28Basel,+Switzerland%29%22%29+AND+%28FIRST_PDATE:%5B2016-07-01+TO+2016-08-15%5D%29
same as
query=(JOURNAL:"Nature+chemistry"+OR+JOURNAL:"Molecules+(Basel,+Switzerland)")+AND+(FIRST_PDATE:[2016-07-01+TO+2016-08-15])

refine to
(TITLE:Samarium) AND (JOURNAL:"Nature chemistry" OR JOURNAL:"Molecules (Basel, Switzerland)") AND (FIRST_PDATE:[2016-07-01 TO 2016-08-15])
or
(JOURNAL:"Nature chemistry" OR JOURNAL:"Molecules (Basel, Switzerland)") AND (METHODS:"sodium chloride") AND (FIRST_PDATE:[2015-08-01 TO 2016-08-15])
```
for sodium chloride anywhere:
```
"sodium chloride" AND (JOURNAL:"Nature chemistry" OR JOURNAL:"Molecules (Basel, Switzerland)") AND (FIRST_PDATE:[2015-08-01 TO 2016-08-15])
```
or OR for text
```
("sodium chloride" OR "rattus rattus") AND (FIRST_PDATE:[2016-07-01 TO 2016-08-15]) 
```


## building queries, quoting, etc

both `crossref` and `epmc` allow the construction of queries - see https://europepmc.org/advancesearch which allows the creation / editing of a query interactively. 

### crossref 
```
/works?query="sodium chloride"&filter=issn:1420-3049,issn:1755-4349,from-pub-date:2016-07-15,type=journal-article
```
The components are"
 * *works* // fixed, required
 * *query* // optional
 * *filter* // normally required
 
The logic is that repeated filters *of the same type* are OR'ed, while different filters are ANDed. Not sure how `query` is ORed.

### epmc

see above. The "query" does not seem to have a keyword.









