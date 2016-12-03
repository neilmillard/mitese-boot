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
provision.sh --role ${init_role} --environment ${init_env} --repouser ${init_repouser} --reponame ${init_reponame} --repobranch ${init_repobranch}
```