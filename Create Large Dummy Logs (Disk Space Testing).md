==========================================================================================================
                                Create Large Dummy Logs (Disk Space Testing)
==========================================================================================================

    sudo fallocate -l 100M /var/log/test-cleanup/big-old.log
    sudo touch -d "25 days ago" /var/log/test-cleanup/big-old.log

    df -h