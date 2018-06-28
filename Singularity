Bootstrap: yum
OSVersion: 7
MirrorURL: http://mirror.centos.org/centos-%{OSVERSION}/%{OSVERSION}/os/$basearch/
Include: yum


%files
	hdf5-1.10.2.tar.gz ~/hdf5

%post
	
	mkdir openmpi
	cd openmpi
	wget https://www.open-mpi.org/software/ompi/v3.0/downloads/openmpi-3.0.0.tar.bz2
	tar xvf openmpi-3.0.0.tar.bz2
	mv openmpi-3.0.0 openmpi-3.0.0_src
	cd openmpi-3.0.0_src
	./configure --prefix=~/usr/local
	make all install
	export PATH=~/usr/local/bin:$PATH
	export LD_LIBRARY_PATH=~/usr/local/lib:$LD_LIBRARY_PATH
	cd ..

  #szip
	mkdir szip && cd szip
	curl -O https://support.hdfgroup.org/ftp/lib...p-2.1.1.tar.gz
	tar xvf szip-2.1.1.tar.gz
	mv szip-2.1.1 szip-2.1.1_src
	cd szip-2.1.1_src
	./configure prefix=~/usr/local
	make
	make check
	make install
	export LD_LIBRARY_PATH=~/usr/local/lib:$LD_LIBRARY_PATH
	cd ..

  #zlib
	mkdir zlib && cd zlib
	wget --no-check-certificate https://zlib.net/zlib-1.2.11.tar.gz
	tar xvf zlib-1.2.11.tar.gz
	mv zlib-1.2.11 zlib-1.2.11_src
	cd zlib-1.2.11_src
	./configure --prefix=~/usr/local
	make test
	make install 
	export LD_LIBRARY_PATH=~/usr/local/lib:$LD_LIBRARY_PATH
	cd ..

  #hdf5
	mkdir ~/hdf5 && cd ~/hdf5
	tar xvf hdf5-1.10.1.tar.gz
	3mv hdf5-1.10.1 hdf5-1.10.1_src
	cd hdf5-1.10.1_src
	CC=mpicc ./configure --prefix=~/usr/local --enable-optimization=high --enable-parallel --with-zlib=~/usr/local/include,~/usr/local/lib --with-szlib=~/usr/local/lib
	make
	make -i check
	make install
	make check-install
	export LD_LIBRARY_PATH=~/usr/local/lib:$LD_LIBRARY_PATH
   #lapack	
	sudo yum install openblas 
   #SU2
	wget https://github.com/su2code/SU2/archive/v6.1.0.tar.gz
	tar -xvzf v6.1.0.tar.gz
	cd SU2-6.1.0
	./configure --prefix=~/usr/local CXXFLAGS="-O3" --enable-mpi --with-cc=mpicc --with-cxx=mpicxx  --with-HDF5-lib=~/usr/local/lib --with-HDF5-include=~/usr/local/include --with-ZLIB-lib=~/usr/local/lib --with-ZLIB-include=~/usr/local/include --with-SZIP-lib=~/usr/local/lib --with-SZIP-include=~/usr/local/include --with-LAPACK-lib=~/usr/local/lib --with-LAPACK-include=~/usr/local/include
	make
	make install
	which SU2_CFD	
%environment

export PATH=~/usr/local/bin:$PATH
export LD_LIBRARY_PATH=~/usr/local/lib:$LD_LIBRARY_PATH
export INCLUDE_PATH=~/usr/local/include:$LD_INCLUDE_PATH
