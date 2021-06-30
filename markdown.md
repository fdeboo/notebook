[Reference: Markdown best practices][best-practices]

# Blockquotes

## Indentification

- Always separate the marker > from the actual content using a single whitespace. 👍

## Multi Line

- Use a greater than sign for every line, including wrapped lines

  Example:

        > Winter

        > Snow

  &nbsp;

        > Many snowflakes are falling down. The winter has sparkling and frozen elements! It is home
        > for many beautiful animals like snowy owls,
        > arctic foxes, and grizzly bears.

  Result:

  > Winter

  > Snow

  &nbsp;

  > Many snowflakes are falling down. The winter has sparkling and frozen elements! It is home
  > for many beautiful animals like snowy owls,
  > arctic foxes, and grizzly bears.

# Code

## Blocks

- Avoid indentation based code blocks 👎
- **use fenced code blocks for multi line code** 👍

  - prevents malformed rendered output due to wrong indentation errors
  - increases the readability
  - allows the usage of language syntax highlighting.

## Syntax Highlighting

- Explicitly declare the language for blocks containing code snippets, so that neither the syntax highlighter nor the next editor must guess.

  Example:

        ```js
        import React, { PureComponent } from "react";

        class Frost extends PureComponent {
        // ...
        }

        ```

  Result:

  ```js
  import React, { PureComponent } from "react";

  class Frost extends PureComponent {
    // ...
  }

  export default Frost;
  ```

## Escape Newlines In Terminal Commands

Many command snippets are intended to be copied and pasted directly into e.g. a terminal. To protect the user to unintentional execute the copied code due to a newline (interpreted by the terminal as Enter) use a single backslash at the end of the line.

Example:

    ```sh
    npx run docs:generate -- --template=winter --description="Sparkling and frozen" \
    --elements="snow,frost,ice" --snowflakes=20
    ```

Result:

```sh
npx run docs:generate -- --template=winter --description="Sparkling and frozen" \
--elements="snow,frost,ice" --snowflakes=20
```

# HTML

- Prefer HTML comment syntax to add hidden, non-rendered comments to the code.
  ```
  <!-- This is a comment only visible in the code and not in the rendered output -->
  ```

# Links

- Always use reference links instead of inline links except for inner anchor links (fragment identifiers).

- There are three kinds of reference links: full, collapsed, and shortcut. This can be one of the three reference link types:

  Example:

        [Winter][winter-info]

        [winter-info]: https://the-winter-is-sparkling-and-frozen.io

## Inline

- If it is necessary to use inline links instead of the preferred reference links try to use shortened URLs wherever possible to keep the line length overhead as small as possible

  Example

        [Winter](https://sho.rt/l1n-k)

## Placement

- Always place reference links at the bottom of the document. This keeps the focus of the reader on the content and increases the maintainability.

<!-- Links -->

[best-practices]: https://arcticicestudio.github.io/styleguide-markdown/rules/
