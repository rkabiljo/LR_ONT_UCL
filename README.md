# LR_ONT_UCL

Log on to hestia
```
ssh rkabiljo@128.40.184.7
```
Install Nextflow
```
curl -s https://get.nextflow.io | bash
echo 'export PATH=$PATH:$HOME' >> ~/.bashrc
source ~/.bashrc
nextflow --version
```

The ONT Nextflow workflow
```
cd /data/hestia/rkabiljo/
#download the demo data
wget https://ont-exd-int-s3-euwst1-epi2me-labs.s3.amazonaws.com/wf-human-variation/hg002%2bmods.v1/wf-human-variation-demo.tar.gz
tar -xzvf wf-human-variation-demo.tar.gz
nano nextflow.config
nextflow run epi2me-labs/wf-human-variation --bam 'wf-human-variation-demo/demo.bam' --ref 'wf-human-variation-demo/demo.fasta' --bed 'wf-human-variation-demo/demo.bed' --sample_name 'DEMO' --snp --sv --mod --phase
```
This was with standard profile.  for cluster - I use standard profile and submit with qsub. Did not manage to get profile cluster to work
```
