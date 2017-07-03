# mitese-boot
Puppet 4 Boot code for server instances
inspired from https://github.com/MSMFG/tru-strap

this is cloned and run from your provision script (on terraform) or userdata script
The reponame is expected to be found on github.com 
```
"git@github.com:${init_repouser}/${init_reponame}.git"
```
for an example of a repo see https://github.com/neilmillard/puppet-dockerhost/tree/master/puppet
example

```
#!/bin/sh
init_role=jenkins
init_env=dev
init_repouser=neilmillard
init_reponame=server-provisioning
init_repobranch=master
init_configbucket=https://s3-eu-west-1.amazonaws.com/config.example.com

exec 1>/var/log/boot.log 2>&1
set -x

yum -y install git

cd /opt/
git clone https://github.com/neilmillard/mitese-boot.git
cd mitese-boot
chmod a+x provision.sh
./provision.sh --role ${init_role} --environment ${init_env} --repouser ${init_repouser} --reponame ${init_reponame} --repobranch ${init_repobranch}
```
