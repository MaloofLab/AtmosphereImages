# Atmosphere-Setup

## Installation notes for Maloof-Biof v10

## All programs are the most update versions at time of creation

### start with image "Ubuntu 14.04.2 XFCE Base"

### General installs

```
apt-get update
apt-get upgrade

apt-get install python3-all --install-suggests
apt-get install python3-numpy python3-scipy
apt-get install python3-dev python-dev python-numpy python-scipy python-support
apt-get install python-pip python3-pip
apt-get install python-biopython python-biopython-doc python-biopython-sql
apt-get install muscle clustalw mafft emboss blast2 probcons
apt-get install bioperl
#note this installed lots of bioinf packages including bwa, bowtie, hmmer, miscule, mafft, tcoffee, and much more
apt-get install openmpi-bin libopenmpi-dev
apt-get install ncbi-blast+ ncbi-blast+-legacy
apt-get install mysql-client mysql-server #password for root = Bioinformatics # Also  created account 'user' with password 'Bioinformatics' with all privileges
apt-get install eclipse
apt-get install libcurl4-openssl-dev #needed for bioconductor
apt-get install libboost-iostreams-dev
apt-get install libgsl0-dev
apt-get install libmysql++-dev
apt-get install libboost-graph-dev
apt-get install libgl1-mesa-dev #for rgl
apt-get install libglu1-mesa-dev #for rgl
apt-get install libmysqlclient-dev #for R mysql
apt-get install libmpfr-dev
apt-get install libgmp-dev
apt-get install git
```

### R (3.3.1)

```
echo 'deb https://cran.cnr.berkeley.edu/bin/linux/ubuntu trusty/' >> /etc/apt/sources.list
apt-get update
apt-get install r-base
apt-get install r-base-dev
```

#### Inside R

```
source("http://bioconductor.org/biocLite.R")
biocLite()
biocLite(c('dichromat', 'ggplot2', 'gtable', 'labeling', 'memoise', 'munsell', 'scales', 'AnnotationDbi', 'BSgenome', 'BayesPeak', 'BiasedUrn', 'Biobase', 'BiocInstaller', 'Biostrings', 'Category', 'DBI', 'DESeq', 'DynDoc', 'EBarrays', 'GO.db', 'GOstats', 'GSEABase', 'GenomicFeatures', 'GenomicRanges', 'IRanges', 'KEGG.db', 'KernSmooth', 'MASS', 'Matrix', 'RBGL', 'RColorBrewer', 'RCurl', 'RMySQL', 'RSQLite', 'RankProd', 'Rcpp', 'Rmpi', 'Rsamtools', 'ShortRead', 'TreeSim', 'VennDiagram', 'XML', 'affy', 'affyPLM', 'affyQCReport', 'affydata', 'affyio', 'annaffy', 'annotate', 'ape', 'arabidopsis.db0', 'ath1121501.db', 'baySeq', 'biomaRt', 'bitops', 'caTools', 'colorspace', 'digest', 'doMC', 'edgeR', 'fdrtool', 'foreach', 'foreign', 'gcrma', 'gee', 'geiger', 'genefilter', 'geneplotter', 'ggplot2', 'goseq',  'hgu95av2.db', 'hopach', 'hwriter', 'igraph', 'iterators', 'itertools', 'lattice', 'latticeExtra', 'limma', 'lme4', 'marray', 'mgcv', 'msm', 'multtest', 'mvtnorm', 'nlme', 'nnet', 'org.At.tair.db', 'ouch', 'phangorn', 'phylobase', 'plyr', 'pmc', 'preprocessCore', 'proto', 'qtl', 'quadprog', 'qvalue', 'reshape', 'reshape2', 'rpart', 'rtracklayer', 'seqLogo', 'seqinr', 'simpleaffy', 'snow', 'snowFT', 'snowfall', 'stringr', 'subplex', 'vsn', 'xtable', 'zlibbioc', 'manipulate', 'chopsticks'))

install.packages(c("genetics","igraph","lmerTest","pacman")) ### Mirror 44

install.packages(c("pvclust","gplots","cluster","LDheatmap","scatterplot3d")) ### Mirror 44

biocLite(c("igraph","WGCNA","lmerTest","Rsubread"))
biocLite("BiocUpgrade")
```

## Placing packages into /usr/local/src
### R Studio Server

```
sudo apt-get install gdebi-core
wget https://download2.rstudio.org/rstudio-server-0.99.903-amd64.deb
sudo gdebi rstudio-server-0.99.903-amd64.deb
mv rstudio-server-0.99.903-amd64.deb /usr/local/src
```

### BWA
#### Remove outdated and put newest

```
sudo apt-get remove bwa
cd /usr/local/src
git clone https://github.com/lh3/bwa.git
cd bwa; make
cd /usr//local/bin
ln -s /usr/local/src/bwa/bwa
```

