# Sydney Airport (sydney-airport)

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
