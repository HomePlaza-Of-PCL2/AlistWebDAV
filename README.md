# Alist WebDAV

**主页市场 OSS · 自动化部署参考文档**

**管理员**\
PCL2 Homepage Plaza Official\
@MoYuan-CN / @Joker2184

---

## 基于 GitHub Actions 的 Alist 全量同步方案

该方案基于 **GitHub Actions**，在仓库发生 `push` 或 `pull_request` 事件时，自动将仓库内容同步至 Alist OSS（通过 WebDAV）。

参考仓库：
[PCL 非官方主页市场第三代，全新的构建技术 · HomePlaza-Of-PCL2/Homepage.Market](https://github.com/HomePlaza-Of-PCL2/Homepage.Market)

---

## 使用前准备

### 1. 启用 GitHub Actions

在**需要同步到 OSS 的仓库**中，完成以下操作：

1. 在仓库根目录创建路径：

```
.github/workflows/
```

2. 将 `Sync-to-Alist-via-WebDAV.yml` 放入该目录中
   （用于激活 GitHub Actions）

---

### 2. 配置 Repository Secrets（重点）

进入仓库：

```
Settings → Secrets and variables → Actions → Repository secrets
```

依次添加以下 Secrets：

| Name             | 说明                                      |
| ---------------- | ----------------------------------------- |
| `WEBDAV_HOST`    | OSS 域名 `pclhomeplazaoss.lingyunawa.top` |
| `WEBDAV_PORT`    | OSS 内部端口（联系管理员获取）            |
| `ALIST_USERNAME` | OSS 用户名（联系管理员获取）              |
| `ALIST_PASSWORD` | OSS 密码（联系管理员获取）                |

示例说明（以 `WEBDAV_HOST` 为例）：

- **Name**：`WEBDAV_HOST`
- **Secret**：`pclhomeplazaoss.lingyunawa.top`

其余项按表格说明填写即可。

> ⚠️ 新成员如未获取账号信息，请私聊 @MoYuan-CN

（Secrets 配置界面示例图略）

---

### 3. WebDAV 权限说明（必须注意）

**默认情况下，OSS 的 WebDAV 功能是关闭的。**

在首次使用前，请联系以下任一管理员开通权限：

- @MoYuan-CN
- @Joker2184

未开通 WebDAV 时，Actions 会正常运行，但同步必然失败。

---

## ⚠️ 注意事项

### 1. 手动触发 GitHub Actions（推荐）

如果你**希望支持手动触发同步**，请在 `Sync-to-Alist-via-WebDAV.yml` 中的 `on:` 节点下添加 `workflow_dispatch`。

示例：

```yml
on:
  push:
  pull_request:
  workflow_dispatch:
```

添加后，你可以在 GitHub 仓库的 **Actions 页面**中，手动点击运行该同步流程，无需额外提交文件或制造无意义改动。

### 2. 什么时候需要手动触发

以下情况适合使用 `workflow_dispatch`：

- Secrets 配置完成后，希望立即同步一次
- WebDAV 权限刚刚开通
- 之前 Actions 因环境或网络问题失败
- 不想通过修改文件来“强行触发”流程

---

## 总结（给人看的版本）

- 本方案用于 **仓库 → Alist OSS 的自动同步**
- 同步触发方式：`push` / `pull_request`
- 核心依赖：

  - GitHub Actions
  - WebDAV（需手动开通）
  - Repository Secrets 配置正确

- 出问题先看：

  1. Secrets 是否填错
  2. 联系管理员检查 WebDAV 是否已开通
