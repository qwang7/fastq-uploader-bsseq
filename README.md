# README

## Overview

gnos_upload_fastq_bsseq.pl is a tool, designed to be used manually, that uploads a single fastq.tar.gz file into a GNOS repository.

This tool needs to produce fastq uploads that conform to the PanCancer fastq file upload spec, see https://wiki.oicr.on.ca/display/PANCANCER/PCAWG+WGBS+fastq+Sequence+GNOS+Submission+SOP+-+v+0.9.

## Dependencies for gnos_upload_fastq_bsseq.pl

You can use PerlBrew (or your native package manager) to install dependencies.  For example:

    cpanm Data::UUID Carp::Always IPC::System::Simple

Once these are installed you can execute the script with the command below.

You also need the gtdownload/gtuplod/cgsubmit tools installed.  These are available on the CGHub site and only run on Linux hosts (for the submission tools).

## Inputs

This tool is designed to work with the following file types:

* tar.gz: a standard gzipped tar file format made with something similar to 'tar czvf bar.tar.gz <files>'.
* tar.gz.md5: md5sum file made with something like 'md5sum bar.tar.gz | awk '{print$1}' > bar.tar.gz.md5'.

## Running gnos_upload_fastq_bsseq

The parameters:

    perl gnos_upload_fastq_bsseq.pl
    --fastq <filename for fastq file tarball>
    --metadata <filename containing key value pairs>
    --fastq-md5sum-file <file_with_fastq_md5sum>
    --outdir <output_dir>
    --key <gnos.pem>
    --upload-url <gnos_server_url>
    [--study-refname-override <study_refname_override>]
    [--analysis-center-override <analysis_center_override>]
    [--make-runxml]
    [--make-expxml]
    [--force-copy]
    [--skip-validate]
    [--skip-upload]
    [--test]

For example:

gnos_upload_fastq_bsseq.pl  --fastq \<your_fastq.tar.gz\>  --fastq-md5sum-file \<your_fastq.tar.gz.md5\> --outdir \<your_outdir\> --upload-url \https://gtrepo-ebi.annailabs.com\> --key \<full/path/to/your/gnos_key.pem\> --metadata \<your_metadata_file.txt\>";

## Notes About GNOS Analysis XML

Here is an example of a metadata file. 
"""
ID:DKFZ:100618_SN500_0169_AD14BGACXX_1
CN:DKFZ
DT:2010-06-18T00:00:00.000+00:00
LB:WGBS:DKFZ:ICGC_MB112
PI:240
PL:ILLUMINA
PM:Illumina HiSeq 2000
PU:DKFZ:100618_SN500_0169_AD14BGACXX_1
aliquot_id:3e042387-8444-406a-bf64-07c29cf889ed
dcc_project_code:PBCA-DE
submitter_donor_id:ICGC_MB112
submitter_specimen_id:ICGC_MB112
submitter_sample_id:ICGC_MB112
dcc_specimen_type:Primary tumour - solid tissue
accession:EGAS00001000215
md5sum:67cebf14e7e73664dab2d00b7b761faf
library_selection:RANDOM
library_type:stranded
includes_spike_ins:yes
spike_ins_content:unmethylated lambda phage
adaptor_sequence:Illumina Early access methylation adapter oligo kit (1006132)
"""