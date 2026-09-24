# Padavan-build说明

本仓库使用 GitHub Actions 编译 Padavan-KVR 固件，支持两种触发方式：**手动触发**与**打 Release 标签触发**。

## 方式一：手动触发（workflow_dispatch）

1. 进入自己 fork 后的仓库（Fork 右上角按钮）。
2. 点击页面上部的 **Actions** 按钮，选择 **Build Padavan** 工作流，点击 **Run workflow**。
3. 在 **TNAME** 输入框填写需要编译的型号，名称必须与 `configs/templates/` 目录下的名字一致
   （例如 `CR660x`、`K2P`、`MI-R3G` 等），默认 `CR660x`。
4. 点击 **Run workflow** 开始编译。

## 方式二：打 Release / 标签触发

- **打标签**：`git tag v1.0.0 && git push --tags`，推送 `v*` 格式的标签即触发编译。
- **发布 Release**：在仓库的 Releases 页面 **Publish a release** 即触发编译。

两种方式均使用工作流中默认型号 `CR660x`，如需更换型号请改用方式一手动触发并填写 TNAME，
或修改工作流里 `env.TNAME` 的默认值。

## 自定义插件

如需增删插件功能，编辑 `/workflows/build-padavan.yml` 中 Build Firmware 步骤里的 `sed`/`echo` 配置段，
格式参考源码 `configs/templates/` 目录下的 config 文件（`sed -i '/自定义项/d' .config` 删除旧项，`echo "自定义项=y" >> .config` 追加新项）。

编译完成后在 Actions 页面对应任务的 **Artifacts（Padavan-packages）** 或 Release 资源中下载固件。
