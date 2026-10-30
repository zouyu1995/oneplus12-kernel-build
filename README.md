# OnePlus12 (PJD110) 强化内核云端编译

基于 cctv18 `OnePlus_Sukisu_Ultra_build/build.sh` 改造为 GitHub Actions，追加内存 dump / BPF 等增强 CONFIG。

## 用法
Actions → "Build OnePlus12 Kernel" → Run workflow。默认参数已适配一加12：
- manifest: `oneplus_12_b.xml`（Android16 / 6.1.141 分支 `oneplus/sm8650_b_16.0.0_oneplus12`）
- bazel_target: `pineapple`
- use_patch_linux: `y`（=启用 KPM）
- apply_lz4kd: `y`
- extra_configs: 内存 dump/BPF/KALLSYMS_ALL 等

产出：`Anykernel3-oneplus_12_b-sukisu-susfs-kpm-memdump-vYYYYMMDD.zip`（Actions Artifacts 里下载）。

## 刷机
1. 解压 zip 得到 AnyKernel3 目录（含 Image 或 oImage、anykernel.sh）
2. 手机进 fastboot / 或 TWRP/内核管理器刷入（**刷 boot_b**，不是 init_boot）
3. 原厂 kernel 已备份：`一加12全套流程/backup/boot.img`，随时 `fastboot flash boot_b boot.img` 回滚

## 注意
- 一加12 kernel 必须与 6.1.141 版本匹配，否则 bootloop。
- 首次刷前确认 BL 已解锁、`adb shell uname -r` = 6.1.141。
