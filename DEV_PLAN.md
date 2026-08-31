# 生词主动回忆小程序 — 最终开发计划（v3.0 定稿）

> 用途：安要「两版 PK」——本文件是龙虾版完整开发计划，主机智能体据此做对照版，谁的逻辑更自洽谁执行。
> 目标：消除一切歧义，主机智能体拿着这份就能准确实现。所有「必须/可选/默认」都说清。

---

## 0. 一句话定位

一个**联网的学术生词采集 + 主动回忆背词器**。
核心 = 「搜索一个词 → 自动联网抓全（英文释义/例句/发音/中文/同义）+ 存库 → 之后用主动回忆方式背」。

⚠️ 前两版最大错误：把产品做成了「手动录词工具」。**本版核心是「联网自动采集」，不是手动录入。**

---

## 1. 技术栈（锁定，勿改）

- Windows 本地网页版，只在电脑用，无手机/无公网
- 后端 Python + Flask（Anaconda base 环境，已装 Flask/requests）
- 数据库 SQLite 单文件 vocab.db
- 前端单页 HTML + 原生 JS + CSS，轻盈简洁
- 运行 `python app.py` → 浏览器 `http://127.0.0.1:5000`

### 联网数据源（两个，混合用）
1. **免费词典 API** —— `https://api.dictionaryapi.dev/api/v2/entries/en/<word>`
   - 免费、无需 key
   - 提供：音标 phonetics、**发音音频 mp3 URL**、词性 partOfSpeech、英文释义 definitions、例句 examples、同义词 synonyms
   - 局限：纯英文，无中文释义
2. **DeepSeek API** —— 补「中文释义 + 同义替换 + 专业术语解释」
   - 模型 deepseek-chat，需 API key
   - 用于词典查不到、或需要中文的场景

---

## 2. 数据库结构（SQLite）

### 表 words（词汇库）
| 字段 | 类型 | 说明 |
|------|------|------|
| id | INTEGER PK | |
| word | TEXT UNIQUE NOT NULL | 词条（headword） |
| phonetic | TEXT | 音标（IPA） |
| audio_path | TEXT | 本地发音文件路径（如 pronunciations/analyse.mp3）；空=无 |
| audio_url | TEXT | 在线发音 URL（备份，本地无时用） |
| note | TEXT | 英文释义（English definition） |
| zh | TEXT | 中文释义（可空） |
| example | TEXT | 英文例句（可空） |
| synonyms | TEXT | 同义替换，逗号分隔（可空） |
| pos | TEXT | 词性 partOfSpeech（可空） |
| in_learn | INTEGER DEFAULT 0 | 是否加入背诵清单 0/1 |
| source | TEXT | 'manual' / 'awl' / 'dict'（词典抓取） |
| sublist | INTEGER DEFAULT 0 | AWL 子表号（非 AWL=0） |
| created_at | TEXT | 时间 |

### 表 reviews（学习记录）
word_id, review_date(YYYY-MM-DD), result('correct'/'wrong'), last_input, created_at

### 表 notebook（两个错题本）
word_id, type('spelling'/'understand'), added_at

### 表 daily_done（防当天重复）
word_id, done_date(YYYY-MM-DD)

---

## 3. 核心概念（务必分清）

**词库 ≠ 背诵清单**
- 词库：所有采集到的词（AWL 570 + 词典抓的 + 手动录的）
- 背诵清单：手动勾选（in_learn=1），**只有这些词进背词流程**
- AWL 预置时 in_learn 默认 0，不自动进背诵

---

## 4. 功能清单（按优先级）

### 【P0 核心】词汇搜索 + 联网自动采集（本次最优先实现）

交互流程：
```
用户输入一个单词 → 点「搜索/添加」
  ↓
① 先查本地词库：有这个词？
  ├─ 有 → 直接显示该词全部信息（秒开，不联网）
  └─ 没有 → 联网采集：
       - 调免费词典 API 抓：音标、发音 mp3、词性、英文释义、例句、同义词
       - 下载发音 mp3 到本地 pronunciations/<word>.mp3
       - 若需中文 / 词典查不到 / 专业术语 → 调 DeepSeek 补中文释义 + 同义替换
  ↓
② 自动填充进一个「编辑表单」（词、音标、发音、英文释义、例句、同义词、中文 各一栏）
   用户可手动修改任意一栏
  ↓
③ 点「保存」→ 写入本地词库（含本地音频路径）
```
关键点：
- **一定有联网**：库没有就自动联网抓，绝不要求用户手动填
- **发音要能播放**：网页里 <audio> 标签，优先播本地 mp3（无本地则播在线 URL）
- **自动填充后必须可手动改**（AI/词典可能不准，用户最终把关）
- 抓取失败要友好提示（"词典查不到，可尝试换个拼写"）

