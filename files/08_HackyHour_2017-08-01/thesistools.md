Writing a thesis with R Markdown
========================================================
author: Jochen Schirrwagen
date: 01.08.2017
autosize: true

Motivation
========================================================

- editing environment allowing to focus on ideas and content
- don't waste time with so-called office software
- don't worry about the layout
- support reproducible research 

Tools required or used
========================================================

* RStudio + RMarkdown
* thesisdown template based on bookdown package [https://github.com/ismayc/thesisdown]()
    * made available on github by Chester Ismay
    * based on Reed College LaTeX template
* zotero as reference management software
* ["Better BibTex"](https://github.com/retorquere/zotero-better-bibtex/wiki)
    * solves some issues with bibtex export from zotero
    * currently not compatible with zotero v5
* optional [gitit](https://github.com/jgm/gitit) wiki (as knowledge management tool)

Prerequisites and Preparations
========================================================

* install thesisdown in RStudio


```r
install.packages("devtools",repos = "http://cran.us.r-project.org")
devtools::install_github("rstudio/bookdown")
devtools::install_github("ismayc/thesisdown")
```

Customization 
========================================================

* YAML header in index.Rmd to specify
    * output format
    * citation style (can be chosen from [https://www.zotero.org/styles]())
    * bibliography file (bibtex file)
    * author, advisor etc.
* TeX template
    * to define the layout
    * to declare packages to use
    * to include values from the YAML header

Thesisdown configuration in index.Rmd
========================================================


```r
---
author: 'Jochen Schirrwagen'
date: '02 June 2017'
division: 'Philosophische Fakultät I'
advisor: 'Prof. Dr. Isabella Peters'
altadvisor: 'Dr. Frank Havemann'
department: 'Institut für Bibliotheks- und Informationswissenschaft'
title: 'Data Citation and reuse - a bibliometric and altmetric analysis of selected research data repositories'
knit: "bookdown::render_book"
site: bookdown::bookdown_site
output: 
  thesisdown::thesis_pdf: default
bibliography: bib/data_citation.bib
# Download your specific bibliography database file and refer to it in the line above.
csl: csl/apa.csl
```

Reference Management and BibTex
========================================================

* "Better BibTex" offers
    * **stable** and unique citation keys
    * Unicode conversion
    * automated background export of reference collections from zotero
    * customized exports, e.g. for specific fields (date, url)


```r
@article{peters_research_2016,
  title = {Research Data Explored: An Extended Analysis of Citations and Altmetrics},
  volume = {107},
  issn = {0138-9130, 1588-2861},
  shorttitle = {Research Data Explored},
  doi = {10.1007/s11192-016-1887-4},
  ...
```

Layout features and structure of files
========================================================

* footnote, endnote
* tables, figures, captions
* section headings
* references
* one R Markdown file per chapter and appendix

RStudio screenshot
========================================================

![Screenshot.](rstudio_screenshot.png)


Support of Data Analysis / reproducible research
========================================================

* incorporation of R-code chunks in different modes
    * include script code as text
    * include results of executed scripts, e.g. as plots
    * combination of both
* embedding of LaTeX-code / equations if needed

Table Example
========================================================


```r
repositories <- read.csv("data/repositories.csv")

kable(repositories, 
      col.names = c("Type", "Name", "Platform","records","Usage Data", "Citation Data"),
      caption = "Investigated Repositories",
      caption.short = "Inv. Repositories",
      longtable = TRUE,
      booktabs = TRUE)
```



|Type       |Name                    |Platform  |records |Usage Data   |Citation Data |
|:----------|:-----------------------|:---------|:-------|:------------|:-------------|
|instit.    |PUB Data                |librecat  |        |OA-Statistik |DCI           |
|multidisc. |zenodo                  |invenio   |        |NA           |DCI           |
|multidisc. |Mendeley Data           |          |        |custom       |NA            |
|instit.    |heiDATA                 |dataverse |        |custom       |DCI           |
|instit.    |CERN Open Data          |invenio   |        |NA           |DCI           |
|instit.    |data.bris               |CKAN      |        |IRUSdata     |DCI           |
|multidisc. |DRYAD                   |DSpace    |        |             |DCI           |
|instit.    |Edinb. DataShare        |DSpace    |        |IRUSdata     |DCI           |
|instit.    |Enlighten Res. Data     |EPrints   |        |             |DCI           |
|disc.      |IQB                     |          |        |DCI          |              |
|disc.      |LINDAT/CLARIN           |DSpace    |        |             |DCI           |
|instit.    |Univ. Southampton       |EPrints   |        |IRUSdata     |DCI           |
|instit.    |Surrey Research Insight |EPrints   |        |             |DCI           |
|instit.    |Univ. of Bath           |EPrints   |        |IRUSdata     |DCI           |
|instit.    |UK Data Service         |EPrints   |y       |IRUSdata     |-             |

Include Data Analysis (repos in Data Citation Index)
========================================================



![Histogram about the number of indexed records per repository in the DCI](thesistools-figure/dciggplot-1.png)
***

| Records|Source                                        |
|-------:|:---------------------------------------------|
| 1427940|GENE EXPRESSION OMNIBUS                       |
|  767973|FIGSHARE                                      |
|  552450|UNIPROT KNOWLEDGEBASE                         |
|  550224|CAMBRIDGE STRUCTURAL DATABASE                 |
|  496558|U S CENSUS BUREAU TIGER LINE SHAPEFILES       |
|  448714|PANGAEA                                       |
|  417791|ARRAYEXPRESS ARCHIVE                          |
|  329876|CRYSTALLOGRAPHY OPEN DATABASE                 |
|  225521|EUROPEAN NUCLEOTIDE ARCHIVE                   |
|  125407|WORLDWIDE PROTEIN DATA BANK                   |
|  113106|YEAST RESOURCE CENTER PUBLIC IMAGE REPOSITORY |
|  111245|DEG A DATABASE OF ESSENTIAL GENES             |
|  106059|PITT QUANTUM REPOSITORY                       |
|   84394|ANIMAL QTL DATABASE                           |
|   65536|PLANT TRANSCRIPTION FACTOR DATABASE           |
|   65094|DRYAD                                         |
|   60196|SIOEXPLORER                                   |
|   58952|LTER NETWORK INFORMATION SYSTEM REPOSITORY    |
|   51708|HUMAN METABOLOME DATABASE                     |
|   47797|ASPERGILLUS GENOME DATABASE                   |
|   44266|MASSBANK                                      |
|   40148|ZENODO                                        |


Typical Workflow
========================================================

* initial configuration / set up
* edit R Markdown files, one file per chapter
* update bibtex file via reference manager software, e.g. zotero
* in RStudio - knitr to generate output formats via pandoc
    * e.g. LaTeX to compile the PDF
* integration with git, run by command line or in RStudio
    * my strategy: git repository on USB-stick
    * run on different workstations, laptops

References
========================================================

* [Mardkown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
* [R Mardown reference](https://www.rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf)
* [Chester Ismay. Getting used to R, RStudio, and R Markdown](https://ismayc.github.io/rbasics-book/)
* [Chester Ismay - blog post about RMarkdown thesis template](https://chesterismay.wordpress.com/2016/09/01/updated-r-markdown-thesis-template/)
