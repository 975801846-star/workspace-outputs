---
marp: true
theme: custom
paginate: true
size: 16:9
---

<style>
/* ===== 自定义中文主题 · 屯军营 ===== */
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@400;700;900&display=swap');

:root {
  --primary: #2d5016;
  --primary-light: #4a7c28;
  --accent: #d4a017;
  --bg-dark: #1a1a2e;
  --bg-light: #f7f5f0;
  --text: #333;
  --text-light: #666;
  --white: #ffffff;
}

section {
  font-family: 'Noto Sans SC', -apple-system, BlinkMacSystemFont, sans-serif;
  color: var(--text);
  padding: 40px 60px;
}

/* ===== 封面 ===== */
section.cover {
  background: linear-gradient(135deg, var(--bg-dark) 0%, #16213e 50%, #0f3460 100%);
  color: var(--white);
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
section.cover h1 {
  font-size: 2.8em;
  font-weight: 900;
  margin-bottom: 8px;
  letter-spacing: 4px;
  background: linear-gradient(90deg, #ffd700, #ffaa00);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
section.cover .subtitle {
  font-size: 1.3em;
  color: #aaa;
  margin-bottom: 50px;
}
section.cover .meta {
  font-size: 0.9em;
  color: #888;
  position: absolute;
  bottom: 50px;
}

/* ===== 章节分隔页 ===== */
section.chapter {
  background: linear-gradient(135deg, var(--primary) 0%, #1a3d0a 100%);
  color: var(--white);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
section.chapter h2 {
  font-size: 2.4em;
  font-weight: 900;
  border-bottom: 3px solid var(--accent);
  padding-bottom: 15px;
}
section.chapter .ch-num {
  font-size: 5em;
  font-weight: 900;
  opacity: 0.15;
  position: absolute;
  right: 60px;
  bottom: 20px;
}

/* ===== 内容页 ===== */
section.content {
  background: var(--white);
}
section.content h2 {
  color: var(--primary);
  font-size: 1.6em;
  border-left: 5px solid var(--accent);
  padding-left: 15px;
  margin-bottom: 25px;
}
section.content h3 {
  color: var(--primary-light);
  font-size: 1.2em;
  margin-top: 15px;
}

/* ===== 表格美化 ===== */
section table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.85em;
  margin: 10px 0;
}
section table th {
  background: var(--primary);
  color: var(--white);
  padding: 10px 8px;
  text-align: left;
  font-weight: 700;
}
section table td {
  padding: 8px;
  border-bottom: 1px solid #e0e0e0;
}
section table tr:nth-child(even) td {
  background: #f9f7f2;
}
section table tr:hover td {
  background: #e8f5e0;
}

/* ===== 卡片布局 ===== */
section.cards {
  background: var(--bg-light);
}
.cards-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 15px;
}
.card {
  background: var(--white);
  border-radius: 10px;
  padding: 18px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
  border-top: 4px solid var(--primary);
}
.card h3 { margin: 0 0 8px 0; font-size: 1em; color: var(--primary); }
.card p { margin: 0; font-size: 0.78em; color: var(--text-light); line-height: 1.5; }

/* ===== 引用/高亮块 ===== */
.highlight-box {
  background: linear-gradient(90deg, #fff8e1, #fff3cd);
  border-left: 5px solid var(--accent);
  padding: 15px 20px;
  border-radius: 0 8px 8px 0;
  margin: 15px 0;
  font-weight: 700;
  font-size: 1.1em;
}

/* ===== 脚本卡片 ===== */
.script-card {
  background: var(--white);
  border-radius: 8px;
  padding: 12px 16px;
  margin: 8px 0;
  border-left: 4px solid var(--primary);
  box-shadow: 0 1px 4px rgba(0,0,0,0.06);
}
.script-card strong { color: var(--primary); }

/* ===== 页脚 ===== */
footer {
  font-size: 0.7em;
  color: #999;
  text-align: right;
}
</style>

<!-- 
_class: cover
_paginate: false
-->

# 屯军营村·村支书王健
## 个人视频账号策划方案

<div class="subtitle">延庆区 · 屯军营村 | 2026年5月</div>

<div class="meta">策划 & 脚本全套方案 · 13条可直接拍摄成品脚本</div>

---

<!-- _class: chapter -->
## 账号定位：8大方向

<div class="ch-num">01</div>

---

<!-- _class: cards -->

# 🎯 8大可量化方向

<div class="cards-grid">
<div class="card">
<h3>A · 村务日记型 ⭐⭐⭐</h3>
<p>每天工作实拍：开会、走访、修路、调解纠纷<br>📊 粉丝量 / 完播率 / 关键词占比</p>
</div>
<div class="card">
<h3>B · 乡村振兴纪实型 ⭐⭐⭐</h3>
<p>村庄变化对比：改造前vs改造后<br>📊 播放量 / 收藏量 / 政务媒体转发</p>
</div>
<div class="card">
<h3>C · 农业产业带货型 ⭐⭐</h3>
<p>农产品展示 → 挂车销售<br>📊 GMV / 转化率 / 复购率</p>
</div>
<div class="card">
<h3>D · 基层政策解读型 ⭐⭐⭐</h3>
<p>大白话解释惠农政策、医保、宅基地<br>📊 粉丝增长 / 提问量 / 二次传播</p>
</div>
<div class="card">
<h3>E · 村支书Vlog型 ⭐⭐⭐</h3>
<p>"村支书的一天"人格化内容<br>📊 粉丝粘性 / 评论情感正负比</p>
</div>
<div class="card">
<h3>F · 乡村文化IP型 ⭐⭐⭐</h3>
<p>村名由来、军屯历史、延庆民俗<br>📊 完播率 / 文旅部门关注</p>
</div>
<div class="card">
<h3>G · 矛盾调解真人秀 ⭐⭐</h3>
<p>真实邻里纠纷调解（脱敏处理）<br>📊 互动率 / 争议出圈概率</p>
</div>
<div class="card">
<h3>H · 村支书带你看延庆 ⭐⭐</h3>
<p>以屯军营为基地辐射延庆文旅资源<br>📊 文旅局合作机会</p>
</div>
</div>

<div class="highlight-box">推荐组合：E+F 主攻（Vlog+文化IP）+ D 辅助（政策引流）+ C 阶段测试（带货）</div>

---

<!-- _class: chapter -->
## 启动逻辑框架

<div class="ch-num">02</div>

---

# 🏗 五层搭建框架

| 层级 | 名称 | 核心内容 |
|------|------|---------|
| **第1层** | 定位层 | 王健是谁？→ 延庆屯军营村的80后支书 / 真实·接地气·有温度 |
| **第2层** | 内容层 | 4大支柱：日常工作 + 政策解读 + 村庄故事 + 支书Vlog |
| **第3层** | 运营层 | 抖音（主）+ 视频号（辅）/ 每周3-5条 / 评论必回 |
| **第4层** | 转化层 | 信任 → 关注 → 铁粉 → 农产品购买 / 村民办事 |
| **第5层** | 风险层 | 内容边界设定 / 舆情预案 / 乡镇领导知情支持 |

---

# 📅 五阶段时间线

| 阶段 | 时间 | 任务 |
|------|------|------|
| 🔍 调研期 | 第1周 | 盘村资源 → 定人设 → 找对标 → 注册账号 |
| 🛠 筹备期 | 第2周 | 写框架 → 备设备 → 试拍3-5条 → 审片调整 |
| 🚀 冷启动 | 第3-4周 | 每天1条发布 → 记录数据 → 找到爆款因子 |
| 📈 增长期 | 第2-3月 | 加大产出 → 尝试直播 → 建立矩阵 |
| 🎯 稳定期 | 第4月+ | 固定栏目 → 商务合作 → 持续迭代 |

---

<!-- _class: chapter -->
## 拍摄装备 & 脚本框架

<div class="ch-num">03</div>

---

# 📷 三级装备清单

| 级别 | 设备 | 用途 | 预算 |
|------|------|------|------|
| **入门** 🥇 | iPhone 14+ / 安卓旗舰 + 大疆OM6稳定器 | 日常Vlog、走访跟拍 | ¥800-1500 |
| **进阶** 🥈 | DJI Pocket 3 + 罗德Wireless GO II | 画质升级、采访、政策讲解 | ¥4000-8000 |
| **专业** 🥉 | 大疆Mini 4 Pro + 补光灯 + 滑轨 | 村庄航拍、夜景、室内访谈 | ¥8000-15000 |

<div class="highlight-box">💡 建议：先入门，出爆款后再升级。必买只有两样：手机稳定器 + 无线领夹麦。</div>

---

# ✍️ 脚本通用结构（30-90秒）

| 时间 | 阶段 | 内容 |
|------|------|------|
| **0-7秒** | 🪝 黄金钩子 | 冲突 / 悬念 / 反常识 / 痛点问题 |
| **7-60秒** | 📖 核心内容 | 三段式：是什么 → 为什么 → 怎么办 |
| **最后5秒** | 💬 互动收尾 | 提问引导评论 / 下集预告 |

### 三大栏目

| 栏目 | 风格 | 时长 | 示例 |
|------|------|------|------|
| **支书日记** | 真实记录型 | 30-60s | 凌晨五点半的屯军营 |
| **王支书跟你说** | 知识输出型 | 30-60s | 医保报销三句话 |
| **屯军营密码** | 文化故事型 | 60-90s | 村名500年历史 |

---

<!-- _class: chapter -->
## 13条成品脚本总览

<div class="ch-num">04</div>

---

# 📋 脚本清单（1-7）

| # | 脚本名 | 栏目 | 时长 | 传播力 |
|---|--------|------|------|--------|
| 1 | 我是王健，屯军营的村支书 | 置顶介绍 | 45s | ⭐⭐ |
| 2 | 屯军营这个名字的来历 | 屯军营密码 | 60s | ⭐⭐⭐ |
| 3 | 一条路，两个样 | 支书日记 | 40s | ⭐⭐⭐ |
| 4 | 医保报销，三句话说清楚 | 王支书跟你说 | 50s | ⭐⭐⭐ |
| 5 | 凌晨五点半的屯军营 | 支书日记 | 35s | ⭐⭐⭐ |
| 6 | 村里最老的____ | 屯军营密码 | 55s | ⭐⭐ |
| 7 | 村民说：我们支书____ | 屯军营密码 | 50s | ⭐⭐⭐⭐ |

---

# 📋 脚本清单（8-13）

| # | 脚本名 | 栏目 | 时长 | 传播力 |
|---|--------|------|------|--------|
| 8 | 王健的办公桌 | 支书日记 | 40s | ⭐⭐⭐ |
| 9 | 一亩地的账本 | 王支书跟你说 | 55s | ⭐⭐⭐⭐ |
| 10 | 致在外打工的屯军营人 | 支书日记 | 60s | ⭐⭐⭐⭐⭐ |
| 11 | 村两委开会，今天吵起来了 | 支书日记 | 55s | ⭐⭐⭐⭐ |
| 12 | 城里人看不懂的农村规矩 | 屯军营密码 | 50s | ⭐⭐⭐⭐⭐ |
| 13 | 屯军营的四季 | 屯军营密码 | 65s | ⭐⭐⭐ |

<div class="highlight-box">🔥 爆款潜力 TOP3：#10 致在外打工的屯军营人 / #12 城里人看不懂的农村规矩 / #7 村民说我们支书</div>

---

<!-- _class: chapter -->
## 启动行动清单

<div class="ch-num">05</div>

---

# ✅ 立即行动

| 优先级 | 时间 | 行动 | 产出 |
|--------|------|------|------|
| 🔴 | **今天** | 找3个对标村支书账号，分析爆款视频 | 对标分析表 |
| 🔴 | **今天** | 跟王健深聊：表达欲？村民常找他办什么事？ | 人设关键词 |
| 🟡 | **本周** | 手机试拍脚本1（自我介绍），看镜头前状态 | 样片 |
| 🟡 | **本周** | 盘村资源：老照片、老物件、特色农产品、愿意出镜的老人 | 资源清单 |
| 🟢 | **两周内** | 拍完3-5条 → 注册账号 → 冷启动 | 首发内容 |

---

<!-- 
_class: cover
_paginate: false
-->

# 屯军营，开拍！

<div class="subtitle">13条脚本已就绪，只等第一声"Action"</div>

<div class="meta">延庆区屯军营村 · 村支书王健 · 2026</div>
