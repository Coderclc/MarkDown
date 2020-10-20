# YRAN

```shell
"5.0.3",
"~5.0.3", 5.0.x最新的版本
"^5.0.3", 5.x.x最新版本
```

## 	Why use

1. 异步下载,并行安装
2. 全局缓存下载的每个包
3. 安装前会校验完整性
4. lockfile 文件保证不同系统安装依赖相同

## Basic use

### install

npm i yarn -g

### check version

yarn --version

### init

yarn init

### install 

yarn add package

yarn add package@version

yarn add package@tag

yarn add package --dev --peer --optional   -D -P -O

devDependencies peerDependencies  optionalDependencies

### upgrade

yarn upgrade package

### uninstall

yarn remove package

### install dependencies

yarn 

yarn install

## CLI

yarn publish

yarn run 

