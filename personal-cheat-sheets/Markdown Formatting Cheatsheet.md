Markdown

# Advanced Markdown Cheatsheet

This is a quick reference guide for the most useful Markdown syntax for creating professional and readable documents on GitHub. It is designed to be scannable, consistent, and easy to follow.

---

### **Text Formatting**

Use these basic styles to add emphasis to your text.

| Style         | Syntax        |
| :------------ | :------------ |
| Bold          | `**text**`    |
| Italic        | `*text*`      |
| Strikethrough | `~~text~~`    |
| Inline Code   | `` `code` ``  |

---

### **Headings**

Use hashtags to create headings. The number of hashtags determines the size.

```markdown
# Heading 1
## Heading 2
### Heading 3
Lists & Task Lists
Markdown

* An unordered item
- Another unordered item

1. A numbered item
2. Another numbered item

- [x] A completed task
- [ ] An incomplete task
Code Blocks
Use triple backticks and specify the language for syntax highlighting.

Markdown

```sql
SELECT
    customer_id,
    order_date
FROM orders;

---

### **Tables**
```markdown
| Header 1 (Left) | Header 2 (Center) | Header 3 (Right) |
| :-------------- | :---------------: | ---------------: |
| Cell 1          |      Cell 2       |           Cell 3 |
Links & Images
Markdown

* Link: [Link Text](https://www.github.com)
* Image: ![Alt Text](URL_to_image)
Advanced Formatting
Alerts
Use these special blockquotes to emphasize critical information.

Markdown

> [!NOTE]
> Useful information that users should know.

> [!IMPORTANT]
> Key information users need to know to achieve their goal.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.
Collapsible Sections
This is extremely useful for hiding long sections of text.

HTML

<details>
<summary><strong>Click to Expand Section Title</strong></summary>

This is the hidden content. You can put text, images, and even code blocks in here.

</details>
Footnotes
You can add footnotes[^1] to your content. They will be rendered at the bottom of the document.

Markdown

Here is a simple footnote[^1].

[^1]: My reference.
Diagrams (Mermaid)
You can create flowcharts and other diagrams directly in Markdown.

Markdown

```mermaid
graph TD;
    A[Start] --> B{Is it broken?};
    B -- Yes --> C[Fix it];
    B -- No --> D[Done];
    C --> D;

> [!TIP]
> This is a powerful tool for visualizing processes and workflows in your project documentation.
[^1]: This is the text for the footnote.
