# mi-centos changelog

## 2.5.1 (not yet released)

- Added kernel tuning for vm.dirty_background_bytes (IMAGE-439) in ks.cfg file.
Will cause dirty data to begin to be background flushed at 100 Mbytes, so that
it writes earlier and more often to avoid the large build up. 

- Changed kickstart post logging location to /var/log

- Removed anaconda-help from yum install in ks.cfg as it's no longer needed.`

- Updated all references (MOTD in ks.cfg etc) to CentOS version to 6.5 and 6.4 
is now deprecated

- Enabled network interface eth0 via dhcp in the ks.cfg file

- Made build_centos_iso.sh and setup_env.sh executable in the repo

- Updated build_centos_iso.sh to use secondary /data for storing the iso and 
layout data. The assumtion is that you'd be using a CentOS VM to build the 
image.

- Updated bootloader line in ks.cfg file to inlcude boot parameters tsc=reliable and divider=10


## 2.5.0

- Initial release
