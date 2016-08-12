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
  getpapers --project proj [params]
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


    
