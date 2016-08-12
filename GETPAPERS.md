# specs for `getpapers`

Initially ONLY used for `crossref`. Other APIs (including EPMC) are much simpler and rarer.

## crossref

The `crossref` api is at :
https://github.com/CrossRef/rest-api-doc/blob/master/rest_api.md
Relatively stable for 2.5 months. Will refer to this doc in the discussion (by named sections).

There is much of this that we do not currently use (or use rarely). 

### works
`/works` (i.e. articles, etc.) will be the only type supported.

"Combining resource components" is not supported in the GUI.
