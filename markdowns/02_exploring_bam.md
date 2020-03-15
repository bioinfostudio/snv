# Exploring BAM files

Let’s spend some time exploring BAM files.

```bash
$ samtools view alignment/normal/normal.sorted.bam | head -n4
```

Here you have examples of alignment results. A full description of the
flags can be found in the [SAM specification](http://samtools.sourceforge.net/SAM1.pdf).

Another useful bit of information in the SAM is the CIGAR string. It’s
the 6th column in the file.

This column explains how the alignment was achieved.

> M == base aligns **but doesn’t have to be a match.** A SNP will have an M even if it disagrees with the reference.  
> I == Insertion  
> D == Deletion  
> S == soft-clips. These are handy to find un removed adapters, viral insertions, etc.

An in-depth explanation of the CIGAR can be found [here](http://genome.sph.umich.edu/wiki/SAM).
The exact details of the CIGAR string can be found in the SAM specification as
well. We won’t go into too much detail at this point since we want to concentrate on
cancer specific issues now.

Now, you can try using Picard's [explain flag](http://broadinstitute.github.io/picard/explain-flags.html)
site to understand what is going on with your reads.
