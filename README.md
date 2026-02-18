# Auto Git Sync

一个用于将本地代码变更自动提交并推送到 GitHub 的轻量级工具集合。

本项目包括三个版本：

* **本地版**（`auto_git_sync_simple.py` / `AutoGitSync_Local.exe`）：通过轮询目录检测文件变化，无需额外第三方依赖。适合大多数用户。
* **完整版**（`auto_git_sync.py` / `AutoGitSync_Full.exe`）：使用 `watchdog` 实时监控文件系统，更加灵敏。
* **图形界面**（`auto_git_sync_gui.py` / `AutoGitSync_GUI.exe`）：基于 Tkinter 的桌面应用，提供浏览目录、模式切换和日志查看功能。

所有版本支持 Windows、macOS 和 Linux，目前只测试过 Git 仓库的 `main` 分支。

---

## 🚀 特性

* 自动检测文件创建、修改、删除和移动
* 忽略常见临时文件/目录（`.git`, `.vscode`, `__pycache__` 等）
* 防抖机制避免频繁提交
* 自动运行 `git add`、`git commit`、`git push`，并处理冲突、网络错误
* 简化版无需任何依赖，完整版可选安装 `watchdog`
* 可打包为单个可执行文件，附带 GUI 界面

---

## 📦 安装与依赖

1. 克隆仓库：

   ```bash
   git clone https://github.com/你的用户名/仓库名.git
   cd 仓库名
   ```

2. 使用 Python 3.6+（推荐 3.8+）。
3. 若运行完整版，需要安装 `watchdog`：

   ```bash
   pip install watchdog
   ```

4. 以下脚本位于 `scripts/` 目录：
   * `auto_git_sync_simple.py`
   * `auto_git_sync.py`
   * `auto_git_sync_gui.py`
   * 启动脚本：`start_sync.bat`, `start_sync.sh`, `start_gui.bat`

5. （可选）打包为可执行文件：
   ```bash
   pip install pyinstaller
   cd scripts
   pyinstaller --onefile AutoGitSync_Full.spec
   pyinstaller --onefile AutoGitSync_Local.spec
   pyinstaller --onefile AutoGitSync_GUI.spec
   ```
   或使用内置的 `build_release.py` / `build_exe.py`。

---

## 🛠 使用指南

### 命令行

```bash
# 简化版（推荐初次使用）
python scripts/auto_git_sync_simple.py [--path /path/to/repo]

# 完整版（需要 watchdog）
python scripts/auto_git_sync.py [--path /path/to/repo]
```

默认监控当前目录（或 exe 所在目录）。`--path` 指定其他目录。

也可以运行启动脚本：

* Windows: 双击 `scripts/start_sync.bat` 或运行 `start_sync.bat`
* macOS/Linux: `bash scripts/start_sync.sh`

### 图形界面

```bash
python scripts/auto_git_sync_gui.py
``` 

或双击 `AutoGitSync_GUI.exe`（打包后）。界面中选择仓库路径、同步模式，点击“开始同步”。

### 停止

* 命令行版本：窗口按 Ctrl+C。
* 图形界面：点击“停止同步”或关闭窗口时确认。

### 发布版说明

发布目录中含三个 exe：

* `AutoGitSync_Local.exe` —— 本地版
* `AutoGitSync_Full.exe` —— 完整版
* `AutoGitSync_GUI.exe` —— GUI

直接将 `*_Local.exe` 或 `*_Full.exe` 复制到目标仓库根目录运行。

> **首次推送提示：** 若使用 HTTPS 地址，首次 `push` 时需提供用户名和个人访问令牌。

---

## 🧪 测试

运行位于 `scripts/` 的 `test_basic.py`:

```bash
python scripts/test_basic.py
``` 

它会验证 Python 版本、当前目录是否为 Git 仓库、脚本导入情况以及启动脚本内容。

---

## 📄 示例演示

请参阅 `scripts/demo_usage.md` 中的详细演示步骤，包括创建测试文件、观察自动提交、故障排除和性能优化。

---

## ⚠️ 注意事项

* 确保 `.gitignore` 已正确配置，敏感文件（如 `.env`、密钥等）不应被提交。
* 在生产环境中使用前，建议先在测试仓库或分支上试运行。
* 若脚本在 Windows 下出现编码问题，请检查控制台编码并确保 UTF‑8。

---

## 📝 贡献与许可证

欢迎提交 issue 或 pull request。请遵守 [贡献指南](CONTRIBUTING.md)（若存在）。

本项目遵循 MIT 许可证，详见 `LICENSE` 文件。

---

感谢使用 Auto Git Sync！如有任何问题或建议，请在仓库中提交 issue。