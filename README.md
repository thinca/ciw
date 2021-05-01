# ciw - CLI Install Wrapper

![](https://img.shields.io/badge/version-v0.0.1-blue)

A wrapper to install cli binary from language associated package manager.


## Requirements

- `jq`
- `curl`

Following commands are required for each plugins.

- `go`
- `npm`
- `cargo`


## Install

Put `bin/ciw` to your `$PATH`.  This is just a Bash script.

```shell
$ curl https://raw.githubusercontent.com/thinca/ciw/master/bin/ciw -o path/to/bin/ciw
$ chmod a+x path/to/bin/ciw
```


## Usage

### Install app

```shell
$ ciw install cargo:ripgrep
```

Arguments of `ciw install` takes a form like `${type}:${package}` or `${type}:${package}@${version}`.

```shell
$ ciw install go:github.com/mattn/jvgrep/v5@v5.8.9
```


### List installed apps

```shell
$ ciw list
cargo:ripgrep
```


### Update apps

`ciw update` without arguments to update all installed apps.

```shell
$ ciw update
```

Or, `ciw update` with arguments to update specified apps.

```shell
$ ciw update cargo:ripgrep
```

`ciw` checks if a newer version exists, and does nothing if there is no newer version.

Note that only apps without `@${version}` can be updated.


### Uninstall app

```shell
$ ciw uninstall cargo:ripgrep
```


## Restore

You can restore all apps from `ciw list`.

```
# Save your apps list to "ciw.list" file
$ ciw list > ciw.list

# Restore your apps from saved list
$ ciw install $(< ciw.list)
```


## Group

By default, all apps are installed to `main` group.

You can change group by `-g` or `--group` option or `$CIW_GROUP` environment variable.

```shell
$ ciw -g local install cargo:ripgrep
```

Installed app is placed at each group, but CLIs are linked at `$CIW_INSTALL_PATH` as same.

`ciw list` lists only the specified group.


## Environment Variables

### `$CIW_INSTALL_PATH`

Installed apps are linked from this directory.
You should add this directory to `$PATH`.

Default: `${HOME}/.local/bin`


### `$CIW_GROUP`

Group name.

Default: `main`


### `$CIW_DATA_PATH`

Base directory to place data of `ciw`.

Default:

- `${XDG_DATA_HOME}/ciw` (if `${XDG_DATA_HOME}` is present.)
- `${HOME}/.local/share/ciw`


### `$CIW_PACKAGES_PATH`

Base directory to install apps.

Default: `${CIW_DATA_PATH}/pkg/${CIW_GROUP}`

### `$CIW_CACHE_PATH`

Some plugin makes cache data under this directory.

Default:

- `${XDG_CACHE_HOME}/ciw` (if `${XDG_CACHE_HOME}` is present.)
- `${HOME}/.cache/ciw`


## License

[Zlib License](LICENSE.txt)


## Author

thinca <thinca@gmail.com>
