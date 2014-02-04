# mi-centos changelog

## 2.6.0 (not yet released)

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

- Updated bootloader line in ks.cfg file to inlcude boot parameters 
  tsc=reliable and divider=10

- Generate /etc/product file as part of kickstart process. product file is no
  longer part of /lib/smartdc guest tools

## 07/xx/2013 - 2.5.0
- Going back to basics
    - Stock Centos 6.4 distro and Kernel
- Added Duo Security (disabled by default)

## xx/xx/xxxx - 2.4.3 ( datasets update )
- Updated /lib/smartdc/run-user-script
    - Moved where user-script and lock file are stored
- Updated /lib/smartdc/format-secondary-disk
    - Changed partition type to gpt to allow for disk partions > 2TB

## 05/09/2013 - 2.4.2 ( dataset update )
- Updated /lib/smartdc/prepare-image
    - Added check to make sure that /etc/fstab is not mounting disk via UUID's
    - Updated to set permissions for /tmp and /var/tmp 1777
    - Updated how /etc/hostname is created
- Updated /lib/smartdc/joyent_product
    - Systems are no longer SmartMachines, but now Instances
- Updated /lib/smartdc/joyent_motd_footer
    - Updated with minor formatting of version info

## 04/17/2013 - 2.4.1 ( ISO image install )
- Update /lib/smartdc/format-secondary-disk
    - Added logging for cration of /data
- Updated /lib/smartdc/prepare-image
    - Removed zero filling of disk and added copying of root disk to a new partition
    - Scripts are now distro specific and added checking to ensure that the script only runs on the distor it is authored for
    - Updated MOTD with minor logo changes
    - Added checks for JPC SmartDC Node.JS utility installed in /opt/local/smartdc
    - Added check to make sure that /etc/fstab is not mounting disk via UUID's
- Enabled Dynamic MOTD to display dataset information
- Added the ability for customers to overwrite /root/.ssh/authorized_keys by adding this metadata variable:
    - overwrite_root_akeys = OVERWRITE
- Added many QA and security checks
- Updated script to use libs and vars from lib_smartdc_scripts.cfg
- Updated /etc/ntp.conf file to listen to IPv4 interfaces
- Added /lib/smartdc/README
- Added /opt/local/smartdc directory
    - This is a static install of Node.JS that is exclusively used to provides Joyent Cloud API access
    - Node.JS 0.10.3 is installed with version 6.5.7
- Updated /lib/smartdc/joyent_product_info
    - Added new URL for CentOS docs
- Updated kernel to 3.8.7
    - Added PPP and QoS 
- Updated /lib/smartdc/joyent_rc.local
    - Removed non-CentOs specific subs this makes this version only specific to Debian datasets
- Updated /lib/smartdc/joyent_motd_footer
    - Minor spacing changes for MOTD banner
    - Changed default that MOTD System Checks and MOTD Alerts/Info/Tips from Joyent are disabled
    - MOTD System Checks can be turned on by setting MDATA tag enable_motd_sys_info = TRUE
     or setting $ENABLE_MOTD_JOYENT_INFO = TRUE in /lib/smartdc/joyent_motd_footer
    - MOTD Alerts/Info/Tips from Joyent can be turned on by setting MDATA tag enable_motd_joyent_info = TRUE
     or setting $ENABLE_MOTD_JOYENT_INFO = TRUE in /lib/smartdc/joyent_motd_footer
    - Updated Joyent MOTD header
    - Updated how free memory is calculated to include disk buffers and cached
- Added /sbin/dhclient-script.joyent
    - This is a reference file for when DHCP client is updated so that hostname setting can be reset
- Updated all distro packages via yum update
- Removed all lsb calls in /lib/smartdc scripts
- Removed all Joyent specific code and now call /lib/smartdc/joyent_rc.local
- Added /lib/smartdc/set-hostname
    - Script that is called by the dhcp client via /sbin/dhclient-script
    - Host name is set in 3 ways in this order:
        1. /etc/hostname is used if exists and is not empty
        2. Metadata value 'hostname' is used if set
        3. Hostname sent from DHCP server is used
- Added /lib/smartdc/joyent_rc.local
    - All Joyent specific calls from /etc/rc.local are now here
- Added /lib/smartdc/joyent_linux_repo_gpg_key
    - This is the public GPG key Joyent uses to validate to the Joyent Linux Repo at linux.joyent.com
    - NOTE: at this time the CentOS repo is not GPG signed
- Added symbolic links for /etc/product, /etc/joyent_dataset_changelog and /etc/joyent_version
    - Their target files now reside in /lib/smartdc to locate Joyent specific files in one place as much as possible.
- Added /lib/smartdc/redhat-powerbtn-acpi-support.sh
    - This is called by the acpi event when API calls reboot via /etc/acpi/events/powerbtn-acpi-support the Joyent specific script will log to /var/log/mesages when an API reboot or shutdown is called
    - Note that reset from the API will not be logged as the KVM is reset immediatly
- Added /lib/smartdc/lib_smartdc_scripts.cfg
    - This is a central script that holds common variables and functions used in /lib/smartdc all scripts in /lib/smartdc now use this config file for common libs and variables

