[![Tests](https://github.com/Roblox/roact-alignment/workflows/ci/badge.svg?branch=master)](https://github.com/Roblox/roact-alignment/actions?query=workflow%3ACI+branch%3Amaster)
[![Coverage Status](https://coveralls.io/repos/github/Roblox/roact-alignment/badge.svg?branch=master&t=TvTSze)](https://coveralls.io/github/Roblox/roact-alignment?branch=master)

# Roact Alignment
A temporary ground-up Roact repository that will track our preliminary alignment with React, starting with leaf nodes like the scheduler.

## Status
The [react repo](https://github.com/facebook/react) is a monorepo with a number of member projects in its `packages` folder, managed by a yarn workspace. Below is a description of each of those package, its status in our alignment repo, and how it likely fits into our future plans.

📌 _Considered part of react's core functionality or testing capabilities; some or all of this package is necessary to build and validate an MVP._

| Project | Description | Status | Plan | Notes |
| - | - | - | - | - |
| `create-subscription` | Used for subscribing to external data | ❌ Not ported | ❔ Not yet assessed | |
| `dom-event-testing-library` | Dom event simulation for tests | ❌ Not ported | ❔ Not yet assessed | May inspire Rhodium improvements |
| `eslint-plugin-react-hooks` | Linting plugin for hooks rules | ❌ Not ported | ❔ Not yet assessed | Depends on future linting tools |
| `jest-mock-scheduler` | Reexports scheduler testing utilities | ❌ Not ported | ❔ Not yet assessed | |
| 📌`jest-react` | Jest matchers and utilities | ❌ Not ported | ➕ Likely to be ported | Haven't yet run into any uses of this in tests we've ported so far |
| 📌`react` | Base react interface | 🔨 Port in progress |  | Defines basic shape of internals like Components and Elements. We may add things like Bindings here. |
| `react-art` | For drawing vector graphics | ❌ Not ported | ➖ Unlikely to be ported | |
| `react-cache` | Basic cache for use with experimental React features | ❌ Not ported | ❔ Not yet assessed | API is flagged as unstable |
| `react-client` | Experimental package for consuming React streaming models | ❌ Not ported | ❔ Not yet assessed | API considered unstable. Might be worth investigating if it stabilizes |
| `react-debug-tools` | Experimental debugger package | ❌ Not ported | ❔ Not yet assessed | API considered unstable |
| `react-devtools` | Top-level app for react devtools | ❌ Not ported | ➕ Likely to be ported | Devtools needs to be addressed as a whole to see where/how it translates |
| `react-devtools-core` | Standalone devtools impl | ❌ Not ported | ➕ Likely to be ported | Devtools needs to be addressed as a whole to see where/how it translates |
| `react-devtools-extensions` | Devtools browser extension | ❌ Not ported | ➖ Unlikely to be ported | |
| `react-devtools-inline` | Impl for embedding in browser-based IDEs | ❌ Not ported | ➕ Likely to be ported | Devtools needs to be addressed as a whole to see where/how it translates |
| `react-devtools-scheduling-profiler` | Experimental concurrent mode profiler | ❌ Not ported | ❔ Not yet assessed | |
| `react-devtools-shared` | Private shared utilities for devtools | ❌ Not ported | ➕ Likely to be ported | Devtools needs to be addressed as a whole to see where/how it translates |
| `react-devtools-shell` | Harness for testing other devtools packages | ❌ Not ported | ❔ Not yet assessed | Devtools needs to be addressed as a whole to see where/how it translates |
| `react-dom` | Entrypoint for DOM and server renderers | ❌ Not ported | ➖ Unlikely to be ported | Will inform top-level interface, but will be mostly replaced with Roblox-specific logic |
| `react-fetch` | For use with experimental React features | ❌ Not ported | ❔ Not yet assessed | API considered unstable |
| `react-interactions` | For use with experimental React features | ❌ Not ported | ❔ Not yet assessed | |
| 📌`react-is` | Runtime type checks for React elements | ✔️ Ported | | |
| `react-native-renderer` | Renderer interface for react-native | ❌ Not ported | ❔ Not yet assessed | This package has no readme, so it's hard to understand its scope |
| 📌`react-noop-renderer` | Renderer used for debugging Fiber | ✔️ Ported |  | Will be needed to verify our Fiber/Reconciler work |
| 📌`react-reconciler` | Reconciler implementation used with various renderers | ✔️ Ported |  | Bulk of React's complicated logic lives here |
| `react-refresh` | Wiring for Fast Refresh | ❌ Not ported | ❔ Not yet assessed, depend on applicability | Officially supported successor to "hot reloading" |
| `react-server` | Experimental package for creating React streaming server renderers | ❌ Not ported | ❔ Not yet assessed | |
| `react-test-renderer` | Test renderer with dom snapshotting | ✔️ Ported | | Used for testing much of React's internals |
| `react-transport-dom-delay` | Internal package, likely for testing | ❌ Not ported | ➖ Unlikely to be ported | No readme in package |
| `react-transport-dom-webpack` | Related to above | ❌ Not ported | ➖ Unlikely to be ported | Appears to be webpack-specific |
| 📌`scheduler` | Cooperative scheduling implementation | ✔️ Ported | | Tracing feature is excluded, will be needed at some point for devtools |
| 📌`shared` | Loose collection of shared utilities and definitions | ✔️ Ported | | Working with upstream to see if this can be cleaned up |
| `use-subscription` | Hook for managing subscriptions in concurrent mode | ❌ Not ported | ❔ Not yet assessed | Not sure if/how this will apply to Roblox |

Projects not in the react repo:
| Project | Description | Notes |
| - | - | - |
| 📌`react-shallow-renderer` | Shallow renderer used in tests for some older React features. Re-exported alongside `react-test-renderer`, source of truth [here](https://github.com/NMinhNguyen/react-shallow-renderer). |  ✔️ Ported - with tests that are helping us exercise functionality in the `react` package |
| `roblox-jest` | Custom matchers and timer logic for TestEZ | A rough approximation of what we'll eventually have with the [`jest` alignment effort](https://github.com/Roblox/lest-alignment) |
| `roblox-js-polyfill` | Implementations of JS specific interfaces or functionality | Most implementations are incomplete or slightly adjusted for Lua |

## Deviations from [Roact](https://github.com/roblox/roact)
This repo is meant to supplant the `Roact` project, which is an open-source project that currently powers the majority of the Lua App and is used by the community as well. Our goal is to be as compatible as possible with Roact by the time we're ready to start adopting this alignment effort for use.

With that in mind, however, there will still be a small number of behavioral deviations that make the transition from existing Roact smoother, or account for nuances of the Roblox ecosystem:
* Stable Keys: Aligned Roact will allow table keys to be used as stable keys for child elements, equivalent to the behavior relied upon in Roact today
* Context: Current Roact's deprecated `_context` feature will not be present in aligned Roact; users will have to switch to the `createContext` feature, which is present in both current and aligned Roact and is semantically equivalent
* Class Component Refs: Aligned Roact will allow refs provided to class components (referred to in Roact documentation as "stateful components") to point to the actual component instance. This is not supported in current Roact, and there may be changes around the `Roact.Ref` prop key to support this with minimal disruption
* Bindings: We intend to keep `createBindings` and `joinBindings`, a feature unique to Roact and [documented here](https://roblox.github.io/roact/api-reference#roactcreatebinding)

See [this document](DEVIATIONS.md) for details about any deviations and the design and refactoring efforts being proposed to address them.

## How to run the tests

You need to create a GitHub Access Token:
* GitHub.com -> Settings -> Developer Settings -> Personal Access Tokens
* Your token must have the `repo` and read:packages` scopes
* On that same page, you then need to click Enable SSO
* BE SURE TO COPY THE ACCESS TOKEN SOMEWHERE 

```
npm login --registry=https://npm.pkg.github.com/ --scope=@roblox
```
For your password here, you will enter the GitHub Access Token from the instructions above.

```
npm install --global @roblox/rbx-aged-cli
```

Before you can use rbx-aged-cli, you need to be logged into the VPN so the Artifactory repository is accessible.

```
mkdir ~/bin
rbx-aged-cli download roblox-cli --dst ~/bin
export PATH=$PATH:~/bin
roblox-cli --help
```
You should see roblox-cli output its help text.
Before going ahead, you might want to add `export PATH=$PATH:~/bin` to your bash profile file of choice, so you don't have to run it every time you open your terminal.

The next step is to clone the repo. When prompted for it, use the personal access token as your password.

```
git clone https://github.com/Roblox/roact-alignment.git
cd roact-alignment
roblox-cli analyze default.project.json
```

Foreman is an un-package manager that retrieves code directly from GitHub repositories. We'll use this to get a Lua package manager and other utilities. The Foreman packages are listed in `foreman.toml`. Foreman uses Rust, so you'll have to install Rust first.

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
export PATH=$PATH:$HOME/.cargo/bin
cargo install foreman
foreman github-auth <your GitHub API token that you used for npm login above>
foreman install
export PATH=$PATH:~/.foreman/bin/ # you might want to add this to your bash profile file too
```

Now you can run the tests, edit code, and contribute! Next we need to install our Lua package dependencies. We do this with a tool called Rotriever, which Foreman just installed for us. The package dependencies are listed in `rotriever.toml`. 

```
rotrieve install
```

Next we're going to use Rojo (installed by Foreman above) to compile and package our Lua code into a format that Roblox understands.

```
rojo build tests.project.json  --output model.rbxmx
```

Now we can use `roblox-cli` to run our tests. We specify the Rojo build output file and our test runner file.

```
roblox-cli run --load.model model.rbxmx --run bin/spec.lua
```

### Common Issues

If rojo doesn't understand the nested project structure, exemplified by require statements not finding things, make sure you don't have a globally-installed rojo binary that is shadowing the one this project specifies locally. You *must* be using rojo 6.0 or above.

Once you remove the global rojo, you'll need to tickle bash's PATH hash cache so it doesn't keep looking in the place rojo *was*. (Yes, this is weird.) To update the bash path hash cache, run:
```hash -d rojo```

To avoid this in the future, be sure that your foreman binary path is *before* the carbo binary path in your `PATH` enviroment.

## Contribution Guidelines

* Try to keep the directory structure, file name/location, and code symbol names aligned with React upstream. At the top of the mirrored files, put a comment in this format that includes the specific hash of the version of the file you're mirroring: 
```
-- ROBLOX upstream https://github.com/facebook/react/blob/9abc2785cb070148d64fae81e523246b90b92016/packages/scheduler/src/Scheduler.js
```


* If you have a deviation from upstream code logic for Lua-specific reasons (1-based array indices, etc) put a comment above the deviated line:
```
-- ROBLOX deviation: use explicit nil check instead of falsey
``` 

* For deviations due to Lua language differences (no spread operator) that don't involve changing the logic, don't put a deviation comment. Just use the appropriate equivalent from the Cryo and other utility libraries.

* For files that are new and Roblox-specific, use the file name: ```Timeout.roblox.lua```

* and for Roblox-specific tests, use the file name format: ```Timeout.roblox.spec.lua```

### How to debug local tests

First, install the roblox-lrdb debugger extension for VSCode (following [the installation instructions here](https://github.com/Roblox/vscode-rbx-lrdb)).

In order for breakpoints to work correctly, you'll need to disable the module reloading behavior that relies on `debug.loadmodule` by providing the `__NO_LOADMODULE__` global. To do so, create a `launch.json` file with the following contents:
```
{
	"version": "0.2.0",
	"configurations": [
		{
			"type": "roblox-lrdb",
			"request": "launch",
			"name": "Debug Unit Tests",
			"args": [
				"--load.project",
				"tests.project.json",
				"--run",
				"bin/spec.lua",
				"--lua.globals",
				"__NO_LOADMODULE__=true",
			],
			"cwd": "${workspaceFolder}",
			"stopOnEntry": true,
		},
	]
}
```

With module resetting disabled, most tests will only work if they're the _first_ test run. Use `itFOCUS` or `fit` to focus a single test in your test suite when debugging this way. Once you've set that up, use `Run -> Start Debugging` or the equivalent keyboard shortcut to start debugging.

### How to debug upstream tests

First, set a breakpoint in the ReactJS code you want to step through, like at the beginning of a specific test.

Note: You probably don't want to set a breakpoint on the `fit`, `it`, or `itFOCUS` line itself, but the first line of the test after that.

Note: Using https://github.com/Roblox/vscode-rbx-lrdb , you can set the same breakpoint in your equivalent Lua test. This allows you to single step in both the JS and Lua implementations, lock-step, to see where they deviate.

In VS Code, press `F1` key. Search for "auto attach" and select it.
![image](https://user-images.githubusercontent.com/1550766/104784482-3cd2c680-573d-11eb-899d-bedcd696dd2d.png)

Set the Auto Attach option to "Smart"
![image](https://user-images.githubusercontent.com/1550766/104784582-760b3680-573d-11eb-9ec0-fd63d37d8c32.png)

Open a JavaScript Debug Terminal, by first using View -> Terminal.
![image](https://user-images.githubusercontent.com/1550766/104784704-b7034b00-573d-11eb-88fc-7fb84397cbd6.png)

In the Terminal window, select "Create Debug JavaScript Terminal".
![image](https://user-images.githubusercontent.com/1550766/104784781-df8b4500-573d-11eb-8e32-9aa18cc87f9c.png)

In Debug JavaScript Terminal window, paste in the command you use to run the specific React test file you are interested in.
An example:
```yarn test --watch -v -r www-modern packages/react-reconciler/src/__tests__/ReactFiberHostContext-test.internal.js```
Note that to match the React feature set that Roblox is aligning to, you *need* to enable the variant *and* www-modern flags.

![image](https://user-images.githubusercontent.com/1550766/104785390-3fceb680-573f-11eb-9421-7df6c1440e3b.png)

You should see your status bar turn __orange__ (depending on your local theme), indicating that VS Code auto attach worked.

![image](https://user-images.githubusercontent.com/1550766/104785254-ecf4ff00-573e-11eb-8364-c1a310897fff.png)

Shortly after you see the status bar change colors to indicate an active debugger attachment, you should hit your breakpoint.
![image](https://user-images.githubusercontent.com/1550766/104785584-b4095a00-573f-11eb-8363-3b73a612e2a2.png)

Note that VS Code even tells you the value of the variables on the line. Pretty cool!

