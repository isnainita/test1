# [TEST] API Doc

# API Documentation

## Overview

This **API Documentation** provides a streamlined workflow for uploading datasets, performing automated statistical analysis, and retrieving processed output files. It is designed to enable development teams to implement these into applications through RESTful endpoints.

The API supports **three major** operations:
1. **Upload** a data file (CSV or JSON)
2. **Analyze** the uploaded dataset using built-in statistical computation
3. **Download** the generated analysis results

All responses are returned in JSON.

---

## Authentication

All endpoints require an API key:

```
X-API-Key: [API_KEY]
```

Requests without a valid key return **`401 Unauthorized`**.

---

## Endpoints

### 1. POST /upload

Upload a dataset for analysis.

to the DataAnalyzer system.

**Description**

Accepts a base64-encoded file. Supported: `.csv`  or `.json`

**Headers**

```
Content-Type: application/json
X-API-Key: [API_KEY]
```

**Request Body**

| Parameter | Description | Data Type | Example |
| --- | --- | --- | --- |
| fileName | Name of the uploaded file | string | "sales_report_q3.csv" |
| fileContentBase64 | File encoded in Base64 | string | "cHJvZHVjdCwgcHJpY2UsIHN0b2NrCg0K..." |

sample request:

```json
{  "fileName": "sales_report_q3.csv",  "fileContentBase64": "cHJvZHVjdCwgcHJpY2UsIHN0b2NrCg0K..."}
```

**Success Response (201 Created)**

```json
{  "uploadId": "upl_502fa8cd89",  "fileName": "sales_report_q3.csv",  "message": "File uploaded successfully."}
```

**Error Codes**

Some error codes you might encounter when hitting this API:

- 400 – Invalid or missing fields
- 401 – Unauthorized
- 413 – File too large
- 415 – Unsupported type
- 500 – Internal error

---

### 2. GET /analyze

Run the automated statistical analysis for an uploaded dataset.

**Descriptions**

Returns the results of the analysis or current progress.

**Headers**

```
X-API-Key: [API_KEY]
```

**Query Parameter**

- `uploadId` (required)

| Parameter | Description | Data Type | Example |
| --- | --- | --- | --- |
| uploadId | ID returned from the `/upload` endpoint | string | "upl_502fa8cd89" |

sample request:

```
GET /analyze?uploadId=upl_502fa8cd89
```

**Success Response (200 OK)**

completed:

```json
{  "analysisId": "anl_34dfac982b",  "status": "completed",  "summary": {    "rowCount": 850,    "columnCount": 12,    "missingValues": 27  },  "statistics": {    "mean": { "price": 34.2 },    "min": { "price": 5.0 },    "max": { "price": 199.0 }  }}
```

processing:

```json
{  "status": "processing",  "progress": "62%"}
```

**Error Codes**

Some error codes you might encounter when hitting this API:

- 400 – Invalid uploadId
- 401 – Unauthorized
- 404 – Upload not found
- 409 – Analysis already running
- 500 – Analysis failure

---

### 3. POST /download

Generate a downloadable analysis results file in CSV or JSON format.

**Description**

Creates a time-limited file download URL based on the analysis results.

**Headers**

```
Content-Type: application/json
X-API-Key: [API_KEY]
```

**Request Body Parameters**

| Parameter | Description | Data Type | Example |
| --- | --- | --- | --- |
| analysisId | ID of completed analysis | string | "anl_34dfac982b” |
| format | Desired output format (`csv` or `json`) | string | "csv” |

sample request:

```json
{  "analysisId": "anl_34dfac982b",  "format": "csv"}
```

**Success Response (200 OK)**

```json
{  "downloadUrl": "https://api.dataanalyzer.com/files/anl_34dfac982b.csv",  "format": "csv",  "expiresAt": "2025-02-15T16:00:00Z"}
```

### Error Codes

Some error codes you might encounter when hitting this API:

- 400 – Invalid analysisId or format
- 401 – Unauthorized
- 404 – Analysis not found
- 500 – Generation error

---

## Standard Error Format

```json
{  "error": {    "code": "INVALID_PARAMETER",    "message": "The field 'analysisId' is required.",    "details": {}  }}
```

---

## Notes & Preconditions

- Timestamps follow ISO 8601 (UTC).
- Maximum upload size: **25 MB**.
- All generated download URLs expire after a set time (automatically).
- Uploaded files and outputs are **temporary** and deleted after processing.