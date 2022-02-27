# Installing PostgreSQL on Ubunutu

## Linux downloads (Ubuntu)

PostgreSQL is available in all Ubuntu versions by default. However, Ubuntu "snapshots" a specific version of PostgreSQL that is then supported throughout the lifetime of that Ubuntu version. Other versions of PostgreSQL are available through the PostgreSQL apt repository.

## PostgreSQL Apt Repository

If the version included in your version of Ubuntu is not the one you want, you can use the `PostgreSQL Apt Repository`. This repository will integrate with your normal systems and patch management, and provide automatic updates for all supported versions of PostgreSQL throughout the support lifetime of PostgreSQL.

The PostgreSQL Apt Repository supports the current versions of Ubuntu:

* impish (21.10)
* hirsute (21.04)
* focal (20.04)
* bionic (18.04)

on the following architectures:

* amd64
* arm64 (18.04 and newer; LTS releases only)
* i386 (18.04 and older)
* ppc64el (LTS releases only)

To use the apt repository, follow these steps:

```sh
# Create the file repository configuration:
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'

# Import the repository signing key:
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

# Update the package lists:
sudo apt-get update

# Install the latest version of PostgreSQL.
# If you want a specific version, use 'postgresql-12' or similar instead of 'postgresql':
sudo apt-get -y install postgresql
```

For more information about the apt repository, including answers to frequent questions, please see the [PostgreSQL Apt Repository](https://wiki.postgresql.org/wiki/Apt) page on the wiki.

## Included in distribution

Ubuntu includes PostgreSQL by default. To install PostgreSQL on Ubuntu, use the apt-get (or other apt-driving) command:

```sh
apt-get install postgresql-12
```

The repository contains many different packages including third party addons. The most common and important packages are (substitute the version number as required):
|  |  |
| :----- | :---------- |
| postgresql-client-12 | client libraries and client binaries |
|postgresql-12 | core database server |
|libpq-dev | libraries and headers for C language frontend development |
|postgresql-server-dev-12 | libraries and headers for C language backend development |
