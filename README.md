# This repository contains the analysis described in the article "Pneumovirus Genome Misassemblies Associated with Duplications in Glycoprotein Genes".

In this repository, we present an analysis of how the reference genome affect the assembly of pneumoviruses, specifically in the detection of nucleotide duplications in the attachment glycoprotein (G) gene. Since 2016, only RSV-A genetic lineages with a 72-nt duplication have been detected, and similarly, RSV-B lineages with a 60-nt duplication. 
In addition, MPV (Metapneumovirus) has shown 111-nt and 180-nt duplications in the G gene, alongside viral strains that do not contain these duplications.

When mapping a sequence that contains a duplication against a reference genome that lacks the duplication, short reads can map overlapping regions of both copies within the original copy. This leads to the introduction of IUPAC nucleotide ambiguities in the final consensus sequence, and the duplication is not detected. The cause of this misalignment is that short reads may only partially map to the original copy, which forces the alignment to fit, while no reads fully cover the duplicated region. 

Inspecting the assembly it is notable a significant number of reads with soft clipping are detected. Soft clipping is a technique used automatically in software mappers that trims nucleotides from the beginning and/or end of a read. These trimmed bases are retained in the read sequence but are not aligned to the reference genome. Soft clipping helps preserve the integrity of the read while minimizing misalignments due to mismatches or poor-quality regions. Consequently, the information soft-clipped is not used for consensus generation.

In this analysis, we evaluate a single FASTQ file for each viral variant containing a duplication and map it against different reference genomes with and without the duplication. Our findings suggest that hybrid de novo assembly methods, followed by mapping to a reference, provide an effective approach to prevent the loss of crucial nucleotide duplications. Identifying ambiguities in specific regions of the consensus genome can also help detect and correct misassemblies.

In addition targeted sequencing approaches, such as amplicon sequencing, can resolve these duplications, as can sequencing larger inserts with longer read lengths. Finally, phylogenetic analyses are crucial in identifying misassemblies, as significant genetic events, such as the emergence or loss of large nucleotide duplications, are expected to be single-time events in the evolutionary history of a viral gene.

- A detailed description of the analysis is provided in the SupplementaryMaterial.pdf. 

- The sequence of the two nucleotide copies in the final well-assembled genome (available in GenBank, with details in SupplementaryMaterial.pdf) is provided in the file Nucleotide_duplications.fasta.

- The analysis for each FASTQ file is organized in folders by viral variant (RSV-A, RSV-B, MPV-111 – containing the 111-nt duplication, and MPV-180 – containing the 180-nt duplication). Each folder contains the indexed, sorted BAM files along with the reference genome used (in FASTA format).
The name of each BAM file includes the viral variant, the SRA accession number (or "deNovoContigs" for hybrid assemblies), and the reference genome used for mapping with BWA MEM. MPV assemblies were mapped against a reference without duplications (denoted by "no" before the reference name in the BAM file), as well as references containing the 111-nt and 180-nt duplications (identified by the length of the duplication in the reference name for easy organization).

- The file RSV_Trees.zip contains the Nextstrain json files of the RSV-A and RSV-B phylogenetic trees, that can be visualized in https://auspice.us/
