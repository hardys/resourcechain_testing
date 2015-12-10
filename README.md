# resourcechain_testing
Temporary repo for ResourceChain testing

Requires heat with https://review.openstack.org/#/c/250010/ applied

Tested on devstack with fedora-software-config image created like this:

https://github.com/openstack/heat-templates/tree/master/hot/software-config/elements

diskimage-builder/bin/disk-image-create vm fedora selinux-permissive \
  os-collect-config os-refresh-config os-apply-config \
  heat-config-cfn-init \
  heat-config-puppet \
  heat-config-script \
  ntp \
  -o fedora-software-config.qcow2

glance image-create --disk-format qcow2 --container-format bare --name fedora-software-config < fedora-software-config.qcow2

I also created a special nova flavor and a default keypair

nova flavor-create m1.mini auto 1024 0 2

nova keypair-add default --pub-key ~/.ssh/id_rsa.pub
