---
layout: post
title: "Average coverage of sequenced exome"
date: 2018-09-06 11:51:02
categories: [bioinformatics, bash]
tags: [genetics, bash]
---

The coverage is a metric that represents how many base copies were generated to cover a specific DNA site.
The average coverage can be measured on the scale of the genome by implementing tools like `bamtools`, `samtools`, `bedtools`, and `awk`.

{% highlight bash %}
for minCov in {10, 20, 30}; do
    avg.coverage=$(bamtools filter -tag XT:U -tag XM:0 -in $sample.bam \
		       | samtools view -uq$mapq -b - -@$threads \
		       | genomeCoverageBed -ibam - -bg \
		       | awk -vm=$minCov '{if($4>= m )print$0}' \
		       | awk '{sum+=$4} END { print "Avg Coverage=",sum/NR,"X"}')
    paste avg.coverage >> summary.average_coverage.txt
done
{% endhighlight %}


The average coverage can also be measured on a specific number of genes that were targeted during a whole exome sequencing run.
The difference between `agilent.bed` file and `ucsc.bed` is that the former was generated by Agilent and the latter by me.
Agilent file contains little information about exons being sequenced by gene, by site, by DNA frame.
Not supportive for more thorough analysis of variant recognition by gene.
That's why with data mining of UCSC databases I can add more informative features to the sites being sequenced.
This would increase the amount of results, improve interpretability, and lastly validate the full price for sequencing a genome.
Thus, taking full advantage of our data.

{% highlight bash %}
for fileCov in {1, 2}; do
    local file[1]=$agilent.bed
    local file[2]=$ucsc.bed

    if [ $fileCov == 1 ]; then
	bamtools filter -tag XT:U -tag XM:0 -in $sample.bam \
	    | samtools view -uq$mapq -b - -@$threads \
	    | bamToBed -i - \
	    | sort-bed - \
	    | bedops --merge - \
	    | bedtools coverage -a $file[$fileCov] -b - \
	    | awk '{if($11>=.8)print$0}' \
	    | awk '{sum+=$8} END { print "Avg coverage=",sum/NR,"X"}'
    else
	bamtools filter -tag XT:U -tag XM:0 -in $sample.bam \
	    | samtools view -uq$mapq -b - -@$threads \
	    | bamToBed -i - \
	    | sort-bed - \
	    | bedops --merge - \
	    | bedtools coverage -a $file[$fileCov] -b - \
	    | awk '{if($8>=.8)print$0}' \
	    | awk '{sum+=$5} END { print "Avg coverage=",sum/NR,"X"}'
done
{% endhighlight %}

* Filtering parameters and thresholds
  - *mapq*, mapping quality
  - *XM*, how many mismatches in alignment
  - *XT*, how many unique reads by site
  - *$8* or *$11*, mapping depth by nucleotide by site
  - Maximum depth can also be used with `samtools -d`
  - Execessive mismatches can also be penalized with `bcftools mpileup -C`


