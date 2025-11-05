---
description: This document explains how we audit the systems scalability.
---

# System scalability

## Architecture

Truvera's SaaS systems are engineered for scalability using tools from Amazon AWS and MongoDB Atlas.

## Service level agreements

Our contractual SLAs are listed in our [MSA](https://www.dock.io/master-services-agreement).&#x20;

## API performance benchmarks

We regularly test our platform to ensure we can meet our performance benchmarks. Verifiable credential implementations are unique for every project. It is configured with a different number of DIDs, ecosystems, different types and numbers of VCs. Those different combinations may affect the application performances differently and are tested separately.

### Creating DID

* **Throughput:** Maximum of 90 requests/second, average of 75 requests/second
* **Response Times**:
  * Average: 200 ms
  * 95% Percentile: 300 ms
  * Maximum: 3000 ms

### Issue non anonymous credential

* **Throughput:** Maximum of 78 requests/second, average of 50 requests/second
* **Response Times**:
  * Average: 343 ms
  * 95% Percentile: 1 s
  * Maximum: 6 s &#x20;

### Issue anonymous credential

* **Throughput:** Maximum of 74 requests/second, average of 49 requests/second
* **Response Times**:
  * Average: 452 ms
  * 95% Percentile: 2 seconds
  * Maximum: 6 seconds

### Verify non-anonymous credential

* **Throughput:** Maximum of 80 requests/second, average of 54 requests/second
* **Response Times**:
  * Average: 340 ms
  * 95% Percentile: 414 ms
  * Maximum: 1 s

### Verify anonymous credential

* **Throughput:** Maximum of 75 requests/second, average of 49 requests/second
* **Response Times**:
  * Average: 386 ms
  * 95% Percentile: 485 ms
  * Maximum: 2 s



{% hint style="info" %}
**95% Percentile Response Time**: Indicates that 95% of the requests were served within this time.
{% endhint %}

