# Release Notes 模板

发新版本时，把下面的内容复制到 GitHub Release 的描述框里，删掉不适用的分类，替换占位内容。分类和顺序与 [CHANGELOG.md](../CHANGELOG.md) 保持一致，方便照抄。

---

## MyTV for Mac vX.Y.Z

### 新增 Added
-

### 变更 Changed
-

### 修复 Fixed
-

### 移除 Removed
-

### 安全 Security
-

---

**下载**：`MyTV-for-Mac-X.Y.Z.dmg`
**SHA-256**：`<校验和>`

**安装**：第一次打开需要手动放行一次 Gatekeeper，步骤见 [README「安装」](../README.md#安装) 或 [docs/installation.md](installation.md)。

---

<!--
发布前检查清单（不用放进 Release 描述里）：
1. CHANGELOG.md 是否已经加了对应的 [X.Y.Z] - YYYY-MM-DD 小节，并从「未发布」挪过来
2. DMG 文件名、版本号、SHA-256 是否三处一致（文件名 / 上面这份 Release Notes / CHANGELOG）
3. README.md 与 README.en.md 的下载徽章/版本号相关内容是否需要同步更新
4. 如果这次改动涉及第三方组件版本升级，THIRD_PARTY_NOTICES.md 是否需要同步
-->
