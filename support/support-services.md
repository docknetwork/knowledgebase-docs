# Support Services

### Service Levels

Dock is committed to an SLA Target Percentage of 99.5% Uptime.

**Uptime** is defined as: (_total minutes in month - Downtime) / total minutes in month_

**Downtime** is defined as the total number of minutes the Dock Certs API was unavailable in a  given month.&#x20;

Downtime excludes the following:

* Non-material slowness or other performance issues with individual features&#x20;
* Any products or features identified as pilot, alpha, beta or similar&#x20;
* External network or equipment problems outside of Dock’s reasonable control, including any force majeure event, Internet access outage, third party hosting service outage, third party blockchain network latency, or other problems beyond the demarcation point of Dock.&#x20;
* Scheduled Downtime for maintenance.

### Severity and Response Times

#### **Severity Levels**

Severity levels refers to the types of issues that may be reported by the Customer, and are defined in the following chart.

<table><thead><tr><th width="150">Severity Level</th><th>Description</th></tr></thead><tbody><tr><td>SEV-1</td><td>Service outage or severe degradation that prevents all business operations.</td></tr><tr><td>SEV-2</td><td>Service degradation that allows business operations to continue at a less than optimal rate or prevents some but not all business operations.</td></tr><tr><td>SEV-3</td><td>Incidents that do not directly affect operations or that have limited impact on production environment.</td></tr><tr><td>SEV-4</td><td>Any issue on a non-production system not covered by SEV-5.</td></tr><tr><td>SEV-5</td><td>Non-functional or aesthetic issue not affecting the usability of a system, or other inquiries.</td></tr></tbody></table>

#### Response Times

**Dock Business Hours** 8AM - 8PM UTC

#### **Priority Support**

The mentioned times are for the Dock’s regular business hours. All resolution targets apply only to those errors that are within the control of Dock.

| Severity Level | Contact Method  | Coverage            | Triage   | Resolution target |
| -------------- | --------------- | ------------------- | -------- | ----------------- |
| SEV-1          | Emergency email | 24x7x365            | 2 hours  | 8 hours           |
| SEV-2          | Slack/Email     | Dock Business Hours | 8 hours  | 24 hours          |
| SEV-3          | Slack/Email     | Dock Business Hours | 24 hours | 2 weeks           |
| SEV-4          | Slack/Email     | Dock Business Hours | 48 hours | 2 weeks           |
| SEV-5          | Slack/Email     | Dock Business Hours | 2 weeks  | N/A               |

#### **Regular Support**

| Severity Level | Contact Method | Coverage            | Triage   | Resolution target |
| -------------- | -------------- | ------------------- | -------- | ----------------- |
| SEV-1          | Slack/Email    | Dock Business Hours | 4 hours  | 12 hours          |
| SEV-2          | Slack/Email    | Dock Business Hours | 24 hours | 4 days            |
| SEV-3          | Slack/Email    | Dock Business Hours | 48 hours | 4 weeks           |
| SEV-4          | Slack/Email    | Dock Business Hours | 96 hours | 4 weeks           |
| SEV-5          | Slack/Email    | Dock Business Hours | 2 weeks  | N/A               |

### Contacting Support

Our regular support process is email based. Most support inquires should be directed to [support@dock.io](mailto:support@dock.io). Creating email based support tickets allows us to track the concern to a satisfactory conclusion.

We can provide a private Slack channel for contacting support as an additional service.

#### Emergency Escalation

Customers who are licensed for production support will receive the emergency escalation email address at the time they deploy to production. This address is used for pager support, where any message sent will be routed to the mobile device of the on-call support representative. It is the fastest way to get help.

This service is available only for premium support customers and allows raising SEV-1 errors.

#### **Raising a support issue**

When raising an issue make sure to communicate in English and we recommend to follow this template:

* Summarize the problem.
* What steps did you follow?
* What behavior did you observe?
* What behavior did you expect?
* What is the impact?
* Describe the environment.
  * Client environment:
    * What device, operating system, and browser? Please include relevant version numbers.
  * Dock environment:
    * Which product are you using? Please include relevant version numbers.
    * When applicable, include the URL of the servers and endpoints that are being accessed.
* Other useful data includes:
  * Any relevant logs,
  * A screen shot,
  * Applicable user names.
