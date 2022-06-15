dcrnctl
======

[![Build Status](https://github.com/Decred-Next/dcrnctl/workflows/Build%20and%20Test/badge.svg)](https://github.com/Decred-Next/dcrnctl/actions)
[![ISC License](https://img.shields.io/badge/license-ISC-blue.svg)](http://copyfree.org)
[![Go Report Card](https://goreportcard.com/badge/github.com/Decred-Next/dcrnctl)](https://goreportcard.com/report/github.com/Decred-Next/dcrnctl)

Dcrctl is a command-line client for interacting with the JSON-RPC servers of
[dcrnd](https://github.com/Decred-Next/dcrnd) and
[dcrnwallet](https://github.com/Decred-Next/dcrnwallet).

## Usage

In its default configuration, dcrnctl connects to dcrnd's mainnet RPC port on
localhost.  The `--wallet` and `--testnet` flags change these defaults to the
dcrnwallet RPC port and/or testnet ports.  The `--rpcserver/-s` flag can be used
to specify other hostnames or IP addresses of the server, and can also be used
to override the port defaults.

Dcrctl will attempt to read dcrnd and dcrnwallet config files for the
user/password authentication.  If these fields cannot be read, dcrnctl must be
manually configured with the correct authentication.  Permanent configuration
changes may be written to a config file in a platform-specific location:

* macOS: `~/Library/Application Support/Dcrctl/dcrnctl.conf`
* Windows: `%LOCALAPPDATA%\Dcrctl\dcrnctl.conf`
* Linux and other Unix: `~/.dcrnctl/dcrnctl.conf`

## Build and installation

The latest dcrnctl may be built in a single command without cloning this
repository:

```
$ GO111MODULE=on go get Decred-Next.org/dcrnctl
```

Appending `@master` to this will perform a release build using the latest code
from the master branch.  This may be useful to execute RPC methods not yet found
in the latest Decred release.

Alternatively, a development build can be performed by running `go install` in a
locally checked-out repository.

## Developing

When developing either the dcrnd or dcrnwallet RPC servers and making
modifications to the RPC methods, you may want to build a development version of
dcrnctl supporting these changes.  Due to dcrnctl being built around
package-global method registrations and reflection, supporting these changes
only requires building with the updated packages.  To perform this, module
replacements may be utilized to point to development versions of dcrnd and
dcrnwallet in your build environment:

```
$ go mod edit -replace=github.com/Decred-Next/dcrnd/rpc/jsonrpc/types/v2=../dcrnd/rpc/jsonrpc/types
$ go mod edit -replace=Decred-Next.org/dcrnwallet/v2=../dcrnwallet
```

These replaces should be removed prior to committing any updated module
requires:

```
$ go mod edit -dropreplace=github.com/Decred-Next/dcrnd/rpc/jsonrpc/types/v2
$ go mod edit -dropreplace=Decred-Next.org/dcrnwallet/v2
```

## Contact

If you have any further questions you can find us at:

https://Decred-Next.org/community

## Issue Tracker

The [integrated github issue tracker](https://github.com/Decred-Next/dcrnctl/issues)
is used for this project.

## License

dcrnctl is licensed under the [copyfree](http://copyfree.org) ISC License.
