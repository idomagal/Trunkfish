# Trunkfi.sh

Copyright 2011 Ido Magal. All rights reserved. M8R-u8t2l4 AT mailinator DOT com


    DISCLAIMER:

    USE AT YOUR OWN RISK. YOU ARE RESPONSIBLE FOR READING AND UNDERSTANDING
    THE CODE IN THIS SCRIPT AND NO GUARANTEE IS GIVEN OR IMPLIED.   
     
    THIS CODE MAY ERASE ANYTHING, ANYWHERE, AT ANY MOMENT.


## What is Trunkfish?

__Trunkfish__ is a script that creates periodic file backups of the machine executing it onto a separate machine. It was explicitly developed for backing up OSX machines onto a DroboFS, but, with some minimal work, should work on linux and cygwin'ed Windows machines. As of now, all but the scheduling works on cygwin. 


## Why Trunkfish?

I wrote __Trunkfish__ because I wanted a periodic hardlinked-based backup system that I could use to backup our home Macs onto the home DroboFS. The top contenders were TimeMachine and rsnapshot.

__Trunkfish__ is differentiated from Time Machine in that it does not use a proprietary storage format. It creates a directory for each day dated as such (e.g. "/2011-11-1/") which contains a complete snapshot of the target directory on the host computer. The trade-off is that it is not a system image backup, but a loose file backup.

__Trunkfish__ is differentiated from rsnapshot in that it is client-driven and does not require running any software other than rsync and ssh on the server. Additionally, it's easier to setup (doesn't require multiple cron jobs and rsync configs), and it uses absolute dates for backup directories rather than relative ones.


## How do I use Trunkfish?


#### How do I install Trunkfish?

  1. First, read this README.
  2. _git clone git://github.com/idomagal/Trunkfish.git_
  3. Edit trunkfish.cfg to suit your backup.
  4. _sudo ./trunkfi.sh --first-time_

#### How can I watch Trunkfish progress?

_tail -f ~trunkfish.log_

#### How do I know if the backup succeeded?

  * If the backup failed, there will be a directory with a .incomplete or .aborted extension in your backup dir. You can safely delete them.
  * Look at ~trunk_err.log to determine what may have gone wrong.
  * Otherwise, if the backup was successful, there'll be a directory named with date and a .d, .w, .m, and or .y extensions. E.g. '2011-11-31.d'

#### What does the .d, .w, .m, and .y extensions mean?

They represent daily, weekly, monthly, and yearly backups, respectively. Eventually the more frequent backup directories get deleted and only the less frequent ones remain, in order to conserve space. By default __Trunkfish__ keeps 30 daily backups, 26 weekly backups, and never deletes monthly or yearly backups. You can change these numbers in trunkfish.cfg.

## What does Trunkfish consist of?

Files that go with this script:


    *  README.md               - This file.
    *  trunkfi.sh              - The main script that does the work.
    *  trunkfish.cfg           - The configuration file.
                                 You need to edit this file before you run trunkfi.sh.
    *  find_trunkfi.sh         - A script to identify when a file was was most recently updated.
                                 This is really only necessary when backing up to a DroboFS,
                                 since the 'find' on those doesn't support '-links'


Temporary files that get generated during every backup:

    *  ~trunkfish_excludes.txt - A temporary txt file that contains rsync filters for the backup.
    *  ~trunkfish.log          - A temporary log of the backup events.
    *  ~trunk_err.log          - A temporary log of backup errors, if there are any.


## What's the status of Trunkfish development?

TODO:
  
* Backup into a sparsebundle to preserve OSX metadata
* Create cfg on first run
* Dynamically choose rsync exclusions based on OS
* Add scheduling support for cygwin
* Add versioning to the script
* fix w/m/y not getting re-made in case of a resumed backup
