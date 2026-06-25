# AppToolkit 现代化重构与扩展路线图 (Roadmap)

本项目将基于 Turborepo + pnpm Workspace 的 Monorepo 架构，拆分为 **Desktop 桌面端** 与 **TUI 命令行终端** 两部分进行双线演进，共享底层核心逻辑。

---

## 🖥️ Desktop 桌面端重构路线图 (React 19 + Electron Vite)

### 阶段一：Monorepo 架构演进与基础工程

- [ ] 1. 初始化 `pnpm workspace`，创建 `pnpm-workspace.yaml` 并配置工作区路由。
- [ ] 2. 引入 `Turborepo`，创建 `turbo.json` 配置全局构建缓存与任务编排。
- [ ] 3. 创建 `packages/core` 目录，用于承载 Node.js 管理、Git 配置、软件安装等底层业务逻辑。
- [ ] 4. 创建 `packages/types` 目录，统一存放全局 TypeScript 类型定义与接口声明。
- [ ] 5. 创建 `packages/config` 目录，抽取共享的 ESLint、Prettier、TypeScript 配置。
- [ ] 6. 配置全局 Git Hooks (Husky) 与 Commit Lint，规范代码提交。
- [ ] 7. 清理根目录原有的旧版依赖（如 gulp、旧版 ts-node 等）。
- [ ] 8. 验证 Monorepo 基础架构下包与包之间的互相引用是否正常。

### 阶段二：Electron Vite 与 React 19 基础框架搭建

- [ ] 9. 在 `apps/desktop` 中使用 `electron-vite` 脚手架初始化桌面端应用结构。
- [ ] 10. 将渲染进程（Renderer）的前端框架全面升级并配置为 React 19。
- [ ] 11. 安装并配置 Ant Design V6 作为主要 UI 组件库。
- [ ] 12. 安装并配置 Tailwind CSS 用于原子化样式开发。
- [ ] 13. 配置主进程（Main）与渲染进程（Renderer）之间安全的 IPC 通信 (基于 `contextBridge`)。
- [ ] 14. 搭建 React Router v7 路由架构，实现多页面切换（如首页、环境管理、设置等）。
- [ ] 15. 引入状态管理方案（如 Zustand），统一管理应用全局状态。

### 阶段三：核心业务逻辑重构与界面实现

- [ ] 16. 实现 Node.js 多版本下载与切换功能（NVM 核心能力接入 Desktop）。
- [ ] 17. 开发 Git 全局/局部配置管理的交互界面。
- [ ] 18. 开发开发工具（软件）的一键下载、解压与安装界面。
- [ ] 19. 实现 NPM/Yarn/pnpm 镜像源的快速测速与切换功能。
- [ ] 20. 开发 SSH 密钥一键生成与复制功能面板。
- [ ] 21. 完善系统环境变量的可视化管理（读取与写入）。

### 阶段四：进阶体验与用户交互优化

- [ ] 22. 实现全局的明暗主题（Dark/Light Mode）自由切换，并随系统自适应。
- [ ] 23. 添加多语言国际化（i18n）支持，首批支持中/英文。
- [ ] 24. 优化无边框窗口体验，实现自定义标题栏及拖拽区域。
- [ ] 25. 开发系统托盘（Tray）支持，增加右键快捷菜单。
- [ ] 26. 增加任务执行时的全局进度条和状态提醒（Toast / Notification）。
- [ ] 27. 优化首屏加载速度，为耗时较长的页面引入骨架屏（Skeleton）。

### 阶段五：跨平台适配与打包发布流水线

- [ ] 28. 配置 `electron-builder` 实现多平台打包构建。
- [ ] 29. 针对 macOS 进行界面与交互适配（如红绿灯按钮位置调整）。
- [ ] 30. 针对 Windows 平台适配原生窗口控件与任务栏特性。
- [ ] 31. 针对 Linux 平台打包生成 AppImage / Snap 格式。
- [ ] 32. 引入 `electron-updater`，实现桌面端应用的静默自动更新。
- [ ] 33. 配置 GitHub Actions 矩阵构建 (Matrix Build)，实现代码推送到主分支后的自动化打包。
- [ ] 34. 完成 macOS 版本的代码签名与公证 (Notarization) 配置。