免费词典 API 返回结构要点（dictionaryapi.dev）：
```json
[{
  "word": "analysis",
  "phonetics": [{"text": "/əˈnælɪsɪs/", "audio": "https://...mp3"}],
  "meanings": [{
    "partOfSpeech": "noun",
    "definitions": [{"definition":"...","example":"..."}],
    "synonyms": ["..."]
  }]
}]
```
- 取第一个 phonetic.audio（非空的）
- 取第一个 meanings[0].partOfSpeech
- 取第一个非空 definition 作 note，第一个非空 example 作 example
- synonyms 合并去重

### 【P1】AWL 学术词库预置
- 570 词，sublist 1-9 各 60 + sublist 10 共 30
- 数据文件 awl_words.json（已备好：word + sublist + related）
- 预置逻辑：启动时词库为空则 seed；note 初值可放 related word forms，其余字段空（音频/中文/例句等用户后续搜索时自动补）
- **重要**：AWL 词预置后，若用户搜索并「联网采集」了某个 AWL 词，应**更新**该词的完整信息（补音频/中文/例句），而不是新插一条

### 【P2】背词（主动回忆）
- 只从背诵清单（in_learn=1）取词
- 一页 20 词（默认，可配 page_size），左词右填英文释义
- 每日学习量 daily_limit 可设；随机打乱；当天学过不重复
- 每页填完点「提交」→ 批量 AI 判定

### 【P3】AI 判定 + 两个笔记本
判定结果四档：
| 结果 | 去向 |
|------|------|
| ✅ 理解正确 | 通过 |
| ⚠️ 拼写错误（不影响理解） | 不自动进；AI 下划线标出，用户点「+」手动加拼写本 |
| ❌ 理解错误 | 自动进「理解笔记本」 |

- AI 返回 JSON：{understand:bool, misspell:[词], advice:中文建议}
- 拼写本手动加；理解本自动进
- 两个本共同规则：连续 3 自然日答对自动移出；有删除按钮手动删
- 判定时把用户输入原样贴出，misspell 的词下划线标出

### 【P4】标准答案三层展示
1. 默认只显示英文释义（note）+ 音标 + 可播放发音
2. 「显示中文」按钮 → 点击展开中文
3. 「例句」按钮 → 展开例句

### 【P5】词库浏览 + 挑词
- 筛 AWL / 自录+词典 / 全部；可只看已加入背诵
- 每词旁 ➕/✅ 切换加入/移出背诵清单
- 显示 sublist 号 或 来源标记

### 【P6】导出
- 「关键词 | 备注」两列表格（语言班关键词表格式）

### 【P7】设置
- DeepSeek API key
- 每日学习量 / 每页词数

---

## 5. 关键交互细节（安特别要求，不可偏离）

1. 一页多词（不是一页一词）——避免学习状态断续
2. 批量判定——整页提交一次判定，结果就地展开
3. 「显示中文」点击才展开——先自己回忆，实在不懂再看
4. 界面轻盈，不臃肿不花哨
5. 拼写错误限制：允许不影响理解的拼写错误；错得离谱的才值得进本
6. 错词用户最终拍板——AI 只提示，加不加进拼写本由用户点「+」决定

---

## 6. DeepSeek 调用约定

- 模型 deepseek-chat，response_format json_object
- 判词 prompt 返回 {understand, misspell, advice}
- 补中文 prompt 返回 {zh, synonyms}

---

## 7. 技术实现要点

- 发音本地存储：抓词时下载 mp3 到 `pronunciations/` 目录（文件名用 word 规范化，防止非法字符）
- 网络请求要 try/except，超时设置（如 10-15s），失败友好降级（词典挂了→至少用 DeepSeek 兜底）
- 免费词典 API 无 key，但可能限流；DeepSeek 有 key
- 词条规范化：统一小写、去首尾空格；带空格短语（如 "carbon footprint"）也要支持

## 8. 本版与之前的差异（说明为什么重做）

前两版错误：做成了「手动录词」，用户要的是「搜索→联网自动采集→自动填充→可手动微调→存库」。
本版 P0 就是「联网采集」，其余都在此基础上。

## 9. 验收标准（做完自测）

1. 输入一个新词 → 能联网抓到「音标+发音+英文释义+例句+中文+同义词」并自动填充
2. 发音能播放（本地 mp3）
3. 自动填充后能手动改任何一栏再保存
4. 再搜同一个词 → 秒开（走本地库，不重复联网）
5. 库没有的词 → 自动联网抓；库有的 → 不重复抓
6. AWL 570 词在词库、默认不进背诵清单
7. 只有勾选进背诵清单的词才进背词
