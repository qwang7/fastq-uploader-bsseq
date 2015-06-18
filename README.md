# README

## Overview

gnos_upload_fastq_bsseq.pl is a tool, designed to be used manually, that uploads a single fastq.tar.gz file into a GNOS repository.

This tool needs to produce fastq uploads that conform to the PanCancer fastq file upload spec, see https://wiki.oicr.on.ca/display/PANCANCER/PCAWG+RNA-Seq+fastq+Sequence+Submission+SOP+-+v0.9.

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
ID:121002_UNC11-SN627_0254_AC0WP5ACXX_3_GTCCGC
CN:DKFZ
PL:ILLUMINA
PM:Illumina Genome Analyzer II
LB:WGBS:DKFZ:Illumina TruSeq for 1e176d9d-dba9-4d41-946e-05b7f35eba64
SM:1e176d9d-dba9-4d41-946e-05b7f35eba64
PU:DKFZ:ICGC_MB1
DT:2012-10-16T11:16:21.365
dcc_project_code:PBCA-DE
submitter_donor_id:0809ba8b-4ab6-4f43-934c-c1ccbc014a7e
submitter_specimen_id:5f613800-55df-497f-a544-5b12cb9446ce
submitter_sample_id:b3b3a27c-ee9a-42af-a6d1-9af5970a98b9
dcc_specimen_type:Primary Tumour - solid tissue
md5sum:d41d8cd98f00b204e9800998ecf8427e
icgc_donor_id:DO48977
icgc_specimen_id:SP107575
icgc_sample_id:SA517451
library_selection:RANDOM
library_type:stranded
includes_spike_ins:yes
spike_ins_content:unmethylated lambda phage
adaptor_sequence:Illumina Early access methylation adapter oligo kit (1006132)
accession:EGAS00001000561
"""