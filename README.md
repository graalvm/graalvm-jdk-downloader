# GraalVM JDK Downloader

[![Tests](https://github.com/graalvm/get.graalvm.org/actions/workflows/main.yml/badge.svg)](https://github.com/graalvm/get.graalvm.org/actions/workflows/main.yml)

This repository is used to maintain and host the GraalVM JDK Downloader at https://get.graalvm.org/.

## Key Features

The GraalVM JDK Downloader

- supports [GraalVM Community Edition (CE)][ce] and [GraalVM Enterprise Edition (EE)][ee]. (EE requires a token, for more information see [Set Up a Download Token for GraalVM Enterprise Installations](#set-up-a-download-token-for-graalvm-enterprise-installations).)
- supports Linux, macOS, and Windows (via [Git Bash][git-bash], [Cygwin][cygwin], or [Windows Subsystem for Linux][wsl])
- is non-interactive and designed to be used in automated build pipelines or on developer machines
- sets up GraalVM installations in the current working directory by default (can be changed using the `--to` option)
- verifies checksums of downloaded artifacts before extracting if either `sha256sum` or `shasum` is available
- only requires `bash`, `curl`, and either `tar` (Linux/macOS) or `unzip` (Windows)


## Examples

```bash
# Download the latest GraalVM JDK incl. Native Image (defaults to the latest release of the JDK and, if a token is found, to EE)
$ bash <(curl -sL https://get.graalvm.org/jdk)

# Download a specific GraalVM CE JDK incl. Native Image
$ bash <(curl -sL https://get.graalvm.org/jdk) graalvm-ce-java17-22.2.0

# Download a specific GraalVM EE JDK incl. Native Image to a specific directory
$ bash <(curl -sL https://get.graalvm.org/jdk) --to "$HOME" graalvm-ee-java17-22.2.0

# Download a specific GraalVM EE JDK incl. Native Image and install the Python and Node.js runtimes
$ bash <(curl -sL https://get.graalvm.org/jdk) -c python,nodejs graalvm-ee-java17-22.2.0
```

## Help

```
$ bash <(curl -sL https://get.graalvm.org/jdk) --help
GraalVM JDK Downloader v0.0.4

Usage:
  bash <(curl -sL https://get.graalvm.org/jdk) [opts] [graalvm-ce-java17-22.2.0]

Options:
  -c | --components   Comma-separated list of GraalVM components (for example,
                      '-c python,nodejs').
  -d | --debug        Enable debug mode.
  -h | --help         Show this help text.
  --no-progress       Disable progress printing.
  --to                Existing path to where artifacts will be downloaded (for example,
                      '--to "$HOME"'; current directory is the default).

Visit https://github.com/graalvm/get.graalvm.org for more information.
```

## Set Up a Download Token for GraalVM Enterprise Installations

A valid download token is required for GraalVM Enterprise installations.
To generate a download token, run the following command in a shell.
Note that, unlike the GraalVM JDK Downloader, this command is interactive and should not be executed as part of an automated build pipeline.
The command will help you store the generated token in the `$HOME/.gu/config` file.
Alternatively, you can also store the token in the `$GRAAL_EE_DOWNLOAD_TOKEN` environment variable.
Download tokens are associated with an email account, so treat them as confidential and encrypt them. (GitHub Actions, for example, supports [encrypted secrets][gha-secrets].)

```bash
$ bash <(curl -sL https://get.graalvm.org/ee-token)
```

## Contribute

We welcome code contributions. To get started, sign the [Oracle Contributor Agreement][oca] (OCA).

We only accept pull requests from committers that can be verified as having signed the OCA.


[ce]: https://github.com/graalvm/graalvm-ce-builds/releases
[cygwin]: https://www.cygwin.com/
[ee]: https://www.oracle.com/downloads/graalvm-downloads.html
[gha-secrets]: https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository
[git-bash]: https://git-scm.com/download/win
[oca]: https://oca.opensource.oracle.com
[wsl]: https://docs.microsoft.com/en-us/windows/wsl/install
