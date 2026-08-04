# Sydney Airport (sydney-airport)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Sydney Airport Corporation Limited (ACN 082 578 809) operates Sydney Kingsford Smith Airport (IATA SYD, ICAO YSSY), Australia's principal international gateway, under private ownership by the Sydney Aviation Alliance consortium since its 2022 ASX delisting. In the travel distribution chain it is infrastructure rather than an intermediary — it sells no seats, holds no inventory, issues no PNRs, and sits outside the GDS and IATA NDC value chain entirely, monetising aeronautical charges, car parking, retail concessions and property instead. Its API posture is effectively nil — Sydney Airport publishes no developer portal, no API documentation, no OpenAPI, and no terms of use for machine access. Its public website is backed by undocumented JSON endpoints under `/_a/` that return live flight and security wait-time data with no published contract, while its only credentialed partner surface, InfoSYD, is gated behind a ForgeRock OAuth 2.0 / OpenID Connect identity provider at id.syd.com.au and is restricted to airlines, ground handlers and on-airport tenants. The published terms of use expressly prohibit automated retrieval, scraping and indexing of the site, so there is public data but no public interface — and no documented exit path beyond an Australian Privacy Principle 12 personal-information access request.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/sydney-airport/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/sydney-airport/refs/heads/main/apis.yml)

## Tags

- Travel
- Australia
- Airports
- Aviation
- Airport Infrastructure
- Transportation
- Flight Information
- Passenger Experience

## Timestamps

- **Created:** 2026-07-28
- **Modified:** 2026-07-28

## APIs

None. Sydney Airport publishes no documented API.

Two live, unauthenticated JSON endpoints back the public website — `GET /_a/flights` (HTTP 200 with query parameters) and `GET /_a/security-wait-times` (HTTP 200) — but neither is documented, versioned, licensed or supported, and the site's terms of use expressly prohibit automated retrieval. They are recorded as evidence in [`review.yml`](review.yml) rather than listed as APIs.

## Switching Cost

| Dimension | Finding |
| --- | --- |
| Interface shape | `proprietary-undocumented` — the only open standard implemented at an integration boundary is OpenID Connect Discovery 1.0 / OAuth 2.0 with PKCE, and it governs authentication only |
| Second source | `alternatives-with-migration` — OAG, FlightAware AeroAPI, FlightLabs, Cirium and aviationstack all resell SYD movements; operator-only data (security wait times, stand and gate state) has no second source |
| Exit path | `export-on-request` — Australian Privacy Principle 12 personal-information access via privacy@syd.com.au; no bulk export, because there is no API |
| Identifier portability | IATA airline designators, IATA flight numbers and T1/T2/T3 terminal codes travel; the flight record key is an opaque vendor-internal string that does not |
| Contractual lock-in | Terms prohibit automated retrieval and redistribution, grant the user no licence, grant SACL a perpetual irrevocable licence over submitted information, and reserve suspension or termination at any time |
| Distribution model | `not-applicable` — an airport operator, not a carrier or agency; no NDC posture, no GDS relationship, slots coordinated by Airport Coordination Australia |
| Access gate | `none-published` — nothing to sign, because nothing is offered; InfoSYD is a partner login, not a developer portal |

## Properties

- [Website](https://www.sydneyairport.com.au/)
- [Corporate](https://www.sydneyairport.com.au/corporate)
- [Flight Status](https://www.sydneyairport.com.au/flights/)
- [Partner Portal — InfoSYD](https://www.sydneyairport.com.au/infosyd)
- [Support — Contact us](https://www.sydneyairport.com.au/contact-us)
- [Blog — Corporate newsroom](https://www.sydneyairport.com.au/corporate/media/corporate-newsroom)
- [Terms of Service](https://www.sydneyairport.com.au/terms)
- [Privacy Policy](https://www.sydneyairport.com.au/privacy)
- [Copyright](https://www.sydneyairport.com.au/copyright)
- [LinkedIn](https://www.linkedin.com/company/sydneyairport/)

## Artifacts

Sydney Airport publishes no API, so there is no OpenAPI, AsyncAPI, GraphQL, SDK, CLI, sandbox, changelog or MCP surface to harvest. What follows is everything that genuinely exists, captured or derived.

- [`authentication/sydney-airport-openid-configuration.json`](authentication/sydney-airport-openid-configuration.json) — the OpenID Connect Discovery 1.0 document for the ForgeRock Access Management realm that gates InfoSYD, harvested verbatim from `https://id.syd.com.au/am/oauth2/.well-known/openid-configuration` on 2026-07-28 (HTTP 200). The single machine-readable contract Sydney Airport publishes.
- [`authentication/sydney-airport-authentication.yml`](authentication/sydney-airport-authentication.yml) — derived OAuth 2.0 / OIDC profile: endpoints, ten supported grant types, client authentication methods (including mTLS and certificate-bound access tokens), and token algorithms.
- [`scopes/sydney-airport-scopes.yml`](scopes/sydney-airport-scopes.yml) — the seven scopes the identity provider advertises, plus the `infosyd` application scope observed on the live authorize redirect.
- [`conformance/sydney-airport-conformance.yml`](conformance/sydney-airport-conformance.yml) — 28 standards assessed. Eighteen conform, all of them at the authentication boundary; OpenAPI, AsyncAPI, GraphQL, RFC 9457, RFC 8414, RFC 9727 and the ACRIS airport data standard do not.
- [`well-known/sydney-airport-well-known.yml`](well-known/sydney-airport-well-known.yml) + [`well-known/sydney-airport-security.txt`](well-known/sydney-airport-security.txt) — the `/.well-known/` discovery surface across four hosts. Two documents exist; everything else is 404, 501 or 502.
- [`security/sydney-airport-vulnerability-disclosure.yml`](security/sydney-airport-vulnerability-disclosure.yml) — the security.txt contact, and the finding that the disclosure policy it advertises returns HTTP 404.
- [`security/sydney-airport-domain-security.yml`](security/sydney-airport-domain-security.yml) — probed TLS 1.3, HSTS with a one-year max-age, SPF and DMARC at `p=reject`; no DNSSEC and no CAA records.
- [`lifecycle/sydney-airport-lifecycle.yml`](lifecycle/sydney-airport-lifecycle.yml) — recorded absence: no versioning scheme, no deprecation policy, no SLA, no status page, and a termination-at-will clause that runs against the consumer.
- [`llms/sydney-airport-llms.txt`](llms/sydney-airport-llms.txt) — generated by API Evangelist (Sydney Airport publishes no `/llms.txt`), stating plainly that there is no API and that the terms prohibit scraping.

## Notes

- `developer.sydneyairport.com.au` and `api.sydneyairport.com.au` both resolve and terminate on a Microsoft Azure Application Gateway v2, but every probed path returns HTTP 502. `developers.` and `docs.` do not resolve.
- The `Policy:` URL advertised in `/.well-known/security.txt` — `https://www.sydneyairport.com.au/vulnerability-disclosure-policy` — returns HTTP 404.
- The only interoperability specification Sydney Airport publishes is a [CADD data exchange guide](https://www.sydneyairport.com.au/corporate/planning-and-projects/planning-approvals/digital-data-reference-guide) — MicroStation `.dgn` seed files on the MGA'94 coordinate system for surveyors and building services. A real contract, for spatial engineering deliverables rather than software.
- Western Sydney International (Nancy-Bird Walton) Airport opens to freight on 27 July 2026 and to passengers on 25 October 2026, giving the Sydney basin a genuine second gateway for the first time.

Full probe log, HTTP statuses and verbatim contract clauses are in [`review.yml`](review.yml).
