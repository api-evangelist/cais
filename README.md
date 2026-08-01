# CAIS

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
