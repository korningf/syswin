
# Syswin 

  *Multiple POSIX systems on windows*

SysWin is a platform standard and a suite to empower multiple simultaneous POSIX runtime environments on Windows.


# Design

Cygwin is a single runtime envirtonment and library called cygwin1.dll that full provides POSIX compatibility layer.
it supports a full POSIX kernel and GNU-POSIX API, msystem calls, dynamic libraries, and compilation tool chains etc.

Crucially cygwin support ELF librtaries, meaning x86 and x64 binary code compiled for linux will work on cygwin.
Use cygwin if you need to integrate with POSIX/UNIX/LINUX libraries or cross-compile or compile such custom code.

MinGW, Mingw32 and Mingw64 Minimal Gnu for Windows, are Gnu POSIX libraries statically compiled for native Windows.

MSys, SysGit, Gitbash are all derived from a fork of cygwin via its own portable runtime library called msys-2.0.dll.
Crucially, as the MSys developers based it off Cygwin, they added a clever mechanism to switch runtime environment.

Thus all MSys derived systems use a `MSYSTEM` environment variable to dynamically switch between MSys and MingW.
Once can set `MSYSTEM` to switch between MSYS, MSYS2, SysGit, GitBash, MINGW32, MINGW64, UCRT64, and CLANG64.

There is no Cygwin equivalent to the MSYSTEM environmen in Cygwin as it is a single environment platform only. 
Anything compiled natively inside Cygwin links against the cygwin1.dll and requires the Cygwin runtime to work.

Syswin's main strategy is is to map drive letters and make use of Symbolic Links fully-portable and reversible.
We combine Windows NTFS Junctions or Windows Native symbolic Links and set the `CYGWIN` and MINGW`

That is, we want make a Cygwin `/usr/bin/` path map to Windows `c:/usr/bin`, but we want the same for Gitbash.
The solution is to make Gitbash live in its own relative drive mapping, thus mapping `/usr/bin` to `g:/usr/bin`.


Install cygwin as Administrator and use it for a full multi-user setp, to compile and run daemons (ex: OpenSSH).

Use GItbash for a light user-space setup, it can also run a daemon as your local user on non-privileged ports.

You can also switch to Msys or MingW64 for specialised environments.



* [Cygwin Guide](https://www.cygwin.com/faq.html)
* [Cygwin and MingW](https://gcc.gnu.org/onlinedocs/gcc/Cygwin-and-MinGW-Options.html)

* [MSys Guide](https://www.msys2.org/)
* [MSys Runtimes](https://www.msys2.org/docs/environments/)
* [MSys Internals](https://www.msys2.org/wiki/MSYS2-introduction/)
* [MSys Notes](https://www.msys2.org/wiki/How-does-MSYS2-differ-from-Cygwin/)



# Powershell


# Chocolatey



# Syswin

Syswin is where we mount the installers, Windows SysInternals, and some custom utilities (`su.exe`).




# Cygwin (Full GNU-POSIX)


.

The cygwin root lives in the `C: drive in `c:\cygwin`

```bash
  CYGWIN=c:/cygwin winsymlinks:nativestrict
```


```
  /              ->      c:/cygwin/

  /bin/          ->      c:/cygwin/bin/
  /sbin/         ->      c:/cygwin/sbin/
  /dev/          ->      c:/cygwin/dev/

  /etc/          ->      c:/cygwin/etc/
  /lib/          ->      c:/cygwin/lib/  
  /src/          ->      c:/cygwin/src/
  /usr/          ->      c:/cygwin/usr/

  /tmp/          ->      c:/cygwin/tmp/
  /var/          ->      c:/cygwin/var/

  /home/         ->      c:/cygwin/home/
  /users/        ->      c:/users/
  ~              ->      c:/cygwin/home/${USERNAME}

  /c/            ->      c:/cygdrive/c/
  /d/            ->      c:/cygdrive/d/
  /g/            ->      c:/cygdrive/g/
  /mnt/          ->      c:/cygwin/mnt/

  /syswin/       ->      c:/syswin/
  /cygwin/       ->      c:/cygwin/
  /gitwin/       ->      g:/gitwin/
  /mingw64/      ->      g:/mingw64/

  /windows/      ->      c:/windows/
  /progdata/      ->     "c:/ProgramData"
  /programs/      ->     "c:/Program Files"
  /prog_x64/      ->     "c:/Program Files"
  /prog_x86/      ->     "c:/Program Files (x86)"

  /system/        ->     "c:/Windows/System"
  /sys_32/        ->     "c:/Windows/System2"
  /sys_64/        ->     "c:/Windows/System2"

```


# Gitwin  (GitBash MSYS2)

MSys and Gitbash and mount simple drive letters, `/c/` instead of `/cygdrive/c`.

Msys and Gitbash user homes default to the Windows Profile Homes in `c:\Users`.

Msys `/bin` maps to `/usr/bin`, we manually maintain an identical `/sbin` link.

`

The Gitwin root lives in the `G:` drive in `g:\gitwin`

```bash
  MSYS=g:/gitwin winsymlinks:nativestrict
```

```
  /              ->      g:/gitwin/

  /bin/          ->      g:/gitwin/bin/
  /sbin/         ->      g:/gitwin/sbin/           
  /dev/          ->      g:/gitwin/dev/

  /etc/          ->      g:/gitwin/etc/
  /lib/          ->      g:/gitwin/lib/
  /usr/          ->      g:/gitwin/usr/

  /tmp/          ->      g:/gitwin/tmp/
  /var/          ->      g:/gitwin/var/

  /home/         ->      g:/gitwin/home/
  /users/        ->      c:/users
  ~              ->      c:/users/${USERNAME}

  /c/            ->      c:/
  /d/            ->      d:/
  /g/            ->      g:/
  /mnt/          ->      g:/gitwin/mnt/

  /syswin/       ->      c:/syswin/
  /cygwin/       ->      c:/cygwin/
  /gitwin/       ->      g:/gitwin/
  /mingw64/      ->      g:/mingw64/

  /windows/      ->      c:/windows/
  /progdata/      ->     "c:/ProgramData"
  /programs/      ->     "c:/Program Files"
  /prog_x64/      ->     "c:/Program Files"
  /prog_x86/      ->     "c:/Program Files (x86)"

  /system/        ->     "c:/Windows/System"
  /sys_32/        ->     "c:/Windows/System2"
  /sys_64/        ->     "c:/Windows/System2"

```

