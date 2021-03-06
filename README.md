# Pulp

A build tool for PureScript.

![Jarvis Cocker dancing](http://24.media.tumblr.com/77b76c557515a801a7e99ca5507b6548/tumblr_n5cx52oT831r4ba6to1_400.gif)

## Installation

```sh
$ cabal install purescript
$ npm install -g pulp
```

## Project Structure

The structure of a `pulp` project should look like this:

```
  root
  - bower.json
  - src/
  - test/
```

Put your `.purs` source files in the `src` directory, and any tests
you might have in the `test` directory.

Also, create a `bower.json` file (see
<http://bower.io/#defining-a-package>). `pulp` expects to find this
file in the root of your project. You can invoke `pulp` from a
subdirectory; if there is no `bower.json` to be found in the current
directory, `pulp` will look through parent directories until it finds
it.

## Commands

`pulp` supports the following commands:

* `pulp install` will install dependencies as given in the
  `bower.json` file. It essentially just invokes `bower install`.
* `pulp build` invokes the PureScript compiler. Currently, it just
  compiles all `.purs` files in your `src` and dependencies into the
  target directory, which defaults to `output`.
* `pulp test` runs your test suite: it expects a `Test.Main` package
  in the `test` directory, containing a `main` function, which is
  required and run using Node. It's expected that failing tests will
  cause the program to terminate with an error. `Test.QuickCheck`
  works well for this purpose.
* `pulp run` will first run `pulp build`, then launch the compiled
  project code in a Node process. The entry point will be the `main`
  function in the module specified with the `--main` option, or, by
  default, the module `Main`.
* `pulp browserify` also runs `pulp build`, then runs the project code
  through [Browserify](http://browserify.org/). The entry point is
  decided in the same way as with `pulp run`. You can specify an
  output file using `--to`; the default is to output the bundle to
  stdout, which is convenient for doing things like `pulp browserify |
  uglifyjs -c`.

## Watch and restart

You can launch any of the above commands with the `--watch` or `-w`
option, which will cause `pulp` to run indefinitely, watching your
`src` and `test` folders for changes, and re-running the command
whenever something changes.

## License

Copyright 2014 Bodil Stokke

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Lesser General Public License as
published by the Free Software Foundation, either version 3 of the
License, or (at your option) any later version.

See the [LICENSE](LICENSE.md) file for further details.
