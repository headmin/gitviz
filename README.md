# Fleet GitViz

Version: v0.0.1

A tiny CLI that visualizes Fleet GitOps configurations as an interactive graph you can open in your browser.

This tool was developed after attending a fleet-gitops workshop in London. While its current focus is exclusively on fleet gitops config files, the approach can be expanded to be a sidecar to other GitOps tools and workflows.


## Getting started (evaluate the tool)

1) Download a sample Fleet GitOps repo

```bash
git clone https://github.com/fleetdm/fleet-gitops
```

2) Run the binary on a source (directory or single YAML file)

```bash
# Using the built binary in this repo
./dist/fleet-gitviz ./fleet-gitops

# Or if installed on your PATH
fleet-gitviz ./fleet-gitops
```

3) Open the visualization in your browser

```bash
open ./output/index.html   # macOS
# or just open the file in any browser: ./output/index.html
```

## Inputs
- You can point to a Fleet GitOps directory (must contain a `default.yml`) or a single YAML file.
- You can pass multiple sources in one run to get multiple tabs in the UI.

## Flags
- `-o, --output <dir>`
  - Where to write outputs (default: `./output`).
  - Example:
    ```bash
    fleet-gitviz -o ./docs/graphs ./fleet-gitops
    ```

- `-m, --mode <mode>`
  - How to handle existing tabs: `replace` (default) clears them, `add` appends.
  - Example (append to an existing visualization):
    ```bash
    fleet-gitviz -m add ./another-fleet-gitops
    ```

- `-n, --name <name>`
  - Custom name for the tab (applies only to the first source in a single run).
  - Example:
    ```bash
    fleet-gitviz -n "After Changes" ./fleet-gitops
    ```

- `-h, --help`
  - Show usage help.
  - Example:
    ```bash
    fleet-gitviz -h
    ```

## Common examples

- Visualize a single Fleet GitOps repository
```bash
fleet-gitviz ./fleet-gitops
```

- Visualize a single YAML file
```bash
fleet-gitviz ./starter-library.yml
```

- Compare two versions (diff) by creating two tabs
  - Option A (two runs, lets you name both tabs):
    ```bash
    fleet-gitviz -n "v1" ./fleet-gitops-v1
    fleet-gitviz -m add -n "v2" ./fleet-gitops-v2
    open ./output/index.html
    ```
  - Option B (single run; first tab uses `-n`, second tab is the directory name):
    ```bash
    fleet-gitviz -n "v1" ./fleet-gitops-v1 ./fleet-gitops-v2
    ```

- Visualize multiple sources at once as separate tabs
```bash
fleet-gitviz ./orig-fleet-gitops ./my-fleet-gitops
```

## Output
- Writes `index.html`, `sources.json`, and one JSON graph per source into the output directory (default `./output`).
- Open `./output/index.html` to explore the graph(s).