### Bowtie
#### Remove outdated and put newest

```
apt-get remove bowtie
cd /usr/local/src
wget https://downloads.sourceforge.net/project/bowtie-bio/bowtie/1.1.2/bowtie-1.1.2-linux-x86_64.zip
unzip bowtie-1.1.2-linux-x86_64.zip
cd /usr/local/bin
ln -sf ../src/bowtie-1.1.2/bowtie ./
```

### Bowtie2

```
cd /usr/local/src
wget https://downloads.sourceforge.net/project/bowtie-bio/bowtie2/2.2.9/bowtie2-2.2.9-linux-x86_64.zip
unzip bowtie2-2.2.9-linux-x86_64.zip
cd /usr/local/bin
cp -sf ../src/bowtie2-2.2.9/bowtie2* ./
```

### blat

```
cd /usr/local/src
wget https://users.soe.ucsc.edu/~kent/src/blatSrc35.zip
unzip blatSrc35.zip
cd blatSrc
nano inc/common.mk #Change BINDIR=${HOME}/bin/${MACHTYPE} to BINDIR=/usr/local/bin
MACHTYPE=x86_64
export MACHTYPE
make
```

### cufflinks

```

cd /usr/local/src
wget http://cole-trapnell-lab.github.io/cufflinks/assets/downloads/cufflinks-2.2.1.Linux_x86_64.tar.gz
tar -xvzf cufflinks-2.2.1.Linux_x86_64.tar.gz
cd /usr/local/bin
cp -sf ../src/cufflinks-2.2.1.Linux_x86_64/cuff* ./
cp -sf ../src/cufflinks-2.2.1.Linux_x86_64/g* ./
```

### fastQC

```
cd /usr/local/src
wget www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.5.zip
cd FastQC/
chmod 0755 fastqc
cd /usr/local/bin
cp -s ../src/FastQC/fastqc ./
```

### Update Java, some programs require 1.8

```
add-apt-repository ppa:openjdk-r/ppa
sudo apt-get update
sudo apt-get install openjdk-8-jdk
#Setting/confirming Java 8 as default
sudo update-alternatives --config java ## select java-8
sudo update-alternatives --config javac ## select java-8
java -version
```

### GATK 3.6 
Download from http://www.broadinstitute.org/gatk/

```
cd /usr/local/src
mkdir GenomeAnalysisTK
mv ~/GenomeAnalysisTK-3.4-46.tar.bz2 /usr/local/src/GenomeAnalysisTK
cd GenomeAnalysisTK
bunzip2 GenomeAnalysisTK-3.6.tar.bz2
tar -xvf GenomeAnalysisTK-3.6.tar
cd /usr/local/bin
### created sh called GenomeAnalysisTK with chmod 755 
### allows GenomeAnalysisTK to be invoked without including "java -jar /path/to/GenomeAnalysisTK.jar"
```

### IGV

```
cd /usr/local/src
wget data.broadinstitute.org/igv/projects/downloads/IGV_2.3.83.zip
unzip IGV_2.3.83.zip
cd /usr/local/bin
cp -sf ../src/IGV_2.3.83/igv.sh ./
### created sh called igv with chmod 755 
### allows igv to be invoked without including "java -jar /path/to/igv.jar"
```

### Trinity

```
cd /usr/local/src
wget https://github.com/trinityrnaseq/trinityrnaseq/archive/v2.2.0.tar.gz
tar -xvf v2.2.0.tar.gz
cd trinityrnaseq-2.2.0/
make
make plugins
cd /usr/local/bin
ln -s /usr/local/src/trinityrnaseq-2.2.0/Trinity
```

### lastz

```
wget http://www.bx.psu.edu/miller_lab/dist/lastz-1.02.00.tar.gz
tar -xvzf lastz-1.02.00.tar.gz
cd lastz-distrib-1.02.00/
### edit make-include.mak to set LASTZ_INSTALL="/usr/local/src/lastz-distrib-1.02.00/bin/" 
### edit src/Makefile to remove -Werror compile flag
make
make install
cd /usr/local/bin
cp -s ../src/lastz-distrib-1.02.00/bin/lastz* ./
```

### augustus

```
cd /usr/local/src
wget http://bioinf.uni-greifswald.de/augustus/binaries/augustus-3.2.2.tar.gz
tar -xvzf augustus-3.2.2.tar.gz
echo 'deb http://us.archive.ubuntu.com/ubuntu vivid main universe' >> /etc/apt/sources.list
apt-get update
apt-get install libbamtools-dev
cd /usr/local/src/augustus-3.2.2
make
make install
```

### tophat

