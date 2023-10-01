By default vim maintains a tree structure of changes history, thus we can get to every state of our changes, not just in a single branch like most of the editors.
 \
- `g-` restore current buffer to previous change (same as undo if only has one branch of changes)
- `g+` next change
 \
Here comes a lovely plugin wraps this feature in to a nice TUI: [mbbill/undotree](https://github.com/mbbill/undotree)
It's darn simple, `:UndotreeToggle` would possibly be the only command ya need :)
