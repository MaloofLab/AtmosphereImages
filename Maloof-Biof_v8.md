# Installation notes for Maloof-Biof v8

## start with image "Ubuntu 12.04 Xfce GUI v2"

### General installs 

    apt-get update
    apt-get upgrade
    apt-get install locate
    updatedb
    apt-get install mosh
    apt-get install htop
    apt-get install python3-all --install-suggests
    apt-get install python3-numpy python3-scipy
    apt-get install python3-dev python-dev python-numpy python-scipy python-support
    apt-get install python-pip
    wget http://biopython.org/DIST/biopython-1.61.tar.gz
    tar -xvzf biopython-1.61.tar.gz
    cd biopython-1.61/
    python setup.py build
    python setup.py test
    python setup.py install #installs for 2.7
    python3 setup.py build
    python3 setup.py test
    python3 setup.py install #installs for 3.2
    apt-get install bioperl
    #note this installed lots of bioinf packages including bwa, bowtie, hmmer, miscule, mafft, tcoffee, and much more
    apt-get install openmpi-dev libopenmpi-dev
    apt-get install ncbi-blast+ ncbi-blast+-legacy
    apt-get install mysql-client mysql-server #password = "34..." with first letters capitilized
    apt-get install eclipse
    apt-get install picard-tools
    apt-get install velvet velvet-example
    apt-get install libcurl3-dev #needed for bioconductor 
    apt-get install libxml2-dev #needed for biocondcutor
    apt-get install libgl1-mesa-dev #for rgl
    apt-get install libglu1-mesa-dev #for rgl
    apt-get install libmysqlclient-dev #for R mysql
    apt-get install git
    
### R
see CRAN
    add the line below to /etc/apt/sources.list
    	deb http://cran.cnr.Berkeley.edu/bin/linux/ubuntu precise/
    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9
    apt-get update
    apt-get install r-base r-base-dev #only 2.15.3 for now
