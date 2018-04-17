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


