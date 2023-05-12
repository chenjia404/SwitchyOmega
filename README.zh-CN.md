[English](./README.md) | [简体中文](./README.zh-CN.md)
SwitchyOmega
============

快速轻松地管理和切换多个代理。

[![翻译状态](https://hosted.weblate.org/widgets/switchyomega/-/svg-badge.svg)](https://hosted.weblate.org/engage/switchyomega/?utm_source=widget)

Chromium 扩展
------------------
本项目可作为 Chromium 扩展使用。

你可以去 [Chrome Web Store](https://chrome.google.com/webstore/detail/padekgcemlokbadohgkifijomclgjgif),
或者去安装离线的开发者版本 [Releases page](https://github.com/chenjia404/SwitchyOmega/releases).

欢迎提供反馈 [report issues on the issue tracker.](https://github.com/FelisCatus/SwitchyOmega/issues)

Firefox Addon (Experimental)
----------------------------

还有一个实验性的 WebExtension 端口，它允许安装在
**Firefox Nightly Version >= 56**.

**由于 WebExtensions API 仍在 Mozilla 方面进行大量开发，
我们强烈建议使用 Nightly 频道 (>= 56.0) 并经常更新。**

Developer Edition 和 Beta 频道不会经常收到修复程序
因此不受 SwitchyOmega 支持。 一些用户报告说它适用于
Firefox Developer Edition (>= 55) 也是如此，但我们强烈建议不要这样做
所以 它在 Firefox 54 稳定版中根本不起作用。

You can try it on [Mozilla Add-ons](https://addons.mozilla.org/en-US/firefox/addon/switchyomega/),
or grab a packaged extension file (XPI) for offline installation on the [Releases page](https://github.com/FelisCatus/SwitchyOmega/releases).

Please make sure that you are using the latest Nightly build before you
[report issues](https://github.com/FelisCatus/SwitchyOmega/issues).
Build number AND build date should be mentioned somewhere in the issue.

NOTE: PAC Profiles DO NOT work on Firefox due to AMO review policies. We will see what we can do.

Development status
------------------

## PAC generator
该项目包含一个名为 omega-pac 的 PAC 生成模块，它处理
配置文件模型并将配置文件编译成 PAC 脚本。 这个模块是独立的
并且可以在文档准备好后发布到 npm。

## Options manager
文件夹“omega-target”包含独立于浏览器的逻辑，用于管理
选项和应用配置文件。 每个公共方法都在评论中有详细记录。
不包含浏览器相关的功能，需要在子类中实现
`omega-target` 类。

`omega-web` 是一个基于网络的配置界面，用于各种选项和配置文件。
该界面与“omega-target”作为后端配合使用效果很好。

单独的 omega-web 是不完整的，需要一个名为 omega_target_web.js 的文件
包含一个角度模块“omegaTarget”。 该模块包含依赖于浏览器的
与“omega-target”后端通信的代码，以及其他代码检索
浏览器相关的状态和信息。
请参阅 `omega-target-chromium-extension/omega_target_web.coffee` 文件
这种模块的例子。

## Targets
`omega-target-*` 文件夹应包含依赖于环境的代码，例如
浏览器 API 调用。

每个目标文件夹都应包含一个扩展的“OmegaTarget”对象，该对象
包含抽象基类的子类，如“选项”。 班级
包含抽象方法的实现，并且可以覆盖其他方法
随意。

目标可以将 `omega-web` 中的文件复制到它的构建中，以提供基于 web 的
配置界面。 如果是这样，目标必须提供 `omega_target_web.js`
选项管理器部分中描述的文件。

此外，每个目标都可以包含其他所需的文件和资源
目标，例如背景页面和扩展清单。

目前，只实现了一个目标：WebExtension 目标。
这个目标允许该项目在大多数情况下用作 Chromium 扩展
基于 Chromium 的浏览器以及如上所述的 Firefox 插件。

## Translation


本项目翻译由Weblate托管。如果您希望帮助改进翻译，或将本项目翻译成一种新的语言，请
点击下方图片链接进入翻译。

[![Translation status](https://hosted.weblate.org/widgets/switchyomega/-/287x66-white.png)](https://hosted.weblate.org/engage/switchyomega/?utm_source=widget)

## Building the project

SwitchyOmega has migrated to use npm and grunt for building. Please note that
npm 2.x is required for this project.

构建本项目:

    # 首先安装 node 和 npm  (确保 npm 版本 > 2.0), 然后:
    
    sudo npm install -g grunt-cli@1.2.0 bower
    # 在项目文件夹:
    cd omega-build
    npm run deps # This runs npm install in every module.
    npm run dev # This runs npm link to aid local development.
    # Note: the previous command may require sudo in some environments.
    # The modules are now working. We can build now:
    grunt
    # After building, a folder will be generated:
    cd .. # Return to project root.
    ls omega-chromium-extension/build/
    # 这个文件夹就是未打包的 chromium 扩展.

To enable `grunt watch`, run `grunt watch` once in the `omega-build` directory.
This will effectively run `grunt watch` in every module in this project.

License
-------
![GPLv3](https://www.gnu.org/graphics/gplv3-127x51.png)

SwitchyOmega is licensed under [GNU General Public License](https://www.gnu.org/licenses/gpl.html) Version 3 or later.

SwitchyOmega is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

SwitchyOmega is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with SwitchyOmega.  If not, see <http://www.gnu.org/licenses/>.

重要声明
--------

SwitchyOmega 目前没有专门的项目主页。 `switchyomega.com` 等网站与 SwitchyOmega 项目并无任何关联，也并非由 SwitchyOmega 项目成员维护。一切信息请以 Github 上的项目和 wiki 为准。

SwitchyOmega 目前未与任何代理提供商、VPN提供商或 ISP 达成任何合作协议，项目或软件中不包含任何此类广告。欢迎代理提供商在教程或说明中推荐 SwitchyOmega ，但请明确说明此软件是独立项目，与代理提供商无关，且不提供任何关于网络连接或代理技术的支持。
