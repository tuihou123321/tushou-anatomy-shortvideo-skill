# 徒手整形解剖短视频流水线（Codex Skill）

把**口播逐字稿**做成解剖科普短视频的可复用 Skill：真源锁结构 → 科技风渲染 → 质检 → **分镜确认（总表 + 真源/科技风对照）** → Seedance 成片 + 口播 + 疏音效。

可走 Grok Bot 或 Codex 两条路径；本仓库是 Codex Skill 真源，Grok Bot 助手复用同一流水线与 `assets/coronal/`。仓库不含 API Key、克隆声线或私有账号资源。

## 两种使用方式

### 1. 通过 Grok Bot 使用

用助手链接打开「徒手整形视频助手」：https://x.ai/bot/xdm8WZlbUUPehrxL_-8cc ，把口播文案发给 Bot，按流水线逐步确认出片。适合不想自己装 Skill、要在对话里逐步验收的人。

### 2. 用 Codex 使用

把本仓库装成本机 Codex Skill（见下方「安装」），在 Codex 对话中触发 `$tushou-anatomy-shortvideo`。不依赖 Grok Bot 会话。

## 安装

macOS / Linux：

```bash
mkdir -p "$HOME/.codex/skills"
git clone https://github.com/tuihou123321/tushou-anatomy-shortvideo-skill.git \
  "$HOME/.codex/skills/tushou-anatomy-shortvideo"
```

Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force "$HOME\.codex\skills"
git clone https://github.com/tuihou123321/tushou-anatomy-shortvideo-skill.git `
  "$HOME\.codex\skills\tushou-anatomy-shortvideo"
```

也可用（若你已装 skills CLI）：

```bash
npx -y skills add tuihou123321/tushou-anatomy-shortvideo-skill -g --all
```

安装后重启 Codex。触发示例：

```text
用 $tushou-anatomy-shortvideo，按下面这份逐字稿做冠状缝开场 15 秒样片分镜，先出确认表再成片。
```

## 你需要准备什么

| 能力 | 是否必须 | 说明 |
| --- | --- | --- |
| 火山引擎 Seedance（`ARK_API_KEY`） | **必须** | 图生视频 / 运镜成片 |
| 口播音色（豆包/火山克隆声） | 强烈建议 | 没有可用系统 TTS 先出样片 |
| 生图网关（如 ZenMux） | 可选 | 新部位科技风静帧更稳；冠状缝默认素材包已自带 |

密钥只放本机环境或 `.env`，不要提交本仓库。详见 `references/deps.md`。

## 正确流程

1. 丢入逐字稿（或先写稿）  
2. 查 `assets/coronal/` 素材包；没有再锁真源（BodyParts3D / Z-Anatomy 等）  
3. 科技风渲染（结构锁死）  
4. 质检 PASS  
5. 出分镜确认文档（总表 + 左真源/右科技风）→ **等人确认**  
6. Seedance + 口播 + 花字 + 疏音效  
7. 交付本地路径  

冠状缝开场已附默认真源/科技风/对照板，见 `assets/coronal/INDEX.md`，**禁止无故重复渲染**。

## 仓库结构

- `SKILL.md`：Codex 主流程  
- `agents/openai.yaml`：界面元数据  
- `assets/coronal/`：冠状缝默认素材包  
- `references/`：依赖说明与分镜模板  

## 许可与素材

代码与 Skill 文本：MIT（见 `LICENSE`）。  
解剖真源素材遵循各自开放许可（常见 CC BY-SA，如 BodyParts3D / Z-Anatomy）；衍生科技风需保留署名与相同许可要求。

## 安全

- 不要提交 `.env`、API Key、客户私密成片或未授权声线。  
- 仅使用你有权使用的口播音色与视频通道。  