---

## 💻 TUI 命令行终端开发路线图 (Node.js CLI)

### 阶段一：CLI 基础框架搭建与包结构

- [ ] 1. 在 `apps/cli` 目录初始化独立的 Node.js 命令行应用结构。
- [ ] 2. 引入 `commander` (或 `yargs`) 构建基础的命令解析与参数处理系统。
- [ ] 3. 在 `package.json` 中配置 `bin` 字段，实现本地化 `apptoolkit` 命令链接。
- [ ] 4. 引入 TUI 框架（如 `ink` 或 `@clack/prompts`）作为命令行交互的基础组件。
- [ ] 5. 将 `apps/cli` 与 `packages/core` 建立关联，复用底层业务逻辑。
- [ ] 6. 搭建全局的错误捕获机制，处理未捕获异常，并返回规范的 Exit Codes。
- [ ] 7. 增加调试模式（如传入 `--verbose` 或 `--debug`），输出详细日志。

### 阶段二：TUI 组件开发与视觉交互

- [ ] 8. 使用 TUI 框架设计并实现欢迎界面和主菜单（Main Menu）。
- [ ] 9. 实现交互式的列表选择组件（如使用方向键选择要安装的 Node 版本）。
- [ ] 10. 为耗时任务（如网络下载、解压缩）实现动态 Loading Spinner。
- [ ] 11. 实现命令行内的实时进度条（Progress Bar）展示下载进度。
- [ ] 12. 封装统一的输出样式，使用不同颜色区分 Success / Error / Warning 信息。
- [ ] 13. 实现多步骤向导（Wizard）交互，用于引导用户完成复杂的初始化配置。

### 阶段三：核心命令与功能实现

- [ ] 14. 实现 `apptoolkit init`：引导式初始化开发环境。
- [ ] 15. 实现 `apptoolkit node list`：表格形式展示本地已安装与远端可用的 Node.js 版本。
- [ ] 16. 实现 `apptoolkit node install <version>`：下载并安装指定的 Node.js 版本。
- [ ] 17. 实现 `apptoolkit node use <version>`：切换全局默认的 Node.js 版本。
- [ ] 18. 实现 `apptoolkit git config`：交互式收集用户名和邮箱，自动完成 Git 配置。
- [ ] 19. 实现 `apptoolkit registry switch`：提供主流 NPM 镜像源列表，供用户上下键选择切换。
- [ ] 20. 实现 `apptoolkit soft install <name>`：静默下载安装指定开发软件。

### 阶段四：进阶 CLI 功能与开发者体验

- [ ] 21. 实现命令自动补全（Auto-completion）功能，支持 Bash/Zsh/PowerShell。
- [ ] 22. 设计详尽的交互式帮助系统，使用户输入 `--help` 时能看到排版精美的说明文档。
- [ ] 23. 支持“静默/无头模式”（Headless Mode），允许在 CI/CD 环境中跳过 TUI 交互直接执行。
- [ ] 24. 支持读取用户级配置文件（如 `~/.apptoolkitrc`），用于保存个性化默认偏好。
- [ ] 25. 提供全局环境状态健康检查命令（如 `apptoolkit doctor`）。
- [ ] 26. 开发 CLI 自身的版本自检与一键升级命令（Self-update）。

### 阶段五：构建、测试与发布

- [ ] 27. 使用打包工具（如 `tsup` 或 `esbuild`）将 CLI 代码打包为单文件，提升执行速度。
- [ ] 28. 引入 `Vitest`，为 CLI 核心命令和交互逻辑编写单元测试。
- [ ] 29. 在 Windows CMD、PowerShell 环境下进行全面的乱码与排版兼容性测试。
- [ ] 30. 在 macOS (Zsh) 与 Linux (Bash) 终端下测试 TUI 渲染效果。
- [ ] 31. 编写清晰的 CLI 使用手册（Markdown 格式），并包含在项目文档中。
- [ ] 32. 配置 GitHub Actions，实现在发布 Release 时自动打包并发布至 NPM Registry。
