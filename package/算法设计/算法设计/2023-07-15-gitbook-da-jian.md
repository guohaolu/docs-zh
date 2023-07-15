# 2023 07 15 GitBook搭建

### 环境准备

1. win11
2. node.js（v10.24.1）
3. VSCode

```shell
# 检查版本
node -v
npm -v
```

### 部署

```shell
# 创建GitBook书籍文件夹
gitbook init
npm init
```

生成结构通过VSCode查看如下：

![explorer](C:%5CUsers%5Cguohao.lu%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20230715140545264.png)

打开`package.json`文件，修改脚本命令：

![image-20230715140707102](C:%5CUsers%5Cguohao.lu%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20230715140707102.png)

通过脚本命令`npm run serve`运行：

![image-20230715140806503](C:%5CUsers%5Cguohao.lu%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20230715140806503.png)

打开网址`http://localhost:4000`，显示如下：

![image-20230715141040861](C:%5CUsers%5Cguohao.lu%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20230715141040861.png)

### 结构完善

1. 添加`.bookignore`在打包时忽略文件
2. 添加`book.json`
3. 通过`npm i gitbook-plugin-XXX`来安装插件，之后在`book.json`的`plugins`中进行开启（或禁用）
