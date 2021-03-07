zmv: Rename Many Files In zsh With Regex
========================================

When you're using the awesome `zsh` shell, you have access to `zmv`: a super powerful way to rename files in bulk with a regex. (It might require `oh-my-zsh` - not sure, didn't check, but I use `oh-my-zsh`)


Example:

```
autoload -U zmv
zmv '2020-03-30_rococo_double_s04_(*).(*)' '2020-03-30_RococoDouble_s04_$1.$2'
```

This will do the following renames:

```
2020-03-30_rococo_double_s04_001.json -> 2020-03-30_RococoDouble_s04_001.json
2020-03-30_rococo_double_s04_002.json -> 2020-03-30_RococoDouble_s04_002.json
2020-03-30_rococo_double_s04_002.html -> 2020-03-30_RococoDouble_s04_002.html
```

It is quite safe: it checks, for example, if more than 1 source file will map to the same destination file and refuse to operate if that is the case. 

Use `-n` for a dry run to inspect the results before applying it.

