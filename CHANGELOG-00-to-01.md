# ARDP Changelog: draft-pioli-agent-discovery-00 to -01

## Summary

This revision clarifies ARDP's scope, layering, and security model based on implementation experience and mailing list feedback.

## Substantive Changes

### New Sections

1. **Non-Goals (Section 3)** - Added explicit list of out-of-scope items:
   - Agent-to-agent interaction/session/task protocols (MCP/A2A semantics)
   - Identity governance frameworks, IAM policy languages
   - Runtime authorization token formats and enforcement proxies
   - Post-execution evidence/audit/compliance logging
   - Billing/accounting/reputation/business frameworks
   - Naming/bootstrap mechanisms (DNS-based discovery, etc.)
   - Centralization requirements

2. **Layering and Composition (Section 6)** - New section explaining how ARDP composes with:
   - Transport security (TLS/mTLS/QUIC)
   - Identity governance/attestation frameworks
   - Bootstrap mechanisms
   - Interaction protocols (MCP/A2A/HTTP/gRPC)

3. **Minimal HTTPS Binding (Section 15.1)** - Non-normative description of implemented endpoints:
   - `GET /.well-known/ardp/meta`
   - `GET /.well-known/ardp/nonce`
   - `POST /.well-known/ardp/register`
   - `POST /.well-known/ardp/deregister`
   - `GET /.well-known/ardp/resolve?aid={aid}`
   - `GET /.well-known/ardp/query` with pagination parameters

### Security Considerations Updates

4. **Proof of Control (Section 12.1)** - Expanded and clarified:
   - Applies to REGISTER/refresh only (not RESOLVE/QUERY)
   - Defined deterministic JSON serialization rules (keys sorted lexicographically, no whitespace, UTF-8, arrays preserved)
   - Nonce acquisition via `GET /.well-known/ardp/nonce` returning `{nonce, expires_in}`
   - Recommended nonce TTL: 300 seconds
   - Algorithm support: MUST support ES256; MAY support RS256/384/512, PS256/384/512, ES384/512
   - EdDSA explicitly not supported

5. **Authorization Scopes (Section 12.2)** - Clarified:
   - Proof-of-control is for REGISTER/refresh
   - Scopes are primary access control for RESOLVE and QUERY
   - Added `registry:override` scope documentation

### Meta Resource Updates

6. **Meta Resource (Section 8.6)** - Updated example to match implementation:
   - New keys: `version`, `registrar_id`, `min_ttl`, `max_ttl`, `default_ttl`, `supported_protocols`, `supported_auth_methods`, `jws_required`, `nonce_endpoint`, `supported_schema_versions`, `compliance_mode`

### Open Issues

7. **Open Issues (Section 18)** - Added:
   - Consider adopting RFC 8785 (JSON Canonicalization Scheme) in a future revision

### References

8. **References** - Added `seriesInfo` elements for better xml2rfc output

## Editorial Changes

- Clarified refresh semantics (refresh = re-REGISTER with same aid/binding_id)
- Added explicit scope requirements to RESOLVE and QUERY sections
- Converted Open Issues from semicolon-separated to bulleted list
