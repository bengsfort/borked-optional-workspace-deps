# workspace-optionals

This repo exists to showcase a bug in yarn v3 where the workspace protocol is not treated correctly for optional dependencies. Instead of being replaced by the local workspace package version, the `workspace:` protocol exists for the dependency post-packing/post-publish, and the dependency is injected into the `dependency` list.

## To reproduce

```
$ cd packages/main
$ yarn pack
```

Afterwards, observe the resulting package.json:

- `required`, a normal dependency, will have its version replaced with the workspace version.
- `optional`, an optional dependency, will retain it's `workspace:*` protocol. It will also be added into the normal dependency list.
