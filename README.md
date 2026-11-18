# OCaml syntax for TerminalCode

Syntax highlighting for [OCaml](https://ocaml.org) (`.ml`) as a [TerminalCode](https://github.com/Tim-kieboom/TerminalCode) plugin. (Interface files, `.mli`, have another grammar in the same repository and are not covered.)

It is a language and nothing else: there is no code in it and no pane. The plugin is

- `ocaml.wasm`, the tree-sitter grammar built for WebAssembly (about 5 MB: the grammar is big, and the editor compiles it when an OCaml file is opened),
- `manifest.toml`, which says which files are OCaml (`[language]`: `extensions`, `grammar_name`) and has the highlight query as text.

TerminalCode loads the grammar in its sandbox (plugin API 1.12, TerminalCode 0.11.0 or later) and colors the
files with the query, using the colors of your theme (`syntax.keyword`, `syntax.string`, ... in the theme file).

## Use

"Plugins: Manage", install **OCaml**, and turn it on. OCaml files are colored when they are opened. OCaml has
only block comments (`(* *)`), so the plugin sets no line comment marker and `ctrl+/` says there is none.

## Where the grammar comes from

The grammar and the query are those of [tree-sitter/tree-sitter-ocaml](https://github.com/tree-sitter/tree-sitter-ocaml) at v0.26.0 (e3c9cf3)
(MIT, `LICENSE-GRAMMAR`). The module was built from that revision with the tree-sitter CLI:

```sh
git clone https://github.com/tree-sitter/tree-sitter-ocaml && cd tree-sitter-ocaml
git checkout v0.26.0
cd grammars/ocaml
tree-sitter build --wasm -o ocaml.wasm
```

A new version of the grammar needs a new `version` in `manifest.toml` and a release (the module is the file the
installer checks). The query is copied into the manifest with its patterns in the opposite order (TerminalCode takes
the first of two patterns on the same text; the grammar's file is written for the last), with some capture names
renamed to ones themes have.

## Licence

The plugin is MIT or Apache-2.0, as the other plugins; the grammar is MIT (`LICENSE-GRAMMAR`).
