# yum-roller
use yum (Redhat/CentOS) and perform customized rolling updates

Create /etc/yroll-saturn.cfg with the repo or repos to pass to yum
yum update -y --enablerepo=$(cat /etc/yroll-saturn.cfg)

base,updates,ius


Schedule the yroll-saturn with ansible, puppet, crontab etc.
