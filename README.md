# Xcode项目一键 git pull + pod update + 运行

如果你所在的iOS团队运用了大量私有pod, 且每天要花很多时间在pod update上, 这个方法将一键完成从更新到运行的所有事情.

**_前提:<br>1.本地代码已Commit, 这一点非常重要<br>2.当前仅开了主工程一个Xcode窗口_**

### 具体实现
cd ***WorkSpace目录*** ;\
***git pull origin {远程分支名}*** ;\
***open -a Xcode {Workspace全名}*** ;\
***pod update*** ;\
***osascript {相应的AppleScript运行脚本所在的Path}***
### AppleScript内容(先保存于本地, 命名为{XXX}.scpt)
```
tell application "Xcode"
    activate
    tell application "System Events"
        perform (keystroke "." using command down)
        perform (keystroke "r" using command down)
    end tell
end tell
```
## 与Mac环境变量结合
### 新建.sh文件
cd 到将存放.sh的目录 <br>
vi {文件名}.sh <br>
输入上文提到的命令: <br>
```
cd {Xcode项目目录};\
git pull origin {远程分支名};\
open -a Xcode {文件名}.xcworkspace;\
pod update;\
osascript {先前保存的AppleScript路径}.scpt
```
然后保存<br>
### 好玩的来了
 vi ~/.bash_profile<br>
 输入:<br>
 alias {自定的命令}='sh {sh文件全路径}'<br>
 刷新:<br>
 source ~/.bash_profile<br>
 之后输入该命令, 一切都将一键完成!
### 关于Mac的环境变量
Mac配置环境有几个地方<br>
 1./etc/profile<br>
（建议不修改这个文件 ）<br>
 全局(公有)配置, 不管是哪个用户, 登录时都会读取该文件.<br>
 
 2./etc/bashrc<br>
 一般在这个文件中添加系统级环境变量<br>
 全局(公有)配置, bash shell执行时, 不管是何种方式都会读取此文件.<br>
 
 3.~/.bash_profile<br>
 一般在这个文件中添加用户级环境变量<br>
 每个用户都可使用该文件输入专用于自己使用的shell信息, 当用户登录时, 该文件仅仅执行一次.<br>
 ## 解释
### 终端依次运行2个及以上命令的方法
***Command1 ; Command2 ; ... ; Command N***<br>用 ; 或者 && 都行
### 拉远程分支
***git pull origin 分支名***
### 用Xcode打开Workspace(可省略)
***open -a Xcode XXX.xcworkspace***
