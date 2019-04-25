# Updating outdated npm dependencies

To update dependencies which have "patch" updates (meaning the `Z` in `X.Y.Z` in the version number)

```shell
npm update
```

You can also run `npm upgrade` or `npm up` which are aliases.

## Updating a module with a "minor" or "major" version

If you need to update a dependency that is a "minor" or "major" release, you can either do:

```shell
npm install --save some-library@latest
```

Or, if you're using npm 5+, you can do the even more succinct, dropping the `--save` as it is now the default behavior:

```shell
npm i some-library@latest
```

## Update all dependencies

This is the nuclear option. Only do this if you know what you're doing as updating "minor" and "major" could break your application. 

To update all your npm packages at once, including "patch", "minor" and "major" version, try using the [`npm-check-updates`](https://github.com/tjunnone/npm-check-updates) pacakge:

```shell
npm install -g npm-check-updates
```

Then update all the packages with:

```shell
ncu -u
```

