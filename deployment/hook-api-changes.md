---
description: >-
  Instructions on how to deploy the new production environment after any changes to the hook api or a `HookUpdate` amendment.
---

# Deploying to Production after a HookUpdate Amendment

## Prerequisites

You will need to clone the following repositories.

- [Macros](https://github.com/XRPLF/hook-macros)
- [Xrpl Hooks Complier](https://github.com/XRPLF/xrpl-hooks-compiler)
- [Readme](https://xrpl-hooks.readme.io/)

## Process

1. Update the `hook-macros` with the changes to the header files and merge in the changes.

- date.h
- error.h
- extern.h
- hookapi.h
- macro.h
- sfcodes.h

2. Update the `hooks-macros` git submodule in the `xrpl-hooks-compiler`. See [readme](https://github.com/XRPLF/xrpl-hooks-compiler/blob/master/c2wasm-api/README.md) for instructions.
4. Redeploy the `c2wasm-api` in the  `xrpl-hooks-compiler` repo. See [readme](https://github.com/XRPLF/xrpl-hooks-compiler/blob/master/README.md#developing-c2wasm-api-without-building-all-the-binaries) for instructions.
3. Update the `xrpl-hooks.readme.io` with any relevant information.

- Transactions will need updates to Transactional Stake Holders.
- HookAPI will need update to reference.
- Review code for other changes!!