# pretty-apt-log

`pretty-apt-log` is a bash script that allows you to view logs of the `apt` package manager in an easy-to-read format.

A video tutorial:

[![Mindful Technology - View APT logs conveniently with pretty-apt-log](https://img.youtube.com/vi/RWkfLKRoWWE/0.jpg)](https://www.youtube.com/watch?v=RWkfLKRoWWE)

## Dependencies

[`bat`](https://github.com/sharkdp/bat) is required to enable colorization of the output.

Install it with

```bash
sudo apt install bat
```

## Installation

1. Clone this repository to a directory of your choice (e.g. `~/repos`):

    ```bash
    cd ~/repos
    git clone https://github.com/linguisticmind/pretty-apt-log.git
    ```

2. Symlink or copy the [script file](pretty-apt-log) to a directory on your `PATH` (e.g. `~/bin`):

    ```bash
    cd ~/bin
    # To symlink:
    ln -sv ../repos/pretty-apt-log/pretty-apt-log
    # To copy:
    cp -av ../repos/pretty-apt-log/pretty-apt-log .
    ```

3. (OPTIONAL) Symlink or copy the [man page](man/man1/pretty-apt-log.1) to a directory on your `MANPATH` (e.g. `~/man`):

    ```bash
    cd ~/man/man1 # The `man` directory should contain subdirectories for different manual sections: `man1`, `man2` etc.
    # To symlink:
    ln -sv ../../repos/pretty-apt-log/man/man1/pretty-apt-log.1
    # To copy:
    cp -av ../../repos/pretty-apt-log/man/man1/pretty-apt-log.1 .
    ```

    A copy of the manual page is also [included in this README file](#manual).

4. (OPTIONAL) Copy the [example config file](config.bash) to the config directory:

    ```bash
    mkdir -v ~/.config/pretty-apt-log
    cp -v ~/repos/pretty-apt-log/config.bash ~/.config/pretty-apt-log
    ```

## Manual

```plain
PRETTY-APT-LOG(1)           General Commands Manual          PRETTY-APT-LOG(1)

NAME
       pretty-apt-log - view apt logs in an easy-to-read format

SYNOPSIS
        pretty-apt-log [<options>] [<log> ...]

DESCRIPTION
       pretty-apt-log  allows  the  user to quickly view apt package manager's
       logs in an easy-to-read format. Each entry includes a  date/time  range
       showing  the  start  and  end time of the installation, and the command
       that was run.

       pretty-apt-log requires `bat` to be installed to colorize the output.

       If no <log> file is passed as an argument, all the  available  logs  in
       `/var/log/apt`  are concatenated together, and displayed in the output.
       This  includes  the  `history.log`  file,  and   the   numbered   `his‐
       tory.log.<number>.gz` archive files.

       Otherwise,  both  `.gz` files and plain text log files can be passed as
       arguments to pretty-apt-log. In that case, only  the  information  from
       those files, concatenated together, is displayed.

OPTIONS
       -i, --os-installer
              Show entries of installs that were done by the OS installer.

       -I, --no-os-installer
              Do  not  show  entries  of installs that were done by the OS in‐
              staller. This is the default.

       -u, --user
              Show username of the user who requested the install.

       -U, --no-user
              Do not show username of the user who requested the install. This
              is the default.

       -n, --user-uid
              Show UID of the user next to the username.

       -N, --user-no-uid
              Do  not  show  UID of the user next to the username. This is the
              default.

       -d, --details
              Show a detailed report about the packages  that  were  installed
              during each session.

       -D, --no-details
              Do  not  show a detailed report about the packages that were in‐
              stalled during each session. This is the default.

       -a, --details-current-architecture
              Always show a full name of the package in the  detailed  report,
              including  the architecture - even if the package's architecture
              matches the current machine architecture. Current machine archi‐
              tecture can be found out by running `dpkg --print-architecture`.

       -A, --details-no-current-architecture
              Do not show the architecture in the name of a package in the de‐
              tailed report if the architecture matches  the  current  machine
              architecture. This is the default.

       -f, --date-format=<value>
              Date  format  string  that changes how date/time is displayed in
              the output. This is the same as the FORMAT string of the  `date`
              command. See date(1) for more details.

              The default value is `%Y/%m/%d %H:%M:%S`.

       -z, --date-timezone=<value>
              Change  the timezone in which date/time is displayed in the out‐
              put.

              The default value is current  system  timezone  (the  output  of
              `date +%Z`).

       -b, --bat-theme=<value>
              Change  the  bat theme that is used to colorized the output. The
              default value is `OneHalfDark`.

              If this value is set to an empty string, bat's currently config‐
              ured theme will be used.

              See  `bat  --list-themes`  for  a list of available themes. Note
              that on Debian, bat's  binary  is  called  `batcat`  instead  of
              `bat`.

       -p, --pager[=<value>]
              Use a pager to display the output.

              <value>  can  be always, auto, or never. No specified <value> is
              equivalent to always. never is equivalent to  --no-pager,  which
              is also the default.

       -P, --no-pager
              Do not use a pager to display the output. This is the default.

       -e, --pager-scroll-to-end
              Scroll to the end of the output when opening a pager.

       -E, --no-pager-scroll-to-end
              Do  not  scroll  to  the end of the output when opening a pager.
              This is the default.

       -c, --color
              Colorize the output. This is the default if bat is installed.

       -C, --no-color
              Disable colorization of the output. If  bat  is  not  installed,
              this is the default.

       -h, --help
              Print help.

       -V, --version
              Print version information.

FILES
       A configuration file can be used to set default options.

       The   configuration  file's  location  is  $XDG_CONFIG_HOME/pretty-apt-
       log/config.bash. If XDG_CONFIG_HOME is not set, it defaults to  ~/.con‐
       fig.

AUTHOR
       Alex Rogers <https://github.com/linguisticmind>

HOMEPAGE
       <https://github.com/linguisticmind/pretty-apt-log>

COPYRIGHT
       Copyright  ©  2023  Alex  Rogers.  License GPLv3+: GNU GPL version 3 or
       later <https://gnu.org/licenses/gpl.html>.

       This is free software: you are free  to  change  and  redistribute  it.
       There is NO WARRANTY, to the extent permitted by law.

PRETTY-APT-LOG 0.1.0                 2023                    PRETTY-APT-LOG(1)
```

## License

[GNU General Public License v3.0](LICENSE)
