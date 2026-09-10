# Clarivate Derwent Patent API

Derwent Patent API provides seamless access to enriched patent data, enabling users to enhance their research capabilities and make faster, more informed decisions.

## Table of Contents

- [Getting Started](#getting-started)
- [Base URL](#base-url)
- [Authentication](#authentication)
- [Error Handling](#error-handling)
- [Rate Limits](#rate-limits)
- [Endpoints](#endpoints)
  - [POST /patents/derwent/search-by-query](#post-patentsderwentsearch-by-query)
  - [POST /patents/derwent/search-by-ids](#post-patentsderwentsearch-by-ids)
  - [POST /patents/derwent/search-by-pns](#post-patentsderwentsearch-by-pns)
  - [POST /patents/derwent/documents-by-id](#post-patentsderwentdocuments-by-id)
  - [POST /patents/derwent/documents-by-pn](#post-patentsderwentdocuments-by-pn)
  - [POST /patents/derwent/documents-by-listref](#post-patentsderwentdocuments-by-listref)
  - [POST /patents/derwent/combined-search](#post-patentsderwentcombined-search)
  - [POST /patents/derwent/class-browse](#post-patentsderwentclass-browse)
  - [POST /patents/derwent/class-search](#post-patentsderwentclass-search)
  - [POST /patents/derwent/corporate-tree](#post-patentsderwentcorporate-tree)
- [Pagination](#pagination)
- [Changelog](#changelog)
- [Support](#support)
- [License](#license)

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

## Rate Limits

_TODO: Add content_

[⬆ Back to Top](#table-of-contents)

---

## Endpoints

### POST /patents/derwent/search-by-query

Perform a search using query

**Request parameters:**

- query: string. Free-text search query

- listref: string. String obtained from search response. Either query or listref can be used in this endpoint

- collections: string. String containing one or more collections separated by comma(”,”)

- return-fields: string. String containing one or more return-fields separated by comma(”,”)

**Sample request:**

```bash
curl -sS \
  -X POST "httpS://api.clarivate.com/patents/derwent/search-by-query" \
  -H "Content-Type: application/json" \
  -H "X-ApiKey: $(x-apikey)" \
  -d '{
    "params": [
      {
        "query": "ti=science",
        "collections": "usapps,usgrants",
        "return-fields": "pn,pd"
      }
    ]
  }'
```

**Sample response:**

```json
{
  "header": {
    "duration": "281",
    "searched": 177324912,
    "found": "3536",
    "size": 3536
  },
  "body": [
    {
      "id": "US12424223B220250923",
      "rank": 2,
      "field": [
        {
          "name": "pn",
          "form": "orig",
          "value": "US12424223B2"
        },
        {
          "name": "pd",
          "form": "orig",
          "value": "2025-09-23"
        }
      ]
    },
    {
      "id": "US12423568B220250923",
      "rank": 2,
      "field": [
        {
          "name": "pn",
          "form": "orig",
          "value": "US12423568B2"
        },
        {
          "name": "pd",
          "form": "orig",
          "value": "2025-09-23"
        }
      ]
    },
    {
      "id": "US12417017B220250916",
      "rank": 2,
      "field": [
        {
          "name": "pn",
          "form": "orig",
          "value": "US12417017B2"
        },
        {
          "name": "pd",
          "form": "orig",
          "value": "2025-09-16"
        }
      ]
    },
    {
      "id": "US12416797B220250916",
      "rank": 2,
      "field": [
        {
          "name": "pn",
          "form": "orig",
          "value": "US12416797B2"
        },
        {
          "name": "pd",
          "form": "orig",
          "value": "2025-09-16"
        }
      ]
    },
    {
      "id": "US12412036B220250909",
      "rank": 2,
      "field": [
        {
          "name": "pn",
          "form": "orig",
          "value": "US12412036B2"
        },
        {
          "name": "pd",
          "form": "orig",
          "value": "2025-09-09"
        }
      ]
    },
    {
      "id": "US12411468B220250909",
      "rank": 2,
      "field": [
        {
          "name": "pn",
          "form": "orig",
          "value": "US12411468B2"
        },
        {
          "name": "pd",
          "form": "orig",
          "value": "2025-09-09"
        }
      ]
    },
    {
      "id": "US12411466B220250909",
      "rank": 2,
      "field": [
        {
          "name": "pn",
          "form": "orig",
          "value": "US12411466B2"
        },
        {
          "name": "pd",
          "form": "orig",
          "value": "2025-09-09"
        }
      ]
    },
    {
      "id": "US12406653B220250902",
      "rank": 2,
      "field": [
        {
          "name": "pn",
          "form": "orig",
          "value": "US12406653B2"
        },
        {
          "name": "pd",
          "form": "orig",
          "value": "2025-09-02"
        }
      ]
    },
    {
      "id": "US12405779B220250902",
      "rank": 1,
      "field": [
        {
          "name": "pn",
          "form": "orig",
          "value": "US12405779B2"
        },
        {
          "name": "pd",
          "form": "orig",
          "value": "2025-09-02"
        }
      ]
    },
    {
      "id": "US12393709B220250819",
      "rank": 2,
      "field": [
        {
          "name": "pn",
          "form": "orig",
          "value": "US12393709B2"
        },
        {
          "name": "pd",
          "form": "orig",
          "value": "2025-08-19"
        }
      ]
    }
  ]
}
```

[⬆ Back to Top](#table-of-contents)

---

### POST /patents/derwent/search-by-ids

Perform a search using document id(s)

**Request parameters:**

- ids: string. String containing one or more document ids separated by comma(”,”)

- collections: string. String containing one or more collections separated by comma(”,”)

**Sample request:**

```bash
curl -sS \
  -X POST "httpS://api.clarivate.com/patents/derwent/search-by-ids" \
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

Perform a search using publication number(s)

**Request parameters:**

- pns: string. String containing one or more publication numbers separated by comma(”,”)

- collections: string. String containing one or more collections separated by comma(”,”)

**Sample request:**

```bash
curl -sS \
  -X POST "httpS://api.clarivate.com/patents/derwent/search-by-pns" \
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

### POST /patents/derwent/documents-by-id

Retrieve a document using document id(s)

**Request parameters:**

- ids: string. String containing one or more document ids separated by comma(”,”)

- collections: string. String containing one or more collections separated by comma(”,”)

**Sample request:**

```bash
curl -sS \
  -X POST "httpS://api.clarivate.com/patents/derwent/documents-by-id" \
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

Retrieve a document using publication number(s)

**Request parameters:**

- pns: string. String containing one or more publication numbers separated by comma(”,”)

- collections: string. String containing one or more collections separated by comma(”,”)

**Sample request:**

```bash
curl -sS \
  -X POST "httpS://api.clarivate.com/patents/derwent/documents-by-pn" \
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

Retrieve a document using listref obtained from the search request

**Request parameters:**

- listref: string. String obtained from the search request

- collections: string. String containing one or more collections separated by comma(”,”)

**Sample request:**

```bash
curl -sS \
  -X POST "httpS://api.clarivate.com/patents/derwent/documents-by-listref" \
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

### POST /patents/derwent/combined-search

Perform a combined search using two or more query

**Request parameters:**

- query: string. Free-text search query. query\\query_number\\ with search_field=search_value

- combination: string. String containing combination condition of queries. Example: "combination": "\\1 and \\2”

- collections: string. collections\\number\\ → a string of collection or comma separated string of multiple collections

**Sample request:**

```bash
curl -sS \
  -X POST "httpS://api.clarivate.com/patents/derwent/combined-search" \
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

### POST /patents/derwent/class-browse

Browse classification databases using class levels and hierarchies

**Request parameters:**

- class-levels: Integer. A numeric value that denotes class level

- classes: string. String containing one or more classification codes that need to be browsed upon

- type: string. String containing classification type

**Sample request:**

```bash
curl -sS \
  -X POST "httpS://api.clarivate.com/patents/derwent/class-browse" \
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

Search classification databases using query and classification type

**Request parameters:**

- query: string. Free-text search query

- type: string. String containing classification type

**Sample request:**

```bash
curl -sS \
  -X POST "httpS://api.clarivate.com/patents/derwent/class-search" \
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

Search corporate hierarchy for the assignees using code or terms

**Request parameters:**

- code: string. String containing assignee code

- terms: string. String containing assignee terms

**Sample request:**

```bash
curl -sS \
  -X POST "httpS://api.clarivate.com/patents/derwent/corporate-tree" \
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

## Pagination

_TODO: Add content_

[⬆ Back to Top](#table-of-contents)

---

## Changelog

_TODO: Add content_

[⬆ Back to Top](#table-of-contents)

---

## Support

_TODO: Add content_

[⬆ Back to Top](#table-of-contents)

---

## License

_TODO: Add content_

[⬆ Back to Top](#table-of-contents)

---