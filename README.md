# Strawberry Festival Extension

草莓音乐节站次延展物料生成 skill。它把主视觉、精确文案、尺寸需求和版式参考转化为系列化海报、Banner、购票信息图及其他线上/线下物料。

## 核心能力

- 读取本轮站次主视觉，并使用该站主视觉的主色；重庆红只属于模板样本，不是固定背景色。
- 以 `version-1-panel` 作为默认版式系统：不规则白色信息平面、黑色描边、超粗正体、隐形网格、模块错位和主视觉色留白。
- 根据文字数量和信息层级重新组织白色平面的数量、大小、位置与内部结构，不直接缩放旧图。
- 使用固定的 Strawberry Music Festival 标题 PNG，不重新生成或重写品牌标题。
- 首次只生成一张预览，用户确认后再继续批量生成。
- 生图执行方式与服务商无关：不绑定模型、接口、API key 或中转站。

## 安装

将整个 `strawberry-festival-extension` 文件夹复制到 Codex skills 目录：

```text
~/.codex/skills/strawberry-festival-extension/
```

如果环境设置了 `CODEX_HOME`，则复制到：

```text
$CODEX_HOME/skills/strawberry-festival-extension/
```

安装后可使用：

```text
$strawberry-festival-extension
```

## 使用方式

请在请求中提供：

1. 当前站次主视觉；
2. 画布尺寸或比例；
3. 必须逐字出现的完整文案；
4. 信息层级和禁止出现的内容；
5. 如有需要，提供人物、产品或其他内容素材。

默认先生成一张代表性预览。确认方向后，再继续生成其余尺寸或系列版本。

## 生图工具配置

本 skill 不包含任何个人 API key、接口地址、模型名称或中转站配置。使用者应在自己的环境中配置生图工具，例如：

- Codex 当前可用的 `imagegen` 能力；
- 自己的图像生成 API 客户端；
- 企业内部图像生成服务；
- 其他已获授权的图像生成方式。

具体适配规则见 [`references/image-generation-adapter.md`](references/image-generation-adapter.md)。凭证只应保存在使用者自己的环境变量、应用设置或密钥管理器中，不要写进 skill、提示词、README 或 Git 仓库。

## 主要资产

| 路径 | 用途 |
| --- | --- |
| `SKILL.md` | skill 入口规则 |
| `references/approved-panel-template.md` | 最终模板与第七张组合方法 |
| `references/grid-layout-system.md` | 隐形网格与尺寸重组规则 |
| `references/reference-study.md` | 参考学习边界与模板优先级 |
| `references/layout-patterns.md` | 信息类型的版式变化方法 |
| `references/image-generation-adapter.md` | provider-agnostic 生图执行说明 |
| `assets/approved-templates/version-1-panel/` | 九张已确认最终模板图 |
| `assets/title-styles/` | 固定 Strawberry Music Festival 标题 PNG |
| `assets/references/` | 基础版式参考与重庆样本参考 |
| `assets/references/artist-playlist-layouts/` | 艺人歌单专项的次级版式参考 |

## 模板优先级

`assets/approved-templates/version-1-panel/07-entry-times.png` 是多模块组合的主要样本。它体现了多个不规则白色信息平面的错位、叠置、超大数字/标题、功能图标和主视觉色留白。

白色底板、黑色描边、字体层级和模块关系属于模板；具体站次颜色、城市、日期、价格、阵容和文案必须从本轮需求读取。

## GitHub 上传前检查

- 不要把个人 API key、`.env`、调试输出或生成结果上传到仓库。
- 保留 `SKILL.md`、`agents/openai.yaml`、`references/` 和 `assets/`。
- 确认模板图片的使用权和共享范围，尤其是用户提供的品牌、人物和版式参考素材。
- 可用仓库根目录的 `git status` 检查是否混入工作区临时文件。

## 导出包

本目录本身就是可上传到 GitHub 的 skill 包。上传时保持 `SKILL.md`、`agents/`、`references/` 和 `assets/` 的相对路径不变。

