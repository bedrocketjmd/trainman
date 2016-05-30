# Example usage

```js
// Configuration options
var config = {
  // Required
  _package: _package,
  environmentName: environmentName,
  environments: environments,
  manifest: manifest,
  // Optional, with defaults shown
  packageName: config._package.name,
  publicDir: 'public',
  indexOutputPath: 'index.html',
  assetOutputPath: 'assets',
  versionedAssets: true,
  addSHAToVersion: true,
  cacheTemplates: false,
  angularModule: null, // (required when using cacheTemplates)
  devHost: 'localhost',
  devPort: 8082,
  theme: undefined,
  livereload: false
};

// Initialization
var trainman = require( 'trainman' )( config );

// Installing Gulp task sets
trainman.install( 'build' );
trainman.install( 'server' );
trainman.install( 'deploy' );
trainman.install( 'open' );

trainman.setDefault( 'server' );
```

# Command-line switches

```sh
--deployment / -d
# Build for deployment
# This option is automatically set to true when running the "deploy" task or when NODE_ENV is set to something other than "development"
```

# Command-line arguments

```sh
--code_name / -c
# com.boxxspring.property.code_name meta tag override
```

The following arguments will override values specified in the config object

```sh
--environment / -e
# Environment to use for build, deploy, and open tasks
# This can be an environment key from the environments object, or the path to a file that contains a complete environment object.
# For an example, see the "Development environment" section below.
```

```sh
--host / -h
# Development server hostname
```

```sh
--port / -p
# Development server port number
```

# Development environment

To use a custom environment for development, create a gitignored file (i.e. `development.json`) and pass this filename to gulp as the `--environment` argument.

File-based environments have the special property `base`, which specifies that this environment should extend an environment from the environments object with the given name. An example file-based environment is below.

```json
{
  "base": "production",

  "dependencies": {
    "javascripts": [
      "//sdk.boxxspring.com/angularjs-boxxspring-sdk-2.0.10.js",
      "//localhost:8081/theme-boxxspring-sdk-1.13.0.js"
    ]
  },

  "metaTags": {
    "com.boxxspring.property.code_name": "networka"
  }
}
```
