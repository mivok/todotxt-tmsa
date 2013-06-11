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
