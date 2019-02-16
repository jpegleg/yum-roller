# yum-roller
use yum (Redhat/CentOS) and perform customized rolling unattended updates
via ansible

Create /etc/yroll-saturn.cfg with the repo or repos to pass to yum
yum update -y --enablerepo=$(cat /etc/yroll-saturn.cfg)

base,updates,ius


Schedule the yroll-saturn with ansible, puppet, crontab etc.

This code base uses ansible to do unattended maintenance.
Using shell scripts executed on each CentOS node,
perform yum updates and checks for kernel changes since
last update, rebooting if kernel change is found.

After each host is rebooted, a checker script is executed
on the node to ensure desired processes are online and 
that the server is healthy. If the server is found to be
unhealthy, send to an arbitrary api a custom message.

The hosts in the default playbook are split into 4 slices.
Use the slices to select high availability inspired choices.

Final check runs double checks, and if nodes are still found down, notify
the admin by sending a custom message to an arbitrary api
from the anisble host.

Then you can schedule your ansible playbooks with crontab entries if
you want to go unattended.

0 23 20 4 6 /usr/bin/ansible -i /etc/cluster-datacenter1 /etc/roll-yum-patch.yml
