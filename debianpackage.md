# Debian Package

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
