# reference: http://xinu.mscs.mu.edu/Build_Xinu#Cross-Compiler

git clone git@github.com:xinu-os/xinu.git

mipsel_dev=/usr/local/cross-compile/mipsel_dev
# Build cross compiler
curl http://ftp.gnu.org/gnu/binutils/binutils-2.24.tar.gz -o binutils-2.24.tar.gz
./configure --prefix=$mipsel_dev --target=mipsel
make
make install


mkdir -p $mipsel_dev/mipsel/usr
ln -s /usr/include $mipsel_dev/mipsel/usr/include

# download gcc
curl http://ftp.tsukuba.wide.ad.jp/software/gcc/releases/gcc-4.8.2/gcc-4.8.2.tar.gz -o gcc-4.8.2.tar.gz

# building the source directory of gcc is one of the least tested feature.
../configure \
	--prefix=$mipsel_dev \
	--target=mipsel \
	--enable-languages=c \
	--without-headers \
	--disable-intl \
    --disable-libssp
make
make install
