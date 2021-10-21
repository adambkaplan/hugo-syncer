# Website sync configuration

This directory includes the configuration for syncing/curating contents from
specific Tekton repositories to the Tekton website.

The configuration is structure as follows:

```yaml
# The name of the component.
# sync.py will use this value to build directories in content/ and vault/.
component: <Component>
# The order of the component in the documentation.
displayOrder: 0
# The GitHub repository where documentation resides.
repository: https://github.com/tektoncd/<component>
# The directory in the GitHub repository where contents reside.
docDirectory: docs
# The link to the GitHub tag page.
archive: https://github.com/tektoncd/<component>/tags
# The tag with content to sync.
tag:
  name: vX.Y.Z               
  displayName: vX.Y.Z
  folders:
    docs:
      target: ''             # optional, default value ''
      index: README.md       # optional, if _index.md exists
      include: ['*.md']      # optional, default value ['*']
      exclude: ['not_in.md'] # optional, default value []
      header: <dict>         # optional, no header added if not set
        See https://www.docsy.dev/docs/adding-content/navigation/#section-menu
    other:
      target: 'other'        # optional, default value ''
      index: README.md       # optional, if _index.md exists
      include: ['*.md']      # optional, default value ['*']
      exclude: ['not_in.md'] # optional, default value []
      header: <dict>         # optional, no header added if not set
        See https://www.docsy.dev/docs/adding-content/navigation/#section-menu
```

See `pipelines.yaml` for more inline instructions.

The YAML files here are used by the scripts in `../sync`.

## Subdirectory configuration

Each doc folder should have its own `folders` config. For example, to configure
all Markdown files in a repo with the following folder structure:

```text
docs
├── subdir
│   └── README.md
└── README.md
```

The `folders` config should look like:

```yaml
folders:
  docs:
    index: README.md
    include: ['*.md']
  docs/subdir:
    target: subdir
    index: README.md
    include: ['*.md']
```