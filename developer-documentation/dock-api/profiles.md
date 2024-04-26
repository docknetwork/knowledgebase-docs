# Profiles

Organization Profiles are used to provide more context for an Issuer DID. Details about the issuer such as name and logo can be added using a Organization Profile. These details will be included in credentials that are issued by the DID.

## Endpoints

[POST /profiles](profiles.md#create-profile)\
[GET /profiles/{did}](profiles.md#get-profile)\
[GET /profiles](profiles.md#list-profiles)\
[PATCH /profiles/{did}](profiles.md#update-profile)\
[DELETE /profiles/{did}](profiles.md#delete-profile)

## Create Profile

The `did` and `name` fields are required to create a new Profile.

### Parameters <a href="#create-profile-parameters" id="create-profile-parameters"></a>

<table data-full-width="false"><thead><tr><th width="133">Name</th><th width="84">In</th><th width="120">Type</th><th width="100">Required</th><th>Description</th></tr></thead><tbody><tr><td>did</td><td>body</td><td><a href="index.html.md#schemadiddock">DIDDock</a></td><td>true</td><td>DID as fully qualified, e.g., <code>did:dock:</code>.</td></tr><tr><td>name</td><td>body</td><td>string</td><td>true</td><td>The name to use for this issuer (e.g. a school name).</td></tr><tr><td>description</td><td>body</td><td>string</td><td>false</td><td>A description of the issuer.</td></tr><tr><td>logo</td><td>body</td><td>string</td><td>false</td><td>A Base64 encoded image to use as the logo for the issuer.</td></tr></tbody></table>

### Responses <a href="#create-profile-responses" id="create-profile-responses"></a>

<table data-full-width="false"><thead><tr><th width="114">Status</th><th width="138">Meaning</th><th width="341">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and the Profile was created.</td><td></td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>The request was unsuccessful, because of invalid params.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>POST /profiles REQUEST PAYLOAD</summary>

```json
{
  "did": "did:dock:xyz",
  "name": "My Test Profile",
  "description": "Testing out the Organization Profiles API",
  "logo":"data:image/png;base64,SomeBase64EncodedImage=="
}
```

</details>

<details>

<summary>POST /profiles REQUEST CURL</summary>

```bash
curl --location --request POST 'https://api.dock.io/profiles' \
--header 'DOCK-API-TOKEN: API_KEY' \
--data-raw '{
  "name": "My Test Profile",
  "did": "did:dock:xyz",
  "description": "Testing out the Organization Profiles API",
  "logo":"data:image/png;base64,SomeBase64EncodedImage=="
}'
```

</details>

<details>

<summary>200 Response</summary>

```json
{
  "did": "did:dock:xyz",
  "name": "My Test Profile",
  "description": "Testing out the Organization Profiles API",
  "logo":"data:image/png;base64,SomeBase64EncodedImage=="
}
```

</details>

## Get Profile

When a DID is provided in the path, the API will retrieve the Profile associated with that DID.

### Parameters <a href="#get-profile-parameters" id="get-profile-parameters"></a>

<table data-full-width="false"><thead><tr><th width="100">Name</th><th width="73">In</th><th width="102">Type</th><th width="109">Required</th><th>Description</th></tr></thead><tbody><tr><td>did</td><td>path</td><td><a href="index.html.md#schemadiddock">DIDDock</a></td><td>true</td><td>Represents a specific DID that uniquely identifies the profile.</td></tr></tbody></table>

### Responses <a href="#get-profile-responses" id="get-profile-responses"></a>

<table data-full-width="false"><thead><tr><th width="112">Status</th><th width="122">Meaning</th><th width="335">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will return the profile.</td><td></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>The requested profile was not found.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>GET /profiles/{did} REQUEST CURL</summary>

```bash
curl --location --request GET 'https://api.dock.io/profiles/did:dock:xyz' \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''

```

</details>

<details>

<summary>200 Response</summary>

```json
{
  "did": "did:dock:xyz",
  "name": "My Test Profile",
  "description": "Testing out the Organization Profiles API",
  "logo":"data:image/png;base64,SomeBase64EncodedImage=="
}
```

</details>

## List Profiles

Return a list of all Profiles that your user account controls.

### Parameters <a href="#list-profiles-parameters" id="list-profiles-parameters"></a>

<table data-full-width="false"><thead><tr><th width="110">Name</th><th width="79">In</th><th width="100">Type</th><th width="109">Required</th><th>Description</th></tr></thead><tbody><tr><td>offset</td><td>query</td><td>integer</td><td>false</td><td>How many items to offset by for pagination</td></tr><tr><td>limit</td><td>query</td><td>integer</td><td>false</td><td>How many items to return at one time (max 64)</td></tr></tbody></table>

### Responses <a href="#list-profiles-responses" id="list-profiles-responses"></a>

<table data-full-width="false"><thead><tr><th width="102">Status</th><th width="97">Meaning</th><th width="357">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>All of a user's profiles.</td><td><a href="index.html.md#schemadiddoc">DIDDock</a></td></tr></tbody></table>

<details>

<summary>GET /profiles REQUEST CURL</summary>

```bash
curl --location --request GET 'https://api.dock.io/profiles' \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''

```

</details>

<details>

<summary>200 Response</summary>

```json
[
  {
    "did": "did:dock:xyz",
    "name": "My Test Profile",
    "description": "Testing out the Organization Profiles API",
    "logo":"data:image/png;base64,SomeBase64EncodedImage=="
  }
]
```

</details>

## Update Profile

The update profile operation means that you can update the details of the profile. To do so, you need to provide a different value for **at least** one of `name`, `description` or `logo`.

### Parameters <a href="#update-profile-parameters" id="update-profile-parameters"></a>

<table data-full-width="false"><thead><tr><th width="132">Name</th><th width="93">In</th><th width="102">Type</th><th width="100">Required</th><th>Description</th></tr></thead><tbody><tr><td>did</td><td>body</td><td><a href="index.html.md#schemadiddock">DIDDock</a></td><td>true</td><td>DID as fully qualified, e.g., <code>did:dock:</code>.</td></tr><tr><td>name</td><td>body</td><td>string</td><td>true</td><td>The name to use for this issuer (e.g. a school name).</td></tr><tr><td>description</td><td>body</td><td>string</td><td>false</td><td>A description of the issuer.</td></tr><tr><td>logo</td><td>body</td><td>string</td><td>false</td><td>A Base64 encoded image to use as the logo for the issuer.</td></tr></tbody></table>

### Responses <a href="#update-profile-responses" id="update-profile-responses"></a>

<table data-full-width="false"><thead><tr><th width="107">Status</th><th width="153">Meaning</th><th width="331">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will update the profile.</td><td></td></tr><tr><td>400</td><td><a href="https://datatracker.ietf.org/doc/html/rfc7231#section-6.5.1">Bad Request</a></td><td>The controller value is incorrect.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>401</td><td><a href="https://tools.ietf.org/html/rfc7235#section-3.1">Unauthorized</a></td><td>The request was unsuccessful, because you don't own the profile.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>The profile does not exist.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>PATCH /profiles/{did} REQUEST PAYLOAD</summary>

```json
{
  "did": "did:dock:xyz",
  "name": "My Test Profile",
  "description": "Testing out the Organization Profiles API",
  "logo":"data:image/png;base64,SomeBase64EncodedImage=="
}
```

</details>

<details>

<summary>PATCH /profiles/{did} REQUEST CURL</summary>

```bash
curl --location --request PATCH 'https://api.dock.io/profiles/did:dock:xyz' \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw '{
  "did": "did:dock:xyz",
  "name": "My Test Profile",
  "description": "Testing out the Organization Profiles API",
  "logo":"data:image/png;base64,SomeBase64EncodedImage=="
}'

```

</details>

<details>

<summary>200 Response</summary>

```json
{
  "did": "did:dock:xyz",
  "name": "My Test Profile",
  "description": "Testing out the Organization Profiles API",
  "logo":"data:image/png;base64,SomeBase64EncodedImage=="
}
```

</details>

## Delete Profile

Deletes a profile from our platform. It does NOT delete the associated DID, nor revoke the credentials issued for the profile.

### Parameters <a href="#delete-profile-parameters" id="delete-profile-parameters"></a>

<table data-full-width="false"><thead><tr><th width="98">Name</th><th width="81">In</th><th width="87">Type</th><th width="105">Required</th><th>Description</th></tr></thead><tbody><tr><td>did</td><td>path</td><td><a href="index.html.md#schemadiddock">DID</a></td><td>true</td><td>Represents a specific DID that uniquely identifies the profile to delete.</td></tr></tbody></table>

### Responses <a href="#delete-profile-responses" id="delete-profile-responses"></a>

<table data-full-width="false"><thead><tr><th width="109">Status</th><th width="150">Meaning</th><th width="312">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will remove the profile.</td><td></td></tr><tr><td>401</td><td><a href="https://tools.ietf.org/html/rfc7235#section-3.1">Unauthorized</a></td><td>The request was unsuccessful because you don't own the profile.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>The profile does not exist.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>405</td><td><a href="https://datatracker.ietf.org/doc/html/rfc7231#section-6.5.5">Method not Allowed</a></td><td>The {did} value is blank/empty. Please ensure that the {did} value does exist.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>DELETE /profiles/{did} REQUEST CURL</summary>

```bash
curl --location --request DELETE https://api.dock.io/profiles/{did} \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw '{
    }'

```

</details>

<details>

<summary>200 Response</summary>

```json
{
}
```

</details>
