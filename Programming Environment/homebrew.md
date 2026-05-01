# homebrew

- Package manager for macos

## Location of packages

- Run `brew -cellar`

## Espanso

- [Text expander](https://espanso.org)

``` shell
brew tap espanso/espanso
brew install espanso
```

## Installation caveats

Caveats shown during installation

```bash
==> **Caveats**

Bash completion has been installed to:

  /opt/homebrew/etc/bash_completion.d

==> **icu4c@78**

icu4c@78 is keg-only, which means it was not symlinked into /opt/homebrew,

because macOS provides libicucore.dylib (but nothing else).

  

If you need to have icu4c@78 first in your PATH, run:

  echo 'export PATH="/opt/homebrew/opt/icu4c@78/bin:$PATH"' >> /Users/wangchuyao/.bash_profile

  echo 'export PATH="/opt/homebrew/opt/icu4c@78/sbin:$PATH"' >> /Users/wangchuyao/.bash_profile

  

For compilers to find icu4c@78 you may need to set:

  export LDFLAGS="-L/opt/homebrew/opt/icu4c@78/lib"

  export CPPFLAGS="-I/opt/homebrew/opt/icu4c@78/include"

  

For pkgconf to find icu4c@78 you may need to set:

  export PKG_CONFIG_PATH="/opt/homebrew/opt/icu4c@78/lib/pkgconfig"

==> **libomp**

libomp is keg-only, which means it was not symlinked into /opt/homebrew,

because it can override GCC headers and result in broken builds.

  

For compilers to find libomp you may need to set:

  export LDFLAGS="-L/opt/homebrew/opt/libomp/lib"

  export CPPFLAGS="-I/opt/homebrew/opt/libomp/include"

==> **llvm**

CLANG_CONFIG_FILE_SYSTEM_DIR: /opt/homebrew/etc/clang

CLANG_CONFIG_FILE_USER_DIR:   ~/.config/clang

  

LLD is now provided in a separate formula:

  brew install lld

  

Using `clang`, `clang++`, etc., requires a CLT installation at `/Library/Developer/CommandLineTools`.

If you don't want to install the CLT, you can write appropriate configuration files pointing to your

SDK at ~/.config/clang.

  

To use the bundled libunwind please use the following LDFLAGS:

  LDFLAGS="-L/opt/homebrew/opt/llvm/lib/unwind -lunwind"

  

To use the bundled libc++ please use the following LDFLAGS:

  LDFLAGS="-L/opt/homebrew/opt/llvm/lib/c++ -L/opt/homebrew/opt/llvm/lib/unwind -lunwind"

Features newer than system libc++ will require the following define to enable

(support for this may be removed in a future major LLVM release):

  CPPFLAGS="-D_LIBCPP_DISABLE_AVAILABILITY"

  

NOTE: You probably want to use the libunwind and libc++ provided by macOS unless you know what you're doing.

  

llvm is keg-only, which means it was not symlinked into /opt/homebrew,

because macOS already provides this software and installing another version in

parallel can cause all kinds of trouble.

  

If you need to have llvm first in your PATH, run:

  echo 'export PATH="/opt/homebrew/opt/llvm/bin:$PATH"' >> /Users/wangchuyao/.bash_profile

  

For compilers to find llvm you may need to set:

  export LDFLAGS="-L/opt/homebrew/opt/llvm/lib"

  export CPPFLAGS="-I/opt/homebrew/opt/llvm/include"

==> **rclone**

Homebrew's installation does not include the `mount` subcommand on macOS which depends on FUSE, use `nfsmount` instead.

==> **pnpm**

pnpm requires a Node installation to function. You can install one with:

  brew install node

==> **fzf**

To set up shell integration, see:

  https://github.com/junegunn/fzf#setting-up-shell-integration

To use fzf in Vim, add the following line to your .vimrc:

  set rtp+=/opt/homebrew/opt/fzf

==> **ffmpeg**

ffmpeg-full includes additional tools and libraries that are not included in the regular ffmpeg formula.
```

