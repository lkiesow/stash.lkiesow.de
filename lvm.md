LVM
===

    lvs
    vgs
    pvs
    
    lvresize -r -n -v -L +60G /dev/VGdata/LVdata
    lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv
    
    resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv
    xfs_growfs /dev/mapper/cs_vm643-root
