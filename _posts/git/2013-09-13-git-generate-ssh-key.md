---
layout: post
title: git push采用SSH方式
description: 在Centos64位系统下,git push采用SSH方式
keywords: [Centos,git]
category : git
tags: [Centos,git,ssh]
---
<H1>问题的来源</H1>
想要使用SSH的方法，不想每次提交的时候都要输入密码，这样让我烦死了

    [user@localhost test]$ git remote set-url origin ssh://git@github.com/username/repository.git
    [user@localhost test]$ git push
    The authenticity of host 'github.com (192.30.252.130)' can't be established.
    RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
    Are you sure you want to continue connecting (yes/no)? yes
    Warning: Permanently added 'github.com,192.30.252.130' (RSA) to the list of known hosts.
    Permission denied (publickey).
    fatal: The remote end hung up unexpectedly
    [user@localhost test]$ ssh -vT git@github.com
    OpenSSH_5.3p1, OpenSSL 1.0.0-fips 29 Mar 2010
    debug1: Reading configuration data /etc/ssh/ssh_config
    debug1: Applying options for *
    debug1: Connecting to github.com [192.30.252.129] port 22.
    debug1: Connection established.
    debug1: identity file /home/user/.ssh/identity type -1
    debug1: identity file /home/user/.ssh/id_rsa type -1
    debug1: identity file /home/user/.ssh/id_dsa type -1
    debug1: Remote protocol version 2.0, remote software version OpenSSH_5.9p1 Debian-5ubuntu1+github5
    debug1: match: OpenSSH_5.9p1 Debian-5ubuntu1+github5 pat OpenSSH*
    debug1: Enabling compatibility mode for protocol 2.0
    debug1: Local version string SSH-2.0-OpenSSH_5.3
    debug1: SSH2_MSG_KEXINIT sent
    debug1: SSH2_MSG_KEXINIT received
    debug1: kex: server->client aes128-ctr hmac-md5 none
    debug1: kex: client->server aes128-ctr hmac-md5 none
    debug1: SSH2_MSG_KEX_DH_GEX_REQUEST(1024<1024<8192) sent
    debug1: expecting SSH2_MSG_KEX_DH_GEX_GROUP
    debug1: SSH2_MSG_KEX_DH_GEX_INIT sent
    debug1: expecting SSH2_MSG_KEX_DH_GEX_REPLY
    debug1: Host 'github.com' is known and matches the RSA host key.
    debug1: Found key in /home/user/.ssh/known_hosts:1
    Warning: Permanently added the RSA host key for IP address '192.30.252.129' to the list of known hosts.
    debug1: ssh_rsa_verify: signature correct
    debug1: SSH2_MSG_NEWKEYS sent
    debug1: expecting SSH2_MSG_NEWKEYS
    debug1: SSH2_MSG_NEWKEYS received
    debug1: SSH2_MSG_SERVICE_REQUEST sent
    debug1: SSH2_MSG_SERVICE_ACCEPT received
    debug1: Authentications that can continue: publickey
    debug1: Next authentication method: publickey
    debug1: Trying private key: /home/user/.ssh/identity
    debug1: Trying private key: /home/user/.ssh/id_rsa
    debug1: Trying private key: /home/user/.ssh/id_dsa
    debug1: No more authentication methods to try.
    Permission denied (publickey).

下面是解决办法：
<br/><br/><br/>
[Generating SSH Keys](https://help.github.com/articles/generating-ssh-keys)<BR/>
If you have decided not to use the recommended(推荐的) HTTPS method, we can use SSH keys to establish a secure connection between your computer and GitHub. The steps below will walk you through generating an SSH key and then adding the public key to your GitHub account.

<h1>Step 1: Check for SSH keys</h1>
First, we need to check for existing ssh keys on your computer. Open up Terminal and run:

    cd ~/.ssh
    ls
    # Lists the files in your .ssh directory

我实际的运行效果：

    [user@localhost test]$ cd ~/.ssh
    [user@localhost .ssh]$ ls
    known_hosts

Check the directory listing to see if you have a file named either id_rsa.pub or id_dsa.pub. If you don't have either of those files go to step 2. Otherwise, you already have an existing keypair, and you can skip to step 3.
<br/>我目前没有id_rsa.pub和id_dsa.pub文件
<H1>Step 2: Generate a new SSH key</H1>

To generate a new SSH key, enter the code below. We want the default settings so when asked to enter a file in which to save the key, just press enter.

    $ssh-keygen -t rsa -C "your_email@example.com"
    # Creates a new ssh key, using the provided email as a label
    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/you/.ssh/id_rsa):
    $ssh-add id_rsa

Now you need to enter a passphrase.

    # Enter passphrase (empty for no passphrase): [Type a passphrase]
    # Enter same passphrase again: [Type passphrase again]
Which should give you something like this:

    Your identification has been saved in /home/you/.ssh/id_rsa.
    Your public key has been saved in /home/you/.ssh/id_rsa.pub.
    The key fingerprint is:
    01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your_email@example.com
