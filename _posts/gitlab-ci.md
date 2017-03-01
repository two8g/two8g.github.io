---
layout: post
title: gitlab ci
categories: Dev/Ops
tags: gitlab ci 持续集成 自动部署
---

# gitlab-ci尝试

## 写在前面

DRY,一切程序能做的事,不要手动重复做.
既然我已经搭建好了gitlab,jenkins,maven-nexus...为何不更进异步呢?

## gitlab-ci


## Runners

### Runners 安装

[Install GitLab Runner using the official GitLab repositories](https://docs.gitlab.com/runner/install/linux-repository.html#install-gitlab-runner-using-the-official-gitlab-repositories)

```shell
[root@xxx ~]# curl -sSL https://get.docker.com/ | sh
+ sh -c 'sleep 3; yum -y -q install docker-engine'
Repository base is listed more than once in the configuration
Repository updates is listed more than once in the configuration
Repository extras is listed more than once in the configuration
Repository centosplus is listed more than once in the configuration
warning: rpmts_HdrFromFdno: Header V4 RSA/SHA1 Signature, key ID 2c52609d: NOKEY
Importing GPG key 0x2C52609D:
 Userid: "Docker Release Tool (releasedocker) <docker@docker.com>"
 From  : https://yum.dockerproject.org/gpg

If you would like to use Docker as a non-root user, you should now consider
adding your user to the "docker" group with something like:

  sudo usermod -aG docker your-user

Remember that you will have to log out and back in for this to take effect!

[root@xxx ~]# curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-ci-multi-runner/script.rpm.sh | sudo bash
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
101  6488    0  6488    0     0   2003      0 --:--:--  0:00:03 --:--:-- 10364
Detected operating system as centos/6.
Checking for curl...
Detected curl...
Downloading repository file: https://packages.gitlab.com/install/repositories/runner/gitlab-ci-multi-runner/config_file.repo?os=centos&dist=6&source=script
done.
Installing pygpgme to verify GPG signatures...
Loaded plugins: security
Repository base is listed more than once in the configuration
Repository updates is listed more than once in the configuration
Repository extras is listed more than once in the configuration
Repository centosplus is listed more than once in the configuration
https://packages.gitlab.com/runner/gitlab-ci-multi-runner/el/6/SRPMS/repodata/repomd.xml: [Errno 14] problem making ssl connection
Trying other mirror.
Error: Cannot retrieve repository metadata (repomd.xml) for repository: runner_gitlab-ci-multi-runner-source. Please verify its path and try again
Installing yum-utils...
Loaded plugins: security
Repository base is listed more than once in the configuration
Repository updates is listed more than once in the configuration
Repository extras is listed more than once in the configuration
Repository centosplus is listed more than once in the configuration
https://packages.gitlab.com/runner/gitlab-ci-multi-runner/el/6/SRPMS/repodata/repomd.xml: [Errno 14] problem making ssl connection
Trying other mirror.
Error: Cannot retrieve repository metadata (repomd.xml) for repository: runner_gitlab-ci-multi-runner-source. Please verify its path and try again
Generating yum cache for runner_gitlab-ci-multi-runner...
Repository base is listed more than once in the configuration
Repository updates is listed more than once in the configuration
Repository extras is listed more than once in the configuration
Repository centosplus is listed more than once in the configuration
Importing GPG key 0xE15E78F4:
 Userid: "GitLab B.V. (package repository signing key) <packages@gitlab.com>"
 From  : https://packages.gitlab.com/runner/gitlab-ci-multi-runner/gpgkey

The repository is setup! You can now install packages.
[root@xxx ~]# sudo yum install gitlab-ci-multi-runner
Loaded plugins: security
Repository base is listed more than once in the configuration
Repository updates is listed more than once in the configuration
Repository extras is listed more than once in the configuration
Repository centosplus is listed more than once in the configuration
runner_gitlab-ci-multi-runner-source/signature                                                                                                                                               |  836 B     00:00
Retrieving key from https://packages.gitlab.com/runner/gitlab-ci-multi-runner/gpgkey
Importing GPG key 0xE15E78F4:
 Userid: "GitLab B.V. (package repository signing key) <packages@gitlab.com>"
 From  : https://packages.gitlab.com/runner/gitlab-ci-multi-runner/gpgkey
Is this ok [y/N]: y
runner_gitlab-ci-multi-runner-source/signature                                                                                                                                               |  951 B     00:06 ...
runner_gitlab-ci-multi-runner-source/primary                                                                                                                                                 |  175 B     00:00
Setting up Install Process
Resolving Dependencies
--> Running transaction check
---> Package gitlab-ci-multi-runner.x86_64 0:1.11.0-1 will be installed
--> Processing Dependency: git for package: gitlab-ci-multi-runner-1.11.0-1.x86_64
--> Running transaction check
---> Package git.x86_64 0:1.7.1-4.el6_7.1 will be installed
--> Processing Dependency: perl-Git = 1.7.1-4.el6_7.1 for package: git-1.7.1-4.el6_7.1.x86_64
--> Processing Dependency: perl(Git) for package: git-1.7.1-4.el6_7.1.x86_64
--> Running transaction check
---> Package perl-Git.noarch 0:1.7.1-4.el6_7.1 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

====================================================================================================================================================================================================================
 Package                                                Arch                                   Version                                          Repository                                                     Size
====================================================================================================================================================================================================================
Installing:
 gitlab-ci-multi-runner                                 x86_64                                 1.11.0-1                                         runner_gitlab-ci-multi-runner                                  25 M
Installing for dependencies:
 git                                                    x86_64                                 1.7.1-4.el6_7.1                                  base                                                          4.6 M
 perl-Git                                               noarch                                 1.7.1-4.el6_7.1                                  base                                                           28 k

Transaction Summary
====================================================================================================================================================================================================================
Install       3 Package(s)

Total download size: 30 M
Installed size: 80 M
Is this ok [y/N]: y
Downloading Packages:
(1/3): git-1.7.1-4.el6_7.1.x86_64.rpm                                                                                                                                                        | 4.6 MB     00:04
(2/3): gitlab-ci-multi-runner-1.11.0-1.x86_64.rpm                                                                                                                                            |  25 MB     00:02
(3/3): perl-Git-1.7.1-4.el6_7.1.noarch.rpm                                                                                                                                                   |  28 kB     00:00
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                                                                               3.6 MB/s |  30 MB     00:08
Running rpm_check_debug
Running Transaction Test
Transaction Test Succeeded
Running Transaction
  Installing : git-1.7.1-4.el6_7.1.x86_64                                                                                                                                                                       1/3
  Installing : perl-Git-1.7.1-4.el6_7.1.noarch                                                                                                                                                                  2/3
  Installing : gitlab-ci-multi-runner-1.11.0-1.x86_64                                                                                                                                                           3/3
GitLab Runner: creating gitlab-runner...
  Verifying  : perl-Git-1.7.1-4.el6_7.1.noarch                                                                                                                                                                  1/3
  Verifying  : gitlab-ci-multi-runner-1.11.0-1.x86_64                                                                                                                                                           2/3
  Verifying  : git-1.7.1-4.el6_7.1.x86_64                                                                                                                                                                       3/3

Installed:
  gitlab-ci-multi-runner.x86_64 0:1.11.0-1

Dependency Installed:
  git.x86_64 0:1.7.1-4.el6_7.1                                                                           perl-Git.noarch 0:1.7.1-4.el6_7.1

Complete!

```

### Runners使用

https://docs.gitlab.com/runner/commands/README.html

#### Register

```shell
[root@xxx ~]# gitlab-runner register
Running in system-mode.                            
                                                   
Please enter the gitlab-ci coordinator URL (e.g. https://gitlab.com/):
https://gitlab.com/
Please enter the gitlab-ci token for this runner:
xyzxyz
Please enter the gitlab-ci description for this runner:
[xxx]: simple
Please enter the gitlab-ci tags for this runner (comma separated):
simple,shell
Whether to run untagged builds [true/false]:
[false]: 
Registering runner... succeeded                     runner=yBdLVN_L
Please enter the executor: docker, parallels, shell, ssh, docker+machine, docker-ssh, virtualbox, docker-ssh+machine, kubernetes:
shell	
Runner registered successfully. Feel free to start it, but if it's running already the config should be automatically reloaded! 
```


## 参考

1. [gitlab-ci-help](https://gitlab.com/help/ci/README.md)
1. [gitlab-ci-help中文](https://doc.gitlab.cc/ce/ci/README.html)
1. [.gitlab-ci.yml语法](https://gitlab.com/help/ci/yaml/README.md)
1. [Gitlab CI 简介](http://www.jianshu.com/p/1c1ecd3ce7c0)
1. [Runners](https://gitlab.com/help/ci/runners/README.md)
1. [Runners Install](https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/#installation)