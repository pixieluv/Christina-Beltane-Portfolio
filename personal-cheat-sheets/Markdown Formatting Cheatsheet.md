Markdown Formatting Cheatsheet

This is a quick reference guide for the most useful Markdown syntax for creating professional and readable documents on GitHub.

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

Headings

# Heading 1 (Largest)
## Heading 2
### Heading 3
#### Heading 4


Lists

Unordered List

* Item 1
* Item 2
  * Nested Item 2a
  * Nested Item 2b


Ordered List

1. First Item
2. Second Item
3. Third Item


Task List

- [x] Completed Task
- [ ] Incomplete Task


Code Blocks

To create a fenced code block, use triple backticks. You can add a language identifier for syntax highlighting.

<pre>

SELECT
    customer_id,
    order_date,
    total_amount
FROM
    orders
WHERE
    order_status = &#39;SHIPPED&#39;;


</pre>

Tables

| Header 1      | Header 2 (Center) | Header 3 (Right) |
| :------------ | :---------------: | ---------------: |
| Cell 1        |      Cell 2       |           Cell 3 |
| Another Row   |   Another Cell    |     Another Cell |


Links & Images

Link: [Link Text](https://www.github.com) -> Link Text

Image: ![Alt Text](URL_to_image)

Quotes & Horizontal Rules

Blockquote:

> This is a blockquote. It is useful for highlighting a passage of text.


Horizontal Rule:

---


Advanced Formatting

Collapsible Sections

This is extremely useful for hiding long sections of text.

<details>
<summary>Click to Expand</summary>

This is the hidden content. You can put text, images, and even code blocks in here.

</details>


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