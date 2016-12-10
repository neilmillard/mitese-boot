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
init_role=webserver
init_env=dev
init_repouser=mitese
init_reponame=server-provisioning
exec 1>/var/log/boot.log 2>&1
set -x

yum -y update
yum -y install git

cd /opt/
git clone https://github.com/neilmillard/mitese-boot.git
chmod +x /opt/provision.sh
./provision.sh --role ${init_role} --environment ${init_env} --repouser ${init_repouser} --reponame ${init_reponame} --repobranch ${init_repobranch}
```
