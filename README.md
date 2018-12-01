# Xcode项目一键 git pull + pod update + 运行

如果你所在的iOS团队运用了大量私有pod, 且每天要花很多时间在pod update上, 这个方法将一键完成从更新到运行的所有事情.

**_前提:<br>1.本地代码已Commit, 这一点非常重要_**
## 步骤
### 1. 新建Shell脚本
打开"终端"<br>
cd 到将要保存Shell的目录
### 2. 编辑Shell脚本
vi {文件名}.sh<br>
输入:
```
cd {Xcode项目目录}
git pull origin {远程分支名}
open -a Xcode {文件名}.xcworkspace
pod update
#再次打开项目, 避免当前为其它Xcode窗口导致误运行
open -a Xcode {文件名}.xcworkspace
osascript <<EOD
tell application "Xcode"
    activate
    tell application "System Events"
        perform (keystroke "." using command down)
        perform (keystroke "r" using command down)
    end tell
end tell
EOD
```
然后保存
### 3. 与macOS环境变量结合
vi ~/.bash_profile<br>
alias {自定的命令}='sh {Shell脚本路径}'
### 4. 刷新环境变量
source ~/.bash_profile
###  5. 完成
在"终端"输入{自定的命令}, 将完成项目的git pull + pod update + 运行, 真正"一键"!
#### 关于macOS环境变量
masOS配置环境有几个地方<br>
 1./etc/profile<br>
（建议不修改这个文件 ）<br>
 全局(公有)配置, 不管是哪个用户, 登录时都会读取该文件.<br>
 
 2./etc/bashrc<br>
 一般在这个文件中添加系统级环境变量<br>
 全局(公有)配置, bash shell执行时, 不管是何种方式都会读取此文件.<br>
 
 3.~/.bash_profile<br>
 一般在这个文件中添加用户级环境变量<br>
 每个用户都可使用该文件输入专用于自己使用的shell信息, 当用户登录时, 该文件仅仅执行一次.<br>
