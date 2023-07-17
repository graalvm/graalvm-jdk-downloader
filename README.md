> **Warning**
> The GraalVM JDK Downloader is no longer maintained.
> Please consider using [script-friendly URLs][script-friendly] or [SDKMAN!][sdkman] to download GraalVM.
> For all download options, visit: https://graalvm.org/downloads.

# GraalVM JDK Downloader

[![Tests](https://github.com/graalvm/graalvm-jdk-downloader/actions/workflows/main.yml/badge.svg)](https://github.com/graalvm/graalvm-jdk-downloader/actions/workflows/main.yml)

This repository is used to maintain and host the GraalVM JDK Downloader at https://get.graalvm.org/.

## Key Features

The GraalVM JDK Downloader

- supports [Oracle GraalVM][graalvm], [GraalVM Community Edition (CE)][ce], and [GraalVM Enterprise Edition (EE)][ee]. (EE requires a token, for more information see [Set Up a Download Token for GraalVM Enterprise Installations](#set-up-a-download-token-for-graalvm-enterprise-installations).)
- supports Linux, macOS, and Windows (via [Git Bash][git-bash], [Cygwin][cygwin], or [Windows Subsystem for Linux][wsl])
- is non-interactive and designed to be used in automated build pipelines or on developer machines
- sets up GraalVM installations in the current working directory (can be changed using the `--to` option)
- verifies checksums of downloaded artifacts before extracting if either `sha256sum` or `shasum` is available
- only requires `bash`, `curl`, and either `tar` (Linux/macOS) or `unzip` (Windows)


## Examples

```bash
# Download the latest GraalVM JDK (defaults to the latest release of the JDK and, if a token is found, to EE)
$ bash <(curl -sL https://get.graalvm.org/jdk)

# Download a specific GraalVM JDK
$ bash <(curl -sL https://get.graalvm.org/jdk) graalvm-jdk-20.0.1           # Oracle GraalVM for JDK 20
$ bash <(curl -sL https://get.graalvm.org/jdk) graalvm-community-jdk-17.0.7 # GraalVM Community Edition for JDK 17
$ bash <(curl -sL https://get.graalvm.org/jdk) graalvm-ce-java17-22.3.1     # GraalVM Community Edition 22.3.X and earlier
$ bash <(curl -sL https://get.graalvm.org/jdk) graalvm-ee-java17-22.3.1     # GraalVM Enterprise Edition 22.3.X and earlier

# Download a specific GraalVM JDK to a specific directory
$ bash <(curl -sL https://get.graalvm.org/jdk) --to "$HOME" graalvm-jdk-20.0.1

# Download a specific GraalVM JDK and install the Python and Node.js runtimes
$ bash <(curl -sL https://get.graalvm.org/jdk) -c python,nodejs graalvm-jdk-20.0.1
```

## Help

```
$ bash <(curl -sL https://get.graalvm.org/jdk) --help
GraalVM JDK Downloader v1.1.0

Usage:
  bash <(curl -sL https://get.graalvm.org/jdk) [opts] [graalvm-community-jdk-20.0.1]

Options:
  -c | --components   Comma-separated list of GraalVM components (for example,
                      '-c python,nodejs').
  -d | --debug        Enable debug mode.
  -h | --help         Show this help text.
  --no-progress       Disable progress printing.
  --to                Existing path to where artifacts will be downloaded (for example,
                      '--to "$HOME"'; current directory is the default).

Visit https://github.com/graalvm/graalvm-jdk-downloader for more information.
```

## Set Up a Download Token for GraalVM Enterprise Edition Installations

A valid download token is required for GraalVM Enterprise Edition installations.
To generate a download token, run the following command in a shell.
Note that, unlike the GraalVM JDK Downloader, this command is interactive and should not be executed as part of an automated build pipeline.
The command will help you store the generated token in the `$HOME/.gu/config` file.
Alternatively, you can also store the token in the `$GRAAL_EE_DOWNLOAD_TOKEN` environment variable.
Download tokens are associated with an email account, so treat them as confidential and encrypt them. (GitHub Actions, for example, supports [encrypted secrets][gha-secrets].)

```bash
$ bash <(curl -sL https://get.graalvm.org/ee-token)
```

Use the `--revoke` option to revoke download tokens:

```bash
# Revoke a persisted token
$ bash <(curl -sL https://get.graalvm.org/ee-token) --revoke
# Revoke a specific token
$ bash <(curl -sL https://get.graalvm.org/ee-token) --revoke mytoken
# Revoke all tokens for an email address
$ bash <(curl -sL https://get.graalvm.org/ee-token) --revoke jane@doe.com
```

## Contribute

We welcome code contributions. To get started, sign the [Oracle Contributor Agreement][oca] (OCA).

We only accept pull requests from committers that can be verified as having signed the OCA.


[ce]: https://github.com/graalvm/graalvm-ce-builds/releases
[cygwin]: https://www.cygwin.com/
[ee]: https://www.oracle.com/downloads/graalvm-downloads.html
[gha-secrets]: https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository
[git-bash]: https://git-scm.com/download/win
[graalvm]: https://graalvm.org
[oca]: https://oca.opensource.oracle.com
[script-friendly]: https://www.oracle.com/java/technologies/jdk-script-friendly-urls/
[sdkman]: https://sdkman.io/
[wsl]: https://docs.microsoft.com/en-us/windows/wsl/install
