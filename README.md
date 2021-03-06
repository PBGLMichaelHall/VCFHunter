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
 python vcf2allPropAndCov.py --conf ../data/config/SorghumVcf.conf --origin ../data/config/SorghumOrigin.tab --acc D2_F2_tt --ploidy 2 --dcurve y --col /data/con
``` 
 ![D2_F2_ttRatio](https://user-images.githubusercontent.com/93121277/179458414-c2c39578-7488-44a0-8e40-8013659e4401.png)
fig/SorghumColor.conf



**In this context, a diploid accession having two chromosomes of the same origin (ex. red) should have a red allele ratio near 1 (see Figure below (A))**
**A diploid accessions with chromosomes of two distinct origin (ex. one red and one green) should have green allele ratio near 0.5 and red allele ratio near 0.5 too**


#It shows from where the allele was inherited and iits allelic frequency which is specified in the SorghumOrigin.tab
V1: Chromosome of Variant
V2: Position of Variant: 
V3: Alternate Allele
V4: From which "sample" the allele was inherited
V5: The allelic Frequency 
![sorghumtab](https://user-images.githubusercontent.com/93121277/179226513-24e5d1f9-49e6-481d-8baa-cbca3b3c7d42.png)


# In additio it provides a coverage mapping alon the chromosome.

![D2_F2_ttCov](https://user-images.githubusercontent.com/93121277/179459882-3818c2e7-a4fe-4367-917c-616183fa29d2.png)


#######################################################################################################################################################

# For Polyplody Organisms Separate VCF by Chromosome


```r
#Grep the Header
bcftools view freebayes~bwa~GCF_000313855.2_ASM31385v2~all_samples~filtered-strict.vcf.gz | grep "^##" > Header.txt

#Grep the #CHROM line
bcftools view freebayes~bwa~GCF_000313855.2_ASM31385v2~all_samples~filtered-strict.vcf.gz | grep "^#CHROM" > HeaderChrom.txt

#Grep the Chromosome Lines
bcftools view freebayes~bwa~GCF_000313855.2_ASM31385v2~all_samples~filtered-strict.vcf.gz | grep "^NC_025202.1" > NC_025202.1.txt

#Concatenate to VCF
cat Header.txt HeaderChrom.txt NC_025202.1.txt > NC_025202.1.vcf.gz
```



