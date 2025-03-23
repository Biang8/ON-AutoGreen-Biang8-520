# auto-green

自动保持 GitHub 提交状态常绿。

## 原理

使用 GitHub Actions 的定时任务功能，每隔一段时间自动执行 `git commit`，提交信息为 "Keep writing documents!"。该任务可通过手动触发，也可在特定条件下自动触发。

有关 Github Action 的原理，可查看官方文档 [Github Action 简介](https://docs.github.com/cn/actions/learn-github-actions/introduction-to-github-actions)。

## 使用

- 点右上角 **Use this template** 按钮复制本 GitHub 仓库，**:warning: 千万不要 Fork，因为 fork 项目的动态并不会让你变绿，而且你的账号可能会被 github 查封！ :warning:**
- 配置 Secrets：在仓库的设置中添加 `EMAIL`、`NAME` 和 `GITHUB_TOKEN` 三个 Secrets，分别对应你的邮箱、昵称和 GitHub 访问令牌。
- （可选）修改 [ci.yml 文件的第 26 行](https://github.com/justjavac/auto-green/blob/master/.github/workflows/ci.yml#L26) 来调整定时任务的触发条件，当前配置为每 15 分钟尝试触发一次，且在 `github.run_number` 能被 2、3 或 4 整除时才会真正执行任务。
- （可选）你可以通过修改 [ci.yml 文件的第 20 行](https://github.com/justjavac/auto-green/blob/master/.github/workflows/ci.yml#L20) 来调整定时任务的频率。

计划任务语法有 5 个字段，中间用空格分隔，每个字段代表一个时间单位。

```plain
┌───────────── 分钟 (0 - 59)
│ ┌───────────── 小时 (0 - 23)
│ │ ┌───────────── 日 (1 - 31)
│ │ │ ┌───────────── 月 (1 - 12 或 JAN - DEC)
│ │ │ │ ┌───────────── 星期 (0 - 6 或 SUN - SAT)
│ │ │ │ │
│ │ │ │ │
│ │ │ │ │
* * * * *
```

每个时间字段的含义：

|符号   | 描述        | 举例                                        |
| ----- | -----------| -------------------------------------------|
| `*`   | 任意值      | `* * * * *` 每天每小时每分钟                  |
| `,`   | 值分隔符    | `1,3,4,7 * * * *` 每小时的 1 3 4 7 分钟       |
| `-`   | 范围       | `1-6 * * * *` 每小时的 1-6 分钟               |
| `/`   | 每         | `*/15 * * * *` 每隔 15 分钟                  |

**注**：由于 GitHub Actions 的限制，如果设置为 `* * * * *` 实际的执行频率为每 5 分执行一次。
