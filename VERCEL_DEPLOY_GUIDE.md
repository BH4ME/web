# Vercel Deployment Guide / Vercel 部署指南

This project is a `pnpm` monorepo. The actual web app that should be deployed to Vercel is under `packages/web`.
这个项目是一个 `pnpm` monorepo。真正要部署到 Vercel 的网页应用在 `packages/web` 目录下。

## Project Structure / 项目结构

- Repo root: `web/`
- 仓库根目录：`web/`
- App directory: `web/packages/web`
- 应用目录：`web/packages/web`
- Vercel config: `web/packages/web/vercel.json`
- Vercel 配置文件：`web/packages/web/vercel.json`
- Build output: `web/packages/web/dist`
- 构建输出目录：`web/packages/web/dist`

## Recommended Vercel Project Settings / 推荐的 Vercel 项目设置

In Vercel, configure the project like this:
在 Vercel 里，建议把项目设置成下面这样：

- Root Directory: `packages/web`
- 根目录：`packages/web`
- Framework Preset: `Vite`
- 框架预设：`Vite`
- Install Command: `pnpm install`
- 安装命令：`pnpm install`
- Build Command: `pnpm build`
- 构建命令：`pnpm build`
- Output Directory: `dist`
- 输出目录：`dist`

## Normal Deployment Workflow / 标准部署流程

When source code changes:
当你修改了源码之后：

1. Enter the repo root:
1. 进入仓库根目录：

```bash
cd /Users/bh4me_macair/Documents/Codex/2026-04-21-github/web
```

2. Install dependencies if needed:
2. 如果有需要，先安装依赖：

```bash
pnpm install
```

3. Build the web app locally:
3. 先在本地构建网页项目：

```bash
pnpm --filter packages/web build
```

4. If the build succeeds, choose one deployment method below.
4. 如果本地构建成功，再选择下面任意一种部署方式。

## Method 1: Git Auto Deploy / 方式一：Git 自动部署

If GitHub is already connected to Vercel:
如果 GitHub 已经连接到 Vercel：

```bash
git add .
git commit -m "describe your change"
git push
```

What happens next:
接下来会发生的是：

- Push to a feature branch: Vercel creates a Preview deployment
- 推送到功能分支：Vercel 会自动创建 Preview 预览部署
- Merge to `main`: Vercel creates a Production deployment
- 合并到 `main`：Vercel 会自动创建 Production 正式部署

This is the easiest long-term workflow.
这是最省事、最适合长期使用的流程。

## Method 2: Manual Deploy with Vercel CLI / 方式二：使用 Vercel CLI 手动部署

From the repo root:
在仓库根目录下执行：

Preview deployment:
预览部署：

```bash
npx vercel --cwd packages/web
```

Production deployment:
正式部署：

```bash
npx vercel --cwd packages/web --prod
```

If the CLI asks to link the project, follow the prompts once and it will remember the project settings.
如果 CLI 第一次要求你关联项目，按提示做一次就行，之后它会记住这套设置。

## Common Daily Flow / 日常最常用流程

For most updates, this is enough:
大多数情况下，下面这套命令就够了：

```bash
cd /Users/bh4me_macair/Documents/Codex/2026-04-21-github/web
pnpm install
pnpm --filter packages/web build
git add .
git commit -m "update web app"
git push
```

Then open Vercel and verify the Preview or Production deployment.
然后打开 Vercel，检查预览部署或正式部署是否成功。

## If Deployment Fails / 如果部署失败

Check these first:
优先检查下面这些地方：

- You are deploying `packages/web`, not the monorepo root
- 你部署的是 `packages/web`，不是整个 monorepo 根目录
- `pnpm install` completed successfully
- `pnpm install` 是否成功执行完毕
- `pnpm --filter packages/web build` passes locally
- `pnpm --filter packages/web build` 是否能在本地通过
- Vercel Root Directory is set to `packages/web`
- Vercel 的 Root Directory 是否设置成 `packages/web`
- Vercel Output Directory is set to `dist`
- Vercel 的 Output Directory 是否设置成 `dist`
- Any required environment variables are configured in Vercel
- 如果项目依赖环境变量，是否已经在 Vercel 中配置好

## Notes for This Repo / 这个仓库的特别说明

- `main` source code in this fork currently matches upstream
- 这个 fork 当前的 `main` 源码与上游仓库一致
- `gh-pages` contains built static site artifacts and is separate from the source deployment flow
- `gh-pages` 分支里主要是已经构建好的静态网页产物，它和源码部署流程是分开的
- For Vercel, source deployment should be based on `packages/web`, not `gh-pages`
- 对于 Vercel，应该部署 `packages/web` 的源码，而不是 `gh-pages`

## Handy Commands / 常用命令

Repo root:
仓库根目录：

```bash
cd /Users/bh4me_macair/Documents/Codex/2026-04-21-github/web
```

Local dev:
本地开发：

```bash
pnpm --filter packages/web dev
```

Local build:
本地构建：

```bash
pnpm --filter packages/web build
```

Preview deploy:
预览部署：

```bash
npx vercel --cwd packages/web
```

Production deploy:
正式部署：

```bash
npx vercel --cwd packages/web --prod
```
