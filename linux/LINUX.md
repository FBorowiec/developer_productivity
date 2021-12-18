---
title: Developer Productivity slides - Linux
author: F.Borowiec
date: 2021-12-16
extensions:
    - qrcode
    - image_ueberzug
styles:
    style: paraiso-dark
    table:
        column_spacing: 3
        header_divider: "-"
---
# Use case

_Find all files in the repository with the word `simple-` and rename them to `simple\_`._
---
# Find

Find all files in the repository matching the `*simple*` string:
`find ./**/*simple*`

_Output:_

```bash
./linux/examples/some/deeply/nested/simple-folder1
./linux/examples/some/deeply/nested/simple-folder2
./linux/examples/some/deeply/nested/simple-folder3
```

# Find & replace `simple-` with `simple_`

We will need the `mv` command.

## Sed

`find ./**/*simple-* | sed 's/simple-/simple_/'`

_Tip:_ use `\c` (case insensitive) or `\c` for case sensitive.

_Output:_

```bash
./linux/examples/some/deeply/nested/simple_folder1
./linux/examples/some/deeply/nested/simple_folder2
./linux/examples/some/deeply/nested/simple_folder3
```

The `mv` command though needs the source AND destination!

## Sed with group matching

`\(.*\)` - match EVERYTHING inside sed and match them into a group accessible with `\1..n`

`find ./**/*simple-* | sed 's/\(.*\)simple-\(.*\)/\1simple-\2 \1simple_\2/'`

_Output:_

```bash
./linux/examples/some/deeply/nested/simple-folder1 ./linux/examples/some/deeply/nested/simple_folder1
./linux/examples/some/deeply/nested/simple-folder2 ./linux/examples/some/deeply/nested/simple_folder2
./linux/examples/some/deeply/nested/simple-folder3 ./linux/examples/some/deeply/nested/simple_folder3
```
---
## Xargs

Now let's pass that result to `mv` using `xargs`:

`find ./**/*simple-* | sed 's/\(.*\)simple-\(.*\)/\1simple-\2 \1simple_\2/' | xargs -n 2 mv`

# Copying all files matching a certain pattern

## Find necessary files

`find ./**/random_file*`

_Output:_

```bash
./linux/examples/files/random_file2
./linux/examples/files/scattered/all/over/random_file4
./linux/examples/files/scattered/all/over/random_file5
./linux/examples/files/scattered/all/over/the/place/random_file1
./linux/examples/files/scattered/all/over/the/random_file3
./linux/examples/files/scattered/random_file6
```
---
## Use `printf`

`find ./**/random_file* -printf "%p"`

_Output:_

```bash
./linux/examples/files/random_file2./linux/examples/files/scattered/all/over/random_file4./linux/examples/file
s/scattered/all/over/random_file5./linux/examples/files/scattered/all/over/the/place/random_file1./linux/examp
les/files/scattered/all/over/the/random_file3./linux/examples/files/scattered/random_file6%
```

Notice no new lines!

Let's add them with `\n` and let's add the whole path AND the path name with `%f`:

`find ./**/random_file* -printf "%p %f\n"`

_Output:_

```bash
./linux/examples/files/random_file2 random_file2
./linux/examples/files/scattered/all/over/random_file4 random_file4
./linux/examples/files/scattered/all/over/random_file5 random_file5
./linux/examples/files/scattered/all/over/the/place/random_file1 random_file1
./linux/examples/files/scattered/all/over/the/random_file3 random_file3
./linux/examples/files/scattered/random_file6 random_file6
```

Notice we have the whole path on the left and just the name on the right. This allows to put all files in another
directory changing what comes before `%f`.

`find ./**/random_file* -printf "%p ./linux/examples/empty_folder/%f\n" | xargs -n 2 cp`
---
Then:

`ls linux/examples/empty_folder | grep random`

_Output:_

```bash
random_file1
random_file2
random_file3
random_file4
random_file5
random_file6
```
---
# The magic build command for catching errors

`bazel build //path/to:target 2>&1 | grep -ie error\: -C0`
---
# `cht.sh`

`curl cht.sh/python/lambda`
---
