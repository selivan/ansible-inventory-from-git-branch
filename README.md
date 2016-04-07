[Ansible best practices](http://docs.ansible.com/ansible/playbooks_best_practices.html#how-to-differentiate-staging-vs-production) recommend to have separate inventory files for production and testing environments. You may also keep your ansible files in git and have separate branches for environments. In such setup it's easy to confuse current branch and apply testing changes to production. It's more convinient and error-prone to automatically switch inventory according to currenty used git branch: if you checkout branch "prod" or named like "*.prod" - `hosts.prod` inventory file is used; otherwise `hosts.test` is used.

How it works: local `ansible.cfg` references to `hosts` inventory file, which is symlink to actual inventory for current branch. `hosts` is added to `.gitignore` to prevent merge conflicts between branches. Git hook is used to change `hosts` symlink each time user switches to other branch.

**P.S.** If this code is useful for you - don't forget to put a star on it's [github repo](https://github.com/selivan/ansible-inventory-from-git-branch).
