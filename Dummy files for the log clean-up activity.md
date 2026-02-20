==========================================================================================================
                                            Dummy log files
==========================================================================================================

# Step 1: Create Dummy Log Files

# test-cleanup folder has been created
    sudo mkdir -p /vboxuser/Bash_Scripting/test-cleanup 

# Dummpy log files created under the folder test-clean
    sudo touch /vboxuser/Bash_Scripting/test-cleanup/old-log1.log
    sudo touch /vboxuser/Bash_Scripting/test-cleanup/old-log2.log
    sudo touch /vboxuser/Bash_Scripting/test-cleanup/new-log1.log
    sudo touch /vboxuser/Bash_Scripting/test-cleanup/new-log2.log

# Try to avoid by creating the files with the sudo user as it will make the root as owner of this file.

    mkdir -p test-cleanup 

    touch old-log1.log
    touch old-log2.log
    touch new-log1.log
    touch new-log2.log

vboxuser@admin:~/Bash_Scripting/test-cleanup$ ls
clean-up.sh  new-log1.log  new-log2.log  old-log1.log  old-log2.log

# Step 2: Modify File Dates

Make two files older than 14 days:

    touch -d "20 days ago" Old-log1.log
    touch -d "30 days ago" old-log2.log

Keep two files recent:

    touch -d "2 days ago" new-log1.log
    touch -d "1 day ago"  new-log2.log

✅ Step 3: Verify Timestamps

    ls -l test-cleanup

You should see:

    vboxuser@admin:~/Bash_Scripting/test-cleanup$ ls -ltra
    total 12
    -rw-r--r-- 1 vboxuser vboxuser    0 Jan 21 12:49 old-log2.log → ~30 days old
    -rw-r--r-- 1 vboxuser vboxuser    0 Jan 31 12:48 old-log1.log → ~20 days old
    -rw-r--r-- 1 vboxuser vboxuser    0 Feb 18 12:49 new-log1.log → recent
    -rw-r--r-- 1 vboxuser vboxuser    0 Feb 19 12:40 new-log2.log → recent
    drwxrwxr-x 3 vboxuser vboxuser 4096 Feb 20 12:05 ..
    -rwxrwxr-x 1 vboxuser vboxuser  104 Feb 20 12:07 clean-up.sh
    drwxr-xr-x 2 vboxuser vboxuser 4096 Feb 20 12:50 .

✅ Step 4: Run Your Cleanup Script

    sudo ./clean-up.sh

==========================================================================================================

#!/bin/bash

echo "Removing old log files..."
find . -type f -name "*.log" -mtime +14 -exec rm -f {} \;

==========================================================================================================

# Important Part here to change the permissions of the log files if the permmission error is occured during the during clean-up script execution.

    vboxuser@admin:~/Bash_Scripting/test-cleanup$ ./clean-up.sh
    Removing old log files...

✅ Step 5: Verify After Execution

    ls -l /var/log/test-cleanup

Expected result:

    You can see here, Older files has been deleteed

    vboxuser@admin:~/Bash_Scripting/test-cleanup$ ls -ltra
    total 12
    -rw-r--r-- 1 vboxuser vboxuser    0 Feb 18 12:49 new-log1.log
    -rw-r--r-- 1 vboxuser vboxuser    0 Feb 19 12:40 new-log2.log
    drwxrwxr-x 3 vboxuser vboxuser 4096 Feb 20 12:05 ..
    -rwxrwxr-x 1 vboxuser vboxuser  104 Feb 20 12:07 clean-up.sh
    drwxr-xr-x 2 vboxuser vboxuser 4096 Feb 20 12:53 .

==========================================================================================================