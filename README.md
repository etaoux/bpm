bpm 是一个针对 brix 组件开发的包管理器。

> bpm = opm + opmext-brix

bpm 是基于 [opm](https://github.com/objectjs/opm) 开发的，通过给 opm 安装 [opmext-brix](https://github.com/etaoux/opmext-brix) 扩展可实现 bpm 工具的所有功能。为了方便 brix 开发者进行了整合。

## 功能介绍

* 发布 brix 组件到中央库
* 安装并使用别人开发的组件
* 方便的创建组件，维护组件版本

# 安装

1. 安装[nodejs](http://nodejs.org/)；
2. 用 npm 安装 bpm：```npm install brix-bpm -g```；
3. 安装后，执行 `bpm` 命令若有输出则安装成功。

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

其中`name`字段命名请使用 `公司名.部门名.项目名` 的形式。此字段将作为此工程下的所有组件的命名空间前缀。

```js
{
    "name": "etao.ux.x1", // 工程名，同时为此工程的所有组件的命名空间
    "version": "0.0.3", // 版本，暂时没什么用
}
```

## 初始化组件

在工程目录中执行 `bpm create component_name` 会在 `components/component_name` 目录中创建一个组件。

会生成一个 `package.json` 文件，以下两项必选：

 - `name`，格式如 `namespace_subname`，工具会根据所在工程目录自动生成一个默认值，若有修改请填写包括命名空间的完整名字。
 - `version`，采用 [semver](http://semver.org/) 规范（[中文版](http://www.cnblogs.com/yaoxing/archive/2012/05/14/semantic-versioning.html)），每次发布组件的新版本前需要手动修改此版本号。
 - `dependencies` 配置此组件的依赖。需要指定依赖组件的版本，始终使用最新版则用`latest`表示。

`package.json` 示例如下：

```js
{
    "name": "etao.ux.ehome_hotsale",
    "version": "0.0.1",
    "dependencies": {
      "etao.ux.x1_banner": "0.0.1",
      "etao.ux.ehome_footer": "latest"
    }
}
```

[参考此例](https://github.com/etaoux/bpm-test/blob/master/projects/etao.ux.x1/components/abc/package.example.json)。

## 发布组件

在组件目录中执行：

```shell
bpm publish
```

将组件发布到中央库，并同时存放在工程目录下 `exports/component_name/version/` 目录中。

发布完成之后，可以到 [一淘 UX 规范中心](http://ux.etao.com/jades) 查看
（由于定时任务暂时还没跑起来，需要知会逸才手工同步）。

## 安装组件

在工程目录中执行：

```shell
bpm install namespace_component
```

组件 __及其依赖__ 会被安装到 `imports/namespace/component_name/version/` 目录中。

安装后的组件中的 `kissy.add` 和 `bx-name` 属性会被替换成新的路径。

可安装组件可到[中心库](http://ux.etao.com/jades/)查询

# 例子

[bpm-test](http://github.com/etaoux/bpm-test/) 项目中有一些用例，参考文档学习看看使用效果吧！

# 升级

bpm 还是一个新生项目，将会持续的进行改进，如果你发现什么问题，不如先尝试 ```npm update brix-bpm -g```看看勤奋的开发者有没有已经修复这个问题。如果还是不行的话，欢迎到Issues中进行提交，或直接联系开发者，谢谢。
