# ajlab

Agent-ready JupyterLab.

![](./screenshot.png)

`ajlab` is a small meta-package that installs JupyterLab plus a few extensions
useful for agent workflows, and ships some defaults under `etc/jupyter/labconfig`.

## What's included

Minimum versions (see [`pyproject.toml`](./pyproject.toml)):

- `jupyterlab >=4.6.1`
- `jupyter-docprovider >=3.0.0` and `jupyter-server-ydoc >=3.0.0`
- `jupyter-server-mcp >=0.3.0a0`
- `jupyterlab-commands-toolkit >=0.1.6`

## Default settings

- Hidden files shown in the file browser.

## Install

```bash
pip install ajlab
```

## Run

Once installed, start JupyterLab with:

```bash
jupyter lab
```

## Configure agents

Agent connectivity is provided by [`jupyter-server-mcp`][mcp], which runs inside
JupyterLab and exposes an MCP endpoint (default port `3001`) that any MCP client
can connect to.

The recommended way to connect a client is the stdio proxy, which auto-discovers
the running Jupyter MCP server and bridges stdio to its HTTP endpoint. It keeps
working unchanged when several Jupyter servers run side by side or when the port
is assigned dynamically. To wire it up to Claude Code:

```bash
claude mcp add jupyter-mcp -- uvx --prerelease allow --from jupyter-server-mcp jupyter-server-mcp-proxy
```

> `jupyter-server-mcp` is currently a pre-release. `uvx` skips pre-releases by
> default, so pass `--prerelease allow` or it silently installs the older stable
> release and the proxy/server versions won't match.

Alternatively, for a single server on a fixed port, connect directly over HTTP:

```bash
claude mcp add --transport http jupyter-mcp http://localhost:3001/mcp
```

See the [`jupyter-server-mcp` README][mcp] for tool registration via
`jupyter_config.py` and snippets for other MCP clients.

[mcp]: https://github.com/jupyter-ai-contrib/jupyter-server-mcp

## License

BSD-3-Clause
