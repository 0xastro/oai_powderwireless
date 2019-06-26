# oai_powderwireless
This repository is meant for using POWDERWireless testbed to work with OAI.

> After login to the testbed.

### Experement Creation
1. create a new experiment:
2. We selected a base Image profile ``` gnuradio_emulab ```
### Image Customization
> modify the selected base image to run our experiment:
1. make your own copy by selecting the “Copy Profile” option. 
2. Include your username in the profile name (to prevent collisions). [If there's exist many memebers in the same project]
> See ``` OAI_Profile.py ``` for modification [Basically contatins the image customization, and the resources configuration(Resources Numbers, topology ..etc)]
3. Instantiate the profile,

### Building the system
> gNB compile instructions:
```bash
sudo bash
cd /mytempdata
git clone https://gitlab.flux.utah.edu/oai/openairinterface5g.git
cd openairinterface5g/
git checkout  develop-nr-working
cd cmake_targets/
./build_oai --gNB -w SIMU
cd ran_build/build
make rfsimulator
```

> UE compile instructions:
```bash
sudo bash
cd /mytempdata
git clone https://gitlab.flux.utah.edu/oai/openairinterface5g.git
cd openairinterface5g/
git checkout  develop-nr-working
cd cmake_targets/
./build_oai --nrUE -w SIMU
cd ran_build/build
make rfsimulator
```

> Now build is done: So we run the binary for both gNB and UE

### Running the system
gNB run instructions:
```bash
cd /mytempdata/openairinterface5g/cmake_targets/ran_build/build
sudo RFSIMULATOR=enb ./nr-softmodem -O ../../../targets/PROJECTS/GENERIC-LTE-EPC/CONF/gnb.band78.tm1.106PRB.usrpn300.conf --parallel-config PARALLEL_SINGLE_THREAD
```

UE run instructions:
```bash
cd /mytempdata/openairinterface5g/cmake_targets/ran_build/build
sudo RFSIMULATOR=`getent hosts node0 | awk '{print $1}'` ./nr-uesoftmodem --numerology 1 -r 106 -C 3510000000 -E -d
```
OR using NoVNC for GUI:
```bash
/share/powder/runvnc.sh
```

