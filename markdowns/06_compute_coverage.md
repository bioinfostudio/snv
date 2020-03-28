# BAM QC

Once your whole BAM is generated, it’s always a good thing to check the
data again to see if everything makes sense.

## Step 1: BAM QC: Compute Coverage

If you have data from a capture kit, you should see how well your
targets worked. [mosdepth](https://academic.oup.com/bioinformatics/article/34/5/867/4583630) has a depth of coverage tool to do this:

```bash
for i in normal tumour
do
    mosdepth \
    --by ref/callable.bed.gz --no-per-base \
    --thresholds 10,25,50,100 alignment/${i}/${i} \
    alignment/${i}/${i}.sorted.dup.recal.bam
done
```

Explanation of parameters:

- **-\-by**: Optional BED file or (integer) window-sizes
- **-\-no-per-base**: Do not output depth of coverage at each base
- **-\-threshold**: For each interval in --by, write number of bases covered by at least threshold bases

In this project, coverage is expected to be 85x. Look at the coverage:

    less -S alignment/normal/normal.mosdepth.summary.txt

Type `q` to return to the prompt.

    less -S alignment/tumour/tumour.mosdepth.summary.txt
