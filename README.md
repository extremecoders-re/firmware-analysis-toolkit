# firmware-analysis-toolkit

FAT is a toolkit built in order to help security researchers analyze and identify vulnerabilities in IoT and embedded device firmware. This is built in order to use for the "*[Offensive IoT Exploitation](http://offensiveiotexploitation.com/)*" training conducted by [Attify](https://attify.com). 

This is a rewrite of original repo available at https://github.com/attify/firmware-analysis-toolkit.


## What's changed ?

The original scripts - `fat.py` & `reset.sh`  required the user to enter the root and database password during running. This updated script automates the process and thus does not require any manual intervention.


## Installation instructions

1. Install `pexpect`

    `pip2 install pexpect`
    
2. Install firmadyne as described in https://github.com/firmadyne/firmadyne

3. Copy over `fat.py` and `reset.sh` to the directory where you installed firmadyne

4. Edit `fat.py` and `reset.py` to adjust the paths to firmadyne and binwalk. Additionally, provide the root password as well. Firmadyne requires root privileges for some of its operations. The root password is provided in the script itself to automate the process.

    ```python
    # Configurations - change this according to your system
    firmadyne_path = "/home/ec/firmadyne"
    binwalk_path = "/usr/local/bin/binwalk"
    root_pass = "root"
    firmadyne_pass = "firmadyne"
    ```


## Usage 

Provide the firmware filename as an argument to the script. If not provided, the script would prompt for it at runtime.

```
$ ./fat.py <firmware binary>
```

To remove all analyzed firmware images, run

```
$ ./reset.py
```


## Example

```
$ ./fat.py DIR850LB1_FW210WWb03.bin 

                               __           _   
                              / _|         | |  
                             | |_    __ _  | |_ 
                             |  _|  / _` | | __|
                             | |   | (_| | | |_ 
                             |_|    \__,_|  \__|                    
                    
                Welcome to the Firmware Analysis Toolkit - v0.2
    Offensive IoT Exploitation Training  - http://offensiveiotexploitation.com
                  By Attify - https://attify.com  | @attifyme
    
[?] Enter the name or absolute path of the firmware you want to analyse : DIR850LB1_FW210WWb03.bin
[?] Enter the brand of the firmware : dlink
[+] Now going to extract the firmware. Hold on..
[+] Firmware : DIR850LB1_FW210WWb03.bin
[+] Brand : dlink
[+] Database image ID : 1
[+] Identifying architecture
[+] Architecture : mipseb
[+] Storing filesystem in database
[!] Filesystem already exists
[+] Building QEMU disk image
[+] Setting up the network connection, please standby
[+] Network interfaces : [('br0', '192.168.0.1'), ('br1', '192.168.7.1')]
[+] Running the firmware finally
[+] command line : sudo /home/ec/firmadyne/scratch/1/run.sh
[*] Press ENTER to run the firmware...
```
