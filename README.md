#start with image "Ubuntu 12.04 Xfce GUI v2"

    apt-get update
    apt-get upgrade
    apt-get install locate
    updatedb
    apt-get install mosh
    apt-get install htop
    apt-get install python3-all --install-suggests
    apt-get install python3-numpy puthon3-scipy
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
    apt-get install mrbayes mrbayes-mpi
    apt-get install mysql-client mysql-server #password = "34..." with first letters capitilized
    apt-get install eclipse
    apt-get install picard-tools
    apt-get install velvet velvet-example
    apt-get install libcurl3-dev #needed for bioconductor 
    apt-get install libxml2-dev #needed for biocondcutor
    apt-get install libgl1-mesa-dev #for rgl
    apt-get install libglu1-mesa-dev #for rgl
    apt-get install libmysqlclient-dev #for R mysql
    
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
    ln -s /usr/local/src/bwa-0.7.4/bwa /usr/local/bin/bwa
    ln -s /usr/local/src/bwa-0.7.4/bwa.1 /usr/local/share/man/man1/
    
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
    ln -s /usr/local/src/bowtie-1.0.0/bowtie /usr/local/bin/bowtie
    
### bowtie2
downloaded from http://www.broadinstitute.org/software/igv/download

    mv ~/Downloads/bowtie2-2.1.0-linux-x86_64.zip ./
    unzip bowtie2-2.1.0-linux-x86_64.zip
    cd /usr/local/bin
    cp -s ../src/bowtie2-2.1.0/bowtie2* ./
    
### blat
    cd /usr/local/bin
    wget http://hgdownload.cse.ucsc.edu/admin/exe/linux.x86_64/blat/blat
    chmod 0755 blat

### cufflinks
    cd /usr/local/src
    wget http://cufflinks.cbcb.umd.edu/downloads/cufflinks-2.1.1.Linux_x86_64.tar.gz
    tar -xvzf cufflinks-2.1.1.Linux_x86_64.tar.gz
    cd /usr/local/bin
    cp -s /usr/local/src/cufflinks-2.1.1.Linux_x86_64/cuff* ./
    cp -s /usr/local/src/cufflinks-2.1.1.Linux_x86_64/g* ./
    	
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
    cd /usr/local/bin/
    cp -s ../src/GenomeAnalysisTK-2.5-2-gf57256b/GenomeAnalysisTK.jar ./
    
must start with:
    
    java -jar GenomeAnalysisTK.jar
    
### IGV
    wget http://www.broadinstitute.org/igv/projects/downloads/IGV_2.3.6.zip
    unzip IGV_2.3.6.zip
    cd /usr/local/bin
    cp -s ../src/IGV_2.3.6/igv.sh ./
    cp -s ../src/IGV_2.3.6/igv.jar ./
    
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
     lastz
     history
    
### orthomcl
	apt-get install mcl
	wget http://orthomcl.org/common/downloads/software/v2.0/orthomclSoftware-v2.0.8.tar.gz

*incomplete*

### tophat
    wget http://tophat.cbcb.umd.edu/downloads/tophat-2.0.8b.Linux_x86_64.tar.gz
    tar -xvzf tophat-2.0.8b.Linux_x86_64.tar.gz
    cd /usr/local/bin
    cp -s ../src/tophat-2.0.8b.Linux_x86_64/* ./
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

### Desktop Aliases
create on local desktop,
then copy to /etc/skel/Desktop

### augustus
    wget http://bioinf.uni-greifswald.de/augustus/binaries/augustus.2.7.tar.gz
    tar -xvzf augustus.2.7.tar.gz
    cd augustus.2.7/
    make
    cd /usr/local/bin
    cp -s /usr/local/src/augustus.2.7/bin/* ./

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
    cd /usr/local/bin
    cp -s ../src/SVDetect_r0.7m/bin/SVDetect ./

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

### dendropy
    pip install dendropy

### ipython
    apt-get install ipython-notebook

### BEAST
    cd /usr/local/src
    wget http://beast-mcmc.googlecode.com/files/BEASTv1.7.5.tgz
    tar -xvzf BEASTv1.7.5.tgz
    cd /usr/local/bin
    cp -s ../src/BEASTv1.7.5/bin/* ./

### bali-phy
    apt-get install libgsl0ldbl
    cd /usr/local/src
    mkdir bali-phy-2.1.1
    cd bali-phy-2.1.1
    wget http://faculty.biomath.ucla.edu/msuchard/bali-phy/bali-phy-2.1.1-linux64.tar.gz
    tar -xvzf bali-phy-2.1.1-linux64.tar.gz
    cd /usr/local/bin
    cp -s ../src/bali-phy-2.1.1/bin/* ./

### raxml
    wget https://github.com/stamatak/standard-RAxML/archive/master.zip
    unzip master.zip
    cd standard-RAxML-master/
    make -f Makefile.SSE3.PTHREADS.gcc
    rm *.o
    ln -s raxmlHPC-PTHREADS-SSE3 /usr/local/bin

### garli
    cd /usr/local/src
    wget https://garli.googlecode.com/files/garli-2.0.tar.gz
    cd garli-2.0/
    ./build_garli.sh

**FAIL**

### SPIMAP
    apt-get install libgsl0-dev
    wget http://compbio.mit.edu/spimap/pub/spimap-1.1.tar.gz
    cd spimap-1.1
    make
    make install prefix=/usr/local




#To Do

Dan Fulop's list

need to set better default key for right-click
	