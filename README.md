shu-thing
=========
A vector shooter game

# Original notes from package authors:
Find these notes in their [darcs repo](https://archives.haskell.org/code.haskell.org/shu-thing/).

Shu-thing for Windows(OpenGL)

Presented by Hideyuki Tanaka & Takayuki Muranushi

**  How to Install

  Extract shu-thing.zip
  Then execute shu-thing.exe
  To play Shu-thing, you need OpenGL installed
  into your computer.

**  Operation

  - move arrow keys
  - shot z
  - exit q; you can also click for a menu

**  Rules

  Control the Hypermonadic space fighter Dodecahedron,
  avoid showering bullets, exterminate enemy forces,
  and destroy the great enemy carrier that awaits you
  at the end of the stage. You are the last hope of survival
  of human race.

  You are equipped with the forcefield that can endure
  3 bullets. You lose your ship if shot after the forcefield
  ran out of power. Be careful because you got nothing like
  invincibilities, remains, or bombers. Hence you immediately
  die if you charge into a cloud of bullets, while this
  operation will save your ship with only 1 point of damage
  in many other games.

  Only enemy bullets, not enemy bodies, are harming.

**  Special Thanks

  Shu-thing is written in Haskell, compiled by Glasgow Haskell Compiler 6.4
    The Haskell Home Page
    http://www.haskell.org/
    The Glasgow Haskell Compiler
    http://www.haskell.org/ghc/

  uses OpenGL for drawing.
    http://www.opengl.org/

# Our installation instructions:

We had a lot of trouble getting this working in different Linux environments, mainly NixOS and Ubuntu 16.04, due mainly to issues with native dependencies. Downloading and trying to run the executable as they say to do did not work on any of our machines initially.

First we did successfully build it with cabal version 1.2.2 on a machine running Ubuntu 16.04:

```shell
$ cabal configure
$ cabal install
$ ./dist/build/shu-thing/shu-thing
```

That *may* be all you need to do. However, this broke for us at some point.

## Adding Stack + Nix

In looking for a more reproducible build process, we initialized Stack, adding a `stack.yaml` file, to which we added

```yaml
nix:
  packages:
    - mesa
    - mesa_glu
    - freeglut
```

You seem to have to first build *with Nix*, then *without Nix* and execute *without Nix*, so it looks like this:

```shell
$ stack build
$ stack build --no-nix
$ stack exec --no-nix -- shu-thing
```

If you do not have Nix enabled in your global (or this project's) Stack configuration, then you may need to add a flag to get it to build with Nix the first time, so those commands above would look like this:

```shell
$ stack build --nix
$ stack build --no-nix
$ stack exec --no-nix -- shu-thing
```

Best of luck staying alive in the game. We would welcome additions to these installation instructions for different environments.
