# Part 2. Design user journeys in Claude Design

&#x20;Now it’s time to think about the story that you want your prototype to tell and the user journeys you want to show.&#x20;

### The three journeys

Most credential prototypes will the same three key journeys:

* **Receive.** The holder gets issued a credential into their wallet.
* **Store.** The holder can see their wallet and what they have in it.
* **Present.** The holder proves to a verifier that they have the information.

### The screens&#x20;

Thinking about those journey we can settle on these 3 main screens:

* **Onboarding**, where the employee creates a wallet and their badge arrives in it.
* **Wallet**, used by the employee. Unlock with the passkey, see the badge.
* **Verification**, the event registration page, which hands off to the wallet for consent and receives the result.

There is no issuer screen. The employee triggers onboarding and issuance happens in the background, which is how this works in production too, where the employer's HR system calls the API rather than someone filling in a form.&#x20;

### &#x20;Example prompt

These are the placeholder values that you will change to match your use case.

| \{{ISSUER\}}               | Quotient, an employer                                                                   |
| -------------------------- | --------------------------------------------------------------------------------------- |
| \{{HOLDER\}}               | a new employee                                                                          |
| \{{CREDENTIAL\}}           | employee badge                                                                          |
| \{{CREDENTIAL\_FIELDS\}}   | employer name, employee ID, full name, role, employment status, valid from, valid until |
| \{{ONBOARDING\_TRIGGER\}}  | an email from HR on the employee's first day                                            |
| \{{VERIFIER\}}             | Event Platform, an online event platform                                                |
| \{{VERIFIER\_SURFACE\}}    | event registration page                                                                 |
| \{{VERIFIER\_GOAL\}}       | enter a members-only event                                                              |
| \{{DISCLOSED\_FIELDS\}}    | employer name, employment status                                                        |
| \{{WITHHELD\_FIELDS\}}     | full name, employee ID, role                                                            |
| \{{SAMPLE\_DATA\_REGION\}} | <p>UK company and personal names<br></p>                                                |

{% prompt description="prompt for the design" %}
```markdown
Build a clickable, multi-screen interactive demo (a self-contained HTML prototype) of
a verifiable credentials journey, powered by Truvera underneath. It is a UI
walkthrough, not a diagram. One screen visible at a time, advanced with Back and Next,
plus a top stepper the viewer can click to jump between steps. Keep navigation state
in memory only (no localStorage).

Do NOT design any issuer, admin, or ecosystem management screens. Issuance and
revocation are handled on the Truvera side and are out of scope.

Scenario: {{ISSUER}} issues a {{CREDENTIAL}} to {{HOLDER}}. {{HOLDER}} holds it in
their own cloud wallet, which runs in the browser. {{VERIFIER}} accepts the
{{CREDENTIAL}} as proof in order to let {{HOLDER}} {{VERIFIER_GOAL}}, without having
any prior relationship with {{ISSUER}}.

Three screens.

SCREEN 1: Onboarding
{{HOLDER}} arrives from {{ONBOARDING_TRIGGER}} and gets a wallet and their
{{CREDENTIAL}} in one flow. Show it as a short sequence of states within the screen:
- A welcome state from {{ISSUER}}, explaining in one or two lines that they are about
  to receive their {{CREDENTIAL}} and that it will be stored in a wallet they control.
- A wallet creation state. Securing the wallet is a single tap using a passkey, with
  the device's own prompt implied. No passwords anywhere in the interface.
- A one-time recovery phrase, shown once, framed clearly as a fallback if the passkey
  is lost. It must not read as a login step.
- A confirmation that the wallet is ready, showing the wallet's DID truncated with a
  copy affordance, framed as the address the credential is issued to. Keep this small
  and secondary.
- The {{CREDENTIAL}} arriving, animated or clearly marked as new.

Issuance happens in the background, so there is nothing for the holder to do here but
see it appear. The point of this screen is that the holder gets a wallet without ever
being asked to understand one.

SCREEN 2: Wallet
A dedicated web wallet app view, visually distinct from the other two screens. Lists the
credentials the holder now holds, each a card showing issuer, credential name, and a
status pill. Tapping a card opens a detail view showing all of {{CREDENTIAL_FIELDS}}
and who issued them. The wallet is locked and unlocked with the passkey, shown as a
single tap.

The status pill must support a revoked state as well as a valid one, and the demo
should let the viewer see both. A revoked card is visibly deadened and cannot be
presented. Make it obvious the holder controls this wallet and that nobody else holds
a copy, while also being clear that the issuer can withdraw the credential.

SCREEN 3: Verification
{{VERIFIER_SURFACE}}, at the point where {{HOLDER}} is asked to prove something in
order to {{VERIFIER_GOAL}}. A primary button reading "present credential". Offer a QR
code as an alternative for holders using a mobile wallet.

Pressing it takes the holder to the wallet, which is the same wallet surface as screen
2. The consent view reads "{{VERIFIER}} is requesting", lists only
{{DISCLOSED_FIELDS}}, and shows {{WITHHELD_FIELDS}} visibly excluded so it is clear
the verifier does not receive them. Confirming uses the passkey. Approve and decline
buttons. Approving returns the holder to {{VERIFIER_SURFACE}}.

Back on {{VERIFIER_SURFACE}}, show exactly which attribute values were received,
{{VERIFIER_GOAL}} confirmed, and an explicit note of what was not received.

Also design the failed path, reached when the credential has been revoked. In the
wallet, the consent view refuses and explains the credential is no longer valid. On
{{VERIFIER_SURFACE}}, nothing arrives at all: a neutral state saying no credential was
presented, with no indication that a credential exists, was revoked, or why.

Use a credential-status colour convention: green = valid and issuer-verified,
amber = pending, gray = expired or revoked. Show a small lock or check motif where a
cryptographic proof has been verified.

Visual style: follow the Truvera design system. Sentence case labels throughout. Use
plausible {{SAMPLE_DATA_REGION}} sample data. Polished enough to present to a client.
```
{% endprompt %}

\
5.4 Handing over Claude Code

Hand over directly from Claude Design to Claude Code. That is the shortest path and there is nothing to move between tools.

If you are designing somewhere else, export the prototype as HTML and put it in the project directory instead. Either way, the prompts in Part 3 assume the design is readable in the working directory, and that it is treated as a visual reference rather than a starting codebase.

<br>
