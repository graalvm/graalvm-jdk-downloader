# GraalVM Download Scripts [![Tests](https://github.com/graalvm/get.graalvm.org/actions/workflows/main.yml/badge.svg)](https://github.com/graalvm/get.graalvm.org/actions/workflows/main.yml)

This repository is used to maintain and host GraalVM download scripts at https://get.graalvm.org/.

## Key Features

The download scripts

- support [GraalVM Community Edition (CE)][ce] and [GraalVM Enterprise Edition (EE)][ee] (requires a token, [see here](#set-up-a-download-token-for-graalvm-enterprise-installations))
- support Linux, macOS, and Windows (via [Git Bash][git-bash], [Cygwin][cygwin], or [Windows Subsystem for Linux][wsl])
- are non-interactive and designed to be used in automated build pipelines or on developer machines
- set up GraalVM installations in the current working directory by default (can be changed with the `--to` option)
- verify checksums of downloaded artifacts before extracting if `sha256sum` or `shasum` are available
- only require `bash`, `curl`, and either `tar` (Linux/macOS) or `unzip` (Windows)


## Download GraalVM Native Image

**Examples**

```bash
# Download the latest GraalVM Native Image (defaults to highest available JDK and to EE if a token is found)
$ bash <(curl -sL https://get.graalvm.org/native-image)

# Download a specific GraalVM Community Native Image
$ bash <(curl -sL https://get.graalvm.org/native-image) graalvm-ce-java17-22.2.0

# Download a specific GraalVM Enterprise Native Image to a specific directory
$ bash <(curl -sL https://get.graalvm.org/native-image) --to "$HOME" graalvm-ee-java17-22.2.0
```

**Help**

```
$ bash <(curl -sL https://get.graalvm.org/native-image) --help
GraalVM Native Image Downloader v0.0.4

Usage:
  bash <(curl -sL https://get.graalvm.org/native-image) [opts] [graalvm-ce-java17-22.2.0]

Options:
  -c | --components   Comma-separated list of GraalVM components (e.g.,
                      '-c python,nodejs')
  -d | --debug        Enable debug mode.
  -h | --help         Show this help text.
  --no-progress       Disable progress printing.
  --to                Existing path to where artifacts will be downloaded (e.g.,
                      '--to "$HOME"'; current directory is the default).

Visit https://github.com/graalvm/get.graalvm.org for more information.
```

## Download a GraalVM JDK

**Examples**

```bash
# Download the latest GraalVM JDK (defaults to highest available JDK and to EE if a token is found)
$ bash <(curl -sL https://get.graalvm.org/jdk)

# Download a specific GraalVM Community JDK
$ bash <(curl -sL https://get.graalvm.org/jdk) graalvm-ee-java17-22.2.0

# Download a specific GraalVM Enterprise JDK and install the Python and Node.js runtimes
$ bash <(curl -sL https://get.graalvm.org/jdk) -c python,nodejs graalvm-ee-java17-22.2.0
```

**Help**

```
$ bash <(curl -sL https://get.graalvm.org/jdk) --help
GraalVM JDK Downloader v0.0.4

Usage:
  bash <(curl -sL https://get.graalvm.org/jdk) [opts] [graalvm-ce-java17-22.2.0]

Options:
  -c | --components   Comma-separated list of GraalVM components (e.g.,
                      '-c python,nodejs')
  -d | --debug        Enable debug mode.
  -h | --help         Show this help text.
  --no-progress       Disable progress printing.
  --to                Existing path to where artifacts will be downloaded (e.g.,
                      '--to "$HOME"'; current directory is the default).

Visit https://github.com/graalvm/get.graalvm.org for more information.
```

### Set Up a Download Token for GraalVM Enterprise Installations

For GraalVM Enterprise installations, a valid download token is required.
To generate such a token, run the following command in a shell.
Note that, unlike the CLI downloaders, this command is interactive and should not be executed as part of an automated build pipeline.
Instead, run the command once and provide the token either via the `$GRAAL_EE_DOWNLOAD_TOKEN` environment variable or within the `$HOME/.gu/config` file.
Since tokens are tied to an email account, please treat them as confidential and encrypt them (GitHub Actions, for example, supports [encrypted secrets][gha-secrets])

```bash
$ bash <(curl -sL https://get.graalvm.org/ee-token)
```

## Contributing

We welcome code contributions. To get started, you will need to sign the [Oracle Contributor Agreement][oca] (OCA).

Only pull requests from committers that can be verified as having signed the OCA can be accepted.


[ce]: https://github.com/graalvm/graalvm-ce-builds/releases
[cygwin]: https://www.cygwin.com/
[ee]: https://www.oracle.com/downloads/graalvm-downloads.html
[gha-secrets]: https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository
[git-bash]: https://git-scm.com/download/win
[oca]: https://oca.opensource.oracle.com
[wsl]: https://docs.microsoft.com/en-us/windows/wsl/install
