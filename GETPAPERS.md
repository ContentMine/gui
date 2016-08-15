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

Most of the emphasis here is on building queries, e.g. quoting:
```
http://www.ebi.ac.uk/europepmc/webservices/rest/profile?query=human%20malaria
or
http://www.ebi.ac.uk/europepmc/webservices/rest/profile?query="human malaria"
```

## building queries






