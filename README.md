# VCFHunter

```r
git clone https://github.com/SouthGreenPlatform/VcfHunter.git
cd VcfHunter
```


**AlleleFreqPython**

**VCFHUNTER**
**Get Ascension Names from VCF**
```r
head -n 1000 DNAseq_prefiltered.vcf | grep "#CHROM" | sed 's/\t/\n/g' | tail -n +10 > all_names.tab

#Filter VCF
python vcfFilter.1.0.py --vcf ../data/Sorghumvcf/freebayes_D2.filtered.vcf --names sorghum_all_names.tab 
--MinCov 10 --MaxCov 300 --MinAl 3 --nMiss 1 --RmAlAlt 1:3:4:5:6 --prefix DNAseq_Filtered -g y


#Separate VCF by Chromosome
vcftools --gzvcf DNAseq_Filtered_filt.vcf.gz --chr Chr01 --recode --out ../data/Sorghumvcf/Chr01_DNAseq_Filtered_filt.vcf.gz
vcftools --gzvcf DNAseq_Filtered_filt.vcf.gz --chr Chr02 --recode --out ../data/Sorghumvcf/Chr02_DNAseq_Filtered_filt.vcf.gz
vcftools --gzvcf DNAseq_Filtered_filt.vcf.gz --chr Chr03 --recode --out ../data/Sorghumvcf/Chr03_DNAseq_Filtered_filt.vcf.gz
vcftools --gzvcf DNAseq_Filtered_filt.vcf.gz --chr Chr04 --recode --out ../data/Sorghumvcf/Chr04_DNAseq_Filtered_filt.vcf.gz
vcftools --gzvcf DNAseq_Filtered_filt.vcf.gz --chr Chr05 --recode --out ../data/Sorghumvcf/Chr05_DNAseq_Filtered_filt.vcf.gz
vcftools --gzvcf DNAseq_Filtered_filt.vcf.gz --chr Chr06 --recode --out ../data/Sorghumvcf/Chr06_DNAseq_Filtered_filt.vcf.gz
vcftools --gzvcf DNAseq_Filtered_filt.vcf.gz --chr Chr07 --recode --out ../data/Sorghumvcf/Chr07_DNAseq_Filtered_filt.vcf.gz
vcftools --gzvcf DNAseq_Filtered_filt.vcf.gz --chr Chr08 --recode --out ../data/Sorghumvcf/Chr08_DNAseq_Filtered_filt.vcf.gz
vcftools --gzvcf DNAseq_Filtered_filt.vcf.gz --chr Chr09 --recode --out ../data/Sorghumvcf/Chr09_DNAseq_Filtered_filt.vcf.gz
vcftools --gzvcf DNAseq_Filtered_filt.vcf.gz --chr Chr10 --recode --out ../data/Sorghumvcf/Chr10_DNAseq_Filtered_filt.vcf.gz

```
**Edit SorgumVcf.conf**


```r
**../data/Sorghumvcf/Chr01_DNAseq_Filtered_filt.vcf.gz.recode.vcf**
**../data/Sorghumvcf/Chr02_DNAseq_Filtered_filt.vcf.gz.recode.vcf**
**../data/Sorghumvcf/Chr03_DNAseq_Filtered_filt.vcf.gz.recode.vcf**
**../data/Sorghumvcf/Chr04_DNAseq_Filtered_filt.vcf.gz.recode.vcf**
```

```r
**../data/Sorghumvcf/Chr05_DNAseq_Filtered_filt.vcf.gz.recode.vcf**
**../data/Sorghumvcf/Chr06_DNAseq_Filtered_filt.vcf.gz.recode.vcf**
**../data/Sorghumvcf/Chr07_DNAseq_Filtered_filt.vcf.gz.recode.vcf**
**../data/Sorghumvcf/Chr08_DNAseq_Filtered_filt.vcf.gz.recode.vcf**
**../data/Sorghumvcf/Chr09_DNAseq_Filtered_filt.vcf.gz.recode.vcf**
**../data/Sorghumvcf/Chr10_DNAseq_Filtered_filt.vcf.gz.recode.vcf**
```

**Edit SorghumOrigin.tab**
```r
**con-all AA**
```
```r
**D2      BB**
```


```r

#Run python script
python vcf2allPropAndCov.py --conf ../data/config/SorghumVcf.conf
--origin ../data/config/SorghumOrigin.tab --acc D2_F2_tt --ploidy 2

```
![sorghum](https://user-images.githubusercontent.com/93121277/179225452-ade0c628-955b-40f3-a7fd-1cb77edf8f20.png)
https://github.com/SouthGreenPlatform/VcfHunter/blob/master/tutorial_ChromosomePainting.md

**In this context, a diploid accession having two chromosomes of the same origin (ex. red) should have a red allele ratio near 1 (see Figure below (A))**

#It shows from where the allele was inherited and iits allelic frequency which is specified in the SorghumOrigin.tab
V1: Chromosome of Variant
V2: Position of Variant: 
V3: Alternate Allele
V4: From which "sample" the allele was inherited
V5: The allelic Frequency 
![sorghumtab](https://user-images.githubusercontent.com/93121277/179226513-24e5d1f9-49e6-481d-8baa-cbca3b3c7d42.png)


