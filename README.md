# skills

个人的 Claude Code **全局 skills** 集合，放在 `~/.claude/skills/` 下，用于在多台机器、多个项目之间同步。未来也会引用别人的优秀 skills，欢迎大家的批评、建议以及大佬的 skills 自荐。

## 收录的 skill

| Skill | 用途 |
| --- | --- |
| [`skill-authoring`](skill-authoring/SKILL.md) | 编写、修改与检查 skill 本身的规范 |
| [`zju-lab-report`](zju-lab-report/SKILL.md) | 浙江大学课程实验报告的撰写、补写、编译与检查（Typst + ZJU-Project-Report-Template submodule） |
| [`git-agents`](git-agents/SKILL.md) | 跨机器、跨 harness 同步全局指令与 harness 文件（submodule 引入 [floklein/git-agents](https://github.com/floklein/git-agents)） |

每个 skill 是一个目录，含必需的 `SKILL.md`（YAML frontmatter 的 `name`、`description`，加上正文），以及可选的 `references/`、`scripts/`、`assets/`。

## 使用

克隆到全局 skills 目录：

```bash
git clone --recurse-submodules <本仓库 URL> ~/.claude/skills
```

已有 `~/.claude/skills` 目录时，把它添加为远端再拉取即可；目录本身就是一个 git 仓库。克隆后记得初始化子模块：

```bash
git submodule update --init --recursive
```

`dsh` 从 `~/.dsh/skills` 读取 skills，可链接到本目录，避免维护两份：

```powershell
New-Item -ItemType SymbolicLink -Path "$env:USERPROFILE\.dsh\skills" -Target "$env:USERPROFILE\.claude\skills"
```

### 子模块与符号链接

`git-agents` 以 submodule 形式引入上游仓库的 `skills/git-agents`，因此在仓库根目录放了一个符号链接 `git-agents -> .upstream/git-agents/skills/git-agents`，让 skill 仍能被正常发现。更新到上游最新版：

```bash
git submodule update --remote .upstream/git-agents
```

符号链接在 Linux/macOS 上开箱即用；Windows 需开启 Developer Mode（或以管理员身份克隆），并确保 `core.symlinks=true`。

## 约定

- **以个人使用为优先。**本仓库主要服务于自己在多台机器上的使用；submodule URL、符号链接、目录布局等取舍以本人使用便利为主，同时兼顾公开克隆者的体验。
- **只放跨项目通用的 skill。**与具体仓库绑定的内容（该项目的目录结构、构建命令、课程或业务约定）放在那个仓库自己的 `.claude/skills/` 下；每次会话都需要的短约定写进该仓库的 `CLAUDE.md`，不放进 skill。
- **本仓库是公开的，不要提交任何真实个人信息**——学号、姓名、邮箱、账号、主机名、内网地址、密钥凭证。需要区分身份时用占位符（`<学号>`、`<姓名>`、`<用户>`）。
- 项目级 skill 应**引用**这里的通用 skill，而不是复制其内容，否则两份内容迟早会漂移成不一致的版本。

新增或修改 skill 的具体流程与自检清单见 [`skill-authoring`](skill-authoring/SKILL.md)。

## 致谢

- 实验报告模板来自 [memset0/ZJU-Project-Report-Template](https://github.com/memset0/ZJU-Project-Report-Template)（MIT License）；`zju-lab-report` 的排版约定、编译方式与注意事项均基于它的 `v1.3` 版本。
