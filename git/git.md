
### 本地目前只有一个账号，想替换本地的git账号（personal access token解决）

1. 如何查看本地的git账号
```
git config --list
```

2. 更改名字和邮箱
```
git config --global user.name "[]"

git config --global user.email "[]"
```
是否加global都无所谓，因为本地此时只有一个账号

3. 删除旧的信息 

3.1 查看config文件保存在哪里

此时push如果报错403，就说明依然使用的是保存在电脑里的github账号信息，先查看一下config文件都保存在哪里

```
git config --list --show-origin
```
![](./images/Screenshot%202025-08-09%20at%2017.44.26.png)
其中有一个credential.helper=osxkeychain，表示从osxkeychain中拿到的登陆信息。

3.2 删除keychain中的信息

此时有两个选择：

一是，删除这一行，然后git push的时候就会重新输入密码，之后可以重新加回来，这样下次就不用重新输入密码了

二是，去删除keychain里的信息，找到keychain access，不同系统版本可能不一样，然后删掉就好了。refers to: https://docs.github.com/en/get-started/git-basics/updating-credentials-from-the-macos-keychain

3.3 产生github账号password（personal token）

接下来是产生github的password，github已经deprecate了password，所以需要产生personal access token，refers to https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-token 。在产生personal access token的时候记得勾选这个token可用的范围 


> Note
>
> 如何找到keychain access
>
> ![](./images/Screenshot%202025-08-09%20at%2017.49.03.png)
> 方法一：直接访问
>
> 打开“访达”（Finder）。在菜单栏中选择“前往” > “前往文件夹”。输入路径 /System/Library/CoreServices/Applications/ 并按回车。在该文件夹中找到“钥匙串访问”应用程序并双击打开。
>
> 方法二：使用Spotlight搜索
>
> 按下 Command + 空格 键，激活Spotlight搜索。
在搜索框中输入“钥匙串访问”。
在搜索结果中找到并点击“钥匙串访问”应用程序。


### TODO ssh方案，且本地可用时拥有多个账号