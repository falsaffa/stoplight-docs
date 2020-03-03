# Using Stoplight Flavored Markdown

Stoplight Flavored Markdown (or SMD, for short) with two guiding principles:

- It must be **human readable**, where the raw Markdown source can be viewed and edited using standard, readily available text editors.
- It must **degrade gracefully**, where rendering Stoplight Flavored Markdown outside of Stoplight should still be usable, clean, and, most importantly, readable.

## Our Approach
Stoplight Flavored Markdown extends CommonMark with inline comment annotations, where the value of the annotations is a YAML object. These annotations tell Stoplight to render the following Markdown object in a specific way.

By leveraging comments to store the annotations, Stoplight Flavored Markdown degrades gracefully when rendered in other CommonMark-compatible Markdown renderers (Github, for example).

## Block Types
### Callouts
A callout is a Markdown block quote with an optional annotation that indicates the theme of the callout and intention of the message. The block annotation for a callout can include:

- **theme** (string), which must be one of the following values:
  - `info`
  - `success`
  - `warning`
  - `danger`

### Info

To create an info block quote, use:

```markdown
<!-- theme: info -->

> ### A thing to know
>
> Here is my info callout
```

<!-- theme: info -->

> ### A thing to know
>
> Here is my info callout

### Success
To create an success block quote, use:

```markdown
<!-- theme: success -->

> ### Mission Accomplished!
>
> Here is my success callout!
```

<!-- theme: success -->

> ### Mission Accomplished!
>
> Here is my success callout!
 

### Warning
To create an warning block quote, use:

```markdown
<!-- theme: warning -->

> ### Watch Out!
>
> Here is my warning callout!
```

<!-- theme: warning -->

> ### Watch Out!
>
> Here is my warning callout!
 

### Danger
To create an danger block quote, use:

```markdown
<!-- theme: danger -->

> ### Danger Will Robinson!
>
> Here is my danger callout!
```

<!-- theme: danger -->

> ### Danger Will Robinson!
>
> Here is my danger callout!
 

## Code Blocks
A SMD code block is a Markdown code fence with an optional YAML annotation used to tweak the presentation of the code block. The annotation can include the following attributes:

- **title** (string), which is a string title for the resulting block
- **lineNumbers** (true|false), which denotes whether line numbers should be included (defaults to true)

```markdown
<!--
title: "My code snippet"
lineNumbers: true
-->

```javascript
function fibonacci(num){
 var a = 1, b = 0, temp;

while (num >= 0){
 temp = a;
 a = a + b;
 b = temp;
 num--;
 }

return b;
}
\```

```

<!--theme: warning-->
> In the example above, be sure to remove the `\` that precedes the last three backticks at the end of the code snippet code fence. This was included for demonstration purposes only.


<!--
title: "My code snippet"
lineNumbers: true
-->

```javascript
function fibonacci(num){
  var a = 1, b = 0, temp;

  while (num >= 0){
    temp = a;
    a = a + b;
    b = temp;
    num--;
  }

  return b;
}
```


## Tables
Tables can include an optional annotation to specify a title:

- **title** (string), the title of the table block
<!-- title: My Table Title -->

```markdown
<!-- title: My Table Title -->

| Tables        | Are           | Cool   |
| ------------- | :-----------: | -----: |
| col 3 is      | right-aligned | \$1600 |
| col 2 is      | centered      | \$12   |
| zebra stripes | are neat      | \$1    |
```

<!-- title: My Table Title -->
| Tables | Are | Cool |
| ------------- | :-----------: | -----: |
| col 3 is | right-aligned | \$1600 |
| col 2 is | centered | \$12 |
| zebra stripes | are neat | \$1 |


## JSON Schema
A JSON Schema block is a code fence with either a json, yaml, or yml language tag, plus an additional json_schema language tag. The contents of the code fence should be the JSON Schema object to be rendered.

```markdown

```json json_schema
{
 "title": "User",
 "type": "object",
 "properties": {
   "id": {
     "type": "string"
   },
   "name": {
     "type": "string",
     "description": "The user's full name."
   },
   "age": {
     "type": "number",
     "minimum": 0,
     "maximum": 150
   }
 },
 "required": [
   "id",
   "name"
 ]
}
\```
```

<!--theme: warning-->
> In the example above, be sure to remove the `\` that precedes the last three backticks at the end of the code snippet code fence. This was included for demonstration purposes only.


```json json_schema
{
 "title": "User",
 "type": "object",
 "properties": {
   "id": {
     "type": "string"
   },
   "name": {
     "type": "string",
     "description": "The user's full name."
   },
   "age": {
     "type": "number",
     "minimum": 0,
     "maximum": 150
   }
 },
 "required": [
   "id",
   "name"
 ]
}
```
 
## Tabs
A tab block allows you to create multiple pages of content nested within tabs. This block type requires two annotations, a leading annotation to denote the start of a tab block, which includes the following attributes:

- `type` (`string`), which must equal "tab"
- `title` (`string`), which is the title of the tab

And a trailing annotation to denote the end of the tab block:

- `type` (`string`), which must equal "tab-end"

For example, using the raw Markdown:

```markdown
<!--
type: tab
title: Some Content
-->

# Content!

Sweet, beautiful content, ready to blow your readers' minds.

<!--
type: tab
title: Some More Content
-->

# More Content!

With more mind-blowing material. Really. Just amazing, grade-A stuff.

<!-- type: tab-end -->
```

Results in the following:


<!--
type: tab
title: Some Content
-->

# Content!

Sweet, beautiful content, ready to blow your readers' minds.

<!--
type: tab
title: Some More Content
-->

# More Content!

With more mind-blowing material. Really. Just amazing, grade-A stuff.

<!-- type: tab-end -->

<!--theme: warning-->
> Tab container start and end annotations are required, and cannot currently be nested.


## HTTP Request Maker
The HTTP Request Maker block allows you to embed example HTTP requests directly in your documentation. The HTTP Request Maker block is a `json` or `yaml` code block, along with an additional `http` language tag.

The contents of the code fence should be a HTTP Request Object (described below). The Stoplight Studio Markdown "Preview" panel includes a sample HTTP Request Maker that you can use to help compose the Request Object automatically.

```markdown
```yaml http
{
 "method": "get",
 "url": "http://todos.stoplight.io/todos"
}
\```
```

<!--theme: warning-->
> In the example above, be sure to remove the `\` that precedes the last three backticks at the end of the code snippet code fence. This was included for demonstration purposes only.

Results in:

```yaml http
{
 "method": "get",
 "url": "http://todos.stoplight.io/todos"
}
```
 

 
