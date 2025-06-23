## Solving

For any terms that you do not recognize, use chat gpt and give it `typescript` as context when asking about it.

## Context

`oav` is a typescript package that is used to verify `examples` and `specifications` for `openapi 2.0` swagger specifications. It scans files that look like [this](https://github.com/Azure/azure-rest-api-specs/blob/main/specification/schemaregistry/data-plane/Microsoft.SchemaRegistry/stable/2021-10/schemaregistry.json) and spits out any violations of `open api 2.0` specification format.

It basically verifies that these specifications meet requirements to be used properly without running into random errors.

The issue is that this package was begun a while ago, and as such, dependencies were out of date. EG:

- `typescript` version was two major versions old (3.X)
- `jest` version was three major versions old (`26.X`)
- `inversify` version was two major versions old, and on the other side of some major changes.

## The problem

I am attempting to bring `oav` into the modern world as far as `typescript` (language version), `testing` (jest version), and `dependency injection` (`inversify`).

To that end, I have:

- Updated the dependencies in `package.json`, as well as updated any other `devdependencies` that would have to update alongside those three dependencies.
- Resolved all build and typing errors caused by `typescript` upgrade
- Fixed `inversifyUtils.ts` and other relevant code to resolve build errors caused by major version breakages to that package.
- Fixed `jest` configuration build errors caused by jest major version upgrade.

[Here is the comparison of my changes to the current latest version in `develop`](https://github.com/Azure/oav/compare/develop...semick-dev:oav:update-devdependencies)

## Necessary Software

- Install `nvm`
- Use `nvm` to install `node 20`
- Install `vscode`
- Clone this repo
- Clone `Azure/azure-rest-api-specs` repo

## Setup and repro of the error I'm trying to solve

- `cd` into the cloned `oav` repo
- `nvm install 20`
- `nvm use 20`
- `npm install`
- `npm run build`
- `npm run cli -- validate-example /path/to/cloned/azure-rest-api-specs/specification/schemaregistry/data-plane/Microsoft.SchemaRegistry/stable/2021-10/schemaregistry.json`

You will see the error. That's what I'm trying to solve.