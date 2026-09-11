# Clarivate Derwent Patent API

Derwent Patent API provides seamless access to enriched patent data, enabling users to enhance their research capabilities and make faster, more informed decisions.

## Table of Contents

- [Getting Started](#getting-started)
- [Base URL](#base-url)
- [Authentication](#authentication)
- [Error Handling](#error-handling)
- [Endpoints](#endpoints)
  - [Overview](#overview)
  - [Fields and Collections](#fields-and-collections)
  - Search endpoints
    - [POST /patents/derwent/search-by-query](#post-patentsderwentsearch-by-query)
    - [POST /patents/derwent/search-by-ids](#post-patentsderwentsearch-by-ids)
    - [POST /patents/derwent/search-by-pns](#post-patentsderwentsearch-by-pns)
    - [POST /patents/derwent/combined-search](#post-patentsderwentcombined-search)
  - Document endpoints
    - [POST /patents/derwent/documents-by-id](#post-patentsderwentdocuments-by-id)
    - [POST /patents/derwent/documents-by-pn](#post-patentsderwentdocuments-by-pn)
    - [POST /patents/derwent/documents-by-listref](#post-patentsderwentdocuments-by-listref)
    - [POST /patents/derwent/document/pdf](#post-patentsderwentdocumentpdf)
    - [GET /patents/derwent/document/pdf/\{document_guid\}](#get-patentsderwentdocumentpdfdocument_guid)
    - [GET /patents/derwent/document/images/\{document_guid\}](#get-patentsderwentdocumentimagesdocument_guid)
  - Utility endpoints
    - [POST /patents/derwent/class-browse](#post-patentsderwentclass-browse)
    - [POST /patents/derwent/class-search](#post-patentsderwentclass-search)
    - [POST /patents/derwent/corporate-tree](#post-patentsderwentcorporate-tree)
    - [POST /patents/derwent/documents-IdMapping](#post-patentsderwentdocuments-idmapping)
- [Support](#support)
- [Terms of service](#terms-of-service)

---

## Getting Started

### Register Developer Portal

1. Go to [Clarivate Developer Portal](https://developer.clarivate.com/) and select **Sign up** to open a new page page
2. Click **Register** to open the register page, following the instruction to input your ***email address***, ***password*** and other information, then click **Register**
3. You will receiven an email, follow the instruction to confirm the registration

### Register Application

1. Go to [Clarivate Developer Portal](https://developer.clarivate.com/) and select **Log in** to open a new page
2. Input your email address and password, and click **Sign in** to your personal home page
3. Click **Applications** in the menu to open the appication page
4. Click **Register a new Application** to show the panel, input the required fields (You can input a few words and update it later), click **Register Application**

### Subscribe Patent API

1. If you haven't subscribed any API, in your **Application** page, you can click **View APIs >>**. Alternatively, you can click **APIs** menu to naviage to APIs page
2. In the APIs page, find and click **Intellectual Property (IP) Data API** You can find it by searching the name in browser or use filter **Derwent** to narrow down the APIs list
3. In the **Intellectual Property (IP) Data API** page,scroll to the bottom, click **Subscribe** to raise the request
4. Please inform your account manager your email address, our approver will check your subscription request and approve

[⬆ Back to Top](#table-of-contents)

---

## Base URL

- https://api.clarivate.com

[⬆ Back to Top](#table-of-contents)

---

## Authentication

Use a bearer token in the Authorization header. Tokens are issued via your developer console.

| **Header**   | **Example**                          | **Description**                    |
|--------------|--------------------------------------|------------------------------------|
| Content-Type | application/json                     | All request bodies are JSON        |
| Accept       | application/json                     | All responses are JSON             |
| X-ApiKey     | 1e3f2b1c-9b0e-4b8a-9a6a-9f7d0a6b4a2f | Authorization key to make requests |

[⬆ Back to Top](#table-of-contents)

---

## Error Handling

- Responses uses the below json format

```json
{
  "code": 2100,
  "error": "Missing mandatory parameter(s): query"
}
```

Common status codes

- 200 OK

- 400 Bad Request

- 401 Unauthorized

- 403 Forbidden

- 404 Not Found

[⬆ Back to Top](#table-of-contents)

---

## Endpoints

This section describe the common concept for Patent APIs

### Overview

Patent API has three types of endpoints

| Type | Description |
|------|-------------|
| **Search** | **Return one or more patents by different query, the reponse fields are limited** |
|            | POST /patents/derwent/search-by-query |
|            | POST /patents/derwent/search-by-ids |
|            | POST /patents/derwent/search-by-pns |
|            | POST /patents/derwent/combined-search |
| **Document** | **Return one or more specified patent documents, the response fields are more comprehensive than *Search* endpoints** |
|            | POST /patents/derwent/documents-by-id |
|            | POST /patents/derwent/documents-by-pn |
|            | POST /patents/derwent/documents-by-listref |
|            | POST /patents/derwent/document/pdf |
|            | GET /patents/derwent/document/pdf/\{document_guid\} |
|            | GET /patents/derwent/document/images/\{document_guid\} |
| **Utility** | **Utitliies that can search classification, corporation tree, Id mapping** |
|            | POST /patents/derwent/class-search |
|            | POST /patents/derwent/class-browse |
|            | POST /patents/derwent/corporate-tree |
|            | POST /patents/derwent/documents-IdMapping |

### Fields and Collections

The API fields and collections are described in [Field List (Excel)](docs/New_Derwent_API_Field_List.xlsx)

#### Fields
All the fields are listed in the **FIELDS** tab, they have a few categories:
- **Search Request**: The fields that can be requested (as parameters) in **Search** endpoints
- **Search Response**: The fields that can be returend in **Search** endpoints
- **Document Response**: The fields that can be returned in **Document** endpoints

#### Collections
All the collections are listed in the **COLLECTIONS** tab.<br>
Each collection is for one specific authority and one specific patent type (application, grant, utility model)<br>
Refer to <a href=“docs/Derwent_API_DataFeed_Coverage.pdf” target="_blank">Coverage and Collections (PDF)</a> to check the start date and patent type for each authority<br>

[⬆ Back to Top](#table-of-contents)

---

### POST /patents/derwent/search-by-query

AI (semantic) search and Boolean search by fields. Results include a listref reference that can be used for subsequent document retrieval.

**Request parameters:**

- query: string. Use search_field=search_value

  - For AI search: The field name is "aisq", e.g. aisq=\"pizza delivery driverless that also takes payment\"
  - For Boolean search: The search fields are **Search Request** category, see [Fields](#fields)

  AI search and Boolean search can't be used at the same search request.

- listref: string. String obtained from search response. Either query or listref can be used in this endpoint

- collections: string. String containing one or more collections separated by comma(”,”)

- return-listref: bool. If true, then the response will return listref for this search result

- return-fields: string. String containing one or more return-fields separated by comma(”,”)

- size: integer. The maximum number of records returned for this search. The default maximum is 30000.

- offset: integer. Return the records after this number. If you query result is large, you can specify the size and offset to only return the limited records

**Response**

The response contains header and body if the search runs successfully.

header: the summary of this search result

- found: integer. The number of records this search found.
- size: integer. The maximum number of records this search can return. It is smaller value between *found* and *size* parameter.

body: the main content of this search result, 

  - id: The patent document Id, wihch can be used in **Document** search
  - rank: The relevancy ranking results. For AI search, it is between 0.0 (0%) to 1.0 (100%). For Boolean search, it is always 1.0
  - field: The returned fields and their values, the fields are specified in *return-fields* parameter.

**Sample request:**

```bash
curl -sS \
  -X 'POST' \
  'https://api.clarivate.com/patents/derwent/search-by-query' \
  -H 'accept: application/json' \
  -H 'X-ApiKey: $(x-apikey)' \
  -H 'Content-Type: application/json' \
  -d '{
  "params": [
      {
        "collections": "usapps,usgrants,epapps,epgrants,woapps",
        "offset": 0,
        "query": "pd>=(20180101) and ti=car",
        "return-fields": "ti,pd,pn",
        "size": 3
      }
    ]
  }'
```

**Sample response:**

```json
{
  "header": {
    "duration": "395",
    "searched": 184834460,
    "found": "113342",
    "size": 30000
  },
  "body": [
    {
      "id": "USD1147626S120260908",
      "rank": "2.0",
      "field": [
        {
          "name": "ti",
          "form": "orig",
          "lang": "en",
          "value": "Car vacuum cleaner"
        },
        {
          "name": "pd",
          "form": "orig",
          "value": "2026-09-08"
        },
        {
          "name": "pn",
          "form": "orig",
          "value": "USD1147626S1"
        }
      ]
    },
    {
      "id": "USD1147476S120260908",
      "rank": "2.0",
      "field": [
        {
          "name": "ti",
          "form": "orig",
          "lang": "en",
          "value": "Car light"
        },
        {
          "name": "pd",
          "form": "orig",
          "value": "2026-09-08"
        },
        {
          "name": "pn",
          "form": "orig",
          "value": "USD1147476S1"
        }
      ]
    },
    {
      "id": "USD1147196S120260908",
      "rank": "2.0",
      "field": [
        {
          "name": "ti",
          "form": "orig",
          "lang": "en",
          "value": "Tire for toy model climbing car"
        },
        {
          "name": "pd",
          "form": "orig",
          "value": "2026-09-08"
        },
        {
          "name": "pn",
          "form": "orig",
          "value": "USD1147196S1"
        }
      ]
    }
  ]
}
```

[⬆ Back to Top](#table-of-contents)

---

### POST /patents/derwent/search-by-ids

Search and retrieval using document IDs (GUIDs).

**Request parameters:**

- ids: string. String containing one or more document ids separated by comma(”,”)

- collections: string. String containing one or more collections separated by comma(”,”)

**Sample request:**

```bash
curl -sS \
  -X POST "https://api.clarivate.com/patents/derwent/search-by-ids" \
  -H "Content-Type: application/json" \
  -H "X-ApiKey: $(x-apikey)" \
  -d '{
    "params": [
      {
        "ids": "AR56578A120071010,BR102022016886A220240305,CA3233250A120230330",
        "collections": "arapps,brapps,caapps,coapps,crapps,cuapps,mxapps,uyapps,usapps,auapps,cnapps,hkapps,idapps,jpapps,krapps,phapps,sgapps,twapps,vnapps,atapps,beapps,bgapps,hrapps,czapps,dkapps,epapps,eeapps,fiapps,frapps,ddapps,deapps,gbapps,grapps,inapps,ieapps,luapps,maapps,nlapps,noapps,ptapps,roapps,ruapps,rsapps,skapps,zaapps,esapps,seapps,chapps,tnapps,trapps,woapps,brgrants,cagrants,cugrants,mxgrants,usgrants,augrants,cngrants,hkgrants,jpgrants,krgrants,mygrants,mngrants,nzgrants,phgrants,sggrants,sugrants,twgrants,thgrants,vngrants,apgrants,amgrants,atgrants,bygrants,begrants,bggrants,hrgrants,czgrants,csgrants,dkgrants,epgrants,eegrants,eagrants,figrants,frgrants,gegrants,ddgrants,degrants,gbgrants,grgrants,gcgrants,hugrants,isgrants,ingrants,iegrants,ilgrants,itgrants,lvgrants,ltgrants,lugrants,mdgrants,mcgrants,magrants,nlgrants,nogrants,oagrants,plgrants,ptgrants,rogrants,rugrants,rsgrants,skgrants,sigrants,esgrants,segrants,chgrants,uagrants,auinnov,inpadoc,arutils,brutils,crutils,cnutils,hkutils,jputils,krutils,mnutils,twutils,atutils,byutils,bgutils,hrutils,czutils,dkutils,eeutils,deutils,ieutils,mdutils,plutils,ptutils,routils,ruutils,rsutils,skutils,siutils,esutils,trutils,uautils"
      }
    ]
  }'
```

**Sample response:**

```json
{
  "header": {
    "duration": "452",
    "searched": 3,
    "found": "3",
    "size": 3
  },
  "body": [
    {
      "id": [
        "AR56578A120071010",
        "BR102022016886A220240305",
        "CA3233250A120230330"
      ]
    }
  ]
}
```

[⬆ Back to Top](#table-of-contents)

---
### POST /patents/derwent/search-by-pns

Search with one or more publication numbers directly.

**Request parameters:**

- pns: string. String containing one or more publication numbers separated by comma(”,”)

- collections: string. String containing one or more collections separated by comma(”,”)

**Sample request:**

```bash
curl -sS \
  -X POST "https://api.clarivate.com/patents/derwent/search-by-pns" \
  -H "Content-Type: application/json" \
  -H "X-ApiKey: $(x-apikey)" \
  -d '{
    "params": [
      {
        "pns": "US12101354B2,US5551212A1,US20070090909A1,WO2007089355A3,BE1019892A5",
        "collections": "arapps,brapps,caapps,coapps,crapps,cuapps,mxapps,uyapps,usapps,auapps,cnapps,hkapps,idapps,jpapps,krapps,phapps,sgapps,twapps,vnapps,atapps,beapps,bgapps,hrapps,czapps,dkapps,epapps,eeapps,fiapps,frapps,ddapps,deapps,gbapps,grapps,inapps,ieapps,luapps,maapps,nlapps,noapps,ptapps,roapps,ruapps,rsapps,skapps,zaapps,esapps,seapps,chapps,tnapps,trapps,woapps,brgrants,cagrants,cugrants,mxgrants,usgrants,augrants,cngrants,hkgrants,jpgrants,krgrants,mygrants,mngrants,nzgrants,phgrants,sggrants,sugrants,twgrants,thgrants,vngrants,apgrants,amgrants,atgrants,bygrants,begrants,bggrants,hrgrants,czgrants,csgrants,dkgrants,epgrants,eegrants,eagrants,figrants,frgrants,gegrants,ddgrants,degrants,gbgrants,grgrants,gcgrants,hugrants,isgrants,ingrants,iegrants,ilgrants,itgrants,lvgrants,ltgrants,lugrants,mdgrants,mcgrants,magrants,nlgrants,nogrants,oagrants,plgrants,ptgrants,rogrants,rugrants,rsgrants,skgrants,sigrants,esgrants,segrants,chgrants,uagrants,auinnov,inpadoc,arutils,brutils,crutils,cnutils,hkutils,jputils,krutils,mnutils,twutils,atutils,byutils,bgutils,hrutils,czutils,dkutils,eeutils,deutils,ieutils,mdutils,plutils,ptutils,routils,ruutils,rsutils,skutils,siutils,esutils,trutils,uautils"
      }
    ]
  }'
```

**Sample response:**

```json
{
  "header": {
    "duration": "226",
    "searched": 5,
    "found": "5",
    "size": 5,
    "inputs": "5",
    "outputs": "5",
    "pns_summary_size": "0"
  },
  "body": [
    {
      "id": [
        "US12101354B220240924",
        "US5551212A_19960903",
        "US20070090909A120070426",
        "WO2007089355A320071004",
        "BE1019892A520130205"
      ]
    }
  ]
}
```

[⬆ Back to Top](#table-of-contents)

---

### POST /patents/derwent/combined-search

Combine and run multiple queries in a single call using Boolean logic. Particularly useful for complex, multi-concept search strategies.

**Request parameters:**

- query\{query_number\}: string. Free-text search query, with search_field=search_value

- collections\{number\}: string. Collection or comma separated string of multiple collections

- combination: string. Containing combination condition of queries. Example: "combination": "\$1 and \$2”

**Sample request:**

```bash
curl -sS \
  -X POST "https://api.clarivate.com/patents/derwent/combined-search" \
  -H "Content-Type: application/json" \
  -H "X-ApiKey: $(x-apikey)" \
  -d '{
    "params": [
      {
        "query1": "pac=IN",
        "collections1": "usapps",
        "query2": "pa=*Atl*",
        "collections2": "usapps",
        "query3": "pa=*US",
        "collections3": "usapps",
        "combination": "($1 AND $2 OR S3)"
      }
    ]
  }'
```

**Sample response:**

```json
[
  {
    "duration": "5885",
    "searched": 177324912,
    "found": "28801,4683,216194,6578197",
    "size": 30000
  },
  {
    "id": "USRE50600E120250923",
    "rank": 7
  },
  {
    "id": "US12426505B220250923",
    "rank": 4
  },
  {
    "id": "US12426464B220250923",
    "rank": 5
  },
  {
    "id": "US12426451B220250923",
    "rank": 4
  },
  {
    "id": "US12426448B220250923",
    "rank": 4
  },
  {
    "id": "US12426437B220250923",
    "rank": 2
  },
  {
    "id": "US12426431B120250923",
    "rank": 4
  },
  {
    "id": "US12426407B220250923",
    "rank": 10
  },
  {
    "id": "US12426400B220250923",
    "rank": 3
  },
  {
    "id": "US12426375B220250923",
    "rank": 5
  }
]
```

[⬆ Back to Top](#table-of-contents)

---

### POST /patents/derwent/documents-by-id

Retrieve document content using document IDs (GUIDs).

**Request parameters:**

- ids: string. String containing one or more document ids separated by comma(”,”)

- collections: string. String containing one or more collections separated by comma(”,”)

**Sample request:**

```bash
curl -sS \
  -X POST "https://api.clarivate.com/patents/derwent/documents-by-id" \
  -H "Content-Type: application/json" \
  -H "X-ApiKey: $(x-apikey)" \
  -d '{
    "params": [
      {
        "ids": "AU2022206581A120230629,CN118786405A_20241015,HK40097707A_20240322,ID201700917A_20170210,JP2024128994A_20240926,KR2024150740A_20241016,SG159132A120100330",
        "collections": "arapps,brapps,caapps,coapps,crapps,cuapps,mxapps,uyapps,usapps,auapps,cnapps,hkapps,idapps,jpapps,krapps,phapps,sgapps,twapps,vnapps,atapps,beapps,bgapps,hrapps,czapps,dkapps,epapps,eeapps,fiapps,frapps,ddapps,deapps,gbapps,grapps,inapps,ieapps,luapps,maapps,nlapps,noapps,ptapps,roapps,ruapps,rsapps,skapps,zaapps,esapps,seapps,chapps,tnapps,trapps,woapps,brgrants,cagrants,cugrants,mxgrants,usgrants,augrants,cngrants,hkgrants,jpgrants,krgrants,mygrants,mngrants,nzgrants,phgrants,sggrants,sugrants,twgrants,thgrants,vngrants,apgrants,amgrants,atgrants,bygrants,begrants,bggrants,hrgrants,czgrants,csgrants,dkgrants,epgrants,eegrants,eagrants,figrants,frgrants,gegrants,ddgrants,degrants,gbgrants,grgrants,gcgrants,hugrants,isgrants,ingrants,iegrants,ilgrants,itgrants,lvgrants,ltgrants,lugrants,mdgrants,mcgrants,magrants,nlgrants,nogrants,oagrants,plgrants,ptgrants,rogrants,rugrants,rsgrants,skgrants,sigrants,esgrants,segrants,chgrants,uagrants,auinnov,inpadoc,arutils,brutils,crutils,cnutils,hkutils,jputils,krutils,mnutils,twutils,atutils,byutils,bgutils,hrutils,czutils,dkutils,eeutils,deutils,ieutils,mdutils,plutils,ptutils,routils,ruutils,rsutils,skutils,siutils,esutils,trutils,uautils"
      }
    ]
  }'
```

**Sample response:**

```json
{
  "body": [
    {
      "id": "AU2022206581A120230629"
    },
    {
      "id": "CN118786405A_20241015"
    },
    {
      "id": "HK40097707A_20240322"
    },
    {
      "id": "ID201700917A_20170210"
    },
    {
      "id": "JP2024128994A_20240926"
    },
    {
      "id": "KR2024150740A_20241016"
    },
    {
      "id": "SG159132A120100330"
    }
  ],
  "header": {
    "download_details": {
      "downloaded_this_day": 7,
      "downloaded_this_month": 56,
      "downloaded_this_year": 621
    },
    "duration": "1",
    "found": "7",
    "response_id": "AU2022206581A120230629,CN118786405A_20241015,HK40097707A_20240322,ID201700917A_20170210,JP2024128994A_20240926,KR2024150740A_20241016,SG159132A120100330",
    "size": 7
  }
}
```

[⬆ Back to Top](#table-of-contents)

---

### POST /patents/derwent/documents-by-pn

Retrieve document content using publication numbers directly.

**Request parameters:**

- pns: string. String containing one or more publication numbers separated by comma(”,”)

- collections: string. String containing one or more collections separated by comma(”,”)

**Sample request:**

```bash
curl -sS \
  -X POST "https://api.clarivate.com/patents/derwent/documents-by-pn" \
  -H "Content-Type: application/json" \
  -H "X-ApiKey: $(x-apikey)" \
  -d '{
    "params": [
      {
        "pns": "US12101354B2,US5551212A1,US20070090909A1,WO2007089355A3,BE1019892A5",
        "collections": "arapps,brapps,caapps,coapps,crapps,cuapps,mxapps,uyapps,usapps,auapps,cnapps,hkapps,idapps,jpapps,krapps,phapps,sgapps,twapps,vnapps,atapps,beapps,bgapps,hrapps,czapps,dkapps,epapps,eeapps,fiapps,frapps,ddapps,deapps,gbapps,grapps,inapps,ieapps,luapps,maapps,nlapps,noapps,ptapps,roapps,ruapps,rsapps,skapps,zaapps,esapps,seapps,chapps,tnapps,trapps,woapps,brgrants,cagrants,cugrants,mxgrants,usgrants,augrants,cngrants,hkgrants,jpgrants,krgrants,mygrants,mngrants,nzgrants,phgrants,sggrants,sugrants,twgrants,thgrants,vngrants,apgrants,amgrants,atgrants,bygrants,begrants,bggrants,hrgrants,czgrants,csgrants,dkgrants,epgrants,eegrants,eagrants,figrants,frgrants,gegrants,ddgrants,degrants,gbgrants,grgrants,gcgrants,hugrants,isgrants,ingrants,iegrants,ilgrants,itgrants,lvgrants,ltgrants,lugrants,mdgrants,mcgrants,magrants,nlgrants,nogrants,oagrants,plgrants,ptgrants,rogrants,rugrants,rsgrants,skgrants,sigrants,esgrants,segrants,chgrants,uagrants,auinnov,inpadoc,arutils,brutils,crutils,cnutils,hkutils,jputils,krutils,mnutils,twutils,atutils,byutils,bgutils,hrutils,czutils,dkutils,eeutils,deutils,ieutils,mdutils,plutils,ptutils,routils,ruutils,rsutils,skutils,siutils,esutils,trutils,uautils"
      }
    ]
  }'
```

**Sample response:**

```json
{
  "body": [
    {
      "id": "US12101354B220240924"
    },
    {
      "id": "US5551212A_19960903"
    },
    {
      "id": "US20070090909A120070426"
    },
    {
      "id": "WO2007089355A320071004"
    },
    {
      "id": "BE1019892A520130205"
    }
  ],
  "header": {
    "download_details": {
      "downloaded_this_day": 12,
      "downloaded_this_month": 56,
      "downloaded_this_year": 621
    },
    "duration": "5",
    "found": "5",
    "inputs": "5",
    "outputs": "5",
    "pns_summary_size": "0",
    "response_id": "US12101354B220240924,US5551212A_19960903,US20070090909A120070426,WO2007089355A320071004,BE1019892A520130205",
    "size": 5
  }
}
```

[⬆ Back to Top](#table-of-contents)

---

### POST /patents/derwent/documents-by-listref

Retrieve document content using listref. The listref option enables efficient batch retrieval following a search. The listref obtained from the response header of the precious search is valid for only **72 hours**.

**Request parameters:**

- listref: string. String obtained from the search request

- collections: string. String containing one or more collections separated by comma(”,”)

**Sample request:**

```bash
curl -sS \
  -X POST "https://api.clarivate.com/patents/derwent/documents-by-listref" \
  -H "Content-Type: application/json" \
  -H "X-ApiKey: $(x-apikey)" \
  -d '{
    "params": [
      {
        "listref": "1769380692808-pc1t026of0N",
        "collections": "arapps,brapps,caapps,coapps,crapps,cuapps,mxapps,uyapps,usapps,auapps,cnapps,hkapps,idapps,jpapps,krapps,phapps,sgapps,twapps,vnapps,atapps,beapps,bgapps,hrapps,czapps,dkapps,epapps,eeapps,fiapps,frapps,ddapps,deapps,gbapps,grapps,inapps,ieapps,luapps,maapps,nlapps,noapps,ptapps,roapps,ruapps,rsapps,skapps,zaapps,esapps,seapps,chapps,tnapps,trapps,woapps,brgrants,cagrants,cugrants,mxgrants,usgrants,augrants,cngrants,hkgrants,jpgrants,krgrants,mygrants,mngrants,nzgrants,phgrants,sggrants,sugrants,twgrants,thgrants,vngrants,apgrants,amgrants,atgrants,bygrants,begrants,bggrants,hrgrants,czgrants,csgrants,dkgrants,epgrants,eegrants,eagrants,figrants,frgrants,gegrants,ddgrants,degrants,gbgrants,grgrants,gcgrants,hugrants,isgrants,ingrants,iegrants,ilgrants,itgrants,lvgrants,ltgrants,lugrants,mdgrants,mcgrants,magrants,nlgrants,nogrants,oagrants,plgrants,ptgrants,rogrants,rugrants,rsgrants,skgrants,sigrants,esgrants,segrants,chgrants,uagrants,auinnov,inpadoc,arutils,brutils,crutils,cnutils,hkutils,jputils,krutils,mnutils,twutils,atutils,byutils,bgutils,hrutils,czutils,dkutils,eeutils,deutils,ieutils,mdutils,plutils,ptutils,routils,ruutils,rsutils,skutils,siutils,esutils,trutils,uautils"
      }
    ]
  }'
```

**Sample response:**

```json
{
  "body": [
    {
      "id": "US12424223B220250923",
      "rank": 2
    },
    {
      "id": "US12423568B220250923",
      "rank": 2
    },
    {
      "id": "US12417017B220250916",
      "rank": 2
    },
    {
      "id": "US12416797B220250916",
      "rank": 2
    },
    {
      "id": "US12412036B220250909",
      "rank": 2
    },
    {
      "id": "US12411468B220250909",
      "rank": 2
    },
    {
      "id": "US12411466B220250909",
      "rank": 2
    },
    {
      "id": "US12406653B220250902",
      "rank": 2
    },
    {
      "id": "US12405779B220250902",
      "rank": 1
    },
    {
      "id": "US12393709B220250819",
      "rank": 2
    }
  ],
  "header": {
    "download_details": {
      "downloaded_this_day": 22,
      "downloaded_this_month": 66,
      "downloaded_this_year": 631
    },
    "duration": "6",
    "found": "3536",
    "response_id": "US12424223B220250923,US12423568B220250923,US12417017B220250916,US12416797B220250916,US12412036B220250909,US12411468B220250909,US12411466B220250909,US12406653B220250902,US12405779B220250902,US12393709B220250819",
    "searched": 177324912,
    "size": 3536
  }
}
```

[⬆ Back to Top](#table-of-contents)

---

### POST /patents/derwent/document/pdf

Return PDF availability with direct DocDel URLs or wrapped URLs for one or more Derwent patents.

**Request parameters:**

- pns: string. String containing one or more publication numbers separated by comma(”,”)

- wrap: bool. If true, then the PDF URL is wrapped

**Sample request:**

```bash
curl -X 'POST' \
  'https://api.clarivate.com/patents/derwent/document/pdf' \
  -H 'accept: application/json' \
  -H 'X-ApiKey: $(x-apikey)' \
  -H 'Content-Type: application/json' \
  -d '{
  "params": [
    {
      "pns": "US20110094542A1,US12368967B2"
    }
  ],
  "wrap": true
}'
```
**Sample response:**

```json
{
  "available": [
    {
      "pn": "US20110094542A1",
      "url": "https://api.clarivate.com/patents/derwent/document/pdf/file?patent=US20110094542A1&token=($token)"
    },
    {
      "pn": "US12368967B2",
      "url": "https://api.clarivate.com/patents/derwent/document/pdf/file?patent=US12368967B2&token=($token)"
    }
  ],
  "unavailable": []
}
```

[⬆ Back to Top](#table-of-contents)

---

### GET /patents/derwent/document/pdf/\{document_guid\}

Retrieves the original patent PDF by document ID (GUID), allowing users to access full patent documents directly.

**Request parameters:**

- document_guid: The patent document Id.

**Sample request:**

```bash
curl -X 'GET' \
  'https://api.clarivate.com/patents/derwent/document/pdf/DE102025002193B3' \
  -H 'accept: */*' \
  -H 'X-ApiKey: $(x-apikey)'
```

**Sample response:**

The request will return PDF binary file directly, which can be rendered direclty in browser.

[⬆ Back to Top](#table-of-contents)

---

### GET /patents/derwent/document/images/{document_guid}

Retrieves patent images by document ID (GUID), useful for quickly reviewing drawings and diagrams of patents.

**Request parameters:**

- document_guid: string. The patent document Id.

- size: integer. Expected image size in pixels, this is optional

- wrap: bool. If true, then return IP API wrapper URLs; if false, then return direct CLIPS URLs. Default value is true

**Sample request:**

```bash
curl -X 'GET' \
  'https://api.clarivate.com/patents/derwent/document/images/DE102025002193B3' \
  -H 'accept: application/json' \
  -H 'X-ApiKey: $(x-apikey)'
```

**Sample response:**

```json
[
  {
    "image_urls": [
      "https://api.clarivate.com/patents/derwent/document/images/file?patent=DE102025002193B3&page=1&fponly=0&size=380&format=gif&token=($token)",
      "https://api.clarivate.com/patents/derwent/document/images/file?patent=DE102025002193B3&page=2&fponly=0&size=380&format=gif&token=($token)",
      "https://api.clarivate.com/patents/derwent/document/images/file?patent=DE102025002193B3&page=3&fponly=0&size=380&format=gif&token=($token)",
      "https://api.clarivate.com/patents/derwent/document/images/file?patent=DE102025002193B3&page=4&fponly=0&size=380&format=gif&token=($token)"
    ]
  }
]
```

[⬆ Back to Top](#table-of-contents)

---

### POST /patents/derwent/class-browse

Browsing through classification databases across various levels and hierarchies to ensure comprehensive technical coverage.

**Request parameters:**

- class-levels: Integer. A numeric value that denotes class level

- classes: string. String containing one or more classification codes that need to be browsed upon

- type: string. String containing classification type

**Sample request:**

```bash
curl -sS \
  -X POST "https://api.clarivate.com/patents/derwent/class-browse" \
  -H "Content-Type: application/json" \
  -H "X-ApiKey: $(x-apikey)" \
  -d '{
    "params": [
      {
        "class-levels": "1",
        "classes": "A01",
        "type": "ipc8"
      }
    ]
  }'
```

**Sample response:**

```json
[
  {
    "duration": "8",
    "classificationresponse": {
      "classdescription": [
        {
          "classes": "A01B",
          "level": 3,
          "child_count": 37,
          "value": "SOIL WORKING IN AGRICULTURE OR FORESTRY; PARTS, DETAILS, OR ACCESSORIES OF AGRICULTURAL MACHINES OR IMPLEMENTS, IN GENERAL(making or covering furrows or holes for sowing, planting or manuring A01C000500; machines for harvesting root crops A01D; mowers convertible to soil working apparatus or capable of soil working A01D004204; mowers combined with soil working implements A01D004312; soil working for engineering purposes E01, E02, E21)"
        },
        {
          "classes": "A01C",
          "level": 3,
          "child_count": 13,
          "value": "PLANTING; SOWING; FERTILISING(parts, details or accessories of agricultural machines or implements, in general A01B005100-A01B007500)"
        },
        {
          "classes": "A01D",
          "level": 3,
          "child_count": 48,
          "value": "HARVESTING; MOWING"
        },
        {
          "classes": "A01F",
          "level": 3,
          "child_count": 14,
          "value": "THRESHING(combines A01D004100); BALING OF STRAW, HAY OR THE LIKE; STATIONARY APPARATUS OR HAND TOOLS FOR FORMING OR BINDING STRAW, HAY OR THE LIKE INTO BUNDLES; CUTTING OF STRAW, HAY OR THE LIKE; STORING AGRICULTURAL OR HORTICULTURAL PRODUCE(arrangements for making or setting stacks in connection with harvesting A01D008500)"
        },
        {
          "classes": "A01G",
          "level": 3,
          "child_count": 21,
          "value": "HORTICULTURE; CULTIVATION OF VEGETABLES, FLOWERS, RICE, FRUIT, VINES, HOPS OR SEAWEED; FORESTRY; WATERING(picking of fruits, vegetables, hops or the like A01D004600; propagating unicellular algae C12N000112)"
        },
        {
          "classes": "A01H",
          "level": 3,
          "child_count": 11,
          "value": "NEW PLANTS OR PROCESSES FOR OBTAINING THEM; PLANT REPRODUCTION BY TISSUE CULTURE TECHNIQUES"
        },
        {
          "classes": "A01J",
          "level": 3,
          "child_count": 15,
          "value": "MANUFACTURE OF DAIRY PRODUCTS(for chemical matters, see subclass A23C)"
        },
        {
          "classes": "A01K",
          "level": 3,
          "child_count": 53,
          "value": "ANIMAL HUSBANDRY; AVICULTURE; APICULTURE; PISCICULTURE; FISHING; REARING OR BREEDING ANIMALS, NOT OTHERWISE PROVIDED FOR; NEW BREEDS OF ANIMALS"
        },
        {
          "classes": "A01L",
          "level": 3,
          "child_count": 8,
          "value": "SHOEING OF ANIMALS"
        },
        {
          "classes": "A01M",
          "level": 3,
          "child_count": 17,
          "value": "CATCHING, TRAPPING OR SCARING OF ANIMALS(appliances for catching swarms or drone-catching A01K005700; fishing A01K006900-A01K009700; biocides, pest repellants or attractants A01N); APPARATUS FOR THE DESTRUCTION OF NOXIOUS ANIMALS OR NOXIOUS PLANTS"
        },
        {
          "classes": "A01N",
          "level": 3,
          "child_count": 23,
          "value": "PRESERVATION OF BODIES OF HUMANS OR ANIMALS OR PLANTS OR PARTS THEREOF(preservation of food or foodstuff A23); BIOCIDES, e.g. AS DISINFECTANTS, AS PESTICIDES OR AS HERBICIDES(preparations for medical, dental or toiletry purposes which kill or prevent the growth or proliferation of unwanted organisms A61K); PEST REPELLANTS OR ATTRACTANTS; PLANT GROWTH REGULATORS"
        },
        {
          "classes": "A01P",
          "level": 3,
          "child_count": 12,
          "value": "BIOCIDAL, PEST REPELLANT, PEST ATTRACTANT OR PLANT GROWTH REGULATORY ACTIVITY OF CHEMICAL COMPOUNDS OR PREPARATIONS"
        },
        {
          "classes": "A01",
          "level": 2,
          "child_count": 12,
          "value": "AGRICULTURE; FORESTRY; ANIMAL HUSBANDRY; HUNTING; TRAPPING; FISHING"
        }
      ]
    }
  }
]
```

[⬆ Back to Top](#table-of-contents)

---

### POST /patents/derwent/class-search

Identify relevant classification codes using query and classification type parameters (e.g., ipc8).

**Request parameters:**

- query: string. Free-text search query

- type: string. String containing classification type

**Sample request:**

```bash
curl -sS \
  -X POST "https://api.clarivate.com/patents/derwent/class-search" \
  -H "Content-Type: application/json" \
  -H "X-ApiKey: $(x-apikey)" \
  -d '{
    "params": [
      {
        "query": "ti=neem",
        "type": "ipc8"
      }
    ]
  }'
```

**Sample response:**

```json
[
  {
    "duration": "40",
    "classificationresponse": {
      "searched": 0,
      "total": 2,
      "classdescription": [
        {
          "classes": "A61K003658",
          "level": 0,
          "child_count": 0,
          "value": "Meliaceae (Chinaberry or Mahogany family), e.g. Azadirachta (neem)"
        },
        {
          "classes": "A01N006526",
          "level": 0,
          "child_count": 0,
          "value": "Meliaceae [Chinaberry or Mahogany family], e.g. mahogany, langsat or neem"
        }
      ]
    }
  }
]
```

[⬆ Back to Top](#table-of-contents)

---

### POST /patents/derwent/corporate-tree

Find where an assignee fit in the corporate hierarchy and look up entities within a corporate hierarchy by assignee code or name, supporting more precise assignee-based searches where an applicant operates under multiple related entities.

**Request parameters:**

- code: string. String containing assignee code

- terms: string. String containing assignee terms

**Sample request:**

```bash
curl -sS \
  -X POST "https://api.clarivate.com/patents/derwent/corporate-tree" \
  -H "Content-Type: application/json" \
  -H "X-ApiKey: $(x-apikey)" \
  -d '{
    "params": [
      {
        "code": "ARCO",
        "terms": "Microsot"
      }
    ]
  }'
```

**Sample response:**

```json
[
  {
    "duration": "165",
    "corporateTreeResponse": {
      "corporationDescription": [
        {
          "code": "ARCO",
          "level": 0,
          "docCount": 0,
          "title": {
            "value": "ARCO"
          },
          "spellings": {
            "spelling": [
              {
                "mapid": "-1",
                "value": "ARCO"
              }
            ]
          }
        }
      ]
    }
  }
]
```

[⬆ Back to Top](#table-of-contents)

---

### POST /patents/derwent/documents-IdMapping

[⬆ Back to Top](#table-of-contents)

---

## Support

Send [Email](mailto:Derwent.support@clarivate.com) to us if you have any feedback.

---

## Terms of service

[Terms of service](https://clarivate.com/legal-center/terms-of-business/product-service-terms/)

<p align="center"><a href="#table-of-contents">⬆ Back to Top</a></p>

---