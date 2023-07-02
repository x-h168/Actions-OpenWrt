Padavan-build说明  https://github.com/chongshengB/Padavan-build
现在不需要新建Release了，已经更改了脚本，直接fork，修改好之后，点击右上角的 Star 星星按钮即可开始自动编译（自己点击才会编译）。
Padavan-build说明 步骤
0.点击右上角的Fork按钮，进入自己fork后的仓库。
1.修改/workflows/build-padavan.yml里的插件与机型。修改TNAME: K2P 中的K2P为需要编译的型号，注意名称要与configs/templates/目录下的名字 相同。 修改后commit changes保存。
2.点击页面上部的Actions按钮，点击I understand my workflows，go ahead and enable them绿色按钮启用action。
3.点击右上角的 Star 星星按钮即可开始自动编译（自己点击才会编译）。修改配置后若需再次编译，先点击Star取消Star后，再点击Star即可重新编译。 编译完成后在Actions页面底部下载固件。



前言
Github Ac­tions 是 Mi­crosoft 收购 GitHub 后推出的 CI/​CD 服务，它提供了性能配置非常不错的虚拟服务器环境（E5 2vCPU/​7G RAM），基于它可以进行构建、测试、打包、部署项目。对于公开仓库可免费无时间限制的使用，且单次使用时间长达 6 个小时，这对于编译 Open­Wrt 来说是非常充足的。不过 GitHub Ac­tions 有一定的使用门槛，首先要了解如何编写 workflow 文件。不过不用担心，博主已经编写好了相关的 work­flow 文件模版，只需要按照教程的步骤来操作即可。

方案特点
免费
一键快速编译
定时自动编译
客制化编译
并发编译（可同时进行20个编译任务）
无需搭建编译环境（在线make menuconfig生成配置文件)
无需消耗自己的计算机与服务器的计算资源（性感E5在线编译）
无需担心磁盘空间不足（近60G磁盘空间）
无需使用清理文件（内核更新不怕 boom ）
编译速度快（编译时间1-2小时）
编译成功率提升200%（万兆自由网络环境）
全新环境（杜绝编译环境不干净导致编译失败）
本解决方案是一个开放平台，任何人都可以基于此打造自己专属的编译方案。
项目地址
https://github.com/P3TERX/Actions-OpenWrt

支持项目请随手点个 star，让更多的人发现、使用并受益。

准备工作
GitHub 账号
搭建编译环境，生成.config文件。(可选)
TIPS: 关于编译环境的搭建，推荐去看我之前写的相关文章，Win­dows 10 可以使用 WSL ，ma­cOS、Linux 可以使用 Docker 。
教程更新
2021-01-03 新增源码更新自动编译使用说明
2020-10-11 新触发方式使用方法、更新上传固件到 releases 页面说明。
2020-04-25 更新 DIY 脚本说明、添加自定义 feeds 配置文件说明
2020-04-09 新增上传固件到 WeTransfer
2020-03-30 新增上传固件到奶牛快传
2020-02-01 新图文教程
2019-12-10 新增 macOS 编译方案使用说明
2019-12-06 添加 tmate 网页终端链接说明
2019-12-05 优化基础使用教程，添加 @lietxia 大佬的图文教程链接
2019-12-04 新增云menuconfig使用方法
2019-12-03 新增并发编译使用方法
2019-11-30 新增自定义源码编译使用方法
2019-11-14 全网独家首发
基础使用
首先你必须要熟悉整个 Open­Wrt 的编译过程，这会让你非常容易的理解如何使用 GitHub Ac­tions 进行编译，即使你没有成功过。因为实际上本地编译近 90% 失败的原因是因为网络问题导致的，中国大陆特色，咱也不敢多说。GitHub Ac­tions 服务器由 Mi­crosoft Azure 提供，拥有万兆带宽，可以使编译成功率大大提升。

