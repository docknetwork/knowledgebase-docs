---
description: This document explains how we audit the systems scalability.
hidden: true
---

# System Scalability

## Architecture

Dock's SaaS systems are engineered for scalability using tools from Amazon AWS and MongoDB Atlas.

## Service Level Agreements

Our contractual SLAs are listed in our [MSA](https://www.dock.io/master-services-agreement).&#x20;

## API Performance Benchmarks

We regularly test our platform to ensure we can meet our performance benchmarks. Verifiable credential implementations are unique for every project. It is configured with a different number of DIDs, ecosystems, different types and numbers of VCs. Those different combinations may affect the application performances differently and are tested separately.

### Creating DID

* **Throughput:** Maximum of 90 requests/second, average of 75 requests/second
* **Response Times**:
  * Average: 200 ms
  * 95% Percentile: 300 ms
  * Maximum: 3000 ms
* **HTTP Failures:** < 0.1%

### Issue non anonymous credential

* **Throughput:** Maximum of 90 requests/second, average of 70 requests/second
* **Response Times**:
  * Average: 110 ms
  * 95% Percentile: 140 ms
  * Maximum: 1200 ms &#x20;
* **HTTP Failures:** < 0.1%

### Issue anonymous credential

* **Throughput:** Maximum of 30 requests/second, average of 20 requests/second
* **Response Times**:
  * Average: 3 seconds
  * 95% Percentile: 6 seconds
  * Maximum: 23 seconds
* **HTTP Failures:** < 10%

### Verify credential

* **Throughput:** Maximum of 80 requests/second, average of 70 requests/second
* **Response Times**:
  * Average: 240 ms
  * 95% Percentile: 260 ms
  * Maximum: 1240 ms
* **HTTP Failures:** < 0.1%



{% hint style="info" %}
**95% Percentile Response Time**: Indicates that 95% of the requests were served within this time.

**Performance Testing Parameters**: Tests involved a maximum of 100 Virtual Users (VUs) for a duration of 6 minutes and 30 seconds with a 1-minute ramp-up period.
{% endhint %}

