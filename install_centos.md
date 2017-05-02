# Instructions to install run sample (example) opendnp app on centos

## Installing Stuff
```
sudo yum install -y wget git boost.x86_64 cmake
sudo yum group install "Development Tools"
sudo yum install -y centos-release-scl-rh
sudo yum install -y devtoolset-3-gcc devtoolset-3-gcc-c++
sudo yum install -y java-1.8.0-openjdk-devel.x86_64
sudo yum install -y openssl-devel.x86_64 openssl.x86_64



/opt/rh/devtoolset-3/root/usr/bin/g++ --version
vi ~/.bashrc 
	#-- ADD FOLLOWING LINES 
	PATH=/opt/rh/devtoolset-3/root/usr/bin/:$PATH
	export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.131-2.b11.el7_3.x86_64
	
export CC=/opt/rh/devtoolset-3/root/usr/bin/gcc
export CXX=/opt/rh/devtoolset-3/root/usr/bin/g++

cd
wget http://mirrors.gigenet.com/apache/maven/maven-3/3.5.0/binaries/apache-maven-3.5.0-bin.tar.gz
tar xvf apache-maven-3.5.0-bin.tar.gz 
mv apache-maven-3.5.0  /usr/local/apache-maven
vi .bashrc
	#-- ADD FOLLOWING LINES
	export M2_HOME=/usr/local/apache-maven
	export M2=$M2_HOME/bin
	export PATH=$M2:$PATH
 
. ~/.bashrc


cd
git clone --recursive https://github.com/automatak/dnp3.git
cd ./dnp3
cmake -DCMAKE_C_COMPILER="/opt/rh/devtoolset-3/root/usr/bin/gcc"  -DCMAKE_CXX_COMPILER="/opt/rh/devtoolset-3/root/usr/bin/g++" ../dnp3 -DDNP3_ALL=ON -Wno-dev
make -j
sudo make install 
cd java
mvn install
```

# Running Demo

## Running Master

```
java -Djava.library.path="/root/dnp3" -cp ./:./opendnp3-example-2.2.0-SNAPSHOT.jar:./lib/opendnp3-bindings-2.2.0-SNAPSHOT.jar:./lib/opendnp3-codegen-2.2.0-SNAPSHOT.jar com.automatak.dnp3.example.MasterDemo
```


## Running Outstation

```
java -Djava.library.path="/root/dnp3" -cp ./:./opendnp3-example-2.2.0-SNAPSHOT.jar:./lib/opendnp3-bindings-2.2.0-SNAPSHOT.jar:./lib/opendnp3-codegen-2.2.0-SNAPSHOT.jar com.automatak.dnp3.example.OutstationDemo
```
