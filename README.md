# ajlab

Agent-ready JupyterLab.

![](./screenshot.png)

`ajlab` is a small meta-package that installs JupyterLab plus a few extensions
useful for agent workflows, and ships some defaults under `etc/jupyter/labconfig`.

## What's included

- JupyterLab 4.6+
- `jupyter-docprovider` and `jupyter-server-ydoc`
- `jupyter-server-mcp`
- `jupyterlab-git`
- `jupyterlab-commands-toolkit`

## Default settings

- `dockPanelPadding` off.
- Hidden files shown in the file browser.

## Install

```bash
pip install ajlab
```

## License

BSD-3-Clause
