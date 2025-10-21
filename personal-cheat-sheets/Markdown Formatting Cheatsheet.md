Advanced Markdown Cheatsheet

This is a quick reference guide for the most useful Markdown syntax for creating professional and readable documents on GitHub, based on the GitHub Flavored Markdown (GFM) Spec.

Text Formatting

Style

Syntax

Example

Output

Bold

**text**

**This is bold**

This is bold

Italic

*text*

*This is italic*

This is italic

Strikethrough

~~text~~

~~Mistake~~

~~Mistake~~

Inline Code

`code`

`git status`

git status

Headings & Horizontal Rules

# Heading 1
## Heading 2
### Heading 3

---


Lists & Task Lists

Type

Syntax

Unordered

* Item or - Item

Ordered

1. Item

Task (Complete)

- [x] Completed Task

Task (Open)

- [ ] Incomplete Task

Code Blocks

Use triple backticks and specify the language for syntax highlighting.

<pre>

SELECT
    customer_id,
    order_date
FROM orders;


</pre>

Tables

| Header 1 (Left) | Header 2 (Center) | Header 3 (Right) |
| :-------------- | :---------------: | ---------------: |
| Cell 1          |      Cell 2       |           Cell 3 |


Links & Images

Link: [Link Text](https://www.github.com)

Image: ![Alt Text](URL_to_image)

Advanced Formatting

Alerts

Use these special blockquotes to emphasize critical information.

Note: > [!NOTE]

[!NOTE]
Useful information that users should know.

Important: > [!IMPORTANT]

[!IMPORTANT]
Key information users need to know to achieve their goal.

Warning: > [!WARNING]

[!WARNING]
Urgent info that needs immediate user attention to avoid problems.

Collapsible Sections

This is extremely useful for hiding long sections of text.

<details>
<summary><strong>Click to Expand Section Title</strong></summary>

This is the hidden content. You can put text, images, and even code blocks in here.

</details>


Footnotes

You can add footnotes[^1] to your content. They will be rendered at the bottom of the document.

Here is a simple footnote[^1].

[^1]: My reference.


Diagrams (Mermaid)

You can create flowcharts and other diagrams directly in Markdown.

graph TD;
    A[Start] --> B{Is it broken?};
    B -- Yes --> C[Fix it];
    B -- No --> D[Done];
    C --> D;


[!TIP]
This is a powerful tool for visualizing processes and workflows in your project documentation.

[^1]:
This is the text for the footnote.