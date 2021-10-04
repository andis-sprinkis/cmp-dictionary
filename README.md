# cmp-dictionary

Dictionary completion source for [nvim-cmp](https://github.com/hrsh7th/nvim-cmp)  

Use the dictionaries set in `dictionary` as the source for cmp.
`:h 'dictionary'`

## setup

```lua
require("cmp").setup({
  -- other settings
  sources = {
    -- other sources
    {
      name = "dictionary",
      -- If you use large dictionaries, this setting is recommended.
      keyword_length = 2,
    },
  }
})
```

## Configuration

to pick any dic with `neovim/vim` you can use `set dictionary`:

```vim
set dictionary+=/usr/share/dict/words
```

In lua

```lua
vim.opt.dictionary:append("/usr/share/dict/words")
```

You can download dic from [aspell.net](https://ftp.gnu.org/gnu/aspell/dict/0index.html) or installing by package manager , xbps extract to

```bash
$ ls /usr/share/dict/
american-english  british-english  words
```

## How to create your own dictionary

The dictionary is recognized as a list delimited by `\s`. `\s` is a space, `\t`, `\n`, `\r`, `\f`.
For example, if you use the following file as a dictionary, the source to be added is `{"hello", "world", "!"}`.

```txt
hello
world !
```

## Update dictionary

On `FileType *`, check the `dictionary` and update the dictionary if it is changed.
Updating only the contents of the dictionary will not detect it.

## Use different dictionaries for each filetype

To set the dictionaries for each filetype, use setlocal in autocmd.
setlocal does not pollute the global settings since it is only valid for that buffer.

```vim
augroup MyCmpDictionary
  au!
  au FileType markdown setlocal dictionary=/path/to/dic1,/path/to/dic2
augroup END
```

If you want to enable or disable this source itself by filetype, use [cmp.setup.buffer](https://github.com/hrsh7th/nvim-cmp#sources-type-tablecmpsourceconfig).

## FAQ

#### Some candidates don't show up.

Returns only candidates where the first two letters match.
In the future, I would like to reference the value of keyword_length, but currently this value is not visible in the source.

## Global options

`g:cmp_dictionary_silent` is a setting for whether to output debug messages.
The default settings are as follows.

```lua
vim.g.cmp_dictionary_silent = true
```
