# gui
Client-side GUI for managing commandline submission

Development of a GUI for managing creattion and submission of commandline tasks, especially
 * getpapers
 * quickscrape
 * norma
 * ami
 
Emphasis on use by early adopters, with GUI-based selection of parameters , editing of commandline, management of resources 
(dictionaries, configuration), launching of jobs, following progress, resubmission.

## architecture

The GUI should allow:
 * chaining of commands, . Example (pseudocode and pseudocommands)
  ```
  getpapers --project proj --api crossref 
     --filter issn:1234-5678,issn:9987-2341,type:journal-article,from-pub-date:2015-01-31,until-pub-date:2015-12-31
  pman --project proj --outUrls urls.txt 

  do {
  // extract unused URLs
    pman --project proj --inUrls urls.txt --outUrls outUrls.txt 
    quickscrape -o proj -r proj/urls.txt
   } until (outUrls.txt.lines > 0)
   
  cmine --project proj --sp.species sp.type binomial genus 
     --w.search(dictionary:file://src/main/resources/org/xmlcml/plugins/disease.xml)
     --w.search(dictionary:http://contentmine.org/dictionaries/phytochem)
     --dataTables 
```
 * pull-downs / drop-down / ranges of parameters
  The commands may be assembled from a number of omittable and repeatable items, with varying types. The `crossref` API is complex and we deliberately limit the scope to `/works`. Among the selectables are:
   * dates for crossref (until-* should be equals or greatr than from-*)
   * messages for logging operator comments
   * project name (mapped onto new /existing directories on disk).
   * service (getpapers/quickscrape/norma/ami)
   * defaults
   * file sources (e.g. dictionaries) or web sources
   * limits and constraints (e.g. times, rates, filesize)
   * filetypes (e.g. PDF/HTML/XML)
  
 * program options
   
about 10 each from `getpapers` and `quickscrape` and `pman`. probably fewer from `norma`. `ami` has many facets (ca 8), and each has sub-parameters.

 * 
 

    
