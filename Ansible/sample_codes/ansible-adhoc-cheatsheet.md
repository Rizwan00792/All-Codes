
# Ansible Ad-Hoc Commands – Cheat Sheet

## Package Management
ansible all -b -m package -a "name=git state=present"
ansible all -b -m apt -a "name=nginx state=present update_cache=yes"
ansible all -b -m yum -a "name=nginx state=present"
ansible all -b -m dnf -a "name=nginx state=present"

## Services
ansible all -b -m service -a "name=nginx state=started"
ansible all -b -m systemd -a "name=nginx state=restarted"

## Files & Permissions
ansible all -b -m file -a "path=/opt/app state=directory mode=0755"
ansible all -b -m copy -a "src=/tmp/a.txt dest=/opt/app/a.txt"
ansible all -b -m lineinfile -a "path=/etc/sysctl.conf line='net.ipv4.ip_forward=1'"

## Users & Security
ansible all -b -m group -a "name=devops"
ansible all -b -m user -a "name=deploy group=devops"
ansible all -b -m cron -a "name=cleanup hour=1 job='rm -f /tmp/*.log'"

## Networking
ansible all -b -m firewalld -a "service=http permanent=yes state=enabled"
ansible all -b -m ufw -a "rule=allow port=80 proto=tcp"

## Downloads
ansible all -b -m get_url -a "url=https://example.com/app.tar.gz dest=/tmp/app.tar.gz"
ansible all -b -m unarchive -a "src=/tmp/app.tar.gz dest=/opt/app remote_src=yes"

## Commands
ansible all -m command -a "uptime"
ansible all -b -m shell -a "echo hello > /tmp/hello.txt"

## Containers
ansible all -b -m docker_image -a "name=nginx source=pull"
ansible all -b -m docker_container -a "name=nginx image=nginx state=started ports=80:80"

## Kubernetes
ansible localhost -m k8s -a "state=present src=deployment.yml"
ansible localhost -m helm -a "name=myapp chart_ref=./myapp-chart"

## System
ansible all -b -m hostname -a "name=prod-server"
ansible all -b -m timezone -a "name=Asia/Kolkata"
ansible all -b -m sysctl -a "name=net.ipv4.ip_forward value=1 state=present"
