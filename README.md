## Prompt

```
任务：批量生成英语词根背诵文案，用于制作背诵清单/卡片
要求：
1.  输入：以我提供的词根列表为唯一依据，**严格逐一根词生成，不添加额外词根**
2.  输出格式：统一采用 Markdown 无序列表格式，每个词根之间使用分隔符间隔，词根的标题需要进行高亮，每个词根的内容结构固定为以下5项，不得增删：
    - 词根：[具体词根]
    - 核心含义：[该词根对应的核心中文释义]
    - 古人发明此词根的意思：[结合拉丁语/希腊语词源，说明词根最初指代的原始含义]
    - 记忆技巧：[使用谐音、具象联想、场景串联等易记方法，拒绝牵强表述]
    - 高频词（3个）：[单词1：前缀+词根+后缀（若有）→ 中文释义；单词2：前缀+词根+后缀（若有）→ 中文释义；单词3：前缀+词根+后缀（若有）→ 中文释义]
3.  内容规范：
    - 高频词限定为四六级核心词汇，3个单词互不重复，拆解逻辑清晰无歧义
    - 整体语言简洁紧凑，无冗余修饰、无废话
4.  交付要求：**仅返回生成的背诵文案内容，不添加任何额外说明、标题、注释**

【Example】
```
#### 11. **spect**

*   **核心含义**：看
*   **古人发明此词根的意思**：源自拉丁语 *specere*，意为“注视、观察”
*   **记忆技巧**：联想“inspect 检查时要仔细看”
*   **高频词**：
    *   **inspect** = in(进入)+spect(看) → 检查
    *   **respect** = re(再次)+spect(看) → 尊重
    *   **prospect** = pro(向前)+spect(看) → 前景

***
```

【root words】
```
1. act = 做 → action, active
2. ag = 做 → agent, agenda
3. oper = 工作 → operate, operation
4. fac/fact = 做 → factory, manufacture
5. fic = 做 → fiction, artificial
6. pos = 放 → position, deposit
7. pon = 放 → component, opponent
8. cap = 拿 → capture, capable
9. cept = 拿 → accept, concept
10. cip = 拿 → participate, anticipate
```
```