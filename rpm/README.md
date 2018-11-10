### Listing files

    rpm -ql mypackage # for installed package
    rpm -qlpv mypackage-0.1.1-1.noarch.rpm # for an rpm
    rpm2cpio mypackage-0.1.1-1.noarch.rpm | cpio -it # alt method for the same

### Extracting files

    rpm2cpio mypackage-0.1.1-1.noarch.rpm | cpio -idmv

### Show spec variables/macros

    rpm --showrc

### Quash the insane default value for topdir

    rpmbuild --define "_topdir $(pwd)/rpmbuild" -ba ./rpmbuild/SPECS/mypackage.spec
