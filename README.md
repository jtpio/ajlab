# ajlab

Agent-ready JupyterLab.

`ajlab` is a small meta-package for installing the JupyterLab pieces we use for
agent-oriented workflows in one step. It does not add a new application layer of
its own. Instead, it defines the dependency set and ships a little JupyterLab
configuration under `etc/jupyter/labconfig`.

The goal is to keep the package easy to inspect: most behavior comes from the
upstream Jupyter packages, while `ajlab` defines the default environment we want
out of the box.

## Approach

The package currently brings together:

- JupyterLab 4.6+
- collaboration and document-provider plumbing
- Jupyter server MCP support
- Git integration
- JupyterLab command-tooling support

These are installed as normal Python dependencies, so deployments can still
override versions and Jupyter configuration in the usual ways.

## Default settings

`ajlab` ships the following JupyterLab defaults:

- `dockPanelPadding` is disabled for the main shell, giving the workspace a
  tighter layout with less padding around docked content.
- Hidden files and folders are shown in the file browser by default. This is
  enabled both in JupyterLab's file browser setting and in Jupyter Server's
  contents manager so hidden paths are available to the browser.
- The extra human-collaboration UI surfaces are disabled by default:
  `rtcPanel`, `shared-link`, `user-menu-bar`, `userEditorCursors`, and
  `userMenu`.

The collaboration and document-provider packages are still installed. The
default UI is just kept quieter for agent-centered sessions.

## Install

```bash
pip install ajlab
```

## License

BSD-3-Clause
