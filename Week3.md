# Maxam-Gilbert Sequencing

* This uses chemicals that split DNA between specific bases and runs the resulting fragments on a gel to infer the sequence.
* Pros:
  * One of the first sequencing technologies.
* Cons:
  * Chemicals used are toxic
  * Sequence was hard to infer from the cleavage/gel
* This technology is currently out of use.

# Sanger Sequencing

* This uses chain-terminating inhibitors during PCR to create oligonucleotides ending in your inhibitor base, which are then separated on a gel to infer the sequence.
* Pros:
  * Sequence easy to infer
  * Less toxic than Maxam-Gilbert
  * Was eventually automated for higher throughput
* Cons:
  * Slower and less efficient than Next-Gen sequencing
* This technique isn't explicitly used currently, but is the basis for most of our current sequencing technology.

# 454-Roche

* 454 uses emulsion bead PCR followed by pyrosequencing, measuring the luminence eminated when a single dNTP base is added in each of its microwells.
* Pros:
  * 1st Next-Gen sequencing
  * Higher-throughput than Sanger using DNA clusters
* Cons:
  * Difficulty reading sequences with repeats (i.e. "AAAAAA")
  * Microwells aren't always filled, possibly wasting money
  * Expensive for a next generation sequencing technology
* 454 still exists, though is rarely used due to better alternatives

# Illumina

* This technique uses bridge amplification to build DNA clusters that will be amplified with fluorescent dNTPs, giving an emission signal to the machine with each base added.
* Pros:
  * Handles repeats better than 454
  * Can run many samples in a single run
  * Cheap and reliable data
* Cons:
  * Can only read short (32-40 bp) sequences
* This is currently the go-to sequencing technology.

# Ion Turrent

* These machines use microbeads like 454, but instead measure the pH change of polymerizing the dNTP added as a signal.
* Pros:
  * Cheaper than most technologies
  * Can handle repeats better than 454
* Cons:
  * More expensive than Illumina sequencing
* This is one of the newer technologies that has some advantages over Illumina, though the video did not go into any more detail.

# Pacific Biosciences

* This uses polymerases fixed to a slide at precise locations with a confocal microscope watching the sites for emissions from fluorescently tagged dNTPs.
* Pros:
  * Only needs one molecule of DNA
  * Is done all in one reaction
  * Fast; 15 bp per second
  * Can achieve very long reads
  * Can read modifications to DNA bases (i.e. methylation)
* Cons:
  * Microscope cannot be turned on for the entirity of long reads to avoid burning out the enzymes
  * High SNP error rate
* More often this is used to study epigenetics of organisms

# Oxford Nanopores MinION

* These tiny machines use protein pores to read a single molecule of DNA.
* Pros:
  * Tiny
  * Possibility for remote location sequencing
  * Sends data straight to your computer
* Cons:
  * Expensive
* This is a very new technology with a lot of possibilities, but is still being tested.
