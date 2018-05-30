# About

A drop-in replacement for the "base" package, which extends it with reexports of the APIs of a bunch of de-facto standard libraries like "text", "bytestring", "vector", "containers", "unordered-containers", "hashable", "transformers", "stm". It reexports all the standard modules from those libraries as well as "base" under **the same** namespaces. To the end-user it looks like his library depends on those packages directly. As an icing it also replaces the standard `Prelude` module with a way richer one packed with types and functionality.

# Pros

* Relieves you from maintaining an endless list of dependencies on de-facto standard libraries with frozen APIs

* Provides a rich `Prelude` module packed with all the standard non-conflicting definitions as well as those coming from the depended on packages

* Makes your packages more portable by approaching some of the incompatibilities of different versions of "base"

* Can be used to relieve you from the dependencies management during the development cycle with an intent to be replaced with specific dependencies for production

* Compared to the alternative solutions like ["rebase"](https://github.com/nikita-volkov/rebase), requires no changes in the actual codebase

# Cons

* Brings in a long list of dependencies. Although, in the end, most apps bring those dependencies in either directly or transitively any way.

* Due to a wide range of dependencies, which in some cases have wide bounds, there is a risk of transitive API-breaking changes

# Recommended use-cases

* End-applications (executables)

* Tests, benchmarks

* Scripts

* During the development phase of a library

# Unrecommended use-cases

It's not recommended to depend on "rerebase" in the release versions of libraries, since it's best for the authors of packages to be directly responsible for the version bounds of their dependencies. Also in the community there is a phenomenon of packages with higher number of dependencies being trusted lesser.

# Supported GHC versions

All versions starting from `7.8`.

# Usage 

## Cabal

Since this package uses exactly the same namespaces as the packages it reexports, you cannot have your project depend directly on both. So, when you have "rerebase" in your dependencies, there must be no "text" or "bytestring" and etc.

## GHCi, Setup.hs and scripts

When "rerebase" is installed in the local package database, GHCi will complain about having two conflicting Prelude modules to import. It is also known that the same applies to the `Setup.hs` build scripts accompanying the Cabal files as well as any scripts executed with the interpreter.

To work around this or any other similar issues you can hide the "rerebase" package from the interpreter using the following command:

```
ghc-pkg hide rerebase
```

Alternatively, if you're brave, and love "rerebase" so much, you can hide the "base" package instead.
