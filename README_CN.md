# libpnet (pnet) 非官方修改版说明

本目录是 `libpnet`（`pnet` crate）的非官方修改副本，用于 `Better-Minecraft-Bedrock-Launcher` / `EasyTier-BMCBL` 的构建与运行。
它不是上游 `libpnet` 的官方仓库或镜像。

- 上游仓库: https://github.com/libpnet/libpnet

## 为什么需要这个修改版

在 Windows 上，上游 `pnet` 的 `std` feature 可能会拉入 `pnet_datalink`，从而链接 WinPcap/Npcap 的 `Packet.lib` / `Packet.dll`。
本项目有意避免对 Npcap/WinPcap（Packet）这一套依赖。

## 我们改了什么（概要）

- `pnet_datalink` 不再由 `std` feature 隐式启用；改为显式 feature：`datalink`。
- 增加空的 `nightly` / `clippy` features，避免某些下游构建配置通过 `cfg_attr` 引用这些 feature 名称时触发 `unexpected_cfgs` 报错。
- 做了少量 `cfg` 相关的 gating 修正。

## 许可证与归属

- 本目录保留上游的许可证文件：`LICENSE-APACHE`、`LICENSE-MIT`。
- 源码文件中的版权声明（copyright headers）也保留不变。
- `libpnet` 为 MIT 或 Apache-2.0 双许可证；详见上述许可证文件。

## 重要提示

如果你需要 `pnet::datalink`（二层收发/抓包等能力），请在依赖方显式启用 `pnet` 的 `datalink` feature，并自行处理对应平台依赖（Windows 可能涉及 Npcap/WinPcap）。
