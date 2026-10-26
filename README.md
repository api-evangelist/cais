# CAIS

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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

CAIS (Capital Integration Systems LLC) operates the leading alternative investment platform for independent wealth management, connecting 65,000+ financial advisors at 2,500+ firms — overseeing roughly $8.5 trillion in end-client assets — with private equity, private credit, hedge fund, real estate, infrastructure, structured note and precious-metals strategies from third-party asset managers and bank issuers. Founded in 2009 by Matt Brown; headquartered in New York.

- Website: https://www.caisgroup.com/
- Member log in: https://members.caisgroup.com
- Integrations: https://www.caisgroup.com/financial-advisor/how-we-partner/integrations

## API surface

CAIS publishes **no OpenAPI, no developer portal and no SDKs**. Its one public machine-readable surface is a remote **Model Context Protocol server** at `https://mcp.caisgroup.com/mcp`, announced 2026-05-19 alongside an Anthropic Claude integration and described as the first interface layer of the company's "Alts Engine" strategy.

The endpoint is OAuth 2.1 gated (authorization code + PKCE S256, RFC 7591 dynamic client registration) and `tools/list` returns `401 invalid_token` anonymously, so the tool catalogue is not public. What *is* public is its RFC 9728 protected-resource metadata, which advertises **12 scopes across four domains** — `caisiq`, `funds`, `iam`, `ips` — with only `funds:orders:create` and `ips:contacts:write` on the write side.

## Artifacts

| Dir | Artifact | Method |
|---|---|---|
| `mcp/` | MCP server manifest (gated tool list recorded as gated, not guessed) | probed |
| `well-known/` | Discovery index + 3 verbatim JSON documents | probed |
| `scopes/` | 12 OAuth scopes from protected-resource metadata | probed |
| `authentication/` | MCP OAuth 2.1 AS + Auth0 member-platform OIDC | probed |
| `conformance/` | MCP, OAuth/RFC 8414/9728/7591/7636/6750, OIDC, DTCC AIP | probed |
| `conventions/` | Transport, error envelope, tracing, caching | probed |
| `errors/` | 4 verbatim observed error responses (OAuth envelope, not RFC 9457) | probed |
| `security/` | Domain security (TLS/HSTS/SPF/DMARC/CAA/DNSSEC) | probed |
| `llms/` | llms.txt | generated |

No A2A agent card, security.txt, trust center, status page, changelog, sandbox, CLI, SDK or event/webhook surface was found — see `conformance/cais-conformance.yml` and the "Not published" section of `llms/cais-llms.txt` for the full negative inventory with probe evidence.
