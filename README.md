# Knowledge Quiz(知识点拷打)

一个 Claude Code skill,用 5 个由浅入深的高质量问题检验你对任意技术知识点的掌握程度,最后把错题自动归档成 Markdown,方便日后复习。

## 它能做什么

- 你说"拷打我 XXX",它会从 **概念定义 → 底层原理 → 典型应用 → 边界误区 → 综合分析** 五个维度各出一道题
- 每答一题,立即给出三选一的判定(对 / 半对半错 / 错)+ 一句话标准答案
- 5 题结束后,自动总结你的薄弱点,并把所有错题写入当前工作目录下的 `<知识点>.md`
- 没有引导式回复、没有评分表、没有废话,该怼就怼

适合场景:面试前突击、学习完一门新技术后自测、想知道自己到底哪里还糊弄着。

## 安装

通过 [`npx skills`](https://skills.sh/) 一行命令安装:

```bash
npx skills add <你的GitHub用户名>/<仓库名>@knowledge-quiz
```

把命令里的 `<你的GitHub用户名>/<仓库名>` 替换成实际的 GitHub 路径,例如:

```bash
npx skills add yourname/claude-skills@knowledge-quiz
```

加 `-g` 安装到全局(用户级),`-y` 跳过确认:

```bash
npx skills add yourname/claude-skills@knowledge-quiz -g -y
```

## 使用

安装后,在 Claude Code 里直接说触发词就行,以下表达任选其一:

- `问问我关于 Docker`
- `考考我 React Hooks`
- `测一下我对 MySQL 索引的掌握`
- `拷打我分布式锁`

Claude 会先告诉你考察维度,然后开始第 1 题。一问一答,节奏不乱。

### 示例片段

![alt text](demo.png)

```
> 拷打我 Docker

我会从「概念定义 → 底层原理 → 典型应用 → 边界误区 → 综合分析」
五个角度各问你一个问题。准备好就开始。

第 1 题:Docker 镜像和容器的本质区别是什么?

> 镜像是模板,容器是运行实例。

1, 对, 镜像是静态的只读文件系统快照,容器是镜像运行起来后的进程实例。

第 2 题:...

...

## 薄弱知识点:
- namespaces 和 cgroups 的分工
- volume 和 bind mount 的区别场景

错题已归档到: ./Docker.md
```

## 错题归档规则

- 归档路径:**当前工作目录** 下的 `<知识点>.md`
- 文件名:知识点中的非法字符(`/ \ : * ? " < > |`)会替换为下划线
- 只记录判定为 "错" 或 "半对半错" 的题目,答对的不写入
- 如果文件已存在,会在末尾追加,用 `---` 分隔

归档文件示例:

```markdown
# Docker 错题集

## 第 2 题

**题目**:Docker 是如何实现进程隔离的?

**用户回答**:用的是虚拟机。

**判定**:错

**标准答案**:Docker 通过 Linux 的 namespaces 实现进程隔离,
cgroups 实现资源限制,二者职责不同。

---
```

## 卸载

```bash
npx skills remove knowledge-quiz
```

或者直接删掉 `~/.claude/skills/knowledge-quiz/`(用户级)或 `.claude/skills/knowledge-quiz/`(项目级)。

## 仓库结构

```
.
├── knowledge-quiz/
│   └── SKILL.md          # skill 定义,符合 npx skills 规范
├── .gitignore
└── README.md             # 本文件
```

`SKILL.md` 包含完整的 skill 行为定义(触发条件、流程、边界)。

## License

MIT