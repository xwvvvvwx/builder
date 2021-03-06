# builder

[![Build Status](https://travis-ci.org/xwvvvvwx/builder.svg?branch=master)](https://travis-ci.org/xwvvvvwx/builder)

`builder` is a tool to help manage dockerized project build environments.

Define your build environment in a Dockerfile and then define custom user commands to be executed in
that build environment.

The environment persists in the background between command executions to allow for incremental compilation.

## Motivation

- Each project has an isolated and reproducible build environment versioned alongside the code
- Easily work on different projects with incompatible build environments on the same machine
- Developers new to the project can be up and running with a functional build environment in seconds

## Usage

**Config**

Configuration is read from a `.builder.json` file in the project root

The following options can be set:

```
{
    "dockerfileDirectory": "<PATH_TO_DOCKERFILE_DIRECTORY>",
    "containerName": "<NAME_OF_BACKGROUND_CONTAINER>",
    "volumes": {
        "<HOST>":"<GUEST>"
    },
    "commands": {
        "name1": "command",
        "name2": "command",
        "name3": "command"
    }
    "privileged": bool
}
```

**Defaults**

- `containerName`: will fallback to a hash of the dockerfile directory name
- `priviliged`: will default to false

**Core Commands**

- `builder up`: spins up the environment specified in the .builder.json
- `builder exec`: executes a single command in the build environment
- `builder attach`: spawns a new bash shell in the build environment
- `builder destroy`: destroys the build environment
- `builder clean`: reset the environment to the state specified in the .builder.json

**User Defined Commands**

Users can define command aliases in the .builder.json. These commands can be accessed via `builder run <ALIAS_NAME>`.

The following aliases are special and can be accessed without the `run` keyword:

- `builder build`
- `builder verify`
- `builder package`
- `builder start`
- `builder benchmark`