在自己搭建编译环境中使用 Lean's OpenWrt 源码生成.config文件。（或使用直接 SSH 连接到 Actions 进行操作，后面有说明。）
TIPS: 方案默认引用 Lean 的源码，因为他的 README 影响了我开始学习编译，也就有了这个项目，而且他的源码非常的优秀。有其它需求可自行修改 work­flow 文件，方法后面的进阶使用中有说明。
进入 P3TERX/Actions-OpenWrt 项目页面，点击页面中的 Use this template （使用这个模版）按钮。

填写仓库名称，然后点击Create repository from template（从模版创建储存库）按钮。

经过几秒钟的等待，页面会跳转到新建的仓库，内容和我的项目是相同的。然后点击Create new file（创建新文件）按钮。

文件名填写为.config，把生成的.config 文件的内容复制粘贴到下面的文本框中。

翻到页面最下方，点击Commit new file（提交新文件）按钮。

在 Actions 页面选择Build OpenWrt，然后点击Run Workflow按钮，即可开始编译。（如果需要 SSH 连接则把SSH connection to Actions的值改为true。其它详情参见进阶使用相关章节）

在等待编译完成的过程中，你可以进入这个页面点击右上角的star，这是对博主最大的支持，而且还可以加快编译速度哦（雾
最后经过一两个小时的等待，不出意外你就可以在 Actions 页面看到已经打包好的固件目录压缩包。

TIPS: 如需 ipk 文件可以在进阶使用章节找到方法。因为大多数人只需要固件，而且总是有萌新问固件在哪，所以现在默认只上传固件。
进阶使用
自定义环境变量与功能
点击查看
DIY 脚本
点击查看
添加额外的软件包
点击查看
自定义 feeds 配置文件
把 feeds.conf.default 文件放入仓库根目录即可，它会覆盖 Open­Wrt 源码目录下的相关文件。

Custom files（自定义文件）
俗称 “files 大法”，在仓库根目录下新建 files 目录，把相关文件放入即可。有关详情请自行搜索了解。

自定义源码
默认引用的是 Lean 的源码，如果你有编译其它源码的需求可以进行替换。

点击查看
源码更新自动编译
在检测到源码更新后自动进行编译。

点击查看
编译多个固件
多 repository 方案
通过 P3TERX/Actions-OpenWrt 项目创建多个仓库来编译不同架构机型的 Open­Wrt 固件。

多 workflow 方案
基于 GitHub Ac­tions 可同时运行多个工作流程的特性，最多可以同时进行至少 20 个编译任务。也可以单独选择其中一个进行编译，这充分的利用到了 GitHub Ac­tions 为每个账户免费提供的 20 个 Ubuntu 虚拟服务器环境。

点击查看
SSH 连接到 Actions
通过 tmate 连接到 GitHub Ac­tions 虚拟服务器环境，可直接进行 make menuconfig 操作生成编译配置，或者任意的客制化操作。也就是说，你不需要再自己搭建编译环境了。这可能改变之前所有使用 GitHub Ac­tions 的编译 Open­Wrt 方式。

点击查看
上传固件到奶牛快传
奶牛快传是中国大陆的一款临时文件传输分享服务网盘，特点是不限速。因国情所致，中国大陆地区 GitHub 访问速度缓慢，有些小伙伴可能无法正常下载固件，上传固件到奶牛快传是个非常好的选择。

点击查看
上传固件到 WeTransfer
WeTransfer 是荷兰的一款临时文件传输分享服务网盘，前面提到的奶牛快传实际上师从自它，二者的网站都非常相似。We­Trans­fer 使用的是 Ama­zon S3 存储并通过 Ama­zon Cloud­Front CDN 全球加速，它在中国大陆的下载体验完全不输奶牛快传，甚至某些情况下要更好。

点击查看
上传固件到 Releases 页面
GitHub 的 Re­leases 页面通常用于发布打包好的二进制文件，无需登录即可下载。Ar­ti­facts 和网盘有保存期限，Re­leases 则是永久保存的。

