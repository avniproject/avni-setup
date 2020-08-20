## Set up avni environment using Docker Compose

Docker compose requires docker engine to be installed in your machine. So install docker engine from [here](https://docs.docker.com/engine/install/#server), 
then you need to install docker compose from [here](https://docs.docker.com/compose/install/). We'll also need VNC to view the emulator,
you can download VNC server from [here](https://www.realvnc.com/en/connect/download/vnc/).

#### Steps to setup Avni
- Clone this repository and `cd avni-setup`. 
- Once you are inside `avni-setup`, run `docker-compose up` to start `avni-server`, `avni-webapp` and `avni-client`. 
- You can see the console logs and when it says app installed then you can start vnc server and connect to `localhost:5901` to access the android emulator. 
- You can access webapp by accessing `localhost:8021` on your browser. 
- Create an organisation and one use to test it out. 
- Next go to the emulator, `avi` is pre-installed and you can login using the user you just created. 
- For connecting to the db you can use `jdbc:postgresql://localhost:5434/openchs` url.


#### Enable hardware virtualization
Before running the emulator please make sure that hardware virtualization is enabled you can follow the steps given
[here](https://2nwiki.2n.cz/pages/viewpage.action?pageId=75202968). Also `kvm` should be installed in the host machine,
you can verify it by executing `kvm-ok` command and it should return 

````
INFO: /dev/kvm exists
KVM acceleration can be used
````

#### Workaround for the device not supporting virtualization
If your device doesn't support hardware virtualization, then you can use arm based avd. To install `avd` ssh into
`avni-app` container run `docker exec -it avni-app bash`.

Once inside the container run `sdkmanager --install "system-images;android-25;google_apis;armeabi-v7a"`.

Next you need to create avd so run `echo "no" | avdmanager create avd --force --name test -k "system-images;android-25;google_apis;armeabi-v7a"`.

After this execute the `emulator.sh` script located under `/tmp` folder.
