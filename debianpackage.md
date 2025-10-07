# Debian Package

## Directory Structure Inside `.deb`
A `.deb` archive contains:
```bash
./usr/include/
./usr/lib/
./DEBIAN/control
./DEBIAN/md5sums
...
```
## Explore Uninstalled Packages
### Search files in uninstalled packages:
```bash
sudo apt install apt-file
apt-file update
apt-file list libc6-dev
```
### Manually inspect `.deb` files;
```sudo apt download libc6-dev
dpkg-db -c libc6-dev_*.deb

# This shows full file list without installing
```

## Identify Source
To see where a header is from:
```bash
dpkg -S /usr/include/netinet/in.h
```
Which will give us:
```bash
libc6-dev:amd64: /usr/include/netinet/in.h
```
Or for kernel headers:
```bash
dpkg -S /usr/include/linux/in.h
```
Gives us:
```bash
linux-libc-dev:amd64: /usr/include/linux/in.h
```
### How `dpkg -S` Works Internally
 * Every installed `.deb` package has a **list of installed files** stored under:
```bash
/var/lib/dpkg/info/<package-name>.list
```
 * When we run:
```bash
dpkg -S /usr/include/stdio.h
```
`dpkg-query` scans all the `.list` files under `/var/lib/dpkg/info/` to see if any contain the full file path.

### View All Header Files in a Package
Let's try with `libc6-dev`:
 * Show all files from the package:
```bash
cat /var/lib/dpkg/info/libc6-dev:amd64.list
```
|Command|Purpose|
|---|---|
|`dpkg -S <file>`|Find which **installed packages** owns a file|
|`cat /var/lib/dpkg/info/<pkg>.list`|View **all installed files** from a package|
|`apt-file list <pkg>`| List files in **available but uninstalled** pakages|
|`dpkg-deb -c <pkg>.deb`|Inspect contents of a downloaded `.deb` file|


## Maintainer Scripts
When we install a `.deb` package, it may include *maintainer scripts* like:
|name|description|
|---|---|
|`preinst`|Before installation|
|`postint`|After installation|
|`prerm`|Before removal|
|`postrm`|After removal|
These scripts live in the **package archive** and get run by ***dpkg***.

## Extracting and Inspecting Maintainer Scripts
```bash
mkdir wiresharkdeb
cd wiresharkdeb
apt download wireshark-common
dpkg-deb -e wireshark-common_*.deb control_files

# Now open/read the postinst file under control_files directory
cat control_files/postinst
```

## Package Configuration
|Command Example|Purpose|
|---|---|
|`sudo apt install wireshark-common`|Install wireshark-common package|
|`apt download wireshark-common`|Downloads a `.deb` file without installing it - useful for inspection|
|`sudo dpkg-reconfigure wireshark-common`|Re-runs the package's configuration dialog to allow or deny non-root packet capture (update group permissions, capabilities, etc.)|

## Interpreting `dpkg -l` short codes
At the top of `dpkg -l` we often see a header like:
```bash
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
```
 * The leftmost two letters we see for each pakage are: **first character=*** desired action, **second charcters=** current status.

 * The first three columns of the output show the desired action, the pakcage status, and errors, int that order.

 * Desired Action:
   * u = Unknown
   * i = Install
   * h = Hold
   * r = remove
   * p = Purge
 * Package status:
   * n = Not-installed
   * c = Config-files
   * H = Half-installed
   * U = Unpacked
   * F = Half-configured
   * W = Triggers-awaiting
   * t = Triggers-pending
   * i = Installed
 * Error flags:
   * <empty> = (none)
   * R = Reinst-required


