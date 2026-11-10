# text-handy

Three small Bash wrappers around `sed` for everyday line edits: add, delete, or replace
text by line number, line range, or pattern, without remembering `sed` syntax.

## Functionality

| Script | Does |
|---|---|
| `text-add` | insert a line above/below a line or pattern; add a prefix or suffix to one line, a range, or every line |
| `text-del` | delete lines (one, a range, all-except-a-range, empty lines); strip a prefix or suffix |
| `text-mod` | replace whole lines or strings inside lines; replace empty lines; replace a prefix or suffix |

Line addresses use `sed` notation: `1` (line 1), `$` (last line), `3,5` (lines 3–5),
`2,4!` (every line except 2–4).

> **The file is edited in place.** Each command first prints the result, then writes it
> back to the file (the last argument). Keep a copy if you're unsure.

Note: the prefix keyword is spelled `preffix` in the scripts.

## Install

Needs only Bash and GNU `sed`:

```bash
git clone https://github.com/nano-rex/text-handy.git
cd text-handy
chmod +x text-add text-del text-mod
sudo install -m 755 text-add text-del text-mod /usr/local/bin/   # optional: put them on PATH
```

Run any script with no arguments to see its examples.

## Examples

```bash
printf 'one\ntwo\nthree\nfour\n' > demo.txt

text-add suffix all ";" demo.txt          # add a semicolon at the end of every line
text-add preffix row 2,4 "\t" demo.txt    # add a tab at the start of lines 2 to 4
text-add above row 1 "#!/bin/bash" demo.txt   # insert a new first line
text-add below pattern "two" "2.5" demo.txt   # insert a line under each line matching "two"

text-del row '$' demo.txt                 # delete the last line
text-del row newline demo.txt             # delete empty lines

text-mod row 1 "first" demo.txt           # replace line 1
text-mod row 1,3 strings "one" "1" demo.txt   # replace "one" with "1" on lines 1-3
```

## License

GPL-3.0, see `LICENSE`.
