=====================================================================================================================
  Copyright 2011 Ido Magal. All rights reserved. 
=====================================================================================================================
                DISCLAIMER: 

                USE AT YOUR OWN RISK. YOU ARE RESPONSIBLE FOR READING AND UNDERSTANDING
                THE CODE IN THIS SCRIPT AND NO GUARANTEE IS GIVEN OR IMPLIED.
               
                THIS CODE MAY ERASE ANYTHING, ANYWHERE, AT ANY MOMENT.
=====================================================================================================================

WHAT IS TRUNKFISH?
==================
Trunkfish is a script that creates periodic backups of the machine executing it onto a separate machine. It was explicitly developed for backing up OSX machines onto a DroboFS, but, with some minimal work, should work for backing up any posix device onto any other posix device, provided they have the requisite programs. 


WHY TRUNKFISH?
==================
I wrote Trunkfish because I wanted a periodic hardlinked-based backup system that I could use to backup our home Macs onto the home DroboFS. The top contenders were TimeMachine and rsnapshot.

Trunkfish's advantage over Time Machine is that it does not use a proprietary storage format. It just creates a directory for each day dated as such (e.g. "/2011-11-1/") which contains a complete snapshot of the backed up computer. Thanks to the magic of hardlinks, it only uses as much space as necessary to save the files that have changed. Just like rsnapshot.

However Trunkfish's advantage over rsnapshot is that it is client-driven and does not require running the software on the server. Additionally, it's easier to setup (doesn't require multiple cron jobs and rsync configs), and it uses absolute dates for backup directories rather than relative ones.

The downside to Trunkfish is that there's no GUI, no large community of users, and it doesn't account for many usage cases (yet).


HOW DO I USE TRUNKFISH?
=======================

  1. First, read this README.
  2. Next, copy all of these files into a permanent new home, such as ~/Trunkfish/
  3. Edit trunkfish.cfg to suit your backup. In the least you'll need to change the backup destination to match the name of the directory you'll be backing up into.
  4. type 'sudo ./trunkfi.sh --firsttime'


WHAT DOES TRUNKFISH CONSIST OF?
=================================

   Files that go with this script:

   README                  - This file.
   trunkfi.sh              - The main script that does the work.
   trunkfish.cfg           - The configuration file. You need to edit this file before you run trunkfi.sh.
   find_trunkfi.sh         - A script to identify when a file was was most recently updated. This is really only necessary when backing up to a DroboFS, since the 'find' on those doesn't support '-links'


   Files that get generated during every backup:

   ~trunkfish_excludes.txt - A temporary txt file that contains rsync filters for the backup.
   ~trunkfish.log          - A temporary log of the backup events.
   ~trunk_err.log          - A temporary log of backup errors, if there are any.


WHAT'S THE STATUS OF TRUNKFISH DEVELOPMENT?
==========================================
   MY TODO:
        - require root for setup scripts
        - create cfg on first run
        - add lots of explanation text to firsttime script

  Email:   M8R-u8t2l4 AT mailinator DOT com

