# Jobs

In Truvera, API calls which depend on external systems may spawn jobs whose status can be queried until they complete. Examples include blockchain operations that we submit on your behalf and credential issuance via email. For instance, revoking a credential may require a blockchain transaction to finalize. This typically takes 5-10 seconds, depending on network load and other factors.

When an API call triggers a job, the response will contain a job ID that can be sent to this endpoint to track the job's status. [Like other asynchronous operations](getting-started.md#asynchronous-responses), you can receive job information either by polling the API or registering a webhook.

## Get job status and data

To check the job status and data, you can use the `GET` method and simply put the job ID. It will return information related to the job being processed and its associated blockchain transaction. On completion or failure, the job data will be updated with a response from the blockchain.

### Parameters <a href="#get-job-status-and-data-parameters" id="get-job-status-and-data-parameters"></a>

<table data-full-width="false"><thead><tr><th width="125">Name</th><th width="109">In</th><th width="103">Type</th><th width="128">Required</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>path</td><td><a href="../developer-documentation/dock-api/index.html.md#schemajobid">JobId</a></td><td>true</td><td>Represents a Job id.</td></tr></tbody></table>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/jobs/{id}" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}
