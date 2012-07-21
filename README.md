# bosh-solo

Develop, test and deploy BOSH releases without BOSH

This is a tool to iteratively develop and test a BOSH release in a local or remote VM, without needing to use a running BOSH system.

## Installation

The project is installed and operated by the [SM framework](https://github.com/sm/sm). Installation instructions for SM, git

Install SM and git:

```
curl -L https://raw.github.com/sm/sm/master/bin/sm-installer | sh
source /etc/profile.d/sm.sh
apt-get install git-core -y
```

Install bosh-solo and prepare the target machine/VM for deploying a BOSH release:

```
sm ext install bosh-solo git://github.com/drnic/bosh-solo.git
sm bosh-solo install_dependencies
```

### Updating bosh-solo

```
sm ext update bosh-solo
```

## Usage

The are two modes to use: a local Vagrant VM or a remote VM.

### Vagrant usage

Coming soon.

### Remote VM usage

Clone your BOSH release into your remote VM. Create a dev release (which will also sync download any blobs that are required), and run the bosh-solo `update` command.

```
git clone git://location.com/your/bosh_release.git
cd bosh_release
bosh create release
sm bosh-solo update path/to/manifest.yml
```

Whenever you update your BOSH release repository, you can fetch the changes and update your remote VM with the new packages and jobs:

```
git pull origin master
bosh create release --force
sm bosh-solo update path/to/manifest.yml
```


### Example usage

```
git clone git://github.com/drnic/bosh-sample-release.git -b examples
cd bosh-sample-release
sm bosh-solo update examples/solo.yml
```

The complete, end-to-end tutorial is therefore:

```
sudo su -
curl -L https://raw.github.com/sm/sm/master/bin/sm-installer | sh
source /etc/profile.d/sm.sh
apt-get install git-core -y

sm ext install bosh-solo git://github.com/drnic/bosh-solo.git
sm bosh-solo install_dependencies

git clone git://github.com/drnic/bosh-sample-release.git -b examples
cd bosh-sample-release
bosh create release
sm bosh-solo update examples/solo.yml
```