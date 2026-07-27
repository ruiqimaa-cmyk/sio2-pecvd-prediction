# SiO2 PECVD 预测模型网页

这是基于 `York-SiO2-PECVD-v1` 的 React/Vite 网页原型。

## 功能

- 输入电极结构、基底位置、压力
- 预测 SiO2 膜厚、沉积速率、均匀性参数
- 展示模型评价图和推荐实验条件
- 可选连接 Supabase，保存每次预测记录

## 本地运行

当前电脑 npm 拉取依赖较慢时，可以先直接打开：

```text
static.html
```

这个静态版不依赖 npm，已经内置同一套模型系数，适合先演示和试用。

React/Vite 工程运行方式：

```bash
npm install
npm run dev
```

## Supabase 配置

1. 在 Supabase SQL Editor 中运行：

```text
supabase/schema.sql
```

2. 复制 `.env.example` 为 `.env.local`，填写：

```text
VITE_SUPABASE_URL=你的 Supabase Project URL
VITE_SUPABASE_ANON_KEY=你的 Supabase anon public key
```

3. 重启开发服务器。

未配置 Supabase 时，网页仍可本地预测，但点击“保存本次预测”不会写入云端。

静态版 `static.html` 如需连接 Supabase，可在文件底部脚本中填写：

```js
const SUPABASE_URL = "";
const SUPABASE_ANON_KEY = "";
```

## Vercel 部署

1. 把本文件夹推送到 GitHub 仓库。
2. 在 Vercel 新建项目并选择该仓库。
3. Framework 选择 Vite。
4. 添加环境变量：
   - `VITE_SUPABASE_URL`
   - `VITE_SUPABASE_ANON_KEY`
5. 部署。

## 模型边界

该网页是预测模型原型，基于 York SiO2 PECVD 公开数据集和当前岭回归模型系数。压力模型的训练范围为 1.0-2.2 Torr，超出范围的预测只适合趋势参考。
