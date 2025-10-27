Hugo provides multiple methods for adding syntax highlighting to code examples within your content. Here's a breakdown of how to use it with Markdown and an explanation of the components involved:

### Using Markdown Fenced Code Blocks

To add syntax highlighting in Markdown, you can use fenced code blocks with a specific format. Here's an example:

#### Markdown File Example

```markdown
content/example.md
```

```markdown
~~~go {linenos=inline hl_lines=[3,"6-8"] style=emacs}
package main
import "fmt"
func main() {
    for i := 0; i < 3; i++ {
        fmt.Println("Value of i:", i)
    }
}
~~~
```

#### Hugo Rendered Output

```markdown
1 package main
2 import "fmt"
3 func main() {
4    for i := 0; i < 3; i++ {
5        fmt.Println("Value of i:", i)
6    }
7 }
```

### Components of the Fenced Code Block

- **LANG**: The language of the code to highlight, such as `go` for Golang. The language identifier is case-insensitive, and you can find supported languages in Hugo's documentation.
- **OPTIONS**: These are key-value pairs that specify additional options for the highlighted code block, such as line numbers or emphasized lines. Options are written within braces.

### Breakdown of Options

- **linenos**: Controls line number display. Can be `true`, `false`, `inline`, or `table`.
- **hl_lines**: A space-delimited list of lines to emphasize within the code block, e.g., `3-5 7`.
- **style**: The CSS style applied to the code. Defaults to `monokai`, and you can choose other styles from Hugo's available themes.
- **noClasses**: Whether to use inline CSS styles instead of an external CSS file (`true` by default).
- **lineNos**: Displays line numbers either `inline`, `table`, or not at all.
- **lineNoStart**: Sets the starting line number, irrelevant if `lineNos` is `false`.
- **hl_inline**: If set to `true`, renders highlighted code without a wrapping container.

### Explanation of Key Options

- **anchorLineNos**: Renders each line number as an HTML anchor element. Only relevant if `lineNos` is `true`.
- **lineAnchors**: Adds a prefix to the `id` attribute of line numbers when they are anchors, providing unique `id`s.
- **wrapClass**: Class for the wrapping element of the highlighted code.
  
### Usage Tips

- Set default values for options in your site's configuration.
- Use the `highlight` shortcode if you prefer more control in your templates.

For more details and use cases, refer to [Hugo's syntax highlighting documentation](https://gohugo.io/content-management/syntax-highlighting/).
