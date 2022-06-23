# Microsoft365开发人员申请（可永久）
##1.免费注册E5账户
   ####首先打开下面网址,使用微软账户进行账户登陆，没有的话注册一个：
https://developer.microsoft.com/office/profile
    ####登陆成功后，进行进行简单的注册：公司随便填，后下一步
    ####这里选择“供我公司内部使用的应用程序“，下一步
    ####选择“可配置沙盒”，下一步。
“用户名”和“域“，随意编一个，设置好“密码”，继续。由于密码比较复杂，建议用记事本记录一下，后面会用到。继续
    ####使用电话号码验证一下。
至此一个E5的免费账户就注册完了，使用管理员账户和密码即可激活Microsoft 365，免费使用三个月。
####注册好的账户，默认只有1TB的空间，实际上最大赠送5TB。我们改一下设置即可。打开网址：
https://admin.onedrive.com/?v=StorageSettings
####点击“设置”，将下面的存储限制默认选项，设置为5120GB，点击“保存”。至此，刚刚获取的E5管理员账户就有5TB免费的空间了。
##2安装Microsoft365
####进入网址：https://www.office.com，使用刚才注册的管理员账户和密码登录。
####点击右上角，下载并安装Microsoft 365。
##3设置E5账户的子账户（扩展25个子账户）
####进入网址：https://www.office.com，使用刚才注册的管理员账户和密码登录。点击左侧的“管理”。
####点击“新增用户”。
####随意设置一下子账户的基本信息。
####选择“向用户分配产品许可证”，下一步。
至此，子账户设置完成。同理，可设置25个子账户。
##4禁用安全默认值
####禁用了该值，续期时才不会失败，务必注意。如果你只想用90天，这一步也不用看。参考下面的地址：
https://docs.microsoft.com/zh-cn/azure/active-directory/fundamentals/concept-fundamentals-security-defaults#disabling-security-defaults
####点击Azure门户(右上角），来到下面的界面。找到“Azure Active Directory”，点击“查看”。点击“属性”。
####点击“管理安全默认值”。把右侧的开关置于“否”，然后点击“保存”。
##5获取PAT密钥
打开：https://github.com/settings/tokens/new
####输入GitHub的登录密码来到下面的页面，Note设置为E5;Expiration设置为No expiration,注意务必勾选workflow。点击“Generate token”。
###然后就得到了PAT密钥，注意复制到记事本中备用，如果这里不记下来，再进此页面就看不到了。如果真的看不到了，可以删除再新建一个。
##6新建一个空仓库
点击右上角“+”，选择“New repository”，名称随便起，也可就叫“E5”。然后勾选“Private”，表示这是私人的，别人看不到。按下图设置后，点击“Generate repository”。
我们可以看到，下图中仓库E5是空的。点击branch，点击画笔，将名称main修改为master。因为源码中用的是master这个路径，如果不改，后面执行会失败。
##将本地源码导入到仓库中
打开Github上的一个开源项目，地址：
https://github.com/vcheckzen/KeepAliveE5
这个项目的原理是：Github中的Actions是一个虚拟环境，写一段脚本在里面自动运行（调用API），微软以为你在搞开发，从而实现自动续期。下载下来
也可从此下：https://wwi.lanzoup.com/b00pu95uf 密码:3k0h
####切换到“<>Code”选项下，点击Add files→Upload files导入文件，但是会发现文件夹导不进来。
由于GitHub只能导入文件，不能直接导入文件夹。Create newfile我们在下图空格处输入“/”，就相当于新建文件夹了，例如：.github/。最后的空格中随便输入一个名称，比如下图中的“0”,这样才能继续下一步。.github文件夹下还有一个文件夹workflows
####新建完文件夹，再把文件夹下的所有文件导入。最后点击“Commit Changes”提交。其他文件导入方法同理，注意核实一下register文件夹下的文件是否也都导入进来了。
####总之，要确保把源码文件，按照原项目的目录层次全部导入。最后核实一遍文件的个数，尤其是文件夹里面的，是否有缺少。
注意：为什么要新建仓库，然后从本地导入。直接用Fork或者“导入仓库”功能更方便，一键就把原项目导进来了。使用“导入仓库”功能后，后面手动触发时没反应。Fork也不建议用，原作者说有漏洞，容易受到攻击。
##8、设置密码
切换到“Settings”选项下，找到Secrets→Actions，点击New repository sectret。新建三条内容如下：PAT的值为上文申请的密钥；USER的值为申请的E5管理员账号；PASSWD的值为E5管理员账户密码。
##9、测试
接下来切换到“Actions”选项中操作。手动触发，看看代码是否执行成功。
####有的人可能找不到Actions选项，可以按下图开启。Settings→Actions→General→Allow all actions and reusable workflows→Save。
####切换到Actions选项下，选择Register APP，然后点击Run workflow。
大约等待2分钟执行完毕。如果是绿色✅，没有报错，表示执行成功。
####同样的方法，再执行一下Invoke APP。
测试成功后，后面不用管它，自动就执行了。如果报错，点击Register API以及Invoke API，进去看看执行的代码，报错的提示是什么
