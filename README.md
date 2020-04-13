#ERPNext basic docker
Final intention of this will be to have an ERPNext docker repo that can be deployed into a production-ready AWS Elastic Beanstalk.

#build
 * install docker-composer if not already `sudo curl -L "https://github.com/docker/compose/releases/download/1.25.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose` then `sudo chmod +x /usr/local/bin/docker-compose`
 * build with `docker-composer build`
 * then run with `docker run -it erpnext-basic-docker_appserv`

## References
 * [some tutorial on installing ERPnext](https://www.howtoforge.com/how-to-install-erpnext-on-ubuntu-1804/)
 * [Bench install reqs](https://github.com/frappe/bench/blob/master/docs/installation.md)
 * [Bench manual setup](https://frappe.io/docs/user/en/bench/guides/manual-setup.html)
 * [Frappé installation Wiki](https://github.com/frappe/frappe/wiki/The-Hitchhiker%27s-Guide-to-Installing-Frappe-on-Linux)
 * [lukptr/erpnext7](https://hub.docker.com/r/lukptr/erpnext7)
 * [Other good docker repo](https://github.com/pipech/erpnext-docker-debian)