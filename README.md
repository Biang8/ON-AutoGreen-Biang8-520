# auto-green

自动保持 GitHub 提交状态常绿。

## 原理

使用 GitHub Actions 的定时任务功能，每隔一段时间自动执行 `git commit`，提交信息为当前时间的 "Keep writing documents at [具体时间]"。

有关 Github Action 的原理，可查看官方文档 [Github Action 简介](https://docs.github.com/cn/actions/learn-github-actions/introduction-to-github-actions)。

## 使用步骤

### 1. 复制仓库
点右上角 **Use this template** 按钮复制本 GitHub 仓库。

**:warning: 千万不要 Fork，因为 fork 项目的动态并不会让你变绿，而且你的账号可能会被 GitHub 查封！ :warning:**

### 2. 配置仓库的 Secrets
在仓库的设置中，添加以下 Secrets：
- `EMAIL`: 你的 GitHub 邮箱
- `NAME`: 你的 GitHub 昵称
- `GITHUB_TOKEN`: 具有仓库读写权限的个人访问令牌

### 3. 配置 `ci.yml` 文件

#### 3.1 启用手动触发功能（可选）
`ci.yml` 文件中已经配置了手动触发事件 `workflow_dispatch`，你可以通过 GitHub 界面手动触发工作流，并选择是否启用自动全绿功能。如果你想调整默认值，可以修改 [ci.yml 文件的第 7 行](https://github.com/your-repo/ON-AutoGreen-Biang4-444520/blob/master/.github/workflows/ci.yml#L7) 的 `default` 值。

#### 3.2 设置自动触发频率
修改 [ci.yml 文件的第 19 行](https://github.com/your-repo/ON-AutoGreen-Biang4-444520/blob/master/.github/workflows/ci.yml#L19) 来调整自动提交的频率。

计划任务语法有 5 个字段，中间用空格分隔，每个字段代表一个时间单位。

```plain
┌───────────── 分钟 (0 - 59)
│ ┌───────────── 小时 (0 - 23)
│ │ ┌───────────── 日 (1 - 31)
│ │ │ ┌───────────── 月 (1 - 12 或 JAN-DEC)
│ │ │ │ ┌───────────── 星期 (0 - 6 或 SUN-SAT)
│ │ │ │ │
│ │ │ │ │
│ │ │ │ │
* * * * *
