# WeFlow

WeFlow 是一个本地微信聊天记录查看、分析与导出工具。

> 本项目是 [hicccc77/WeFlow](https://github.com/hicccc77/WeFlow) 的 Linux 适配分支。完整功能说明、使用文档、构建指南等请查阅原仓库。

## 本分支新增 / 修复

针对 Linux 平台（特别是 Flatpak 安装的微信和 AppImage 打包）做了以下工作：

1. **Flatpak 微信支持**：新增 `flatpak run com.tencent.WeChat` 及 Flatpak 沙箱内二进制路径，解决原代码无法拉起 Flatpak 微信的问题
2. **Flatpak 数据目录软链接**：自动创建 Flatpak 微信数据目录软链接，兼容图片密钥获取
3. **AppImage PATH 补全**：AppImage 内部 PATH 极简，补全 `/usr/bin`、`/var/lib/flatpak/exports/bin` 等路径，修复 `flatpak`、`pidof` 等命令找不到的问题
4. **可执行权限修复**：修复 `xkey_helper_linux` 和 `welive` 二进制文件权限（644 → 755），解决 AppImage 打包后 EACCES 错误
5. **FUSE 隔离修复**：AppImage 通过 FUSE 挂载时 root 无法访问挂载点文件，执行 `db_hook`（需 sudo）前先将 `xkey_helper_linux` 复制到 `/tmp/`
6. **图片解密权限修复**：修复 Linux 下图片解密 `image_mem` 权限问题
7. **CI 自动构建**：添加 GitHub Actions workflow，自动构建 AppImage

## 快速开始

从 [Releases](https://github.com/hicccc77/WeFlow/releases) 下载对应平台的安装包。

ArchLinux 用户可以通过 AUR 安装：`yay -S weflow`

## 致谢

- [密语 CipherTalk](https://github.com/ILoveBingLu/miyu) 为本项目提供了基础框架
- [WeChat-Channels-Video-File-Decryption](https://github.com/Evil0ctal/WeChat-Channels-Video-File-Decryption) 提供了视频解密相关的技术参考
