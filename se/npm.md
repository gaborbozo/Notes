# NPM
Generally `package.json` is the map of a _NodeJS_ based project containing information such as the
- project information
> name, version, description, main entry point of the project, ...
- scripts
- dependencies and devDepenenceis
- repository
> repository, license, author, ...
- configuration tools
> Babel, ESLint, Prettier, ...

---

**Package**  is a module containing one or multiple files combined together to represent a specific function f.e. working with dates with the _moment_ package.
**Dependency** is a package that the project relies on and listed in the `package.json` under dependencies (or devDependencies).
# Managing packages
Accross so many packages we may only need some. In order to manage dependencies  _NPM_ is used to install the necessary ones to our local environment.

`npm install`
`npm uninstall`

## Local and global packages
Local packages are installed inside the project directory, `/node_modules` available only for the application.

Global packages are installed system-wide, `/usr/local/lib/node_modules` or `/usr/local/lib/node`.
## dependencies and devDepenenceis
Dependencies are needed for the application to run.

DevDependencies are only needed for development, such as testing, linting, or building the app.
## Outdated packages
`npm outdated` shows a list of installed packages that have newer versions available, including:
-   current - the version we have,
-   wanted - the latest version that satisfies our `package.json` range,
-   latest - the newest available version.
### Semantic versioning
_x.y.z_ where
x - **major** relase
y - **minor** release
z - **patch** release (bug fixes in most common)

1. Install packages specifically leave the `x.y.z` as it is.

2. `^x.y.z` (caret) is the **default** when a dependency is installed and means that when running installation it will look for the most recent one of the defined major release.
> e.g. `^8.y.z` will install the most recent package of the major version _8_, never below or above. 

> In other words its the _max(z)_ of _max(y)_ of x.

3. `~x.y.z` (tilde) is a more strict definition which means that it will search for the most recent patch release.

> in other words its the _max(z)_ of y of x.
#### `package-lock.json`
In the context of package.json acting as an input, package-lock.json serves as the output. Its purpose is to lock specific package versions during development, ensuring consistency across different environments and preventing version mismatches.
> Thus it is also included in the commits. 
# Cache
Stores downloaded packages locally to speed up future installations and reduce redundant network requests. Calling for installation npm will first check the cache before fetching it from the registry.

`npm cache clean --force` removes cached packages.

`npm cache verify` is used to check the integrity of the npm cache. It ensures that the cache is not corrupted and the stored packages are in good condition. If issues are found, it will attempt to fix them.
# Audit
It is the process of scanning the project's dependencies for known security vulnerabilities. Check for any reported security issues and provides a detailed report with recommendations on how to address them.
# Scripts
Custom defined commands in `package.json`.
## Lifecycles
Help automate tasks during different phases of the package management process.
Common ones are `preinstall, install, postinstall, preuninstall, uninstall, postuninstall, prepublish, ...`

For example when running `start` it will automatically run
```
1.`prestart` (if defined)
2.`start`
3.`poststart` (if defined)
```
# NPX
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MTY3MDQ2OTJdfQ==
-->