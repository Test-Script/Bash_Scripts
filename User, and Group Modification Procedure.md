==========================================================================================================
                                User, and Group Modification Procedure
==========================================================================================================

1. For a single file:

    sudo chown user:group <file-name>

    sudo chown vboxuser:vboxuser new-log1.log

    This sets both the User and the Group to vboxuser at the same time.

2. For all files in the current folder:

    sudo chown user:group <for all files we can use *>

    sudo chown vboxuser:vboxuser *

3. Using the specific group command:

    sudo chgrp vboxuser old-log1.log

==========================================================================================================