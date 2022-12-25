# pg_user

[![Release](https://img.shields.io/github/v/release/frederikhs/pg_user.svg)](https://github.com/frederikhs/pg_user/releases/latest)
[![GoDoc](https://godoc.org/github.com/frederikhs/pg_user?status.svg)](https://godoc.org/github.com/frederikhs/pg_user)
[![Test](https://github.com/frederikhs/pg_user/actions/workflows/test.yml/badge.svg?branch=main)](https://github.com/frederikhs/pg_user/actions/workflows/test.yml)

Is a cli application for managing postgres users.

Features

- Creating new users with roles
- Deleting existing users
- Extending the validity of existing users
- Resetting passwords of existing users
- Listing existing users and their associated roles
- Listing all configured hosts
- Listing existing roles 

## Installation

### Linux amd64

```bash
# install
curl -L https://github.com/frederikhs/pg_user/releases/latest/download/pg_user-linux-amd64.tar.gz -o pg_user.tar.gz
tar -xvf pg_user.tar.gz
sudo chmod +x pg_user
sudo mv pg_user /usr/local/bin/pg_user

# clean up
rm pg_user.tar.gz
```

### Other

Other distributions or OS visit the [releases page](https://github.com/frederikhs/pg_user/releases/latest)

## Configuration

`pg_user` uses the format and location of the `.pgpass` file the resides in the `$HOME` directory of the user running the program.

---

Example of a host details in the `.pgpass` format

```
<HOST>:<PORT>:<DATABASE>:<USERNAME>:<PASSWORD>
```

## Examples of usage

`$ pg_user add test@example.org --host mydatabase.com`

This requires the hostname `mydatabase.com` must be configured in the `.pgpass` file

To also add roles to the user when creating use

`$ pg_user add test@example.org --host mydatabase.com --roles role1,role2`

## Development

This repository is very plain and simple and development of the application only required `go`.

`$ go run main.go hosts` will compile the application and list all configured hosts in your `.pgpass` file.

## Creating a new release

To create a new release of the application, a tag needs to be created first.

Look up existing tags

`$ git tag -l`

Choose the correct semantic versioning of the to be created release

Tag commit for release

`$ git tag vX.X.X`

Push tag

`$ git push origin vX.X.X`

Now that the tag has been pushed, a release needs to be create using GitHub. After creating a new release the [release](.github/workflows/release.yml) workflow will compile binaries for major platforms and architectures and attach them to the release.
