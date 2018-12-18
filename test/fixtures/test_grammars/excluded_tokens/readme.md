This grammar shows an example of the `EXCLUDE` rule.

Tree-sitter uses context-aware lexing. In a given parse state, the lexer will only match tokens that are syntactically valid in that state. This means that you can have a keyword like `if` that has special meaning in certain places, but is treated as a normal identifier in other places.

To match the behavior of some programming languages (e.g. `C`, where the keywords are not context-aware), you may want to explicitly state that certain tokens can *not* be used in some places. This ensures that even when there are syntax errors, those tokens will still be identified specifically, as opposed to being treated as identifiers.

For example, consider this C code:

```c
float // <-- error

int main() {}
```

By default, Tree-sitter would match the `int` as an `identifier`, because an `identifier` token would be valid after the word `float`, whereas the `int` token would not. This results in a *worse* error recovery than if Tree-sitter could tell that `int` is still a keyword.

The `EXCLUDE` rule tells Tree-sitter that it should continue to distinguish certain tokens at a given position, even if those tokens aren't syntactically valid.
