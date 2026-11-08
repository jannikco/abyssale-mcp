# Abyssale MCP server

Discover design templates, request asset generation and poll until the generated files are ready.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `ABYSSALE_API_KEY`



Credential help: https://developers.abyssale.com/rest-api/authentication

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call abyssale_list_designs '{}'
```

## Use with an MCP client

Launch `node /absolute/path/abyssale-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| abyssale_list_designs | Read | abyssale list designs |
| abyssale_get_generation | Read | abyssale get generation |
| abyssale_generate_formats | Explicit approval required | Queue asset generation using an existing design; poll get_generation. Acceptance does not mean files are finished. |

## Concrete workflow

Discover design templates, request asset generation and poll until the generated files are ready.

1. abyssale_list_designs
2. abyssale_get_generation
3. abyssale_generate_formats

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=abyssale&integration=abyssale-mcp&utm_source=github&utm_campaign=github-abyssale-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/abyssale/).

## Provenance and maintenance

- https://developers.abyssale.com/api-reference/listDesigns
- https://developers.abyssale.com/api-reference/getGenerationRequest
- https://developers.abyssale.com/api-reference/generateMultiFormatMedia

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
