---
description: Git 提交并推送代码，自动生成 commit message，支持中文
---

## 流程

### Step 1: 查看改动
// turbo
1. 运行 `git status` 查看当前改动
// turbo
2. 运行 `git diff --stat` 汇总变更文件

### Step 2: 暂存并提交
// turbo
1. 运行 `git add .`
2. 分析 diff 内容，按修改的文件/功能逐条列举，自动生成中文 commit message，格式：
   ```
   feat/fix/refactor/chore: 概要标题
   
   1️⃣、具体改动一
   2️⃣、具体改动二
   3️⃣、具体改动三
   ```
// turbo
3. 运行 `git commit --no-verify -m '<生成的 commit message>'`

### Step 3: 拉取远程代码
// turbo
1. 运行 `git pull --no-edit`
2. 检查输出是否包含 "CONFLICT" 或 "Automatic merge failed"
3. **如果有冲突：**
   - 运行 `git diff --name-only --diff-filter=U` 列出冲突文件
   - 告诉用户："⚠️ 有冲突，请手动解决以下文件的冲突，解决完后告诉我"
   - 列出每个冲突文件
   - **必须停在这里，禁止继续操作，等待用户确认**
4. **如果没有冲突：** 直接跳到 Step 5

### Step 4: 用户解决冲突后
- 等待用户说"解决了""好了""继续"等
// turbo
1. 运行 `git add .`
2. 运行 `git commit --no-verify -m '解决冲突: <简要描述合并内容>'`

### Step 5: 推送
// turbo
1. 运行 `git push`
2. 如果推送失败，停下来报告错误
3. 如果成功，输出："✅ 已推送成功" 并附上本次的 commit message 内容

## 规则
- commit message 用中文，简洁描述改动内容
- 所有 commit 必须带 `--no-verify`
- 遇到冲突必须停下来，禁止自动解决
- 每步执行前展示命令，执行后展示结果
- 任何步骤失败立即停止并报告
