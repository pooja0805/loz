# Building Apache Pulsar

The instructions provided below specify the steps to build Apache Pulsar version 2.10.1 on Linux on IBM Z for the following distributions:

* RHEL (8.6, 9.0)
* Ubuntu (18.04, 20.04, 22.04)

### _General Notes_ :

* _When following the steps below please use a standard permission user unless otherwise specified.
* _A directory /<source_root>/ will be referred to in these instructions, this is a temporary writable directory anywhere you'd like to place it.

## Step 1: Build and Install Apache Pulsar

### 1.1) Build using script
* _If you want to build Pulsar using manual steps, go to STEP 1.2.
* _Use the following commands to build Pulsar using the build script. Please make sure you have wget installed.

### If the build completes successfully, go to STEP 3. In case of error, check logs for more details or go to STEP 1.2 to follow manual build steps.

### 1.2) Install dependencies

    export SOURCE_ROOT=/<source_root>/

* RHEL
    ```
    yum install -y sudo git vim nano curl zip unzip tar wget 
    ```
* Ubuntu
  ```
  apt update && apt upgrade -y
  apt install -y sudo git vim nano curl zip unzip tar wget
  ```

### 1.3) Install Java
* With OpenJDK 11

* RHEL (8.6, 9.0)
  ```
  sudo yum install -y java-11-openjdk-devel
  ```

* Ubuntu (18.04, 20.04, 22.04)
  ```
  sudo apt-get install -y openjdk-11-jdk
  ```

### 1.4) Set JAVA_HOME
 
    export JAVA_HOME=/<path to java>/
    export PATH=$JAVA_HOME/bin:$PATH

### 1.5) Install maven
  ```
  wget https://archive.apache.org/dist/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
  tar -xvzf apache-maven-3.6.3-bin.tar.gz
  export PATH=$PATH:$SOURCE_ROOT/apache-maven-3.6.3/bin/  
  ```

### 1.6) Install Protobuf
  
  * Ubuntu 18.04
    ```
    sudo apt-get update  
    sudo apt-get install -y autoconf automake g++-4.8 git gzip libtool make zlib1g-dev
    sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 10
    sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 10
    ```
  * GCC 4.9.4 (Only for RHEL 8.x and Ubuntu 20.x, above)
    ```
    sudo apt-get update
    sudo apt-get install -y autoconf automake bzip2 g++ git gzip libtool make tar wget zlib1g-dev
    cd $SOURCE_ROOT
    wget http://ftp.gnu.org/gnu/gcc/gcc-4.9.4/gcc-4.9.4.tar.gz
    tar xzf gcc-4.9.4.tar.gz
    cd gcc-4.9.4/
    ./contrib/download_prerequisites
    mkdir build
    cd build/
    ../configure --enable-shared --disable-multilib --enable-threads=posix --with-system-zlib --enable-languages=c,c++
    make -j 2       # Or a higher number for more parallelism
    sudo make install
    export PATH=/usr/local/bin:$PATH
    ```
  * Build and Install Protobuf
    ```
    cd $SOURCE_ROOT
    git clone https://github.com/protocolbuffers/protobuf.git
    cd protobuf
    git checkout v3.19.2
    git submodule update --init --recursive
    ./autogen.sh
    ./configure
    make -j 4
    sudo make install
    sudo ldconfig
    ```
### 1.7) Install grpc-java

  ```
  cd $SOURCE_ROOT/
  git clone https://github.com/grpc/grpc-java.git
  cd grpc-java
  git checkout v1.45.1
  cd compiler
  rm -rf check-artifact.sh
  wget https://raw.githubusercontent.com/haubenr/grpc-grpc-java/haubenr_add-s390x-support/compiler/check-artifact.sh
  
  (For RHEL Only)
    sed -i '69,69 s/$(s390x-linux-gnu-objdump -f "$1" | grep -o "file format .*$/elf64-s390"/g' check-artifact.sh
    sed -i '123d' check-artifact.sh
  
  cd ..
  ./gradlew build -PskipAndroid=true -PskipCodegen=true -x test
  ./gradlew publishToMavenLocal -PskipAndroid=true
  ```

### 1.8) Install netty-tcnative
  ```
  cd $SOURCE_ROOT/
  wget -q https://raw.githubusercontent.com/linux-on-ibm-z/scripts/master/netty-tcnative/2.0.52/build_netty.sh
  bash build_netty.sh -y  # Provide -j for java to use [Temurin11, OpenJDK11]
  ```

### 1.9) Download Pulsar

  ```
  cd $SOURCE_ROOT/
  git clone https://github.com/apache/pulsar.git
  cd pulsar
  git checkout v2.10.1
  sed -i 's/<rocksdb.version>6.10.2</rocksdb.version>/<rocksdb.version>6.29.5</rocksdb.version>/gI' pom.xml
  sed -i 's/<jna.version>4.2.0</jna.version>/<jna.version>5.12.0</jna.version>/gI' pom.xml
  sed -i 's/<surefire.version>3.0.0-M3</surefire.version>/<surefire.version>2.19.1</surefire.version>/gI' pom.xml
  sed -i 's/<snappy.version>1.1.7</snappy.version>/<snappy.version>1.1.8.4</snappy.version>/gI' pom.xml
  ```

### 1.10) Build
  ```
  cd $SOURCE_ROOT/pulsar
  mvn install -DskipTests
  ```

## Step 2: Run test suite 
    
    cd $SOURCE_ROOT/pulsar
    mvn test
    
## Step 3: Start Pulsar Standalone Service

    bin/pulsar standalone


