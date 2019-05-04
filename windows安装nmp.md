### windows安装nmp(nodejs)


步骤很简单
-----
- [官网地址](https://nodejs.org/en/)下载nodejs
- 安装，检测是否成功`CMD，node -v 和 npm -v命令`
- 在安装目录打开命令行小黑框，即可nmp操作。（要不要配置环境变量什么随便你自己选择，我比较直接）




##### 其他
卡在
`fetchMetadata: sill...` 
换一下nmp源，国内真的慢阿。
换成某宝的源
`npm config set registry https://registry.npm.taobao.org `
检查换源是否OK
`npm config get registry `

