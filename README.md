# ECDSA-OpenCL

This library is a fork of Sipa's Secp256k1 library, currently in use for Bitcoin.
The change we made here is the signature verification unit, we re-wrote it in OpenCL in order for it to be run on a GPU and thus to accelerate signature verification for a Bitcoin block, we wrote the kernel call as well.
The choice of OpenCL as a programming language was to have it run on a wider range of GPUs (unlike with company-owned programming language for GPUs).

We've  changed `secp256k1-ocl/src/tests.c` and we've created `secp256k1-ocl/src/k.cl` 


## Compilation
To compile it:

1.Clone the Git directory.


2.Go inside `secp256k1-ocl/` dir :

run

``` sh
chmod u+x *
./autogen.sh 
./configure
make
./tests
```
### Set OpenCL Environment 
On Linux, in order to set an OpenCL environment, if you haven't done so before, you must run the following steps:
``` sh
export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/usr/local/cuda/lib64
export LD_LIBRARY_PATH=/usr/lib/x86_64-linux-gnu/lib:$LD_LIBRARY_PATH
export C_INCLUDE_PATH=/usr/local/cuda/include
```
And then, run:

`ldconfig`

### Signatures Number
To change the number of signatures that are beig verified, modify in `secp256k1-ocl/src/test.c` the `NUM_OF_SIGS` Define.

### Results
for 100,000+ signatures the GPU run is x25 faster than the CPU run

STATUS: In a near futur, we're going to integrate this library to the Bitcoin-Core.

## Copyright
Copyright Ilay Chen & Yakir Fenton, March 30th 2020.
