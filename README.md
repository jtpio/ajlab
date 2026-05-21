# ajlab

Agent-ready JupyterLab.

![](./screenshot.png)

`ajlab` is a small meta-package that installs JupyterLab plus a few extensions
useful for agent workflows, and ships some defaults under `etc/jupyter/labconfig`.

## What's included

Minimum versions (see [`pyproject.toml`](./pyproject.toml)):

- `jupyterlab >=4.6.0a5`
- `jupyter-docprovider >=2.4.0a0` and `jupyter-server-ydoc >=2.4.0a0`
- `jupyter-server-mcp >=0.3.0a0`
- `jupyterlab-commands-toolkit`

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
claude mcp add jupyter-mcp -- uvx --from jupyter-server-mcp jupyter-server-mcp-proxy
```

Alternatively, for a single server on a fixed port, connect directly over HTTP:

```bash
claude mcp add --transport http jupyter-mcp http://localhost:3001/mcp
```

See the [`jupyter-server-mcp` README][mcp] for tool registration via
`jupyter_config.py` and snippets for other MCP clients.

[mcp]: https://github.com/jupyter-ai-contrib/jupyter-server-mcp

## License

BSD-3-Clause
