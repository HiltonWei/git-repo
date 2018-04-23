<<<<<<< HEAD
Repo部署

项目git仓库比较多，一次修改可能涉及多个仓库，所以要应用多仓库功能，引入Repo。

#### 背景：
- Git环境搭配好
- 安装Python27（必须是2.7，3.x版本暂时不支持）

#### 1、

获取 url，本地下载并设置环境变量。[(esrlabs 参考)](https://github.com/esrlabs/git-repo)

<pre>
md %USERPROFILE%\bin

curl https://raw.githubusercontent.com/esrlabs/git-repo/stable/repo > 
%USERPROFILE%/bin/repo

curl https://raw.githubusercontent.com/esrlabs/git-repo/stable/repo.cmd > 
%USERPROFILE%/bin/repo.cmd

</pre>

`%USERPROFILE%\bin` （基本为 C:\Users\Administrator\bin）加入到环境变量中，cmd下方可执行repo命令。Win10需要重启，环境变量方可生效。

#### 2、添加节点
<pre>
   ~/.gitconfig:

  [portable]
      windowsNoSymlinks = true
</pre>

#### 3、执行repo命令
基础是，当前目录支持repo，也就是已经执行过 repo init操作。(**Win10下 要用管理员权限的cmd**，否则报 `repo GitError: cannot initialize work tree`。)

举例:
	`repo init -u git@github.com:hiltonwei/manifest -b master -m def.xml`

`-b` 指定分支
`-m` 指定工程映射
<p>
manifest/default.xml 采用的 https://github.com/hiltonwei
<p>
manifest/def.xml      采用的 git@github.com:hiltonwei


#### 4、 repo --trace sync 带trace的日志

#### 5、repo 命令略

#### 6、其他问题：
《3》 中，如果采用def.xml中的git协议，会找不到项目地址。
`YourPath\.repo\projects\atree.git\Config`文件中的 url是错误的。
`url = git@github.com:hiltonwei/git@github.com:HiltonWei/atree )`

需要修改 repo的python文件，manifest_xml.py的 Line:95 (`_resolveFetchUrl()` 函数内拼接 url的函数实现)。

<pre>
Line:95 (_resolveFetchUr()） ）

    if manifestUrl.find('git@') != -1: 
      url = url#_print("find git@")
    elif manifestUrl.find(':') != manifestUrl.find('/') - 1:
      url = urllib.parse.urljoin('gopher://' + manifestUrl, url)
      url = re.sub(r'^gopher://', '', url)
    else:
      url = urllib.parse.urljoin(manifestUrl, url)
</pre>


=======

**NOT MAINTAINED ANYMORE**
Please use the up-to-date version on the [stable branch](https://github.com/esrlabs/git-repo/tree/stable).

## Repo for Microsoft Windows and Linux ##

Note: No support for Mac (untested).

This is E.S.R.Labs Repo - just like Google Repo but this one also runs under Microsoft Windows.
For more information, see [Version Control with Repo and Git](http://source.android.com/source/version-control.html).

Repo is a repository management tool that Google built on top of Git. Repo unifies many Git repositories when necessary,
does the uploads to a revision control system, and automates parts of the development workflow.
Repo is not meant to replace Git, only to make it easier to work with Git in the context of multiple repositories.
The repo command is an executable Python script that you can put anywhere in your path.
In working with the source files, you will use Repo for across-network operations.
For example, with a single Repo command you can download files from multiple repositories into your local working directory.

### Setup steps for Microsoft Windows ###

##### Fix priviledges to allow for creation of symbolic links #####
* If you are a member of the Administrators group you have to [turn off User Access Control (UAC)](http://windows.microsoft.com/en-us/windows7/turn-user-account-control-on-or-off) and then restart the computer.
* Otherwise you have to adjust your user rights to [get SeCreateSymbolicLinkPrivilege priviledges](http://stackoverflow.com/questions/6722589/using-windows-mklink-for-linking-2-files).
The editrights tools is provided as part of git-repo for Microsoft Windows.

##### Download and install Git #####
* Download [Git (http://git-scm.com/downloads)](http://git-scm.com/downloads)
* Add Git to your path environment variable: e.g. C:\Program Files (x86)\Git\cmd;
* Add MinGW to your path environment variable: e.g. C:\Program Files (x86)\Git\bin;

##### Download and install Python #####
* Download [Python 3+ (http://python.org/download/releases/3.3.0/)](http://python.org/download/releases/3.3.0/)
* Add Python to your path environment variable: e.g. C:\Python33;

##### Download and install Repo either using the Windows Command Shell or Git Bash #####
###### Windows Command Shell ######

    md %USERPROFILE%\bin
    curl https://raw.githubusercontent.com/esrlabs/git-repo/master/repo > %USERPROFILE%/bin/repo
    curl https://raw.githubusercontent.com/esrlabs/git-repo/master/repo.cmd > %USERPROFILE%/bin/repo.cmd

###### Git Bash ######

    mkdir ~/bin
    curl https://raw.githubusercontent.com/esrlabs/git-repo/master/repo > ~/bin/repo
    curl https://raw.githubusercontent.com/esrlabs/git-repo/master/repo.cmd > ~/bin/repo.cmd

* Add Repo to your path environment variable: %USERPROFILE%\bin;
* Create a HOME environment variable that points to %USERPROFILE% (necessary for OpenSSH to find its .ssh directory).
* Create a GIT_EDITOR environment variable that has an editor executable as value. For this, first add the home directory of the editor executable to the path environment variable. GIT_EDITOR can than be set to "notepad++.exe", "gvim.exe", for example.

### Setup steps for Linux ###

##### Downloading and installing Git and Python #####
* sudo apt-get install git-core
* Since our Repo requires Python 3.3, we recommend to change the first line of the ~/bin/repo executable to:

<!-- code block -->

    #!/usr/bin/env python3.3

* Alternatively, use the following commands to switch between multiple Python versions:

<!-- code block -->

    sudo update-alternatives --install /usr/bin/python python /usr/bin/python2 10
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.3 20
    sudo update-alternatives --config python

##### Download and install Repo #####

    $ mkdir ~/bin
    $ PATH=~/bin:$PATH
    $ curl https://raw.githubusercontent.com/esrlabs/git-repo/master/repo > ~/bin/repo
    $ chmod a+x ~/bin/repo

### Usage ###

For more detailed instructions regarding git-repo usage, please visit [git-repo](http://source.android.com/source/version-control.html).
>>>>>>> 24278757f838150e3b368ba0aff2c12a7348babe
