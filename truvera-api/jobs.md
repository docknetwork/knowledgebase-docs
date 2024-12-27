# Jobs

In Truvera, "jobs" are blockchain transactions that we submit on your behalf. You can choose to either register a webhook or poll the API to receive job information. Certain things in the API, such as revoking a credential, require a blockchain transaction to finalize before the job can be considered "done". The time to wait varies on network load and other factors, but typically is within 5-10 seconds.

You can track the current job status by querying the job id returned as part of the initial API response that triggered the job. The work is done asynchronously.

## Get Job Status and Data

To check the Job status and data, you can use the `GET` method and simply put the Job id. It will return information related to the job being processed and its associated blockchain transaction. On completion or failure, the job data will be updated with a response from the blockchain.

### Parameters <a href="#get-job-status-and-data-parameters" id="get-job-status-and-data-parameters"></a>

<table data-full-width="false"><thead><tr><th width="125">Name</th><th width="109">In</th><th width="103">Type</th><th width="128">Required</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>path</td><td><a href="../developer-documentation/dock-api/index.html.md#schemajobid">JobId</a></td><td>true</td><td>Represents a Job id.</td></tr></tbody></table>

{% swagger src="https://swagger-api.truvera.io/openapi.yaml" path="/jobs/{id}" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endswagger %}
