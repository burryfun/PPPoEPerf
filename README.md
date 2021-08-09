## pppoe_perf
PPPoEPerf is a pppoe server performance test tool.  
 

## Building

mkdir -p build  
cd build  
cmake ..  
make  
sudo make install  

note  
this program has dependency on boost log,system,program_option,random,regex you should boost first  
if all that haved been install, and cmake also cannot found your boost path, you can specify the boost root with command  
cmake -DBOOST_ROOT=path  

## Building for Ubuntu 20.04

apt-get update
apt-get install cmake
apt-get install vim
apt-get install wget
apt-get install git
apt-get install g++
git clone https://github.com/iKuaiNetworks/PPPoEPerf.git
apt-get install libboost-all-dev
apt install build-essential checkinstall zlib1g-dev -y
cd /usr/local/src/
apt-get install libpcap-dev libssl-dev
wget https://www.openssl.org/source/openssl-1.1.1c.tar.gz
tar -xf openssl-1.1.1c.tar.gz
cd openssl-1.1.1c
./config --prefix=/usr/local/ssl --openssldir=/usr/local/ssl shared zlib
make
make install
cd /etc/ld.so.conf.d/
    vim openssl-1.1.1c.conf   :
            /usr/local/ssl/lib
ldconfig -v
mv /usr/bin/c_rehash /usr/bin/c_rehash.backup
mv /usr/bin/openssl /usr/bin/openssl.backup
    vim /etc/environment      :
            PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/usr/local/ssl/bin"
source /etc/environment

## Usage

pppoe_perf -h  
```
Allow options:  
  -h [ --help ]              print help messages  
  -c [ --config ] arg        config file  
  --resend-timeout arg (=20) Specify the resend timeout  
  --discovery                Only discover the PPPoE servers  
  --ppp-stage                Use ppp-stage  
  --terminate                Terminate the session directly  
  --summary                  Show the summary stats  
```
 * --resend-timeout  
  the wait time out value after sending request packet to pppoe server  
 *  --discover   
  only to send padi packet to pppoe server to get server info, not enter the session stage  
 *  --ppp-stage  
  if you want test ppp session stage, you should use it  
 *  --terminate  
  if you use this option, your test will not enter lcp, auth stage, after received a valid session id,  
  send padt actively  
 *  --summary  
  with this option you will see the performance result in a file named 'pppoe_perf.txt'  


## configure file
  after you install pppoe_perf, you will find the configure file at the direcory /etc/pppoe_perf/conf.json  
```
  {  
  		"interface"  : "eth0",  
  		"duration"   : 1000,  
        "padi-cnt"   : 1000,  
        "period"     : 60,  
        "log"        : "error",  
        "login-rate" : 100,  
  
        "account":{  
                "fgao_test"  :  "fgao123",  
                "zhang_test" :  "zhang_test"  
        }  
  }  
  ```

* interface  
   which interface to bind
*  duration  
   how long the test will run
*  padi-cnt  
   the pppoe users you are going to simulate
*  period  
   user online period, after one user get an valid ip, it will keep sending udp packet to the internet, after the period seconds gone,  
   the user will offline, and after double period time gone, the user will online again
* login-rate  
   how many simuate users send padi request every second   
* account  
   the pppoe account and password  
   
## 
Author: Xiaopei Feng                                                                                                                                                                          
Contact me: xpfeng@ikuai8.com  
Copyright(C) 2017  ikuai8.com   
PPPoEPerf software is distributed under GPL3 license and includes contributions from numberous individuals and organizations. Please see the COPYING and CONTRIBUTORS files for details.  
 