点击查看
定时自动编译（已弃用）
点击查看
点击 star 开始编译（已弃用）
点击查看
macOS 虚拟机编译方案（已弃用）
点击查看
写在最后
博主只是提供基本入门用法和思路，更高阶的玩法还需要小伙伴们自己去发觉。此外希望大家合理使用免费的服务器资源，必要时再编译。让出更多的服务器资源让开发者来充分利用才能产生更多更好的软件，这样大家才能受益。最后感谢 Mi­crosoft 为我们免费提供 GitHub Ac­tions 这样强大的服务。

相关推荐
深港 IPLC & 洛杉矶/日本/香港 CN2 GIA 高速跨境专线
国外便宜高性价比和免费白嫖 VPS 推荐
本博客已开设 Telegram 频道，欢迎小伙伴们订阅关注。

本文作者：P3TERX

本文链接：https://p3terx.com/archives/build-openwrt-with-github-actions.html

版权声明：本博客所有文章除特别声明外，均采用 CC BY-NC-SA 4.0 许可协议。非商业转载及引用请注明出处（作者、原文链接），商业转载请联系作者获得授权。




**English** | [中文](https://p3terx.com/archives/build-openwrt-with-github-actions.html)

# Actions-OpenWrt

[![LICENSE](https://img.shields.io/github/license/mashape/apistatus.svg?style=flat-square&label=LICENSE)](https://github.com/P3TERX/Actions-OpenWrt/blob/master/LICENSE)
![GitHub Stars](https://img.shields.io/github/stars/P3TERX/Actions-OpenWrt.svg?style=flat-square&label=Stars&logo=github)
![GitHub Forks](https://img.shields.io/github/forks/P3TERX/Actions-OpenWrt.svg?style=flat-square&label=Forks&logo=github)

A template for building OpenWrt with GitHub Actions

## Usage

- Click the [Use this template](https://github.com/P3TERX/Actions-OpenWrt/generate) button to create a new repository.
- Generate `.config` files using [Lean's OpenWrt](https://github.com/coolsnowwolf/lede) source code. ( You can change it through environment variables in the workflow file. )
- Push `.config` file to the GitHub repository.
- Select `Build OpenWrt` on the Actions page.
- Click the `Run workflow` button.
- When the build is complete, click the `Artifacts` button in the upper right corner of the Actions page to download the binaries.

## Tips

- It may take a long time to create a `.config` file and build the OpenWrt firmware. Thus, before create repository to build your own firmware, you may check out if others have already built it which meet your needs by simply [search `Actions-Openwrt` in GitHub](https://github.com/search?q=Actions-openwrt).
- Add some meta info of your built firmware (such as firmware architecture and installed packages) to your repository introduction, this will save others' time.

## Credits

- [Microsoft Azure](https://azure.microsoft.com)
- [GitHub Actions](https://github.com/features/actions)
- [OpenWrt](https://github.com/openwrt/openwrt)
- [Lean's OpenWrt](https://github.com/coolsnowwolf/lede)
- [tmate](https://github.com/tmate-io/tmate)
- [mxschmitt/action-tmate](https://github.com/mxschmitt/action-tmate)
- [csexton/debugger-action](https://github.com/csexton/debugger-action)
- [Cowtransfer](https://cowtransfer.com)
- [WeTransfer](https://wetransfer.com/)
- [Mikubill/transfer](https://github.com/Mikubill/transfer)
- [softprops/action-gh-release](https://github.com/softprops/action-gh-release)
- [ActionsRML/delete-workflow-runs](https://github.com/ActionsRML/delete-workflow-runs)
- [dev-drprasad/delete-older-releases](https://github.com/dev-drprasad/delete-older-releases)
- [peter-evans/repository-dispatch](https://github.com/peter-evans/repository-dispatch)

## License

[MIT](https://github.com/P3TERX/Actions-OpenWrt/blob/main/LICENSE) © [**P3TERX**](https://p3terx.com)
