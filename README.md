# 人工智能english — ai-english-skill（专四口语思辨陪练）

开源 Skill：围绕争议话题进行一轮一轮的英文口语思辨训练，自动诊断中式英语并给出口语优化句，专为专四（TEM-4）口语备考设计。

## 项目解决什么问题

专四（TEM-4）口语考试的思辨（critical thinking）环节，要求考生拿到争议话题后即兴发表观点。中国学生常见的三大痛点：

- **开口没话说**：观点缺乏立场与支撑，不知从何说起；
- **中式英语**：中文直译语序、中式搭配（如 learn knowledge / search information）、母语负迁移拉低表达质量；
- **缺少针对性反馈**：平时练习没人逐句指出问题、给出口语化的改写。

本项目提供"陪练型"Skill：AI 出题并给参考句型 → 用户口头作答 → 逐字转写 + 口语优化 + 中式英语诊断 → 追问或重答，一轮一轮把口语思辨能力练上去。

## 主要功能

- **一轮一轮训练**：每轮先给出英文思辨 Topic，再附一正一反两句参考句型（纯英文：For 肯定立场 / Against 否定立场）；
- **作答反馈三件套**：
  - ①【我的原句】原样转写用户口述英文，保留原始表达，不做任何修正；
  - ②【优化句】仅生成 1 版，优先修正中式英语（中文直译语序、中式搭配、逻辑断层、母语负迁移），拒绝浅层同义词替换，核心改动**加粗**，适配口头表达、不过度书面化；
  - ③【简短点评】点明本次中式英语问题，并说明逻辑、句式、用词地道度情况；
- **训练循环**：用户选【继续】= 基于当前话题深度追问、开启新一轮；选【重新回答】= 不换话题重新作答，循环直至【继续】；
- **内置 10 个专四难度思辨话题库**，新会话自动换新话题；
- **纯对话式**，无需任何外部工具。

## 安装方法

**方式一：Agent Skill 环境（豆包等）**

1. 将 `ai-english-skill` 目录放入环境的 skills 根目录（例如 `workspace/.user_skills`）；
2. 对话中触发（如说"开始口语练习"）即可使用。

**方式二：OpenAI Agents SDK**

1. 安装依赖：`pip install openai-agents`；
2. 加载配置：`agent = Agent.from_yaml_file("ai-english-skill/agents/openai.yaml")`；
3. 需要更换模型时，修改 `openai.yaml` 中的 `model` 字段。

## 使用方法

1. 触发后，AI 输出 Topic + For/Against 两句参考句型；
2. 用户围绕话题用英文口头作答；
3. AI 依次输出【我的原句】【优化句】【简短点评】；
4. 用户选择【继续】深入追问（同话题新一轮），或【重新回答】同话题重答；
5. 重复步骤 2-4，直到训练结束；新会话自动从话题库换新话题。

## 输入输出示例

```
用户：开始口语练习
AI：Topic: Should schools ban smartphones on campus?
    For: I believe schools should ban smartphones, because they distract students from learning.
    Against: In my view, a total ban is unnecessary, since students need phones to contact their parents.

用户（口述）：I think school should not ban smartphone, because phone is useful for student to search information.

AI：①【我的原句】I think school should not ban smartphone, because phone is useful for student to search information.
    ②【优化句】I think schools should not ban smartphones, because they are useful for students to look up information and keep in touch with their parents.
    ③【简短点评】复数缺失（school / smartphone / student），"search information" 为中式搭配（应为 look up information）。逻辑成立，句式简单，用词需加强搭配。
    【继续】【重新回答】

用户：重新回答 → 同话题重答，再次输出①②③；
用户：继续 → AI 基于当前话题深度追问（如 Some people argue that smartphones help students look up materials in class. How would you respond to that?），进入新一轮。
```

## 局限

不支持网页抓取、PDF、图形界面，纯对话式训练。

## 校验与开源

官方校验：`python quick_validate.py ai-english-skill` → `Skill is valid!`

本 Skill 以 MIT 协议开源（见根目录 LICENSE），可自由修改与分发。
