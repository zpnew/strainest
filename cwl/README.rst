CWL implementation of the StrainEst pipeline
============================================
We have implemented a basic version of the StrainEst pipeline using the 
`Common Workflow Language <https://www.commonwl.org/>`_ standard 

#. Install Docker for `Linux <https://docs.docker.com/linux/>`_, 
   `Mac OS X <https://docs.docker.com/mac/>`_ or 
   `Windows <https://docs.docker.com/windows/>`_.

#. Install `cwltool <https://www.commonwl.org/>`_

Usage:

  .. code-block:: sh
  
        cwl-runner ~/path-to-workflow/strainest.cwl --reference_dir reference_dir \
        --reference_basename reference_basename \
        --bowtie2_read1 bowtie2_read1 \
        --bowtie2_read2 bowtie2_read2 \
        ---snv snv  \
        --strainest_est_output_dir_name strainest_est_output_dir_name

where:
"reference_dir" is the directory where the bowtie2-indexed reference database is located;

"reference_basename" is the basename of the bowtie2-indexed database;

"bowtie2_read1" is the forward read file in fastq or fastq.gz format

"bowtie2_read2" is the reverse read file in fastq or fastq.gz format

"snv" is the reference SNV file

"strainest_est_output_dir_name" is the name of the output directory.

Requirements:

#. an installation of docker on the local machine;

#. a working internet connection;

The CWL implementation of the pipeline performs the following steps: 

#. alignment of metagenomic reads on the reference database suing bowtie2; 

#. conversion of the sam file into bam, sorting and indexing;

#. estimation of the relative abundace of strains using the "strainest est"  subcommand. 

The workflow assumes that the bowtie2-indexed referece database exists, with 
basename ""reference_basename" and located in the "reference_dir" directory. 

The containerized version of the software is 
automatically downloaded
from the compmetagen repository on Docker Hub and run locally. For this reason, a
working internet connection and a running installation of docker is needed.
The strainest.cwl workflow uses relative paths to locate the cwl-wrappers of the 
individual 
tools, and assumes that they are located in a directory "../tools" from the 
path where the workflow is located. If you want to move it around, build a self contained 
version the command "cwltool --pack strainest.cwl > strainest-pack.cwl".

For details of how to run a CWL pipeline and on the CWL implementations on the 
different platforms, please see https://www.commonwl.org/ 