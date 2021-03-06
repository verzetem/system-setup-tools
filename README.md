# system-setup-tools

## Docker Host Server Setup
Tested on Ubuntu 16.04+, Debian 7, 8, 9.

1. Add Admin/YOUR SSH Keys to authorized_keys for current user (root, i know, send a PR) - You should configure this w/ your .pub keys ;) 
1. Sets up common dependencies (nfs, zfs, aufs, curl, openssl, vim)
1. If not installed, install [Docker](https://www.docker.com)
1. If needed, it [creates new id_rsa & id_ed25519 keys](https://github.com/justsml/system-setup-tools/blob/master/README.md#setup-secure-rsa--ed25519-keys) for current $USER
1. Sets up Bash env w/ pimped out [.bashrc](https://raw.githubusercontent.com/justsml/system-setup-tools/master/home-scripts/.bashrc) and [.bash_aliases](https://raw.githubusercontent.com/justsml/system-setup-tools/master/home-scripts/.bash_aliases)
1. Sets [better defaults](https://russ.garrett.co.uk/2009/01/01/linux-kernel-tuning/) for [`net.core.rmem_max` `net.ipv4.tcp_max_syn_backlog` `net.core.somaxconn` `net.ipv4.ip_local_port_range`](https://tweaked.io/guide/kernel/)
1. Tuned for mongodb, redis, couchbase, et al. with [disabled transparent-hugepages](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/)
1. Adds `cgroup` support to GRUB, **update will require a reboot**

```sh
curl -L https://github.com/justsml/system-setup-tools/raw/master/server-setup-2016.sh | bash
```

--------------------------------

> #### Post 'Docker Host Server Setup' - SSL & a Secure Rancher Server

1. [Get Free Working SSL Cert(s) w/ Letsencrypt](https://github.com/justsml/system-setup-tools/blob/master/letsencrypt-docker.sh) 
1. [Setup HTTPS Rancher Server](https://github.com/justsml/ssl-proxy#example-for-a-rancher-server)

--------------------------------


## Setup [Secure RSA](https://github.com/justsml/system-setup-tools/blob/master/modules/ssh-key-generator.sh#L45) & [ED25519 Keys](https://github.com/justsml/system-setup-tools/blob/master/modules/ssh-key-generator.sh#L37)

```sh
curl -L https://raw.githubusercontent.com/justsml/system-setup-tools/master/modules/ssh-key-generator.sh | bash
```

--------------------------------

## 3 Steps: Get my `Bash on Steroids` .Env Scripts

#### 1. PRE REQ / PRE INSTALL

**Debian/Ubuntu:**
`apt-get update && apt-get install -y curl pv wget sudo apt-transport-https ca-certificates`

**OSX:**
`brew update && brew install curl pv wget`

**Windows:**
['upgrade'](https://google.com/search?q=install+ubuntu)

#### 2. Backup Current Scripts:

```sh
BACK_DIR=~/backups/profile-`date +%F`
mkdir -p $BACK_DIR
cp -ra ~/.bash* $BACK_DIR
```

### Choose between:

#### 3a. APPEND bashrc & bash_aliases (Klunky, needs cleanup in post...) 
`curl -sSL https://raw.githubusercontent.com/justsml/system-setup-tools/master/home-scripts/.bashrc >> ~/.bashrc    &&    curl -sSL https://raw.githubusercontent.com/justsml/system-setup-tools/master/home-scripts/.bash_aliases >> ~/.bash_aliases`
#### 3b. OVERWRITE existing scripts, (don't lose existing env vars you may need, see step ##2: Backup)
`curl -sSL https://raw.githubusercontent.com/justsml/system-setup-tools/master/home-scripts/.bashrc > ~/.bashrc    &&    curl -sSL https://raw.githubusercontent.com/justsml/system-setup-tools/master/home-scripts/.bash_aliases > ~/.bash_aliases`

