# GCPDocs Archive

This tool allows you to be able to retrieve all documentation for GCP providing you with a local copy you can archive, search, and diff for security research. 
All credit and glory for this project goes to [Jonathan Walker](https://github.com/jonathanwalker) who created the AWS docs version.  

- Retrieves all sitemap.xml files
- Recursively retrieves all links within them
- Ignores all URLs included in the sitemaps that do not include `cloud.google.com`
- Ignores all non https links
- Avoids most non-product documentation such as docs for `java`, `ruby` and `architecture` specific pages.
- Supports both outputting as warc or html file formats
- Saves all files by `gcp_warcs/` or `gcp_html/` and `YYYY/MM/DD/cloud.google.com/docs/compute/index.warc`

## Usage

The following command allows you to be able to retrieve all the documentation in `gcp_warcs/YYYY/MM/DD`.

```bash
gcpdocs --rate-limit --workers 15 -logfile=gcpdocs.log
```

## Searching

[ripgrep](https://github.com/BurntSushi/ripgrep) will help massively reduce the time to search through all the files recursively as quickly as possible. Grep took `36.78s` and ripgrep spent `0.67s` for the exact same search. So I strongly advise getting familiar with ripgrep to help speed up your search. 

## Retrieve URLs From Query

To search for a specific string and retrieve all GCP Documentation urls containing that string you can use a combination of ripgrep and xargs to do so. 

```bash
$ cd 2024/09/26/cloud.google.com
$ rg "gs://google-cloud-" . -l | xargs -I {} rg "Warc-Target-Uri" {} | awk '{print $2}' | sort | uniq
```

## Simple Search

```bash
$ rg "gs://google-cloud-" .

```


## To Do

- Exlude non-english documentation pages

## Acknowledgements

This project is a fork of: [awsdocs](https://github.com/SecurityRunners/awsdocs) from [Jonathan Walker](https://github.com/jonathanwalker)
