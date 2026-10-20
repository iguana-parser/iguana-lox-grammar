<h1 align="center">Lox grammar for Iguana</h1>

A grammar for Lox, the language of Robert Nystrom's
[Crafting Interpreters](https://craftinginterpreters.com/), written for
[Iguana](https://github.com/iguana-parser/iguana-rs) in
[Iggy](https://iguana-parser.org/docs/grammar-definition/). The reference is
the book's [Appendix I](https://craftinginterpreters.com/appendix-i.html). The
grammar is defined in [`lox.iggy`](lox.iggy).

It follows the appendix with two differences:

- **Expressions** use a single ambiguous `Expr` rule. Precedence and
  associativity select the intended tree instead of the appendix's chain of
  nonterminals, one per precedence level. The
  [disambiguation documentation](https://iguana-parser.org/docs/grammar-definition/disambiguation/)
  explains the notation.
- **Assignment** accepts any expression on its left side, where the appendix
  allows only a variable or a property access. The parser does not reject
  `1 = 2`.

## Development

The Rust sources under `src/` are generated from [`lox.iggy`](lox.iggy) and
should not be edited directly. After changing the grammar, regenerate the
parser and run it on a file:

```sh
iguana generate --grammar lox.iggy --output .
cargo run --release -- --start Program example.lox
```

## License

Licensed under either of [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE) at
your option.

Copyright (c) 2026 Ali Afroozeh.
