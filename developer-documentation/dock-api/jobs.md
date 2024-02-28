# Jobs

In Dock Certs, "jobs" are blockchain transactions that we submit on your behalf. You can choose to either register a webhook or poll the API to receive job information. Certain things in the API, such as revoking a credential, require a blockchain transaction to finalize before the job can be considered "done". The time to wait varies on network load and other factors, but typically is within 5-10 seconds.

You can track the current job status by querying the job id returned as part of the initial API response that triggered the job. The work is done asynchronously.

## Endpoints

[GET /jobs/{Id}](index.html.md#get-job-status-and-data-parameters)\\

## Get Job Status and Data

To check the Job status and data, you can use the `GET` method and simply put the Job id. It will return information related to the job being processed and its associated blockchain transaction. On completion or failure, the job data will be updated with a response from the blockchain.

### Parameters <a href="#get-job-status-and-data-parameters" id="get-job-status-and-data-parameters"></a>

<table><thead><tr><th width="125">Name</th><th width="109">In</th><th width="103">Type</th><th width="128">Required</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>path</td><td><a href="index.html.md#schemajobid">JobId</a></td><td>true</td><td>Represents a Job id.</td></tr></tbody></table>

> GET /jobs/{Id} REQUEST

```shell
curl --location --request GET https://api.dock.io/jobs/{id} \
  --header 'DOCK-API-TOKEN: API_KEY'

```

### Responses <a href="#get-job-status-and-data-responses" id="get-job-status-and-data-responses"></a>

<table><thead><tr><th width="121">Status</th><th width="169">Meaning</th><th width="277">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and return the job description.</td><td><a href="index.html.md#schemajobdesc">JobDesc</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>The request was unsuccessful, because the Job id was not found.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

> 200 Response

```json
{
  "id": "123",
  "result": {
    "InBlock": "0x00"
  },
  "status": "finalized"
}
```
