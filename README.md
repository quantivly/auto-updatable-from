# `auto_updatable_from` Version Checker

This is a simple
[composite action](https://docs.github.com/en/actions/sharing-automations/creating-actions/creating-a-composite-action)
for checking from which version of a service may the checked out version be
automatically updated. This is required beyond [semver](https://semver.org/) semantics
when the service has a breaking change that is not reflected in the version number
(e.g., a requirement in terms of the Quantivly platform's configuration).

The `auto_updatable_from` field should be a string in the format `MAJOR.MINOR.PATCH`,
where `MAJOR`, `MINOR`, and `PATCH` are integers. There are three supported methods for
packages to declare their compatibility:

1. **Python packages** may include an `auto_updatable_from` field in their
   _pyproject.toml_ file, under the `[project]` section. For example:

   ```toml
   [project]
   name = "example"
   version = "0.1.0"
   auto_updatable_from = "0.1.0"
   ```

2. **Node.js packages** may include an `auto_updatable_from` field in their
   _package.json_ file. For example:

   ```json
   {
     "name": "example",
     "version": "0.1.0",
     "autoUpdatableFrom": "0.1.0"
   }
   ```

3. **Other packaged repositories** may include a _.q_ file in the root of the
   repository. This file is meant to be general-purpose, format-agnostic, configuration
   file, and may contain any number of key-value pairs. For example:
   ```
   auto_updatable_from=0.1.0
   ```
