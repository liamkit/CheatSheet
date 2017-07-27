This note describes how to install libreoffice to ubuntu 10. I don't really need full
working version of libreoffice, just enough to run in batch mode to convert xls and
xlsx to csv.

# Perl

I also need perl. Instead of using the vanilla version of perl from ubuntu 10, I build it from source
and install under /opt/perl5. You can find the tarball at <http://www.cpan.org/src/5.0/perl-5.24.1-RC3.tar.gz>.

	1. download tarball
	2. zcat perl-5.24.1-RC3.tar.gz
	3. cd perl-5.24.1-RC3
	4. ./Configure -des -Dprefix=/opt/perl5
	5. make
	6. make test
	7. make install
	8. PATH=/opt/perl5/bin:${PATH}

Also http://www.cpan.org/src/

# Perl Modules

I need to use perl to transfer and decrypt files. I am adding in a few perl modules

	1. apt-get install libgmp3-dev haveged
	2. cpan CPAN (need to update to the latest)
	3. cpan Log::Log4perl
	4. cpan Archive::Zip
	5. cpan Net::SFTP
	6. cpan Spreadsheet::ParseExcel
	7. cpan Crypt::GPG
	8. cpan MIME::Parser (have to force since one test fails)
	9. cpan Text::CSV

libgmp3-dev is for doing long integer arithemetics and haveged is for fast generating random number entropy used by GPG.

# CoreUitls

libreoffice needs an updated touch program. This is only needed to build and not deploy. I install
all build only binaries under /opt/tool. You can find the tarball at 
<http://ftp.gnu.org/gnu/coreutils/coreutils-8.24.tar.xz> 

	1. download tarball
	2. xzcat coreutils-8.24.tar.xz
	3. cd coreutils-8.24
	4. ./configure --prefix=/opt/tool
	5. make
	6. make install

# GNU make

To take advantage of parallel make, you'll need an updated version of gnumake. You can get the tarball
at <http://ftp.gnu.org/gnu/make/make-4.2.tar.gz>

	1. download tarball
	2. zcat make-4.2.tar.gz
	3. cd make-4.2
	4. ./configure --prefix=/opt/tool
	5. make
	6. make install

# more packages

To build libreoffice, a bunch of ubuntu packages are needed. If you don't install them, autogen/configure will fail 
and tell you which package to install. 

	1. apt-get install autoconf pkg-config libfontconfig-dev gperf libjpeg-dev libxslt-dev xsltproc libxml2-utils libxext-dev libxt-dev libxrender-dev bison flex libgtk2.0-dev libgconf2-dev zip


# ccache

If you have to run make to build libreoffice more than once, you should use ccache. libreoffice takes forever to build and adding
ccache speeds things up a lot if you have to rebuild it.

	1. apt-get install ccache
	2. ccache --max-size 20G
	3. export CCACHE_COMPRESS=1

# libreoffice

Finally, build the libreoffice.

	1. git clone --depth 50 git://anongit.freedesktop.org/libreoffice/core soffice
	2. cd soffice
	3. git checkout -b 4.2.8.2 libreoffice-4.2.8.2
	4. PATH=/opt/perl5/bin:/opt/tool/bin:${PATH}
	5. export CCACHE_COMPRESS=1
	6. ./autogen.sh --prefix=/opt/soffice --without-java --without-help --without-myspell-dicts --disable-dbus --disable-opengl --disable-cups --disable-python --disable-postgresql-sdbc --disable-gstreamer-0-10 --disable-firebird-sdbc --disable-cairo-canvas --without-ppds --disable-pdfimport --without-afms --with-parallelism 
	7. make
	8. make install

Also https://wiki.documentfoundation.org/Development/BuildingOnLinux
