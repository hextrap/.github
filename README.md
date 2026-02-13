
## What is hextrap?

[hextrap](https://hextrap.com) is a cybersecurity platform that sits between your package manager and the upstream registry. Instead of scanning for known vulnerabilities after the fact, hextrap prevents malicious, typosquatted, and risky packages from reaching your codebase in the first place.

It works with the tools you already use &mdash; no agents to install, no code changes required. Point your package manager at your hextrap firewall and every install is checked against your security policies in real time.

## Key Features

### Package Firewall
Create firewalls for each project, team, or environment. Every package installation request passes through your firewall and is evaluated against your rules before the package is allowed through. Supports **PyPI**, **npm**, and **Go modules**.

### Allow Lists & Deny Lists
Take explicit control over what gets installed. Allow lists restrict installs to only approved packages ("only allow known good"). Deny lists block specific packages you've identified as unwanted. Use them together for defense in depth.

### Typosquat Detection
hextrap continuously monitors PyPI, npm, and the Go module index for newly published packages. Each new package is compared against popular packages using fuzzy string matching. Suspected typosquats are flagged and blocked automatically &mdash; before a developer can accidentally install them.

### Malicious Package Blocking
Packages identified as malicious through advisories, community reports, or behavioral analysis are blocked across all firewalls. Combined with integration data from [deps.dev](https://deps.dev) and [OpenSSF Scorecard](https://scorecard.dev), every package gets Security, Quality, and Maintenance scores (0&ndash;100).

### Soak Time
Delay newly published package versions from being installable for a configurable period. This creates a window for the security community to catch compromised releases before they enter your dependency tree &mdash; a critical defense against supply chain attacks that weaponize new versions.

### Block Unmaintained Packages
Automatically block packages that show signs of abandonment. Unmaintained dependencies are a growing risk vector &mdash; they don't receive security patches and can be targeted for takeover.

### MCP Server for AI Coding Assistants
hextrap provides a [Model Context Protocol](https://modelcontextprotocol.io) (MCP) server that integrates with **Claude Code**, **Claude Desktop**, **ChatGPT**, and other MCP-compatible AI assistants. Your AI checks every package against your firewall before suggesting it, blocking typosquats and enforcing your allow/deny lists automatically.

```json
{
  "mcpServers": {
    "hextrap": {
      "type": "http",
      "url": "https://hextrap.com/mcp/",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

**Available MCP tools:** `check_package`, `list_firewalls`, `add_to_allowlist`, `add_to_denylist`, `remove_from_allowlist`, `remove_from_denylist`, `get_activity`, `get_proxy_config`, `roll_proxy_credential`, `create_service_credential`

> See the full [MCP Setup Guide](https://hextrap.com/docs/setting-up-your-llm-to-use-hextrap-as-an-mcp-server) for detailed configuration instructions.

## Supported Ecosystems

| Registry | Proxy | Configure via |
|----------|-------|---------------|
| **PyPI** (Python) | `pypi.hextrap.com` | `pip install --index-url` or `PIP_INDEX_URL` |
| **npm** (JavaScript) | `npm.hextrap.com` | `.npmrc`, `bunfig.toml` (Bun), or `yarnrc.yml` |
| **Go modules** | `go.hextrap.com` | `GOPROXY` environment variable |

## Quick Start

1. **Sign up** at [hextrap.com](https://hextrap.com) &mdash; free for open source projects
2. **Create a firewall** from the dashboard
3. **Generate credentials** on the Credentials tab
4. **Configure your package manager** to route through hextrap:

```bash
# Python
pip install --index-url https://USERNAME:PASSWORD@pypi.hextrap.com/simple/ requests

# npm
npm config set registry https://npm.hextrap.com/

# Go
export GOPROXY=https://USERNAME:PASSWORD@go.hextrap.com,direct
```

5. Install packages as usual &mdash; hextrap handles the rest


## Resources

- [Documentation](https://hextrap.com/docs/) &mdash; Getting started, firewall setup, package manager configuration
- [MCP Setup Guide](https://hextrap.com/docs/setting-up-your-llm-to-use-hextrap-as-an-mcp-server) &mdash; Connect Claude, ChatGPT, and other AI assistants
- [API Reference](https://hextrap.com/api/) &mdash; REST API for programmatic access
- [Blog](https://hextrap.com/blog/) &mdash; Supply chain security insights and product updates
- [Contact](https://hextrap.com/contact/) &mdash; Questions, partnerships, and enterprise inquiries

---

<p align="center">
  <a href="https://hextrap.com">hextrap.com</a> &nbsp;&bull;&nbsp;
  <a href="https://hextrap.com/privacy/">Privacy Policy</a> &nbsp;&bull;&nbsp;
  <a href="https://hextrap.com/terms/">Terms of Service</a>
</p>
