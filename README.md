# Glue
C++ dependency management is hard, is it possible to make it easy?

# Rationale

There's no easy way to manage dependencies in the C++ projects.

Existing solutions rely on customizations/patches applied to 3rd party code and/or
some kind of central repository to pull pre-built binaries from.

The problem is that it is extreemely hard and time consuming to patch/pre-build each ever created C++ library.

# Inspiration

There are some successful tools which provide OS-specific way to manage 'packages':
* [Homebrew](http://brew.sh/)
* [CocoaPods](https://cocoapods.org/)
* [Portage](https://wiki.gentoo.org/wiki/Project:Portage)
* [Sorcery](http://sourcemage.org/Sorcery)

# Philosophy

Build system should produce binaries from source code. Dependency manager should take care about dependencies. KISS FTW.

# Key features

* it should be able to pull source code from remote location
* it should be able to drive build process for `Makefile`, `GNU Autotools`, `CMake`, `Boost.Build`, `Meson`, `Scons` -based projects
* it should be able to install multiple versions of the same library
* it should be able to provide dependencies integration for `CMake`, `Meson`, `Boost.Build` build systems
* it should be able to deal with the dependencies of dependencies

# dependencies.yml

```yaml
boost:
  git: git@github.com:boostorg/boost.git
  tag: boost-1.62.0
  build:
    unix:
      - bootstrap.sh --prefix=<%= Glue.install_dir %>
    win:
      - bootstrap
  install:
    unix:
      - ./b2 install
    win:
      - b2
```

