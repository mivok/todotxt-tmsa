# Todo.txt helper scripts for working with the cycle

This repository contains a set of todotxt-cli addons that make working with
The Cycle (as described in [Time Management for Systems
Administrators](http://shop.oreilly.com/product/9780596007836.do)) easier.
Specifically it assists with the management of dated todo files, and allows
you to easily move tasks between different todo lists.

## Installation instructions

 * Install [todotxt-cli](https://github.com/ginatrapani/todo.txt-cli)
 * Edit the todo.cfg file. Change the locaitons of the TODO_FILE and
   DONE_FILE:

        export TODO_FILE="$TODO_DIR/$(date +%Y-%m-%d).txt"
        export DONE_FILE="$TODO_DIR/$(date +%Y-%m-%d)-done.txt"
 * It is also recommended (but not necessary) to add the following config
   options to your todotxt config file:

        export TODOTXT_DATE_ON_ADD=0
        export TODOTXT_AUTO_ARCHIVE=1
 * Copy the contents of this repository (excluding this readme) into
   `~/.todo.actions.d`. If you configured a custom `TODO_ACTIONS_DIR`, then
   place them in that directory instead.
 * Run `todo.sh help` and you should see the new actions at the bottom of the
   help. If not, make sure the files you put in `~/.todo.actions.d` are
   executable.
 * Run `todo.sh tmsa`. This will generate symlinks for all actions provided by
   the `tmsa` addon.

## Helper commands provided by the tmsa addon

 * bump - bump a single task to the next day. Use this for when you decide you
   won't be doing that task today.
 * bumpall - bump all the remaining tasks for today on to tomorrow's todo
   list. Do this at the end of the day with any tasks you didn't get to
   complete. Be sure to review any high priority tasks and deal with them
   before bumping to the next day.
 * verify - Search all files for unmanaged tasks (those that haven't been
   completed and/or bumped to a later day)
 * bringforward - bring all the tasks you forgot to manage on to today's todo
   list.

## Other addons in this repository

 * push - A quick command to commit changes and push to git.
   * This is intended to be run at the end of the day after running bumpall to
     commit your changes.
 * addto - A modified 'addto' command.
   * Automatically create a new todo file if it looks like a dated file.
   * If 'tomorrow' is passed as the filename, expand it to tomorrow's todo
     list.
 * goals - view/edit goals.txt, a life goals list
   * Passing in no arguments will view the goals list
   * Passing in arguments will add an entry to the goals list
   * goals.txt is like any other todo file, but is used for longer term goals
     or someday/maybe items.

## Examples

    $ todo.sh ls
    1 Some task
    2 Some other task
    3 A third task
    --
    2013-06-11: 3 of 3 tasks shown

    $ todo.sh bump 1
    Some task
    TODO: 1 bumped from 2013-06-11.txt to 2013-06-12.txt

    $ todo.sh lf 2013-06-12
    1 Some task
    --
    2013-06-12: 1 of 1 tasks shown

    $ todo.sh lsa
    1 Some other task
    2 A third task
    0 x 2013-06-11 Some task bumped:2013-06-12

    $ todo.sh bumpall
    Some other task
    A third task

    TODO: all items bumped from 2013-06-11.txt to 2013-06-12.txt

    $ todo.sh lsf 2013-06-10.txt
    1 Some task I forgot about
    --
    2013-06-10: 1 of 1 tasks shown

    $ todo.sh verify
    2013-06-10.txt

    $ todo.sh bringforward
    Some task I forgot about
    TODO: all items bumped from 2013-06-10.txt to 2013-06-11.txt
