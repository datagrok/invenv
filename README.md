# invenv

**invenv** ("in this virtual environment, ...") runs a command or launches a subshell in an "activated" Python "virtual environment."

It depends on and is not a replacement for `virtualenv` or the `venv` module.

It is a replacement for, and does not use, the `bin/activate` mechanism created by `virtualenv`/`venv`.

For a discussion of the motivation behind this tool, see [Prefer Subshells for Context](https://datagrok.org/python/activate/).
(Previously titled "Virtualenv's `bin/activate` is Doing It Wrong.")

```
usage: invenv [OPTIONS] [COMMAND [ARGS]]

For use with Ian Bicking's virtualenv tool. Executes COMMAND with ARGS with
the specified or current virtual environment activated.

options:
   -C DIRECTORY    use a virtual environment located at DIRECTORY
   -n NAME         use a virtual environment named NAME in $WORKON_HOME
```

If no virtual environment is specified, the current directory is used.

If [`findup`][] is installed, all ancestor directories will be checked for the existence of a virtual environment.
This way, invenv will work from any subdirectory within the virtual environment.

If no `COMMAND` is given, a subshell is launched instead. "Deactivate the environment" by exiting the subshell.

Using invenv in an already-active virtual environment is idempotent (the redundant invocation will have no ill effects.)

Using invenv in a virtual environment while a different one is active will show a warning or fail, to avoid ambiguity or environment cross-contamination.

In the past I have called this tool "inve" or just "activate."

## Dependencies

- a POSIX shell, like `bash` or `dash`.
- coreutils `readlink`
- the [venv module](https://docs.python.org/3/library/venv.html) included with Python >=3.3, or [virtualenv](https://virtualenv.pypa.io/), creates the virtual environments that this tool works with.
- (optional) my utility [`findup`][]

## License: AGPL-3.0+

All of the code herein is copyright 2019 [Michael F. Lamb](http://datagrok.org) and released under the terms of the [GNU Affero General Public License, version 3][AGPL-3.0+] (or, at your option, any later version.)

[AGPL-3.0+]: http://www.gnu.org/licenses/agpl.html
[`findup`]: https://github.com/datagrok/findup-sh