我运行的实际效果：

    [user@localhost .ssh]$ ssh-keygen -t rsa -C "xinllaang@sina.com"
    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/user/.ssh/id_rsa): 
    Enter passphrase (empty for no passphrase): 
    Enter same passphrase again: 
    Your identification has been saved in /home/user/.ssh/id_rsa.
    Your public key has been saved in /home/user/.ssh/id_rsa.pub.
    The key fingerprint is:
    01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your_email@example.com
    The key's randomart image is:
    +--[ RSA 2048]----+
    |  +              |
    |     .  .        |
    |  . .    o       |
    |          +      |
    |          .      |
    |      .          |
    |       o  .      |
    |                 |
    |       o+        |
    +-----------------+
    [user@localhost .ssh]$ ls
    id_rsa  id_rsa.pub  known_hosts

<h1>Step 3: Add your SSH key to GitHub</h1>

Run the following code to copy the key to your clipboard.

    $ sudo apt-get install xclip
    # Downloads and installs xclip. If you don't have `apt-get`, you might need to use another installer (like `yum`)

    $ xclip -sel clip < ~/.ssh/id_rsa.pub
    # Copies the contents of the id_rsa.pub file to your clipboard

我的操作：

    [user@localhost .ssh]$ sudo yum install xclip
    [sudo] password for user: 
    Sorry, try again.
    [sudo] password for user: 
    user is not in the sudoers file.  This incident will be reported.
    
    [user@localhost .ssh]$ su root
    Password: 
    
    [root@localhost .ssh]# yum install xclip
    Loaded plugins: fastestmirror, priorities, refresh-packagekit, security
    Loading mirror speeds from cached hostfile
      * epel: mirrors.hustunique.com
      * nux-dextop: mirror.li.nux.ro
      Setting up Install Process
      Resolving Dependencies
      --> Running transaction check
      ---> Package xclip.x86_64 0:0.12-1.el6 will be installed
      --> Finished Dependency Resolution

      Dependencies Resolved

      ================================================================================
       Package          Arch              Version               Repository       Size
       ================================================================================
       Installing:
        xclip            x86_64            0.12-1.el6            epel             25 k

     Transaction Summary
     ================================================================================
     Install       1 Package(s)

     Total download size: 25 k
     Installed size: 43 k
     Is this ok [y/N]: y
     Downloading Packages:
     xclip-0.12-1.el6.x86_64.rpm                              |  25 kB     00:00     
     Running rpm_check_debug
     Running Transaction Test
     Transaction Test Succeeded
     Running Transaction
          Installing : xclip-0.12-1.el6.x86_64                                      1/1 
          Verifying  : xclip-0.12-1.el6.x86_64                                      1/1 

         Installed:
              xclip.x86_64 0:0.12-1.el6                                                     

          Complete!

    [root@localhost .ssh]# su user
    [user@localhost .ssh]$ xclip -sel clip < ~/.ssh/id_rsa.pub 

<LI>Go to your Account Settings</LI>
<LI>Click "SSH Keys" in the left sidebar</LI>
<LI>SSH Key buttonClick "Add SSH key"</LI>
<LI>Paste your key into the "Key" field</LI>
<LI>Click "Add key"</LI?
<LI>Confirm the action by entering your GitHub password</LI>
我的操作：
<br/>
<img src="/mjj/assets/images/git/github_ssh_setting.png">
<H1>Step 4: Test everything out</H1>

To make sure everything is working you'll now SSH to GitHub. When you do this, you will be asked to authenticate this action using your password, which for this purpose is the passphrase you created earlier. Don't change the git@github.com part. That's supposed to be there.

    $ssh -T git@github.com
    # Attempts to ssh to github

It's possible that you'll see this error message:

    ...
    Agent admitted failure to sign using the key.
    debug1: No more authentication methods to try.
    Permission denied (publickey).

This is a known problem with certain Linux distributions. For a resolution, see [our help article](https://help.github.com/articles/error-agent-admitted-failure-to-sign).

You may see this warning:

    # The authenticity of host 'github.com (207.97.227.239)' can't be established.
    # RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
    # Are you sure you want to continue connecting (yes/no)?

Don't worry, this is supposed to happen. Verify that the fingerprint matches the one here and type "yes".

    # Hi username! You've successfully authenticated, but GitHub does not provide shell access.

If that username is correct, you've successfully set up your SSH key. Don't worry about the shell access thing, you don't want that anyway.
<BR/>
If you see "access denied" please consider using [HTTPS](https://help.github.com/articles/error-permission-denied-publickey) instead of SSH. If you need SSH start at [these instructions](https://help.github.com/articles/error-permission-denied-publickey) for diagnosing the issue.
<br/>
我的操作过程：
    
    [user@localhost .ssh]$ ssh -T git@github.com
    Warning: Permanently added the RSA host key for IP address '192.30.252.131' to the list of known hosts.
    Hi user! You've successfully authenticated, but GitHub does not provide shell access.

<br/>
测试一下是否真的成功了：
    
    [user@localhost test]$ git push
    Counting objects: 9, done.
    Delta compression using up to 8 threads.
    Compressing objects: 100% (6/6), done.
    Writing objects: 100% (6/6), 1.47 KiB, done.
    Total 6 (delta 3), reused 0 (delta 0)
    To ssh://git@github.com/username/resposity.git
    2a28518..aa2d8e4  gh-pages -> gh-pages
    [user@localhost test]$ git remote -v
    origin	ssh://git@github.com/maijunjin/resposity.git (fetch)
    origin	ssh://git@github.com/username/resposity.git (push)