```
cd /usr/local/src
sudo -s
wget https://ccb.jhu.edu/software/tophat/downloads/tophat-2.1.1.Linux_x86_64.tar.gz
tar xvfz tophat-2.1.1.Linux_x86_64.tar.gz
cd ../bin
ln -s /usr/local/src/tophat-2.1.1.Linux_x86_64/tophat* ./
```

### Cap3

```
wget seq.cs.iastate.edu/CAP3/cap3.linux.x86_64.tar
tar -xvf cap3.linux.i686_xeon64.tar
cd /usr/local/bin
cp -s ../src/CAP3/cap3 ./
cp -s ../src/CAP3/formcon ./
```

### varscan

```
wget https://downloads.sourceforge.net/project/varscan/VarScan.v2.3.9.jar
cd /usr/local/bin
### Create sh called VarScan with chmod 755 for VarScan.v2.3.9.jar
```

### Satsuma

```
wget https://archive.broadinstitute.org/ftp/distribution/software/spines/satsuma-3.0.tar.gz
tar -xvzf satsuma-3.0.tar.gz
cd /usr/local/bin/
cp -s ../src/satsuma-code-0/Satsuma* ./
```

### Smartgit

```
wget https://www.syntevo.com/static/smart/download/smartgit/smartgit-linux-8_0_3.tar.gz
tar -xvzf smartgit-linux-8_0_3.tar.gz
### Made desktop launcher
```

### SRA toolkit
```
wget https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/2.8.0/sratoolkit.2.8.0-ubuntu64.tar.gz
tar -xvf sratoolkit.2.8.0-ubuntu64.tar.gz
cd /usr/local/bin
ln -sf /usr/local/src/sratoolkit.2.8.0-ubuntu64/bin/* ./
```

### Samtools
#### Remove outdate and put newest

```
apt-get remove samtools
wget https://github.com/samtools/samtools/releases/download/1.3.1/samtools-1.3.1.tar.bz2
tar -xvf samtools-1.3.1.tar.bz2
cd samtools-1.3.1/
make
make prefix=/usr/local/src/samtools-1.3.1 install
## Added to PATH
```

### Bamtools

```
apt-get install cmake
cd /usr/local/src
git clone git://github.com/pezmaster31/bamtools.git
cd bamtools
mkdir build
cd build/
cmake ..
make
cd /usr/local/bin
ln -sf /usr/local/src/bamtools/bin/bamtools
```

### Velvet

```
cd /usr/local/src
git clone git://github.com/dzerbino/velvet.git
cd velvet
make
make 'MAXKMERLENGTH=75'
cd /usr/local/bin
cp -sf ../src/velvet/velvet* ./
```

### Picard tools

```
cd /usr/local/src
wget https://github.com/broadinstitute/picard/releases/download/2.7.0/picard.jar
cd /usr/local/bin
### created sh called picard with chmod 755 
### allows picard to be invoked without including "java -jar /path/to/picard.jar"
```

### circos

```
cd /usr/local/src
wget http://circos.ca/distribution/circos-0.69-3.tgz
tar -xvzf circos-0.69-3.tgz
cd circos-0.69-3
export PATH=/usr/local/src/circos-0.69-3/bin:$PATH
### In order to use, must put circos.conf file in /etc/
```

### SVDetect

```
cd /usr/local/src
wget http://downloads.sourceforge.net/project/svdetect/SVDetect/0.70/SVDetect_r0.7m.tar.gz
tar -xvzf SVDetect_r0.7m.tar.gz
cpan Tie::IxHash
cpan Parallel::ForkManager
cd /usr/local/bin
cp -sf ../src/SVDetect/bin/SVDetect ./
```

### orthomcl

```
cd /usr/local/src
apt-get insatll mcl
wget http://orthomcl.org/common/downloads/software/v2.0/orthomclSoftware-v2.0.9.tar.gz
tar -xvzf orthomclSoftware-v2.0.9.tar.gz
cd orthomclSoftware-v2.0.9/
mkdir my_orthomcl_dir
cp doc/OrthoMCLEngine/Main/orthomcl.config.template my_orthomcl_dir/orthomcl.config
### created mysql database called orthomcl using `create database orthomcl` inside mysql
bin/orthomclInstallSchema my_orthomcl_dir/orthomcl.config  my_orthomcl_dir/install_schema.log
### In order to use orthomcl, the user must input their own data and follow the program's instructions on their own
cd /usr/local/bin
ln -s ../
```

### Trimmomatic

```
cd /usr/local/src
wget www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-0.36.zip
unzip Trimmomatic-0.36.zip
cd /usr/local/bin
### created sh called trimmomatic with chmod 755 
### allows trimmomatic to be invoked without including "java -jar /path/to/trimmomatic.jar"
```

### STAR

```
git clone https://github.com/alexdobin/STAR.git
cp STAR/bin/Linus_x86_64_static/STAR ../bin
```
