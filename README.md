# 介绍

bpm 是一个针对 brix 组件开发的包管理器。

bpm = opm + opmext-brix

bpm 是基于 opm 开发的，通过给 opm 安装 opmext-brix 扩展可实现 bpm 工具的所有功能。

bpm 的整合是为了方便 brix 开发者准备的。

# 安装

```bash
npm install brix-bpm -g
```

# 使用

## 注册

发布组件前需要在注册服务器上进行注册，命令是：

```bash
bpm adduser
```

根据提示完成即可。阿里用户请使用与域账号相同的用户名进行注册，密码则可以不同。后续我们将支持域账户登录。

## 初始化工程

所有 brix 组件都应该隶属于一个工程，同样的，这个工程也是一个被 bpm 维护的包。

在创建好的工程目录中执行 `bpm init` 命令初始化一个工程，命令会用收集到的信息生成一个 `package.json`。

其中`name`字段将作为此工程下的所有组件的命名空间前缀。

```js
{
    "name": "etao.ux.x1", // 命名空间
    "version": "0.0.3", // 版本，暂时没什么用
}
```

## 初始化组件

在工程目录中执行 `bpm create component_name` 可以初始化一个组件。

会生成一个 `package.json` 文件，以下两项必选：

 - `name`，格式如 `namespace_subname`
 - `version`，建议采用 [semver](http://semver.org/) 规范（[中文版](http://www.cnblogs.com/yaoxing/archive/2012/05/14/semantic-versioning.html)）

另外，还可以用 `dependencies` 配置此组件的依赖。当组件被安装时，其依赖也会被安装到 `imports` 目录中。

`package.json` 示例如下：

```js
{
    "name": "etao.ux.ehome_hotsale",
    "version": "0.0.1"
}
```

[参考此例](https://github.com/etaoux/bpm-test/blob/master/projects/etao.ux.x1/components/abc/package.example.json)。

## 发布组件

在组件目录中执行：

```shell
bpm publish
```

将组件发布到中央库，并同时存放在 `exports/component_name/version/` 目录中。

发布完成之后，可以到 [一淘 UX 规范中心](http://ux.etao.com/jades) 查看
（由于定时任务暂时还没跑起来，需要知会逸才手工同步）。

## 安装组件

在工程目录中执行：

```shell
bpm install namespace_component
```

组件 __及其依赖__ 会被安装到 `imports/namespace/component_name/version/` 目录中

可安装组件可到[中心库](http://ux.etao.com/jades/)查询

# 升级

bpm 还是一个新生项目，将会持续的进行改进，如果你发现什么问题，不如先尝试 ```npm update brix-bpm -g```看看勤奋的开发者有没有已经修复这个问题。如果还是不行的话，欢迎到Issues中进行提交，或直接联系开发者，谢谢。
