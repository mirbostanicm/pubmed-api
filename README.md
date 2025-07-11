# PubMed API

- https://pubmed.ncbi.nlm.nih.gov/
- https://www.ncbi.nlm.nih.gov/home/develop/api/
- https://www.ncbi.nlm.nih.gov/books/NBK25498/
- https://www.ncbi.nlm.nih.gov/books/NBK25499/

## Workflow

- **ESearch**: Finds PubMed article IDs (PMIS) matching a query.
- **ESummary**: Retrieves article summaries (title, author, journal, date, etc.).
- **EFetch**: Fetches full article records or abstracts.

## ESearch

Finds PMIDs (PubMed article IDs) based on a search term.

```bash
$ curl "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?db=pubmed&term=high+blood+pressure&retmode=json&retstart=0&retmax=10"

{
  "header": {
    "type": "esearch",
    "version": "0.3"
  },
  "esearchresult": {
    "count": "785129",
    "retmax": "10",
    "retstart": "0",
    "idlist": [
      "40642747",
      "40642746",
      "40642742",
      "40642741",
      "40642733",
      "40642730",
      "40642705",
      "40642694",
      "40642682",
      "40642675"
    ],
    "translationset": [
      {
        "from": "high blood pressure",
        "to": "\"hypertension\"[MeSH Terms] OR \"hypertension\"[All Fields] OR (\"high\"[All Fields] AND \"blood\"[All Fields] AND \"pressure\"[All Fields]) OR \"high blood pressure\"[All Fields]"
      }
    ],
    "querytranslation": "\"hypertension\"[MeSH Terms] OR \"hypertension\"[All Fields] OR (\"high\"[All Fields] AND \"blood\"[All Fields] AND \"pressure\"[All Fields]) OR \"high blood pressure\"[All Fields]"
  }
}
```

## ESummary

Retrieves an article summary based on a PMID.

```bash
$ curl "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esummary.fcgi?db=pubmed&id=40642746&retmode=json"

{
  "header": {
    "type": "esummary",
    "version": "0.3"
  },
  "result": {
    "uids": [
      "40642746"
    ],
    "40642746": {
      "uid": "40642746",
      "pubdate": "2025",
      "epubdate": "2025 Jun 26",
      "source": "Front Cardiovasc Med",
      "authors": [
        {
          "name": "Yang Y",
          "authtype": "Author",
          "clusterid": ""
        },
        {
          "name": "Liang L",
          "authtype": "Author",
          "clusterid": ""
        },
        {
          "name": "Pei W",
          "authtype": "Author",
          "clusterid": ""
        },
        {
          "name": "Sun Y",
          "authtype": "Author",
          "clusterid": ""
        }
      ],
      "lastauthor": "Sun Y",
      "title": "Interaction of ferroptosis and cuproptosis in the perspective of pulmonary hypertension.",
      "sorttitle": "interaction of ferroptosis and cuproptosis in the perspective of pulmonary hypertension",
      "volume": "12",
      "issue": "",
      "pages": "1611449",
      "lang": [
        "eng"
      ],
      "nlmuniqueid": "101653388",
      "issn": "2297-055X",
      "essn": "",
      "pubtype": [
        "Journal Article",
        "Review"
      ],
      "recordstatus": "PubMed",
      "pubstatus": "258",
      "articleids": [
        {
          "idtype": "pubmed",
          "idtypen": 1,
          "value": "40642746"
        },
        {
          "idtype": "pmc",
          "idtypen": 8,
          "value": "PMC12240957"
        },
        {
          "idtype": "pmcid",
          "idtypen": 5,
          "value": "pmc-id: PMC12240957;"
        },
        {
          "idtype": "doi",
          "idtypen": 3,
          "value": "10.3389/fcvm.2025.1611449"
        }
      ],
      "history": [
        {
          "pubstatus": "medline",
          "date": "2025/07/11 06:29"
        },
        {
          "pubstatus": "pubmed",
          "date": "2025/07/11 06:28"
        },
        {
          "pubstatus": "received",
          "date": "2025/04/14 00:00"
        },
        {
          "pubstatus": "accepted",
          "date": "2025/06/09 00:00"
        },
        {
          "pubstatus": "entrez",
          "date": "2025/07/11 05:21"
        }
      ],
      "references": [],
      "attributes": [
        "Has Abstract"
      ],
      "pmcrefcount": "",
      "fulljournalname": "Frontiers in cardiovascular medicine",
      "elocationid": "doi: 10.3389/fcvm.2025.1611449",
      "doctype": "citation",
      "srccontriblist": [],
      "booktitle": "",
      "medium": "",
      "edition": "",
      "publisherlocation": "",
      "publishername": "",
      "srcdate": "",
      "reportnumber": "",
      "availablefromurl": "",
      "locationlabel": "",
      "doccontriblist": [],
      "docdate": "",
      "bookname": "",
      "chapter": "",
      "sortpubdate": "2025/06/26 00:00",
      "sortfirstauthor": "Yang Y",
      "vernaculartitle": ""
    }
  }
}
```

Retrieves multiple summaries:

```bash
$ curl "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esummary.fcgi?db=pubmed&id=40642746,40642742&retmode=json"
```

## Fetch Abstract

Retrieves an article abstract in plain text.

```bash
curl "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=pubmed&id=40642746&retmode=json&rettype=abstract"

Front Cardiovasc Med. 2025 Jun 26;12:1611449. doi: 10.3389/fcvm.2025.1611449. 
eCollection 2025.

Interaction of ferroptosis and cuproptosis in the perspective of pulmonary 
hypertension.

Yang Y(1), Liang L(1), Pei W(1), Sun Y(1).

Author information:
(1)School of Medicine, Hunan University of Chinese Medicine, Changsha, Hunan, 
China.

Copper (Cu) and iron (Fe) are essential trace elements that are involved in 
normal human metabolic processes. Disruption of their homeostasis contributes to 
disease pathogenesis through mechanisms such as cuproptosis and ferroptosis. 
Cuproptosis targets lipoylated proteins to disrupt mitochondrial respiration, 
whereas ferroptosis is driven by lipid peroxidation. These processes may 
independently or interactively exacerbate pulmonary hypertension (PH), a 
condition characterized by progressive pulmonary vascular remodeling, clinical 
manifestations of dyspnea, right-sided heart failure, and high mortality, via 
oxidative stress, metabolic reprogramming, and other mechanisms. This review 
systematically elucidates: (1) the updated molecular mechanisms of 
cuproptosis/ferroptosis, (2) research evidence for their roles in PH, and (3) 
synergistic crosstalk in different subtypes of PH progression. We propose that 
coordination and regulation of the crosstalk network between cuproptosis and 
ferroptosis may represent a novel therapeutic strategy for pulmonary vascular 
remodeling.

© 2025 Yang, Liang, Pei and Sun.

DOI: 10.3389/fcvm.2025.1611449
PMCID: PMC12240957
PMID: 40642746

Conflict of interest statement: The authors declare that this study was 
conducted in the absence of any commercial or financial relationships that could 
be construed as potential conflicts of interest.
```

Retrieves multiple abstracts:

```bash
$ curl "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=pubmed&id=40642746,40642742,40642741&retmode=json&rettype=abstract"
```
