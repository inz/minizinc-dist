# MiniZinc Distributions

In this repository, you will find pre-packaged MiniZinc distributions complete with a third-party solver (currently [Google or-tools](https://github.com/google/or-tools)).

The distribution comes in two variants: a regular archive and a Heroku-friendly archive that will extract to a `vendor/minizinc/` directory to be installed alongside your application.

# Installation

To install the regular distribution, fetch the archive and unpack it.
Currently, there are releases for `linux64`, `darwin`, and `win64`.
See [Releases](https://github.com/inz/minizinc-dist/releases) for details.

# Installation on Heroku/Cloud Foundry

Using the `*-vendor*` archives you can easily add the MiniZinc distribution to your buildpack-based 12factor app.

* Add `https://github.com/peterkeen/heroku-buildpack-vendorbinaries` to your buildpacks in `app.json`.
* Add the release URL to `.vendor_urls`:

        echo 'https://github.com/inz/minizinc-dist/releases/download/minizinc-2.0.13_or-tools-v2016-06/minizinc-2.0.13_or-tools-v2016-06-linux64-vendor.tar.gz' >.vendor_urls

* Add the `bin/` directory to your `$PATH` using a `profile.d` script:

        mkdir -p .profile.d
        echo 'PATH=$PATH:$(pwd)/vendor/minizinc/bin' >.profile.d/minizinc-path.sh

* You should now be able to invoke minizinc with the or-tools backend using

        minizinc -G or-tools -f fzn-or-tools <path/to/model.mzn> ...