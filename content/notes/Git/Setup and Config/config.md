---
title: "Git"
weight: 2
# bookFlatSection: false
# bookToc: true
# bookHidden: false
bookCollapseSection: true
# bookComments: false
# bookSearchExclude: false
---

# `git-config` - Get and set repository or global options

## Synopsis

```
git config [<file-option>] [--type=<type>] [--fixed-value] [--show-origin] [--show-scope] [-z|--null] <name> [<value> [<value-pattern>]]
git config [<file-option>] [--type=<type>] --add <name> <value>
git config [<file-option>] [--type=<type>] [--fixed-value] --replace-all <name> <value> [<value-pattern>]
git config [<file-option>] [--type=<type>] [--show-origin] [--show-scope] [-z|--null] [--fixed-value] --get <name> [<value-pattern>]
git config [<file-option>] [--type=<type>] [--show-origin] [--show-scope] [-z|--null] [--fixed-value] --get-all <name> [<value-pattern>]
git config [<file-option>] [--type=<type>] [--show-origin] [--show-scope] [-z|--null] [--fixed-value] [--name-only] --get-regexp <name-regex> [<value-pattern>]
git config [<file-option>] [--type=<type>] [-z|--null] --get-urlmatch <name> <URL>
git config [<file-option>] [--fixed-value] --unset <name> [<value-pattern>]
git config [<file-option>] [--fixed-value] --unset-all <name> [<value-pattern>]
git config [<file-option>] --rename-section <old-name> <new-name>
git config [<file-option>] --remove-section <name>
git config [<file-option>] [--show-origin] [--show-scope] [-z|--null] [--name-only] -l | --list
git config [<file-option>] --get-color <name> [<default>]
git config [<file-option>] --get-colorbool <name> [<stdout-is-tty>]
git config [<file-option>] -e | --edit
```

## Description

You can query/set/replace/unset options with this command. The name is actually the section and the key separated by a dot, and the value will be escaped.

Multiple lines can be added to an option by using the `--add` option. If you want to update or unset an option which can occur on multiple lines, a `value-pattern` (which is an extended regular expression, unless the `--fixed-value` option is given) needs to be given. Only the existing values that match the pattern are updated or unset. If you want to handle the lines that do not match the pattern, just prepend a single exclamation mark in front, but note that this only works when the `--fixed-value` option is not in use.

The `--type=<type>` option instructs git config to ensure that incoming and outgoing values are canonicalize-able under the given <type>. If no `--type=<type>` is given, no canonicalization will be performed. Callers may unset an existing `--type` specifier with `--no-type`.

When reading, the values are read from the system, global and repository local configuration files by default, and options `--system`, `--global`, `--local`, `--worktree` and `--file <filename>` can be used to tell the command to read from only that location.

When writing, the new value is written to the repository local configuration file by default, and options `--system`, `--global`, `--worktree`, `--file <filename>` can be used to tell the command to write to that location (you can say `--local` but that is the default).

This command will fail with non-zero status upon error. Some exit codes are:

- The section or key is invalid (ret=1),
- no section or name was provided (ret=2),
- the config file is invalid (ret=3),
- the config file cannot be written (ret=4),
- you try to unset an option which does not exist (ret=5),
- you try to unset/set an option for which multiple lines match (ret=5), or
- you try to use an invalid regexp (ret=6).

On success, the command returns the exit code 0.

A list of all available configuration variables can be obtained using the `git help --config` command.