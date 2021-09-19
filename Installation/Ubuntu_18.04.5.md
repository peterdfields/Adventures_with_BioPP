# Details for setting up BioPP on an Ubuntu 18.04 environment
#### GCC v.7.5.0
#### CMake v.3.10.2
#### GLIBC 2.27

##### Let's setup some environmental variables
`bpp_dir=$HOME/popgen/bpp; mkdir -p $bpp_dir/sources`

##### Let's pull the sources for each of the libraries
```
cd $bpp_dir/sources
git clone https://github.com/BioPP/bpp-core
git clone https://github.com/BioPP/bpp-seq
git clone https://github.com/BioPP/bpp-popgen
git clone https://github.com/BioPP/bpp-phyl
```

##### Now we need to do the build the individual libraries in a non-standard (non-default) location; NOTE: you need to start with bpp-core, then bpp-seq, and the order of the last two doesn't matter.

```
# bpp-core
cd bpp-core
mkdir build
cd build
cmake -DCMAKE_INSTALL_PREFIX=$bpp_dir ..
make -j 4
make install
```

```
# bpp-seq
cd ../../bpp-seq/
mkdir build
cd build
cmake -DCMAKE_INSTALL_PREFIX=$bpp_dir ..
make -j 12
make install
```

```
# bpp-phyl
cd ../../bpp-phyl/
mkdir build
cd build
cmake -DCMAKE_INSTALL_PREFIX=$bpp_dir ..
make -j 12
make install
```

```
# bpp-popgen
cd ../../bpp-popgen/
mkdir build
cd build
cmake -DCMAKE_INSTALL_PREFIX=$bpp_dir ..
make -j 12
make install
```

##### That's basically it! An idiosyncrasy I found when I built the example files is that the addition of modifications to .bashrc to setup linkers isn't necessary, though they are actually placed under .local. I'll add more about this in other environment setups and link back.
##### Let's test it out!

```
git clone https://github.com/BioPP/bpp-seq-example.git
cd bpp-seq-example
make
```
##### Look for errors, rinse, repeat
