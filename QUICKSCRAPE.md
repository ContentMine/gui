# Quickscrape

Considerations for a quickscrape GUI.

## context

This could be used in the following situations:

 * standalone with one URL (possible overkill)
 * standalone with a list of URLs in a file
 * using a `cproject` created by `getpapers`

### operation

 User selects (list of URLs OR a `cproject`), scraperDir, sets download directory, max hits and speed and launches `quickscrape`. 
 It should be possible for the user to:
 * monitor progress
 * kill downloads
 * restart download from last success (this exist in `cproj` software
 
 again create an editable commandline
 
### parameters

`quickscrape` has parameters:
```
-h, --help               output usage information
-V, --version            output the version number
-u, --url <url>          URL to scrape
-r, --urllist <path>     path to file with list of URLs to scrape (one per line)
-s, --scraper <path>     path to scraper definition (in JSON format)
-d, --scraperdir <path>  path to directory containing scraper definitions (in JSON format)
-o, --output <path>      where to output results (directory will be created if it doesn't exist
-r, --ratelimit <int>    maximum number of scrapes per minute (default 3)
-h --headless            render all pages in a headless browser
-l, --loglevel <level>   amount of information to log (silent, verbose, info*, data, warn, error, or debug)
-f, --outformat <name>   JSON format to transform results into (currently only bibjson)
```

Suggest we support 
 * `--url` and --urlist (radiobutton choice, and then textbox or filebrowser)
 * `-scraper or --scraperdir (radiobutton and then filebrowser)
 * `--output` filebrowser for new/existing project.
 * `--ratelimit` (numeric)
 
 Do we need the others?
 
 ### interaction
 
  * display of output to screen and capture in file
  * abort job
  * monitor number and rate of downloads
  * capture of errors
  * restart (using log or existing files as guide)
  
  
  
