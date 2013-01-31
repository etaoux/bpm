# 介绍

bpm 是为 brix 提供的面向组件开发，基于 npm 的包管理工具。

# 安装

npm install brix-bpm -g

# 使用：

## 注册

bpm 同 npm 一样，发布组件前需要在注册服务器上进行注册，命令是 ```bpm adduser```，根据提示完成即可。

需要注意的是，这里的验证信息在本机保存在 npm 的配置信息里，为避免 bpm 注册后 npm 无法使用，请使用同样的用户名密码进行注册。

## 在工程目录中：

### 初始化工程

请自行在工程目录中写一个 <var>package.json</var>，用于描述此工程的一些信息。

[这里](https://github.com/etaoux/bpm-test/blob/master/projects/etao.ux.x1/package.example.json)有一个例子。

### 安装组件

```shell
bpm install namespace_component
```

组件 __及其依赖__ 会被安装到 <code>imports/<var>namespace</var>/<var>component</var>/<var>version</var>/</code> 目录中

## 在组件目录中：

### 初始化组件

```shell
bpm init
```

会生成一个 package.json，其中的 name 是 <var>namespace</var>\_<var>subname</var> 格式的， <var>version</var> 为必选。<var>dependencies</var> 用于配置此组件的依赖，当组件被安装时，其依赖也会被安装到 <var>imports</var> 目录中。

[这里](https://github.com/etaoux/bpm-test/blob/master/projects/etao.ux.x1/components/abc/package.example.json)有一个例子。

### 发布组件

```shell
bpm publish
```

将组件发布到中央库，并同时存放在 <code>exports/<var>component</var>/<var>version</var>/</code> 目录中
