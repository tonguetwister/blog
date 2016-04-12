---
layout: post
title: git on linux
---

## Using git on linux 


For some forgotten reason, I installed epel-release, by using this command: yum install epel-release. Then my yum install git does not work. I have to fix this problem by using yum upgrade ca-certificates --disablerepo=epel
      And, god knows why, yum install git workded after that.

After git is installed. A key needs to be created by ssh-keygen -t rsa . You supposed to ssh the git depo.

Creating a configure file is supposed to make this much easier. Thus, go to .ssh directory and vi config. the content of this config file is:
      Host whatever
           HostName github.com or enterprisegithub.com
           PreferredAuthentications publickey
           IdentityFile ~/.ssh/id_rsa
           User xxx

You need to chmod 755 config, odd, isn't it. linux has an odd logic. for example, this chmod and sudo command...More secure I guess. 

The next step is to add key by ssh-add ~/.ssh/id_rsa, then authentificate by ssh -T git@whatever 

Remember to go to the github web and manually add the key to the site, under settings/SSH keys

If it says that you are successful, then, git clone git@whatever:xxx/xxx.git 

I like linux. But Honestly speaking, I miss windows sometimes when I worke on linux. 
