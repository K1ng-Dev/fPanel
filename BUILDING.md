# Local Development
Pterodactyl is now powered by React, Typescript, and Tailwindcss using webpack at its core to generate compiled assets.
Release versions of Pterodactyl will include pre-compiled, minified, and hashed assets ready-to-go.

However, if you are interested in running custom themes or making modifications to the React files you'll need a build
system in place to generate these compiled assets. To get your environment setup you'll need at minimum:

* [Node.js](https://nodejs.org/en/) v14.x.x
* [Yarn](https://classic.yarnpkg.com/lang/en/) v1.x.x
* [Go](https://golang.org/) 1.17.x

### Install Dependencies
```bash
yarn install
```

The command above will download all of the dependencies necessary to get Pterodactyl assets building. After that, its as
simple as running the command below to generate assets while you're developing. Until you've run this command at least
once you'll likely see a 500 error on your Panel about a missing `manifest.json` file. This is generated by the commands
below.

```bash
# Build the compiled set of assets for development.
yarn run build

# Build the assets automatically as they are changed. This allows you to refresh
# the page and see the changes immediately.
yarn run watch
```

### Hot Module Reloading
For more advanced users, we also support 'Hot Module Reloading', allowing you to quickly see changes you're making
to the Vue template files without having to reload the page you're on. To Get started with this, you just need
to run the command below.

```bash
PUBLIC_PATH=http://192.168.1.1:8080 yarn run serve --host 192.168.1.1
```

There are two _very important_ parts of this command to take note of and change for your specific environment. The first
is the `--host` flag, which is required and should point to the machine where the `webpack-serve` server will be running.
The second is the `PUBLIC_PATH` environment variable which is the URL pointing to the HMR server and is appended to all of
the asset URLs used in Pterodactyl.

#### Development Environment
If you're using the [`pterodactyl/development`](https://github.com/pterodactyl/development) environments, which are
highly recommended, you can just run `yarn run serve` to run the HMR server, no additional configuration is necessary.

### Building for Production
Once you have your files squared away and ready for the live server, you'll be needing to generate compiled, minified,
and hashed assets to push live. To do so, run the command below:

```bash
yarn run build:production
```

This will generate a production JS bundle and associated assets, all located in `public/assets/` which will need to
be uploaded to your server or CDN for clients to use.

### Running Wings
To run `wings` in development all you need to do is set up the configuration file as normal when adding a new node, and
then you can build and run a local version of Wings by executing `make debug` in the Wings code directory. This must
be run on a Linux VM of some sort, you cannot run this locally on macOS or Windows.