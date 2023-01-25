# CentOS python and pip upgrade
*use root user account!*
## Preparation
yum -y install epel-release <br />
yum -y update <br />
reboot <br />
yum groupinstall "Development Tools" -y <br />
yum install wget openssl-devel libffi-devel bzip2-devel zlib-devel -y <br />

## Choose /usr/src directory to do the manipulations with source code
cd /usr/src

## Get the opensll disrib 
wget https://www.openssl.org/source/openssl-1.1.1s.tar.gz --no-check-certificate <br />
tar -xzvf openssl-1.1.1s.tar.gz <br />
*or* <br />
curl https://www.openssl.org/source/openssl-1.1.1s.tar.gz | sudo tar xz

## Install perl ssl tests and ssl
cd openssl-1.1.1s <br />
yum install perl-CPAN <br />
cpan -i -f Test2 <br />
./config --prefix=/usr --openssldir=/etc/ssl --libdir=lib no-shared zlib-dynamic <br />
make <br />
make test <br />
make install <br />
*if something is wrong use make clean after* ./config command

## check ssl installed
openssl version <br />
OpenSSL 1.1.1s  1 Nov 2022 <br />
which openssl <br />
/bin/openssl <br />
cd ..

wget https://www.python.org/ftp/python/3.10.2/Python-3.10.2.tgz <br />
tar xvf Python-3.10.2.tgz <br />
*or* <br />
curl https://www.python.org/ftp/python/3.10.2/Python-3.10.2.tgz | sudo tar xz <br />
cd Python-3.10.2 <br />
./configure --enable-optimizations --with-openssl=/usr <br />
make altinstall <br />
python3.10 --version


## Check python and ssl:
python3.10 -c "import ssl; print(ssl.OPENSSL_VERSION)"

python3 -m pip install certifi

## Update the alternatives:
update-alternatives --install /usr/bin/python3 python3 /usr/local/bin/python3.10 2 <br />
ls -l /usr/bin/python3

which python3 <br />
/bin/python3 <br />
python3 --version <br />
Python 3.10.2

python3 -m pip install --upgrade pip <br />
python3 -m pip install requests

## Change to non-root user and check pip working:
python3 -m pip install --user ansible <br />
python3 -m pip install docker

ansible --version <br />
ansible-playbook --version
