This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more details.



# 🎮 RPG 网站项目

本项目基于 Next.js App Router + Supabase + Vercel + GitHub 构建的全栈 RPG 社区网站。

## 📂 项目结构树

```text
my-rpg-project/
├── public/                 # 静态资源目录
│   ├── fonts/              # 自定义字体文件
│   ├── images/             # Logo、背景图、世界观插画、人设图
│   └── icons/              # 网站图标、Favicon
├── src/
│   ├── app/                # 【核心】Next.js App Router 路由层
│   │   ├── (public)/       # 路由组：无需登录的公开页面
│   │   │   ├── page.tsx    # 首页 (公告、世界观、人设展示)
│   │   │   ├── help/       # 帮助中心 (左右切换图片)
│   │   │   ├── register/   # 注册账号/提交审核申请页
│   │   │   └── layout.tsx  # 公开页面布局 (含顶部导航)
│   │   ├── (auth)/         # 路由组：认证相关
│   │   │   ├── login/      # 登录页
│   │   │   └── layout.tsx  # 登录页布局 (居中卡片)
│   │   ├── (dashboard)/    # 路由组：玩家登录后界面
│   │   │   ├── profile/    # 个人信息、背包、过本记录
│   │   │   ├── messages/   # 站内信 (收发列表)
│   │   │   ├── dungeons/   # 副本库、正在招募、投稿入口
│   │   │   ├── shop/       # 商城、每日抽奖
│   │   │   ├── achievements/# 成就库、排行榜
│   │   │   ├── guild/      # 公会管理、贡献值兑换
│   │   │   ├── calendar/   # 活动日历
│   │   │   ├── settings/   # 申请换人设、修改密码
│   │   │   └── layout.tsx  # 玩家后台布局 (含侧边栏)
│   │   ├── (admin)/        # 路由组：管理员后台
│   │   │   ├── audit/      # 审核后台 (账号审核、副本二审)
│   │   │   ├── master/     # 主审后台 (发福利、改数据、道具创建)
│   │   │   ├── logs/       # 经济数据看板、操作日志
│   │   │   └── layout.tsx  # 管理员布局 (深色严肃风格)
│   │   ├── api/            # API 路由 (用于 Webhook 或特殊接口)
│   │   ├── globals.css     # 全局样式 (Tailwind, shadcn 变量)
│   │   ├── layout.tsx      # 根布局 (ThemeProvider, Toaster)
│   │   └── not-found.tsx   # 404 页面
│   ├── components/         # 【UI】组件库
│   │   ├── ui/             # shadcn/ui 基础组件 (Button, Input等)
│   │   ├── layout/         # 全局布局组件 (Navbar, Sidebar, Footer, ThemeToggle)
│   │   ├── public/         # 首页专用 (WorldViewCard, AnnouncementBanner)
│   │   ├── player/         # 玩家业务组件 (BackpackGrid, DungeonFilter, MessageItem)
│   │   ├── admin/          # 管理员组件 (AuditTable, UserBanModal, EconomyChart)
│   │   └── forms/          # 复杂表单 (RegisterForm, DungeonSubmitForm, GuildApplyForm)
│   ├── lib/                # 【工具】核心工具库
│   │   ├── supabase/       # Supabase 客户端配置
│   │   │   ├── client.ts   # 浏览器端 Client
│   │   │   ├── server.ts   # 服务端 Client (带 Cookies)
│   │   │   └── middleware.ts # 中间件辅助函数
│   │   ├── utils.ts        # cn() 类名合并工具
│   │   └── constants.ts    # 常量 (如：每日发信上限5条, 积分汇率)
│   ├── actions/            # 【后端】Server Actions (增删改查逻辑)
│   │   ├── auth-actions.ts # 注册、登录、注销、换人设逻辑
│   │   ├── dungeon-actions.ts # 副本投稿、报名、取消报名、筛选
│   │   ├── message-actions.ts # 发送站内信、读取、封禁发信功能
│   │   ├── shop-actions.ts # 购买、抽奖、积分扣除 (事务处理)
│   │   └── admin-actions.ts # 审核通过/驳回、封号、发福利、修改记录
│   ├── hooks/              # 【逻辑】自定义 React Hooks
│   │   ├── use-user.ts     # 获取当前用户信息 & 审核状态
│   │   ├── use-points.ts   # 获取/刷新积分
│   │   └── use-toast.ts    # 全局提示框 Hook
│   ├── stores/             # 【状态】Zustand 状态管理
│   │   ├── use-dungeon-store.ts # 副本筛选条件、报名弹窗状态
│   │   └── use-ui-store.ts # 侧边栏开关、全局 Loading 状态
│   ├── types/              # 【类型】TypeScript 类型定义
│   │   ├── database.types.ts # Supabase 自动生成的数据库类型
│   │   ├── user.types.ts   # 用户、背包、积分、人设类型
│   │   └── dungeon.types.ts # 副本、招募、审核状态类型
│   └── middleware.ts       # 【网关】路由中间件 (登录拦截、管理员权限校验)
├── .env.local              # 真实环境变量 (密钥/URL，已加入 .gitignore)
├── .gitignore              # Git 忽略文件 (包含 .env.local)
├── components.json         # shadcn/ui 配置文件
├── next.config.mjs         # Next.js 配置 (支持 Supabase transpile)
├── package.json            # 项目依赖与脚本
├── postcss.config.mjs      # Tailwind CSS 配置
├── tailwind.config.ts      # Tailwind 主题配置 (暗色模式, 颜色)
├── tsconfig.json           # TypeScript 配置
└── README.md               # 项目说明文档

#RPG网站开发计划
|——Phase 1: 基础设施与公开访问
|    |——基础环境搭建
111|    |    |——Next.js + Supabase + Tailwind 初始化
|    |    |——配置 src/lib/supabase (Client/Server/Middleware)
|    |    |——定义全局 TypeScript 类型 (src/types)
|    |——公开主页 (Public)
|    |    |——首页面联网进入
|    |    |    |——公告栏 (不可复制文字)
|    |    |    |——群观/世界观展示 (下标分页)
|    |    |    |——审核须知 (不可复制)
|    |    |    |——人设表/审核标准 (可复制文字)
|    |    |    |——模块右上角更新公告 & 历史版本存储
|    |——注册与审核流程
|         |——注册账号
|         |    |——复杂表单 (文字/数字/单选/多选/QQ号/密码)
|         |    |——提交审核按钮
|         |——审核进度
|              |——待审核期间禁止二次提交
|              |——审核通过后开放登录权限
|
|——Phase 2: 玩家核心系统 (Dashboard)
|    |——账户与安全
|    |    |——登录账号 (Supabase Auth)
|    |    |——玩家界面基础
|    |         |——暗色模式切换
|    |         |——帮助中心 (左右切换图片)
|    |——个人信息系统
|    |    |——信息展示
|    |    |    |——自动生成显示 (基于注册填表)
|    |    |    |——积分显示
|    |    |    |——背包系统
|    |    |    |——过副本记录
|    |    |——账号维护
|    |         |——申请换人设 (重新填表，继承积分，二次确认，删除旧人设)
|    |         |——玩家信息修改
|    |         |——玩家账号删除/注销 (数据保留策略：账号删但数据留痕，拉黑QQ号防重注)
|    |——社交与通讯
|    |    |——站内信
|    |         |——接收列表
|    |         |——发送限制 (每天最多5条，频繁骚扰封禁功能)
|    |——副本系统 (核心玩法)
|    |    |——副本库
|    |    |    |——已结束/未开始分类
|    |    |    |——标签筛选
|    |    |——正在招募
|    |    |    |——报名/取消报名逻辑
|    |    |    |——符合要求才能报名校验
|    |    |——副本投稿
|    |         |——填表发送申请
|    |         |——审核通过后一键发布招募
|    |         |——筛选器 (称号/时间/人数/要求/介绍)
|    |——经济与成就
|         |——商城
|         |    |——商品列表 & 详情
|         |    |——每日抽奖逻辑
|         |    |——右上角实时积分显示
|         |    |——商品投稿入口
|         |——成就
|         |    |——成就库展示
|         |    |——获得成就通知
|         |    |——排行榜
|         |——公会
|         |    |——贡献物品/积分兑换贡献值
|         |    |——退出申请
|         |    |——公会商店 (专属商品)
|         |——活动日历
|
|——Phase 3: 管理员后台 (Admin)
     |——审核后台 (Audit)
     |    |——账号注册申请 (查看/通过/驳回)
     |    |——副本投稿申请
     |    |    |——通过 -> 自动加入副本系统
     |    |    |——打回 -> 填写理由 -> 发送站内信通知
     |    |——玩家信息修改审核 (查看修改前后对比)
     |——主审后台 (Master)
          |——二次审核副本
          |——福利发放 (发放积分/道具)
          |——副本奖励发放
          |——物品道具创建
          |——权限管理 (除副本审核外全部功能)
          |——经济数据看板
          |——操作日志 (公开页和玩家信息修改记录，审计追踪)