3.0 should be available soon, see [post](http://www.personal.psu.edu/mar36/blogs/the_ubuntu_r_blog/2013/03/moving-to-r-300-on-ubuntu.html)

#### From within R:
	source("http://bioconductor.org/biocLite.R")
	biocLite()

I am lazy so just throwing whole library list from MaloofBionfV6 at biocList().

	biocLite(c('dichromat', 'ggplot2', 'gtable', 'labeling', 'memoise', 'munsell', 'scales', 'AnnotationDbi', 'BSgenome', 'BayesPeak', 'BiasedUrn', 'Biobase', 'BiocInstaller', 'Biostrings', 'Category', 'DBI', ,'DESeq', 'DynDoc', 'EBarrays', 'GO.db', 'GOstats', 'GSEABase', 'GenomicFeatures', 'GenomicRanges', 'IRanges', 'KEGG.db', 'KernSmooth', 'MASS', 'Matrix', 'RBGL', 'RColorBrewer', 'RCurl', 'RMySQL', 'RSQLite', 'RankProd', 'Rcpp', 'Rmpi', 'Rsamtools', 'ShortRead', 'TreeSim', 'VennDiagram', 'XML', 'affy', 'affyPLM', 'affyQCReport', 'affydata', 'affyio', 'annaffy', 'annotate', 'ape', 'arabidopsis.db0', 'ath1121501.db', 'baySeq', 'biomaRt', 'bitops', 'caTools', 'colorspace', 'cosmo', 'digest', 'doMC', 'edgeR', 'fdrtool', 'foreach', 'foreign', 'gcrma', 'gee', 'geiger', 'genefilter', 'geneplotter', 'ggplot2', 'goseq',  'hgu95av2.db', 'hopach', 'hwriter', 'igraph', 'iterators', 'itertools', 'lattice', 'latticeExtra', 'limma', 'lme4', 'marray', 'mgcv', 'msm', 'multicore', 'multtest', 'mvtnorm', 'nlme', 'nnet', 'org.At.tair.db', 'ouch', 'phangorn', 'phylobase', 'plyr', 'pmc', 'preprocessCore', 'proto', 'qtl', 'quadprog', 'qvalue', 'reshape', 'reshape2', 'rpart', 'rpvm', 'rtracklayer', 'seqLogo', 'seqinr', 'simpleaffy', 'snow', 'snowFT', 'snowfall', 'stringr', 'subplex', 'vsn', 'xtable', 'zlibbioc', 'manipulate'))  

> warnings()
Warning messages:
1: packages  cosmo,  pmc, rpvm, , manipulate are not available (for R version 2.15.3)

pmc seems to be a temporary removal, I think the others are really gone.
	install.packages("genetics")
	


### R Studio Server
 	sudo apt-get install gdebi-core
 	sudo apt-get install libapparmor1  # Required only for Ubuntu, not Debian
 	wget http://download2.rstudio.org/rstudio-server-0.97.449-amd64.deb
	gdebi rstudio-server-0.97.449-amd64.deb
	
### BWA
the installed BWA is out of date

    apt-get remove bwa

downloaded bwa 0.7.4 from source forge into /usr/local/src

    bunzip2 bwa-0.7.4.tar.bz2
    tar -xvf bwa-0.7.4.tar
    cd bwa-0.7.4/
    make
    cd ../
    ln -s /usr/local/src/bwa-0.7.4 /usr/local/src/bwa
    ln -sf /usr/local/src/bwa/bwa /usr/local/bin/bwa
    ln -sf /usr/local/src/bwa/bwa.1 /usr/local/share/man/man1/
    
### bowtie

the installed bowtie is out of date

    apt-get remove bowtie

 downloaded bowtie 1.0.0 from source forge

    mv bowtie-1.0.0-linux-x86_64.zip /usr/local/src
    cd /usr/local/src
    unzip bowtie-1.0.0-linux-x86_64.zip
    cd bowtie-1.0.0/
    chmod -R o+r *
    chmod  o+x bowtie
    ln -s bowtie-1.0.0/ bowtie
    cd /usr/local/bin
    cp -sf ../src/bowtie/bowtie ./
    
### bowtie2
downloaded from http://www.broadinstitute.org/software/igv/download

    mv ~/Downloads/bowtie2-2.1.0-linux-x86_64.zip ./
    unzip bowtie2-2.1.0-linux-x86_64.zip
    ln -s bowtie2-2.1.0/ bowtie2
    cd /usr/local/bin
    cp -sf ../src/bowtie2/bowtie2* ./
    
### blat
    cd /usr/local/bin
    wget http://hgdownload.cse.ucsc.edu/admin/exe/linux.x86_64/blat/blat
    chmod 0755 blat

### cufflinks
    cd /usr/local/src
    wget http://cufflinks.cbcb.umd.edu/downloads/cufflinks-2.1.1.Linux_x86_64.tar.gz
    tar -xvzf cufflinks-2.1.1.Linux_x86_64.tar.gz
    cd /usr/local/bin
    cp -sf /usr/local/src/cufflinks/cuff* ./
    cp -sf /usr/local/src/cufflinks/g* ./
    	
### FastQC
    wget http://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.10.1.zip
    unzip fastqc_v0.10.1.zip
    cd FastQC/
    chmod 0755 fastqc
    cd /usr/local/bin
    cp -s ../src/FastQC/fastqc ./
    
### GATK
Download from http://www.broadinstitute.org/gatk/

    mv GenomeAnalysisTK-2.5-2.tar.bz2 /usr/local/src
    cd /usr/local/src
    bunzip2 GenomeAnalysisTK-2.5-2.tar.bz2
    tar -xvf GenomeAnalysisTK-2.5-2.tar
    ln -s 
    cd /usr/local/bin/
    cp -sf ../src/GenomeAnalysisTK/GenomeAnalysisTK.jar ./
        
must start with:
    
    java -jar GenomeAnalysisTK.jar
    
### IGV
    wget http://www.broadinstitute.org/igv/projects/downloads/IGV_2.3.6.zip
    unzip IGV_2.3.6.zip
    ln -s IGV_2.3.6 IGV
    cd /usr/local/bin
    cp -sf ../src/IGV/igv.sh ./
    cp -sf ../src/IGV/igv.jar ./
    
### lastz
      wget http://www.bx.psu.edu/miller_lab/dist/lastz-1.02.00.tar.gz
      tar -xvzf lastz-1.02.00.tar.gz
      cd lastz-distrib-1.02.00/
      
edit make-include.mak  to set LASTZ_INSTALL="/usr/local/src/lastz-distrib-1.02.00/bin/"
edit src/Makefile to remove -Werror compile flag

     make
     make install
     cd /usr/local/bin
     ls
     cp -s ../src/lastz-distrib-1.02.00/bin/lastz* ./
    
### orthomcl
	apt-get install mcl
	wget http://orthomcl.org/common/downloads/software/v2.0/orthomclSoftware-v2.0.8.tar.gz

*incomplete*

### tophat
    wget http://tophat.cbcb.umd.edu/downloads/tophat-2.0.8b.Linux_x86_64.tar.gz
    tar -xvzf tophat-2.0.8b.Linux_x86_64.tar.gz
    ln -s tophat-2.0.8b.Linux_x86_64 tophat
    cd /usr/local/bin
    cp -sf ../src/tophat-2.0.8b.Linux_x86_64/* ./
    rm AUTHORS COPYING README

### cap3
      wget http://seq.cs.iastate.edu/CAP3/cap3.linux.i686_xeon64.tar
      tar -xvf cap3.linux.i686_xeon64.tar
      cd /usr/local/bin
      cp -s ../src/CAP3/cap3 ./
      cp -s ../src/CAP3/formcon ./
      
### varscan
download from http://sourceforge.net/projects/varscan/files/
copy into usr/local/bin
needs to be run with:

    java -jar VarScan.v2.3.5.jar mpileup2snp
    
### satsuma
    wget http://www.broadinstitute.org/ftp/distribution/software/spines/satsuma-2.0.tar.gz
    tar -xvzf satsuma-2.0.tar.gz
    cd satsuma-2.0/
    make

doesn't work when linked from /usr/local/bin
added /usr/local/src/satsuma-2.0 to PATH in /etc/environment

### SmartGit
downloaded from website and unpacked in /usr/local/src
Create desktop launcher 

### Desktop Aliases
create on local desktop,
then copy to /etc/skel/Desktop
image icons can go in /usr/share/pixmaps

### augustus
    wget http://bioinf.uni-greifswald.de/augustus/binaries/augustus.2.7.tar.gz
    tar -xvzf augustus.2.7.tar.gz
    cd augustus.2.7/
    make
    ln -s augustus.2.7 augustus
    cd /usr/local/bin
    cp -sf /usr/local/src/augustus/bin/* ./

### circos
    wget http://circos.ca/distribution/circos-0.64.tgz
    tar -xvzf circos-0.64.
    cd circos-0.64/bin
    ./test.modules
    cpan Config::General
    cpan Font::TTF::Font
    cpan Math::Round Math::VecStat
    cpan Readonly
    cpan Regexp::Common Text::Format

Add /usr/local/src/circos-0.64/bin to path in /etc/environment

### SVDetect
Download from sourceforge

    cpan Tie::IxHash
    cpan Parallel::ForkManager
    mv ~/Downloads/SVDetect_r0.7m.tar.gz ./
    tar -xvzf SVDetect_r0.7m.tar.gz
    ln -s SVDetect_r0.7m SVDetect
    cd /usr/local/bin
    cp -sf ../src/SVDetect/bin/SVDetect ./

### update R to 3.0
    apt-get update
    apt-get upgrade #might as well do the whole thing

within R:

    update.packages(ask=F,checkbuilt=T) 
    source("http://bioconductor.org/biocLite.R")
    biocLite()             # now updates installed...
    biocValid()            # also useful

## Dan Fulop Stuff

### Stan:

    wget https://stan.googlecode.com/files/stan-src-1.3.0.tgz   458  tar -xvzf stan-src-1.3.0.tgz
    cd stan-src-1.3.0/ 
    make bin/libstan.a
    make bin/stanc

### DanF R list

    install.packages(c("RStan", "ape", "geiger", "phytools", "picante", "vegan", "phylobase", "pmc", "coefplot2", "bbmle", "rethinking", "MCMCglmm", "blme", "caper", "baySeq", "QuasiSeq", "ouch", "scaleboot", "OUwie", "surface", "gpairs", "GGally", "geomorph", "phyloclim", "spider", "adephylo", "treebase", "phylolm", "gee", "gam", "mgcv", "gammSlice", "nlme", "lme4", "glmer2stan", "rbugs", "coda", "DPpackage", "pvclust"))

The following need to be done separately:
RStan, pmc, coefplot2, rethinking, baySeq, glmer2stan

    biocLite("baySeq")
    #pmc has been removed from CRAN so not installed
    install.packages("coefplot2",repos="http://r-forge.r-project.org/")
    #not available for R 3.0.1

    options(repos=c(getOption('repos'), rethinking='http://xcelab.net/R'))
    install.packages('rethinking',type='source',dependencies='Depends')

    options(repos=c(getOption('repos'), glmer2stan='http://xcelab.net/R'))
    install.packages('glmer2stan',type='source',dependencies='Depends')

    options(repos = c(getOption("repos"), rstan = "http://wiki.stan.googlecode.com/git/R"))
    install.packages('rstan', type = 'source')

#### coefplot2
in bash:

    svn checkout svn://scm.r-forge.r-project.org/svnroot/coefplot2/
    R CMD INSTALL coefplot2/pkg/

### dendropy
    pip install dendropy

### ipython
    apt-get install ipython-notebook

### BEAST
    cd /usr/local/src
    wget http://beast-mcmc.googlecode.com/files/BEASTv1.7.5.tgz
    tar -xvzf BEASTv1.7.5.tgz
    ln -s BEASTv1.7.5 BEAST
    cd /usr/local/bin
    cp -sf ../src/BEAST/bin/* ./

### bali-phy
    apt-get install libgsl0ldbl
    cd /usr/local/src
    mkdir bali-phy-2.1.1
    cd bali-phy-2.1.1
    wget http://faculty.biomath.ucla.edu/msuchard/bali-phy/bali-phy-2.1.1-linux64.tar.gz
    tar -xvzf bali-phy-2.1.1-linux64.tar.gz
    cd /usr/local/src
    ln -s bali-phy-2.1.1 bali-phy
    cd /usr/local/bin
    cp -s ../src/bali-phy/bin/* ./

### raxml
    wget https://github.com/stamatak/standard-RAxML/archive/master.zip
    unzip master.zip
    cd standard-RAxML-master/
    make -f Makefile.SSE3.PTHREADS.gcc
    rm *.o
    cd /usr/local/bin
    cp -s ../src/standard-RAxML-master/raxmlHPC-PTHREADS-SSE3 ./

### garli (not working)
    cd /usr/local/src
    wget https://garli.googlecode.com/files/garli-2.0.tar.gz
    cd garli-2.0/
    ./build_garli.sh
 *FAIL*

### SPIMAP
    apt-get install libgsl0-dev
    wget http://compbio.mit.edu/spimap/pub/spimap-1.1.tar.gz
    cd spimap-1.1
    make
    make install prefix=/usr/local

### TreeFix
    apt-get install swig
    cd /usr/local/src
    wget http://compbio.mit.edu/treefix/pub/sw/treefix-1.1.7.tar.gz
    tar -xvzf treefix-1.1.7.tar.gz
    cd treefix-1.1.7/
    python setup.py build
    python setup.py install

### PrIME
    apt-get install libxml2 liblapack3gf libatlas3gf-base libgfortran3 libopenmpi1.3 libquadmath0 libstdc++6 libxerces-c3.1 zlib1g
    apt-get install libboost-mpi1.46.1 libboost-serialization1.46.1
    wget http://prime.sbc.su.se/download/ubuntu/amd64/12.04/prime-phylo_1.0.10-1_amd64.deb
    dpkg -i prime-phylo_1.0.10-1_amd64.deb

### bucky
    wget http://dstats.net/download/http://www.stat.wisc.edu/~ane/bucky/v1.4/bucky-1.4.2.tgz
    tar -xvzf bucky-1.4.2.tgz
    cd bucky-1.4.2/
    cd src
    make
    cd ../
    ln -s bucky-1.4.2 bucky
    cd /usr/local/bin
    cp -sf ../src/bucky/src/bucky ./
    cp -sf ../src/bucky/src/mbsum ./

### Threshml
    wget http://evolution.gs.washington.edu/phylip/download/threshml/threshml.zip
    unzip threshml.zip
    cd ../bin/
    cp -s ../src/threshml/threshml.linuxi64 ./threshml

### hyphy
    cd /usr/local/src
    git clone git://github.com/veg/hyphy.git
    apt-get install cmake
    cmake .
    make MP2
    make install

### prank (& exonerate & mafft)
    wget https://prank-msa.googlecode.com/files/prank.linux64.130410.tgz
    tar -xvzf prank.linux64.130410.tgz
    cd ../bin
    cp -s ../src/prank/bin/prank ./
    cp -s ../src/prank/bin/exonerate ./
    cp -s ../src/prank/bin/bppancestor ./
    cp -s ../src/prank/bin/mafft ./

### probalign
    apt-get probalign

### jalview
    apt-get jalview
And setup desktop launcher

### RevTrans
    cd /usr/local/src
    wget http://www.cbs.dtu.dk/services/RevTrans/releases/revtrans-1.4.tgz
    tar -xvzf revtrans-1.4.tgz
    cd ../bin
    cp -s ../src/RevTrans-1.4/*.py ./
edit beginning of .py files to change python location

### Dendroscope
    wget http://ab.inf.uni-tuebingen.de/data/software/dendroscope3/download/Dendroscope_unix_3_2_7.sh
    chmod 0777 Dendroscope_unix_3_2_7.sh
    ./Dendroscope_unix_3_2_7.sh

### BEAGLE
    sudo apt-get install build-essential autoconf automake libtool subversion pkg-config openjdk-6-jdk
    svn checkout http://beagle-lib.googlecode.com/svn/trunk/ beagle-lib
    cd beagle-lib
    ./autogen.sh
    ./configure --prefix=/usr/local
    make install

### Mr Bayes
    apt-get install mpi-default-bin
    autoconf
    ./configure --enable-mpi=yes

edit the Makefile as described [here](http://sourceforge.net/mailarchive/message.php?msg_id=29653672)
Also remove "-L/usr/local/lib" from LDFLAGS

(technically I think this is the wrong way to do it, but it works...)

    make
    cd /usr/local/bin
    cp -s ../src

## Mike

### Perlbrew

*Free up space by cleaning apt-get cache (disk space was nearly full from other installations):*

    sudo apt-get clean

*Install Perlbrew:*

    sudo mkdir /perlbrew
    sudo chown mfc /perlbrew/
    export PERLBREW_ROOT=/perlbrew
    curl -kL http://install.perlbrew.pl | bash

*Add to `/etc/bash.bashrc`:*

    # For Perlbrew (added by Mike Covington)
    export PATH=/perlbrew/bin:$PATH
    export PERLBREW_ROOT=/perlbrew
    source /perlbrew/etc/bashrc

*Install Perl:*

Perl 5.18.0 just came out, but there are some hash-related changes that may break some modules; therefore, will install 5.16.3 for now.

    perlbrew install perl-5.16.3
    perlbrew switch perl-5.16.3
    perlbrew install-cpanm

*Install Perl modules:*

    cpanm --sudo Modern::Perl
    cpanm --sudo DateTime
    cpanm --sudo Data::Printer
    cpanm --sudo Moose
    cpanm --sudo Statistics::R
    cpanm --sudo Parallel::ForkManager
    cpanm --sudo Perl::Tidy
    cpanm --sudo Perl::Critic
    cpanm --sudo Mojo
    cpanm --sudo URI
    cpanm --sudo Math::Random
    cpanm --sudo Image::ExifTool
    cpanm --sudo Statistics::Descriptive
    cpanm --sudo Text::Table

*Installing DB_File:*

    sudo apt-get install libdb4.8-dev
    cpanm --sudo DB_File

/usr/bin/samtools

*Installing BioPerl:*

Keep getting errors related to 'Failed to upconvert metadata to 1.3.'; therfore, updated `CPAN::Meta::Converter`, but still get errors.

    cpanm --sudo CPAN::Meta::Converter

Figured out that `cpanm` was trying to install an OLD version of BioPerl. This was successful:

    wget http://www.cpan.org/authors/id/C/CJ/CJFIELDS/BioPerl-1.6.901.tar.gz
    cpanm --sudo BioPerl-1.6.901.tar.gz

*Install Bio::DB::Sam:*

Need a built-from-source copy of samtools. Samtools 0.1.19 just came out a couple weeks ago, but I'm going to use 0.1.18, since that is the version that was installed (by Rsamtools?) and is the version I've been using for genotyping. I'm not yet sure what has changed between the versions.

    cd /usr/local/src/
    sudo wget http://downloads.sourceforge.net/project/samtools/samtools/0.1.18/samtools-0.1.18.tar.bz2
    sudo tar -xjf samtools-0.1.18.tar.bz2 
    cd samtools-0.1.18/
    sudo make CXXFLAGS=-fPIC CFLAGS=-fPIC CPPFLAGS=-fPIC

    cpanm --sudo Bio::DB::Sam

At `Please enter the location of the bam.h and compiled libbam.a files:`prompt, enter: `/usr/local/src/samtools-0.1.18`


*Install vcftools and tabix (and Vcf.pm)*

    cd /usr/local/src/
    sudo wget http://downloads.sourceforge.net/project/vcftools/vcftools_0.1.10.tar.gz
    sudo tar -xzf vcftools_0.1.10.tar.gz
    sudo chmod -R 755 vcftools_0.1.10
    cd vcftools_0.1.10/
    sudo make
    cd /usr/local/bin/
    for i in ../src/vcftools_0.1.10/bin/*; su do echo $i; ln -s $i; done

    cd /usr/local/src/
    sudo wget http://downloads.sourceforge.net/project/samtools/tabix/tabix-0.2.6.tar.bz2
    sudo tar -xjf tabix-0.2.6.tar.bz2
    sudo chmod -R 755 tabix-0.2.6
    cd tabix-0.2.6/
    sudo make
    cd /usr/local/bin/
    sudo ln -s ../src/tabix-0.2.6/tabix
    sudo ln -s ../src/tabix-0.2.6/bgzip

Add to `/etc/bash.bashrc`:

    # For vcftools
        export PERL5LIB=/usr/local/src/vcftools_0.1.10/perl:/usr/local/src/tabix-0.2.6/perl



#To Do

* SnpEff


need to set better default key for right-click
