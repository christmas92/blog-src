---
title: Ubuntu14.04安装配置Gitlab
date: 2016/07/22
tag:
- Linux
- Git
- 项目管理
---
#### <font face="黑体" >关于Ubuntu、CentOS其他版本下安装配置，Gitlab官网提供了相关教程</font>
<font face="黑体" size=4 >https://about.gitlab.com/downloads/</font>

#### 1. Install and configure the necessary dependencies

If you install Postfix to send email please select 'Internet Site' during setup. Instead of using Postfix you can also use Sendmail or <a href="https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/settings/smtp.md">configure a custom SMTP server</a> and <a href="https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/settings/smtp.md#smtp-on-localhost">configure it as an SMTP server.</a>

On Centos 6 and 7, the commands below will also open HTTP and SSH access in the system firewall.
```Bash
sudo apt-get install curl openssh-server ca-certificates postfix
```
<!-- more -->
#### 2. Add the GitLab package server and install the package
```Bash
curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
sudo apt-get install gitlab-ce
```
If you are not comfortable installing the repository through a piped script, you can find the <a href="https://packages.gitlab.com/gitlab/gitlab-ce/install">entire script here</a> and <a href="https://packages.gitlab.com/gitlab/gitlab-ce">select and download the package manually</a> and install using
```Bash
curl -LJO https://packages.gitlab.com/gitlab/gitlab-ce/packages/ubuntu/precise/gitlab-ce-XXX.deb/download
dpkg -i gitlab-ce-XXX.deb
```
#### 3. Configure and start GitLab
```Bash
sudo gitlab-ctl reconfigure
```
#### 执行第三步之前可对/etc/gitlab/gitlab.rb进行修改配置
1. 将external_url '<font>http</font>://gitadmin-VirtualBox'修改为external_url '<font>http</font>://IP地址'或进行DNS解析，使其他内网主机能够访问
2. 设置SMTP使其能够进行自动发送邮件提示(所提供邮箱必须开启STMP服务)   
<a href="https://gitlab.com/gitlab-org/omnibus-gitlab/blob/master/doc/settings/smtp.md">configure a custom SMTP server</a>   
上述提供了大部分邮箱的配置，下面提供163邮箱和QQ邮箱的配置：

```bash
#163邮箱配置
gitlab_rails['smtp_address'] = "smtp.163.com"
gitlab_rails['smtp_port'] = 25
gitlab_rails['smtp_user_name'] = "xxx@163.com"  //邮箱
gitlab_rails['smtp_password'] = "xxxxx"  //密码
gitlab_rails['smtp_domain'] = "163.com"
gitlab_rails['smtp_authentication'] = :login
gitlab_rails['smtp_enable_starttls_auto'] = true  

#修改gitlab配置的发信人
gitlab_rails['gitlab_email_from'] = "xxx@163.com"
user["git_user_email"] = "xxx@163.com"

#QQ邮箱配置
gitlab_rails['smtp_enable'] = true
gitlab_rails['smtp_address'] = "smtp.qq.com"
gitlab_rails['smtp_port'] = 25
gitlab_rails['smtp_user_name'] = "xxx@qq.com"
gitlab_rails['smtp_password'] = "xxxxx"   //开启smtp的独立密码
gitlab_rails['smtp_authentication'] = :plain
gitlab_rails['smtp_enable_starttls_auto'] = true

#修改gitlab配置的发信人
gitlab_rails['gitlab_email_from'] = "xxx@qq.com"
user["git_user_email"] = "xxx@qq.com"
```
#### 4. Browse to the hostname and login

On your first visit, you'll be redirected to a password reset screen to provide the password for the initial administrator account. Enter your desired password and you'll be redirected back to the login screen.

The default account's username is root. Provide the password you created earlier and login. After login you can change the username if you wish.

输入<font>http<font>://IP地址(gitlab.rb中配置的url)，首次访问会要求你修改管理员(root)密码。修改完成后登入，管理员用户名为root

#### 5. 生成和上传SSH key

设置管理员的邮箱(eg.admin@163.com)，生成SSH key的时候要用到。   
生成SSH key:   
打开Git Bash
```Bash
$ ssh-keygen -t rsa -C "admin@163.com"
```
按三下空格，表示生成五米密钥对，此时会在提示目录下生成一个密钥对，id_rsa为私钥，id_rsa.pub为公钥，公钥是要上传的。打开公钥文件复制里面的内容，在Gitlab管理后台Profile Setting->SSH Keys处粘贴，Add key完成。

上传SSH key后可以使用SSH进行远程pull/push
