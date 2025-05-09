First, thank you for contributing to DIM! We're a community-driven project and we appreciate improvements, large and small.

Here are some tips to make sure your Pull Request (PR) can be merged smoothly:

1. If you want to add a feature or make some change to DIM, consider [filing an issue](https://github.com/DestinyItemManager/DIM/issues/new) describing your idea first. This will give the DIM community a chance to discuss the idea, offer suggestions and pointers, and make sure what you're thinking of fits with the style and direction of DIM. If you want a more free-form chat, [join our Discord](https://discordapp.com/invite/UK2GWC7).
1. Resist the temptation to change more than one thing in your PR. Keeping PRs focused on a single change makes them much easier to review and accept. If you want to change multiple things, or clean up/refactor the code, make a new branch and submit those changes as a separate PR.
1. All of our code is written in [TypeScript](https://typescriptlang.org) and uses React to build UI components.
1. Be sure to run `pnpm fix` before submitting your PR - it'll catch most style problems and make things much easier to merge.
1. Don't forget to add a description of your change to [docs/CHANGELOG.md](CHANGELOG.md) so it'll be included in the release notes!

## Developer Quick start

1. [Install Pre-requisites](#pre-requisites)
1. [Clone](#clone-the-repo)
1. [Start Dev Server](#start-dev-server)
1. [Get your own API key](#get-your-own-api-key)
1. [Enter API credentials](#enter-api-credentials)

### Pre-requisites

**Note:** It's often easier to use a package manager like [Homebrew](https://brew.sh/) for Mac, or [Chocolatey](https://docs.chocolatey.org/en-us/choco/setup) for Windows, and install the prerequisites through them.

* Homebrew: `brew install git nodejs corepack visual-studio-code`
* Chocolatey: `choco install git nodejs-lts corepack vscode`

#### Manual Install

* Install [Git](https://git-scm.com/downloads)
* Install [NodeJS](https://nodejs.org/)
* It is highly recommended to use [VSCode](https://code.visualstudio.com/) to work on DIM. When you open DIM in VSCode, accept the recommended plugins it suggests (find them manually by searching "@recommended" in the Extensions window).
* On Windows, restart your system after installing everything.

### Enable Corepack

Corepack manages the version of pnpm, the package manager used by DIM. It comes with NodeJS and will automatically get the right version of pnpm for you.

* [`corepack enable`](https://github.com/nodejs/corepack#how-to-install)

### Clone the repo

To locally **run a copy** of DIM, you can simply clone the code repository:

```sh
git clone https://github.com/DestinyItemManager/DIM.git
```

To **contribute changes to the project**, you'll want to:

1. Make an account on GitHub
1. [Create an SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) and [add it to your account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
1. Fork DIM to make your own copy of the repository
1. Clone the forked repository to your local machine
1. Edit the local files
1. Commit and push your code changes to your fork
1. Create a Pull Request from your forked repository to the original upstream repository, allowing DIM maintainers to accept and merge your changes

More detailed information on these steps is [here](https://docs.github.com/en/get-started/quickstart/contributing-to-projects).

### Start Dev Server

Once you have cloned the repository or a fork of the repository to your local machine, in the root directory:

* Run `pnpm install`
  * If `pnpm` isn't installed, run `corepack enable` and try again, or [install it manually](https://pnpm.io/installation).
    * If `corepack enable` fails, try running it with Administrator privileges.
    * If you're using PowerShell on Windows, you may need to run `Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy Unrestricted` to allow pnpm to run.
  * Linux-based developers will need to install `build-essential` (`sudo apt-get install -y build-essential`) prior to running `pnpm install`.
* Run `pnpm start`

On Windows machines, this will also install SnoreToast to provide notifications for parts of the development process, like when a build completes.

### Get your own API key:

1. Go to [Bungie's Developer Portal](https://www.bungie.net/en/Application) (you will have to be signed in)
1. Click `Create New App`
1. Enter any application name
1. Enter `https://github.com/YourGithubUsername/DIM` under website
1. For `Oauth Client type`, select `Confidential`
1. Set your redirect url to `https://localhost:8080/return.html` (or whatever the IP or hostname is of your dev server)
1. Select all scopes _except_ the Administrate Groups/Clans
1. Enter `https://localhost:8080` as the `Origin Header`
1. Check the box to agree to the Terms of Use and click Create New App

### Enter API Credentials

This step will need to be done each time you clear your browser cache. You will be automatically redirected to a screen to enter these credentials
if the app can't load them from local storage when it starts.

1. Open your browser and navigate to https://localhost:8080 (your browser will likely give a security warning, it is safe to continue anyways, see Overview below for details)
1. Copy your API-key, Oauth Client_id, and OAuth client_secret from bungie.net into DIM developer settings panel when it is loaded
1. Below the section for Bungie API credentials, follow the instructions to generate a DIM API key

### Development

**Overview**

The `pnpm start` step will create a hot-loading web server and a TLS cert/key pair. You will access your local development site by visiting https://localhost:8080.
You will likely get a security warning about the certificate not being trusted. This is because it's a self-signed cert generated dynamically for your environment
and is not signed by a recognized authority. Dismiss/advance past this warning to view your local DIM application.

**Check code Style**

* `pnpm fix` will tell you if you're following the DIM code style (and automatically fix what it can).
Check out the [docs]() folder for more tips.

**Translation**

* We use [i18next](https://github.com/i18next/i18next) for all our translated strings, so if you want to translate something that's currently English-only, take a look at that. Usually it's as simple as replacing some text with `<span>{t('KEY')}</span>` and then defining KEY in the `config\i18n.json` file.

* `pnpm i18n` will add, sort, and prune `src/locale/en.json`. You should never manually edit `src/locale/en.json`. Some keys are obfuscated by code and will need to be added as comments into the code such as `// t('LoadoutBuilder.ObfuscatedKey1')`. If you have any questions, ping @delphiactual via GitHub, Slack, or Discord.

### Android Debugging

Assuming you have an Android phone:

1. Enable Developer Mode
2. Enable USB debugging
3. In Chrome, visit chrome://inspect/#devices and connect to the device.
4. Enable port forwarding for port 8080.
5. Visit https://localhost:8080/developer on your laptop and copy the "Open this link in another browser" link address.
6. Back in the inspect devices screen, paste that URL into the "Open tab with URL" box to open it on your Android device.
7. Save the API keys on the Android device and log in as normal.
8. Back in the inspect devices screen, click "inspect" under the tab you want to debug.