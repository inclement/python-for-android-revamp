# Development of this revamp has moved to the revamp branch of the
  [Kivy python-for-android repository](https://github.com/kivy/python-for-android/tree/revamp)


# P4A experiment

This is an experimental Python for Android APK builder based on the
pythonic toolchain of kivy-ios. Broad goals are:

Update: Basic SDL2 support **is done**. Support for building an APK is
still rudimentary (only a few options supported), but it should now be
possible to properly attack any feature of the current
python-for-android without this all needing to be refactored
later. I'd be grateful to anyone interested in testing this, and will
start writing documentation on how to do so shortly (beyond the brief
snippets below).

- Support SDL2
- Support multiple bootstraps (user-chosen java + NDK code)
- Support python3
- Support some kind of binary distribution
  (including on Windows)
- Be a standalone Pypi module

This is at an early (but working!) stage. The following command will try to
download and build some recipes. It should duplicate the functionality
of distribute.sh (and you can build an apk with the result using
build.py!), but the code is currently bad and only the few essential
recipes are supported.

     python2 toolchain.py create --name=testproject --bootstrap=pygame --recipes=sdl,python2

Add the `--debug` option to any command to enable printing all the
debug information, including output of shell commands (there's a lot if it!).

It's also now possible to build working APKs that run kivy with
sdl2. The following command *should* work:

    python2 toolchain.py create --name=testsdl2 --bootstrap=sdl2 --recipes=sdl2,python2

Like the pygame bootstrap, this makes a dist dir with a build.py. This
doesn't support all the same options as the old bootstrap (yet), but
you can customise things like the APK name.

All the details here are highly preliminary; the current priority is
to get different parts of the tool basically working (even if hacky)
before going back to set technical decisions in stone.

# Dependencies

- Virtualenv
- Android SDK (link by setting the ANDROIDSDK environment variable)
- Android NDK (link by setting the ANDROIDNDK environment variable)
- Cython

Pip:
- sh
- appdirs
- colorama
- jinja2


# Known missing stuff from P4A

This list relates only to the SDL2 bootstrap unless stated otherwise -
the pygame version has many of them implemented internally

- Pymodules install (all bootstraps)
- Public dir installation
- Some recipes/components aren't stripped properly of doc etc. (all bootstraps)
- Downloaded file md5 and headers aren't checked
- Some command line options of distribute.sh
- Biglink is essential (the p4a disable option isn't implemented)
- Android services are not implemented at all
- App loading screen
- Billing support
- Kivy Launcher build (can now be implemented as a bootstrap...maybe?)
- Several build options for build.py
- Probably some other stuff

# Untested recipes

These recipes exist and probably should work, but haven't been
properly tested (if at all).

- vispy
- numpy


# Current status

Working to make the basic API stable, ready for people to try it.
