# Trust registry JSON-RPC API

## Methods

[trustRegistry\_schemaMetadata](JSON-RPC.md#method-trustregistry_schemametadata)

[trustRegistry\_schemaIssuers](JSON-RPC.md#method-trustregistry_schemaissuers)

[trustRegistry\_schemaVerifiers](JSON-RPC.md#method-trustregistry_schemaverifiers)

[trustRegistry\_schemaMetadataInRegistry](JSON-RPC.md#method-trustregistry_schemametadatainregistry)

[trustRegistry\_schemaIssuersInRegistry](JSON-RPC.md#method-trustregistry_schemaissuersinregistry)

[trustRegistry\_schemaVerifiersInRegistry](JSON-RPC.md#method-trustregistry_schemaverifiersinregistry)

[trustRegistry\_allRegistrySchemaMetadata](JSON-RPC.md#method-trustregistry_allregistryschemaverifiers)

[trustRegistry\_allRegistrySchemaIssuers](JSON-RPC.md#method-trustregistry_allregistryschemaissuers)

[trustRegistry\_allRegistrySchemaVerifiers](JSON-RPC.md#method-trustregistry_allregistryschemaverifiers)

[trustRegistry\_registriesInfoBy](JSON-RPC.md#method-trustregistry_registriesinfoby)

[trustRegistry\_registrySchemaMetadataBy](JSON-RPC.md#method-trustregistry_registryschemametadataby)

## Method: `trustRegistry_schemaMetadata`

### Description

This method retrieves metadata for a trust registry schema identified by the provided schema ID, optionally filtered by block hash.

### Parameters

* `id`: `TrustRegistrySchemaId` - The unique identifier of the trust registry schema for which to retrieve metadata.
* `at`: `Option<BlockHash>` - Optional block hash to query the metadata at a specific point in the blockchain.

### Return type

`{ TrustRegistryId, AggregatedTrustRegistrySchemaMetadata }` Returns a dictionary where each key is a TrustRegistryId and the corresponding value is AggregatedTrustRegistrySchemaMetadata associated with that schema.

### Example request

```bash
curl -X POST -H "Content-Type: application/json" -d '{
    "jsonrpc": "2.0",
    "method": "trustRegistry_schemaMetadata",
    "params": [
        "0x9ef236a84164f99a80e832d6e3c212908f59ed0baa069898205db3762751235c"
    ],
    "id": 1
}' http://localhost:9933
```

### Example response

```jsx
{
  "0x46da29a5412d39c98f956ab6ae289311eec782d9f426110f41945bc64fe2c96c": {
    "issuers": [
      [
        {
          "did": "0x054a1d26f736c727c4a5dfcaa89193fa169cecae7f1daeb9f80103598d280020"
        },
        {
          "verificationPrices": {
            "DOCK": 10000000
          },
          "suspended": false,
          "delegated": []
        }
      ],
      [
        {
          "did": "0xa7fdcd52cfe8de3fea13bd41a7fcf37ce8f8744065965070b284b008ab128903"
        },
        {
          "verificationPrices": {
            "DOCK": 10000000
          },
          "suspended": false,
          "delegated": []
        }
      ]
    ],
    "verifiers": [
      {
        "did": "0x00b3aee1a65251e77cb21428150b55e71dc67110098f8a6934f593536b95f0e3"
      },
      {
        "did": "0x654084fd61a3f7655f03bd0b208d57ce5eff159d1fac40f9a0364b9eec782c2f"
      },
      {
        "didMethodKey": {
          "ed25519": "0x5285836546cf62b9e148663f33c08c75763011eabc11cc76f6ac97ec758516c3"
        }
      }
    ]
  },
  "0xdf081ea7a27d9bb1fdba8c21046fc9d30d7cfe9bd87096c5917bd08a17e245b6": {
    "issuers": [
      [
        {
          "did": "0x054a1d26f736c727c4a5dfcaa89193fa169cecae7f1daeb9f80103598d280020"
        },
        {
          "verificationPrices": {
            "DOCK": 10000000
          },
          "suspended": false,
          "delegated": []
        }
      ],
      [
        {
          "did": "0xa7fdcd52cfe8de3fea13bd41a7fcf37ce8f8744065965070b284b008ab128903"
        },
        {
          "verificationPrices": {
            "DOCK": 10000000
          },
          "suspended": false,
          "delegated": []
        }
      ]
    ],
    "verifiers": [
      {
        "did": "0x00b3aee1a65251e77cb21428150b55e71dc67110098f8a6934f593536b95f0e3"
      },
      {
        "did": "0x654084fd61a3f7655f03bd0b208d57ce5eff159d1fac40f9a0364b9eec782c2f"
      }
    ]
  }
}
```

## Method: `trustRegistry_schemaIssuers`

### Description

This method retrieves information about the issuers of a trust registry schema identified by the provided schema ID, optionally filtered by block hash.

### Parameters

* `id`: `TrustRegistrySchemaId` - The unique identifier of the trust registry schema for which to retrieve issuer information.
* `at`: `Option<BlockHash>` - Optional block hash to query the issuer information at a specific point in the blockchain.

### Return type

`{ TrustRegistryId, AggregatedTrustRegistrySchemaIssuers<T::T> }` Returns a dictionary where each key is a TrustRegistryId and the corresponding value is AggregatedTrustRegistrySchemaIssuers associated with that schema.

### Example request

```bash
curl -X POST -H "Content-Type: application/json" -d '{
    "jsonrpc": "2.0",
    "method": "trustRegistry_schemaIssuers",
    "params": [
        "0x9ef236a84164f99a80e832d6e3c212908f59ed0baa069898205db3762751235c"
    ],
    "id": 1
}' http://localhost:9933
```

### Example response

```jsx
{
  "0x46da29a5412d39c98f956ab6ae289311eec782d9f426110f41945bc64fe2c96c": [
    [
      {
        "did": "0x054a1d26f736c727c4a5dfcaa89193fa169cecae7f1daeb9f80103598d280020"
      },
      {
        "verificationPrices": {
          "DOCK": 10000000
        },
        "suspended": false,
        "delegated": []
      }
    ],
    [
      {
        "did": "0xa7fdcd52cfe8de3fea13bd41a7fcf37ce8f8744065965070b284b008ab128903"
      },
      {
        "verificationPrices": {
          "DOCK": 10000000
        },
        "suspended": false,
        "delegated": []
      }
    ]
  ],
  "0xdf081ea7a27d9bb1fdba8c21046fc9d30d7cfe9bd87096c5917bd08a17e245b6": [
    [
      {
        "did": "0x054a1d26f736c727c4a5dfcaa89193fa169cecae7f1daeb9f80103598d280020"
      },
      {
        "verificationPrices": {
          "DOCK": 10000000
        },
        "suspended": false,
        "delegated": []
      }
    ],
    [
      {
        "did": "0xa7fdcd52cfe8de3fea13bd41a7fcf37ce8f8744065965070b284b008ab128903"
      },
      {
        "verificationPrices": {
          "DOCK": 10000000
        },
        "suspended": false,
        "delegated": []
      }
    ]
  ]
}
```

## Method: `trustRegistry_schemaVerifiers`

### Description

This method retrieves information about the verifiers of a trust registry schema identified by the provided schema ID, optionally filtered by block hash.

### Parameters

* `id`: `TrustRegistrySchemaId` - The unique identifier of the trust registry schema for which to retrieve verifier information.
* `at`: `Option<BlockHash>` - Optional block hash to query the issuer information at a specific point in the blockchain.

### Return type

`{ TrustRegistryId, AggregatedTrustRegistrySchemaIssuers<T::T> }` Returns a dictionary where each key is a TrustRegistryId and the corresponding value is TrustRegistrySchemaVerifiers associated with that schema.

### Example request

```bash
curl -X POST -H "Content-Type: application/json" -d '{
    "jsonrpc": "2.0",
    "method": "trustRegistry_schemaVerifiers",
    "params": [
        "0x9ef236a84164f99a80e832d6e3c212908f59ed0baa069898205db3762751235c"
    ],
    "id": 1
}' http://localhost:9933
```

### Example response

```jsx
{
  "0x46da29a5412d39c98f956ab6ae289311eec782d9f426110f41945bc64fe2c96c": [
    {
      "did": "0x00b3aee1a65251e77cb21428150b55e71dc67110098f8a6934f593536b95f0e3"
    },
    {
      "did": "0x654084fd61a3f7655f03bd0b208d57ce5eff159d1fac40f9a0364b9eec782c2f"
    },
    {
      "didMethodKey": {
        "ed25519": "0x5285836546cf62b9e148663f33c08c75763011eabc11cc76f6ac97ec758516c3"
      }
    }
  ],
  "0xdf081ea7a27d9bb1fdba8c21046fc9d30d7cfe9bd87096c5917bd08a17e245b6": [
    {
      "did": "0x00b3aee1a65251e77cb21428150b55e71dc67110098f8a6934f593536b95f0e3"
    },
    {
      "did": "0x654084fd61a3f7655f03bd0b208d57ce5eff159d1fac40f9a0364b9eec782c2f"
    }
  ]
}
```

## Method: `trustRegistry_schemaMetadataInRegistry`

### Description

This method retrieves metadata for a trust registry schema identified by the provided schema ID within a specific trust registry, optionally filtered by block hash.

### Parameters

* `id`: `TrustRegistrySchemaId` - The unique identifier of the trust registry schema for which to retrieve metadata.
* `registry_id`: `TrustRegistryId` - The unique identifier of the trust registry within which to search for the schema metadata.
* `at`: `Option<BlockHash>` - Optional block hash to query the metadata at a specific point in the blockchain.

### Return type

`Option<AggregatedTrustRegistrySchemaMetadata>` If the schema metadata is found within the specified registry, it returns AggregatedTrustRegistrySchemaMetadata; otherwise, it returns null.

### Example request

```bash
curl -X POST -H "Content-Type: application/json" -d '{
    "jsonrpc": "2.0",
    "method": "trustRegistry_schemaMetadataInRegistry",
    "params": [
        "0x9ef236a84164f99a80e832d6e3c212908f59ed0baa069898205db3762751235c",
        "0xdf081ea7a27d9bb1fdba8c21046fc9d30d7cfe9bd87096c5917bd08a17e245b6"
    ],
    "id": 1
}' http://localhost:9933
```

### Example response

```jsx
{
  "issuers": [
    [
      {
        "did": "0x054a1d26f736c727c4a5dfcaa89193fa169cecae7f1daeb9f80103598d280020"
      },
      {
        "verificationPrices": {
          "DOCK": 10000000
        },
        "suspended": false,
        "delegated": []
      }
    ],
    [
      {
        "did": "0xa7fdcd52cfe8de3fea13bd41a7fcf37ce8f8744065965070b284b008ab128903"
      },
      {
        "verificationPrices": {
          "DOCK": 10000000
        },
        "suspended": false,
        "delegated": []
      }
    ]
  ],
  "verifiers": [
    {
      "did": "0x00b3aee1a65251e77cb21428150b55e71dc67110098f8a6934f593536b95f0e3"
    },
    {
      "did": "0x654084fd61a3f7655f03bd0b208d57ce5eff159d1fac40f9a0364b9eec782c2f"
    }
  ]
}
```

## Method: `trustRegistry_schemaIssuersInRegistry`

### Description

This method retrieves information about the issuers of a trust registry schema identified by the provided schema ID within a specific trust registry, optionally filtered by block hash.

### Parameters

* `id`: `TrustRegistrySchemaId` - The unique identifier of the trust registry schema for which to retrieve issuer information.
* `registry_id`: `TrustRegistryId` - The unique identifier of the trust registry within which to search for the schema issuers.
* `at`: `Option<BlockHash>` - Optional block hash to query the issuer information at a specific point in the blockchain.

### Return type

`Option<AggregatedTrustRegistrySchemaIssuers>` If the schema issuers are found within the specified registry, it returns AggregatedTrustRegistrySchemaIssuers; otherwise, it returns null.

### Example request

```bash
curl -X POST -H "Content-Type: application/json" -d '{
    "jsonrpc": "2.0",
    "method": "trustRegistry_schemaIssuersInRegistry",
    "params": [
        "0x9ef236a84164f99a80e832d6e3c212908f59ed0baa069898205db3762751235c",
        "0xdf081ea7a27d9bb1fdba8c21046fc9d30d7cfe9bd87096c5917bd08a17e245b6"
    ],
    "id": 1
}' http://localhost:9933
```

### Example response

```jsx
[
  [
    {
      "did": "0x054a1d26f736c727c4a5dfcaa89193fa169cecae7f1daeb9f80103598d280020"
    },
    {
      "verificationPrices": {
        "DOCK": 10000000
      },
      "suspended": false,
      "delegated": []
    }
  ],
  [
    {
      "did": "0xa7fdcd52cfe8de3fea13bd41a7fcf37ce8f8744065965070b284b008ab128903"
    },
    {
      "verificationPrices": {
        "DOCK": 10000000
      },
      "suspended": false,
      "delegated": []
    }
  ]
]
```

## Method: `trustRegistry_schemaVerifiersInRegistry`

### Description

This method retrieves information about the verifiers of a trust registry schema identified by the provided schema ID within a specific trust registry, optionally filtered by block hash.

### Parameters

* `id`: `TrustRegistrySchemaId` - The unique identifier of the trust registry schema for which to retrieve issuer information.
* `registry_id`: `TrustRegistryId` - The unique identifier of the trust registry within which to search for the schema verifiers.
* `at`: `Option<BlockHash>` - Optional block hash to query the issuer information at a specific point in the blockchain.

### Return type

`Option<TrustRegistrySchemaVerifiers>` If the schema issuers are found within the specified registry, it returns `TrustRegistrySchemaVerifiers`; otherwise, it returns null.

### Example request

```bash
curl -X POST -H "Content-Type: application/json" -d '{
    "jsonrpc": "2.0",
    "method": "trustRegistry_schemaVerifiersInRegistry",
    "params": [
        "0x9ef236a84164f99a80e832d6e3c212908f59ed0baa069898205db3762751235c",
        "0xdf081ea7a27d9bb1fdba8c21046fc9d30d7cfe9bd87096c5917bd08a17e245b6"
    ],
    "id": 1
}' http://localhost:9933
```

### Example response

```jsx
[
  {
    "did": "0x00b3aee1a65251e77cb21428150b55e71dc67110098f8a6934f593536b95f0e3"
  },
  {
    "did": "0x654084fd61a3f7655f03bd0b208d57ce5eff159d1fac40f9a0364b9eec782c2f"
  }
]
```

## Method: `trustRegistry_allRegistrySchemaMetadata`

### Description

This method retrieves metadata for all trust registry schemas within a specific trust registry, optionally filtered by block hash.

### Parameters

* `registry_id`: `TrustRegistryId` - The unique identifier of the trust registry for which to retrieve schema metadata.
* `at`: `Option<BlockHash>` - Optional block hash to query the metadata at a specific point in the blockchain.

### Return type

`{ TrustRegistrySchemaId => AggregatedTrustRegistrySchemaMetadata }` Returns a dictionary where each key is a TrustRegistrySchemaId and the corresponding value is AggregatedTrustRegistrySchemaMetadata associated with that schema within the specified registry.

### Example request

```bash
curl -X POST -H "Content-Type: application/json" -d '{
    "jsonrpc": "2.0",
    "method": "trustRegistry_allRegistrySchemaMetadata",
    "params": [
        "0xdf081ea7a27d9bb1fdba8c21046fc9d30d7cfe9bd87096c5917bd08a17e245b6"
    ],
    "id": 1
}' http://localhost:9933
```

### Example response

```jsx
{
  "0x9ef236a84164f99a80e832d6e3c212908f59ed0baa069898205db3762751235c": {
    "issuers": [
      [
        {
          "did": "0x054a1d26f736c727c4a5dfcaa89193fa169cecae7f1daeb9f80103598d280020"
        },
        {
          "verificationPrices": {
            "DOCK": 10000000
          },
          "suspended": false,
          "delegated": []
        }
      ],
      [
        {
          "did": "0xa7fdcd52cfe8de3fea13bd41a7fcf37ce8f8744065965070b284b008ab128903"
        },
        {
          "verificationPrices": {
            "DOCK": 10000000
          },
          "suspended": false,
          "delegated": []
        }
      ]
    ],
    "verifiers": [
      {
        "did": "0x00b3aee1a65251e77cb21428150b55e71dc67110098f8a6934f593536b95f0e3"
      },
      {
        "did": "0x654084fd61a3f7655f03bd0b208d57ce5eff159d1fac40f9a0364b9eec782c2f"
      }
    ]
  },
  "0xb20491944374c9ae375663616fbe11e8d9976190e180eb0bbf6cd64592f771e5": {
    "issuers": [
      [
        {
          "did": "0xa7fdcd52cfe8de3fea13bd41a7fcf37ce8f8744065965070b284b008ab128903"
        },
        {
          "verificationPrices": {
            "DOCK": 20000000
          },
          "suspended": false,
          "delegated": []
        }
      ]
    ],
    "verifiers": []
  }
}
```

## Method: `trustRegistry_allRegistrySchemaIssuers`

### Description

This method retrieves information about the issuers of all trust registry schemas within a specific trust registry, optionally filtered by block hash.

### Parameters

* `registry_id`: `TrustRegistryId` - The unique identifier of the trust registry for which to retrieve schema issuers.
* `at`: `Option<BlockHash>` - Optional block hash to query the issuer information at a specific point in the blockchain.

### Return type

`{ TrustRegistrySchemaId => AggregatedTrustRegistrySchemaIssuers }` Returns a dictionary where each key is a TrustRegistrySchemaId and the corresponding value is AggregatedTrustRegistrySchemaIssuers associated with that schema within the specified registry.

### Example request

```bash
curl -X POST -H "Content-Type: application/json" -d '{
    "jsonrpc": "2.0",
    "method": "trustRegistry_allRegistrySchemaIssuers",
    "params": [
        "0xdf081ea7a27d9bb1fdba8c21046fc9d30d7cfe9bd87096c5917bd08a17e245b6"
    ],
    "id": 1
}' http://localhost:9933
```

### Example response

```jsx
{
  "0x9ef236a84164f99a80e832d6e3c212908f59ed0baa069898205db3762751235c": [
    [
      {
        "did": "0x054a1d26f736c727c4a5dfcaa89193fa169cecae7f1daeb9f80103598d280020"
      },
      {
        "verificationPrices": {
          "DOCK": 10000000
        },
        "suspended": false,
        "delegated": []
      }
    ],
    [
      {
        "did": "0xa7fdcd52cfe8de3fea13bd41a7fcf37ce8f8744065965070b284b008ab128903"
      },
      {
        "verificationPrices": {
          "DOCK": 10000000
        },
        "suspended": false,
        "delegated": []
      }
    ]
  ],
  "0xb20491944374c9ae375663616fbe11e8d9976190e180eb0bbf6cd64592f771e5": [
    [
      {
        "did": "0xa7fdcd52cfe8de3fea13bd41a7fcf37ce8f8744065965070b284b008ab128903"
      },
      {
        "verificationPrices": {
          "DOCK": 20000000
        },
        "suspended": false,
        "delegated": []
      }
    ]
  ]
}
```

## Method: `trustRegistry_allRegistrySchemaVerifiers`

### Description

This method retrieves information about the verifiers of all trust registry schemas within a specific trust registry, optionally filtered by block hash.

### Parameters

* `registry_id`: `TrustRegistryId` - The unique identifier of the trust registry for which to retrieve schema verifiers.
* `at`: `Option<BlockHash>` - Optional block hash to query the verifier information at a specific point in the blockchain.

### Return type

`{ TrustRegistrySchemaId => TrustRegistrySchemaVerifiers }` Returns a dictionary where each key is a TrustRegistrySchemaId and the corresponding value is TrustRegistrySchemaVerifiers associated with that schema within the specified registry.

### Example request

```bash
curl -X POST -H "Content-Type: application/json" -d '{
    "jsonrpc": "2.0",
    "method": "trustRegistry_allRegistrySchemaVerifiers",
    "params": [
        "0xdf081ea7a27d9bb1fdba8c21046fc9d30d7cfe9bd87096c5917bd08a17e245b6"
    ],
    "id": 1
}' http://localhost:9933
```

### Example response

```jsx
{
  "0x9ef236a84164f99a80e832d6e3c212908f59ed0baa069898205db3762751235c": [
    {
      "did": "0x00b3aee1a65251e77cb21428150b55e71dc67110098f8a6934f593536b95f0e3"
    },
    {
      "did": "0x654084fd61a3f7655f03bd0b208d57ce5eff159d1fac40f9a0364b9eec782c2f"
    }
  ],
  "0xb20491944374c9ae375663616fbe11e8d9976190e180eb0bbf6cd64592f771e5": []
}
```

## Method: `trustRegistry_registriesInfoBy`

### Description

This method retrieves information about trust registries based on specified criteria, optionally filtered by block hash.

### Parameters

* `by`: `QueryTrustRegistriesBy` - Specifies the criteria by which to query trust registries.
* `at`: `Option<BlockHash>` - Optional block hash to query the information at a specific point in the blockchain.

### Return type

`{ TrustRegistryId, TrustRegistryInfo }` Returns a dictionary where each key is a TrustRegistryId and the corresponding value is TrustRegistryInfo associated with that registry.

### Example request

```bash
curl -X POST -H "Content-Type: application/json" -d '{
    "jsonrpc": "2.0",
    "method": "trustRegistry_registriesInfoBy",
    "params": [
        { "issuers": { "anyOf": [{ "did": "0x054a1d26f736c727c4a5dfcaa89193fa169cecae7f1daeb9f80103598d280020" }] } }
    ],
    "id": 1
}' http://localhost:9933
```

### Example response

```jsx
{
  "0x12a6a092361a6b419f92a6a9625597c7938cab98963d659f3a9fb31f2ae7b8f1": {
    "convener": {
      "did": "0x8c2afbf2338eec7112d923a318366de2395da2f57c46bf2ca0db454e72045fbb"
    },
    "name": "Test Registry",
    "govFramework": "0x476f76206672616d65776f726b"
  },
  "0x46da29a5412d39c98f956ab6ae289311eec782d9f426110f41945bc64fe2c96c": {
    "convener": {
      "did": "0x8c2afbf2338eec7112d923a318366de2395da2f57c46bf2ca0db454e72045fbb"
    },
    "name": "Test Registry 2",
    "govFramework": "0x476f76206672616d65776f726b"
  },
  "0x6559fe67a1869fd1f4c0cc3902caebd205eb2129c7c8e8ae38198aff439b1a19": {
    "convener": {
      "did": "0x8c2afbf2338eec7112d923a318366de2395da2f57c46bf2ca0db454e72045fbb"
    },
    "name": "Test Registry",
    "govFramework": "0x476f76206672616d65776f726b"
  },
  "0x7ee547102886dd9614bd317b6eb522c846f9227f265b15920b46dfe23b63cf29": {
    "convener": {
      "did": "0x8c2afbf2338eec7112d923a318366de2395da2f57c46bf2ca0db454e72045fbb"
    },
    "name": "Test Registry",
    "govFramework": "0x476f76206672616d65776f726b"
  },
  "0xbf778eca90a9976932dc53ea1af5594022c203152b31a19b52e15cc7057404bf": {
    "convener": {
      "did": "0x8c2afbf2338eec7112d923a318366de2395da2f57c46bf2ca0db454e72045fbb"
    },
    "name": "Test Registry",
    "govFramework": "0x476f76206672616d65776f726b"
  },
  "0xdf081ea7a27d9bb1fdba8c21046fc9d30d7cfe9bd87096c5917bd08a17e245b6": {
    "convener": {
      "did": "0x8c2afbf2338eec7112d923a318366de2395da2f57c46bf2ca0db454e72045fbb"
    },
    "name": "Test Registry",
    "govFramework": "0x476f76206672616d65776f726b"
  }
}
```

## Method: `trustRegistry_registrySchemaMetadataBy`

### Description

This method retrieves metadata for trust registry schemas based on specified parameters, such as the registry ID, and optionally filtered by block hash.

### Parameters

* `by`: `QueryTrustRegistryBy` - Specifies the criteria by which to query the trust registry schemas.
* `reg_id`: `TrustRegistryId` - The unique identifier of the trust registry for which to retrieve schema metadata.
* `at`: `Option<BlockHash>` - Optional block hash to query the metadata at a specific point in the blockchain.

### Return type

`{ TrustRegistrySchemaId => AggregatedTrustRegistrySchemaMetadata }` Returns a dictionary where each key is a TrustRegistrySchemaId and the corresponding value is AggregatedTrustRegistrySchemaMetadata associated with that schema.

### Example request

```bash
curl -X POST -H "Content-Type: application/json" -d '{
    "jsonrpc": "2.0",
    "method": "trustRegistry_registrySchemaMetadataBy",
    "params": [
        { "issuers": { "anyOf": [{ "did": "0x054a1d26f736c727c4a5dfcaa89193fa169cecae7f1daeb9f80103598d280020" }] } },
        "0xdf081ea7a27d9bb1fdba8c21046fc9d30d7cfe9bd87096c5917bd08a17e245b6"
    ],
    "id": 1
}' http://localhost:9933
```

### Example request

```jsx
{
  "0x9ef236a84164f99a80e832d6e3c212908f59ed0baa069898205db3762751235c": {
    "issuers": [
      [
        {
          "did": "0x054a1d26f736c727c4a5dfcaa89193fa169cecae7f1daeb9f80103598d280020"
        },
        {
          "verificationPrices": {
            "DOCK": 10000000
          },
          "suspended": false,
          "delegated": []
        }
      ],
      [
        {
          "did": "0xa7fdcd52cfe8de3fea13bd41a7fcf37ce8f8744065965070b284b008ab128903"
        },
        {
          "verificationPrices": {
            "DOCK": 10000000
          },
          "suspended": false,
          "delegated": []
        }
      ]
    ],
    "verifiers": [
      {
        "did": "0x00b3aee1a65251e77cb21428150b55e71dc67110098f8a6934f593536b95f0e3"
      },
      {
        "did": "0x654084fd61a3f7655f03bd0b208d57ce5eff159d1fac40f9a0364b9eec782c2f"
      }
    ]
  }
}
```

## Method: `trustRegistry_registriesIdsBy`

### Description

This method retrieves ids of trust registries based on specified parameters, and optionally filtered by block hash.

### Parameters

* `by`: `QueryTrustRegistriesBy` - Specifies the criteria by which to query the trust registry identifiers.
* `at`: `Option<BlockHash>` - Optional block hash to query the metadata at a specific point in the blockchain.

### Return type

`[TrustRegistryId]` Returns an array where each value is a TrustRegistrySchemaId.

### Example request

```bash
curl -X POST -H "Content-Type: application/json" -d '{
    "jsonrpc": "2.0",
    "method": "trustRegistry_registriesIdsBy",
    "params": [
        { "issuers": { "anyOf": [{ "did": "0x054a1d26f736c727c4a5dfcaa89193fa169cecae7f1daeb9f80103598d280020" }] } }
    ],
    "id": 1
}' http://localhost:9933
```

### Example response

```jsx
[
  "0x12a6a092361a6b419f92a6a9625597c7938cab98963d659f3a9fb31f2ae7b8f1",
  "0x46da29a5412d39c98f956ab6ae289311eec782d9f426110f41945bc64fe2c96c",
  "0x6559fe67a1869fd1f4c0cc3902caebd205eb2129c7c8e8ae38198aff439b1a19",
  "0x7ee547102886dd9614bd317b6eb522c846f9227f265b15920b46dfe23b63cf29",
  "0xbf778eca90a9976932dc53ea1af5594022c203152b31a19b52e15cc7057404bf",
  "0xdf081ea7a27d9bb1fdba8c21046fc9d30d7cfe9bd87096c5917bd08a17e245b6"
]
```

## Method: `trustRegistry_registrySchemaIdsBy`

### Description

This method retrieves ids for trust registry schemas based on specified parameters, such as the registry ID, and optionally filtered by block hash.

### Parameters

* `by`: `QueryTrustRegistryBy` - Specifies the criteria by which to query the trust registry schemas.
* `reg_id`: `TrustRegistryId` - The unique identifier of the trust registry for which to retrieve schema metadata.
* `at`: `Option<BlockHash>` - Optional block hash to query the metadata at a specific point in the blockchain.

### Return type

`[TrustRegistrySchemaId]` Returns an array where each value is a TrustRegistrySchemaId.

### Example request

```bash
curl -X POST -H "Content-Type: application/json" -d '{
    "jsonrpc": "2.0",
    "method": "trustRegistry_registrySchemaIdsBy",
    "params": [
        { "issuers": { "anyOf": [{ "did": "0x054a1d26f736c727c4a5dfcaa89193fa169cecae7f1daeb9f80103598d280020" }] } },
        "0xdf081ea7a27d9bb1fdba8c21046fc9d30d7cfe9bd87096c5917bd08a17e245b6"
    ],
    "id": 1
}' http://localhost:9933
```

### Example response

```jsx
[
  "0x9ef236a84164f99a80e832d6e3c212908f59ed0baa069898205db3762751235c"
]  
```
