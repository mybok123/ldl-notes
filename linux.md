### 在后台运行进程 注意 nohup 和 &
  nohup java -jar edb_SDK_V0_0_1.jar &
 
### 查看后台java进程
  ps -ef | grep java

### ssh 将文件复制到远程服务器
  scp /Users/aircos/Documents/workspace/edb_SDK_V0_0_1.jar deploy@101.200.75.87:/home/deploy/server/
   
### 远程登录服务器
  ssh deploy@101.200.75.87

### 修改别名 sublime
  alias subl=\''/Applications/Sublime Text 2.app/Contents/SharedSupport/bin/subl'\'
  可以用 subl . 打开当前路径的项目
  引出全局 export subl

 ### 

