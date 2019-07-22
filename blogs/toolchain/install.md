# Installing the Genesis Toolchain on Linux

There are a series of tools you'll need in order to work with Genesis. This is
a compilation of how to download and install each of those tools. Most of these
are static Go binaries, and therefore usually only require downloading the
binary and putting it into your path.

## Table of Contents

* [genesis, bosh, spruce, and safe](#genesis-bosh-spruce-and-safe)
* [jq](#jq)
* [vault](#vault)
* [cf](#cf)

<a name="genesis-bosh-spruce-and-safe"></a>
## Genesis, BOSH, Spruce, and Safe

```
wget -q -O - https://raw.githubusercontent.com/starkandwayne/homebrew-cf/master/public.key | sudo apt-key add -
echo "deb http://apt.starkandwayne.com stable main" | sudo tee /etc/apt/sources.list.d/starkandwayne.list
sudo apt-get update
sudo apt-get install genesis
```

<a name="jq"></a>
## jq

```
sudo apt-get install jq
```

<a name="vault"></a>
## Vault

The genesis installation installs a version of Vault, but it installs it from the apt
package which is very old. 

Determine the most recent version of Vault from:

https://www.vaultproject.io/downloads.html

Set the `LATEST_VAULT_VERSION` environment variable as shown below and run the following commands:

```
export LATEST_VAULT_VERSION=1.1.3
wget "https://releases.hashicorp.com/vault/${LATEST_VAULT_VERSION}/vault_${LATEST_VAULT_VERSION}_linux_amd64.zip"
sudo apt-get update
sudo apt-get install unzip
sudo unzip "vault_${LATEST_VAULT_VERSION}_linux_amd64.zip" -d /usr/local/bin
sudo chmod 0777 /usr/local/bin/vault
```

<a name="cf"></a>
## CF

While CF is not strictly required by Genesis, there's a good chance that if
you're using Genesis, you're looking at using Cloud Foundry.

```
wget -q -O - https://packages.cloudfoundry.org/debian/cli.cloudfoundry.org.key | sudo apt-key add -
echo "deb https://packages.cloudfoundry.org/debian stable main" | sudo tee /etc/apt/sources.list.d/cloudfoundry-cli.list
sudo apt-get update
sudo apt-get install cf-cli
```