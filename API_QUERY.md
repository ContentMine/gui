# API

## design parameters


## architecture

This covers the components:
 * `getpapers` (retrieves papers or metadata into a `cproject`) Node
 * `cproj` (better name than `pman`). Creates, edits, extracts, `cproject`s with additional boolean operations. Java
 *  `quickscrape` - unnecessary with `epmc` queries. Node
 *  `norma` (hopefully silent) but options may need to be selected. Java.
 *  `ami` (runs `facet`s or `plugin`s (old term) which adds resuts to `ctree`s . Java.
 *  
 `cproj` provides glue between `getpapers` and `quickscrape` which may, in time, be replaced by Node.
  
 The data architecture is one or more `cproject`s which consist of a directory of `ctree`s supported by metadata (`*_results?.json`)

## concept


The query builder/submitter could look like
http://europepmc.org/advancesearch
which has an interactively created, editable, query text box (Under "Advanced Search")

? do we want explicit "AND/OR", etc. I suspect not.

Ideally there should be a single GUI which ran some.all of the chain:

 * `getpapers` 
 * `cproj`  and `quickscrape` (only really necessary with `crossref`)
 * `norma` 
 * `ami` - select which `facet`. 
 
In many cases it should be possible to process the whole chain in one set of commands, but in other cases (e.g. broken quickscrape) it may be useful to restart halfway through. It should ideally be possible to monitor long-running jobs and stop them if necessary.


  
## components

The query should be built from components, currently of the types:

 * simple text box (query text)
 * check box (multiple selection)  (e.g. for journals or dictionaries)
 * radiobutton (to select single option).
 * date box
 * file browser
 * help links
  
## `epmc` and `crossref` 

It would be nice to have a single GUI which ran either (through a checkbox)

## customisation

Users may be able to run their own local strategies, and use their own resources.

The main customisations are:

 * creating and using their own dictionaries.
 
## proposed components for `getpapers`

### data source
 
 switch between `crossref` and `epmc`

### query box

This has the text of the query (it *may* be editable to include other fields).

### Publishers.

This should allow ORing of entries. Unfortunately there are 1000 publishers and their names are often not obvious.  `crossref` `member` names could be used. Looking up the correct info for every publisher is out of scope. Suggest we have a list of about 30 of the most frequent ones.

### Journals

This is similar to "Publishers" but worse. One use case is when there are specialist journals and the user is happy to stick to these. In this case the user will probably have to look up the ISSN (may with an online service). Later we might coopt `crossref` to do this.

### Access

Radiobutton between "Open" and "closed"

### Dates

 * Start date (inclusive). If blank, all dates are ignored (i.e not defaulting to 1970)
 * end date (inclusive). If blank defaults to "today"
 
### download parameters

 * max hits (to be passed to remote API) - numeric box
 * download rate (for `quickscrape` only) - numeric box with downloads/min.
 
### `cproject` directory

Save results to directory. If existent, should warn of overwriting. If non-existent should create directory.




 
 
