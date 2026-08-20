# Yuyu's Dotfiles

跨平台 dotfiles 配置管理，使用 [chezmoi](https://www.chezmoi.io/)。

## 支持平台

- ✅ Windows (Git Bash / PowerShell)
- ✅ Linux (Ubuntu/Debian, CentOS)
- ✅ macOS (Unix 通用配置)

## 快速部署到新机器

```bash
# 安装 chezmoi
# Windows: winget install twpayne.chezmoi
# Linux:   sudo snap install chezmoi --classic
# macOS:   brew install chezmoi

# 一键拉取并应用所有配置
chezmoi init --apply https://github.com/youkq95/dotfiles.git
```

## 目录结构

```
.chezmoi/              # chezmoi 配置
├── .chezmoi.toml.tmpl    # chezmoi 自身配置（模板）
├── .chezmoiignore.tmpl   # 跨平台忽略规则
├── .chezmoiversion       # 最低版本要求
├── dot_bashrc.tmpl       # .bashrc（跨平台模板）
├── dot_gitconfig.tmpl    # .gitconfig（跨平台模板）
├── dot_config/
│   └── git/
│       └── ignore        # git 全局忽略
└── run_once_before_setup.ps1.tmpl  # Windows 初始化脚本
```

## 日常使用

```bash
chezmoi edit ~/.bashrc    # 编辑配置文件（模板）
chezmoi diff              # 查看待应用的变更
chezmoi apply             # 应用到本地
chezmoi update            # 拉取远程更新并应用
chezmoi cd                # 进入源仓库目录
```

## 新机器上的凭据

API 凭据不放入仓库。首次 `chezmoi init` 时会询问
`claude_api_token`、`deepseek_api_key` 和 `stepfun_api_key`，并将结果保存在
本机 `~/.config/chezmoi/chezmoi.toml`；该文件应设置为仅用户可读
（`chmod 600`）。

## 跨平台注意事项

- `.gitconfig`: Windows 使用 `autocrlf=true` + VS Code，Unix 使用 `autocrlf=input`，编辑器由目标机器决定
- `.bashrc`: 根据 OS 和主机名调整 PATH、别名、prompt
- `run_once_*`: 只在首次部署时执行，Windows 用 PowerShell，Linux 用 bash
