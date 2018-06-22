# Symfony

Here lies the documentation for the lovely Symfony framework. We always
assume that the documentation was written for the latest version at the
time of writing. This means that the documentation may or may not be
outdated. It's like reading a minefield, really...

Also, all pages assume you have at least a mediocre knowledge of the
Symfony framework.

## Bundles

* [FOSOAuthBundle](bundles/fos-oauth-bundle.md)

## Sexy console commands

It kills me to type `php bin/console` every time I want to run a
command. Wouldn't it be nice to just type `./c`? Yes it would, this
wasn't a question.

1. Simply create a text file at the root of your project and name it `c`.

2. Now open up that file in a text editor and paste this

        #!/bin/bash

        php bin/console "$@"

3. Now add execute permissions to that file

        chmod +x c

That's it, now your fingers wont break. Unless a truck rides over them
or something...
