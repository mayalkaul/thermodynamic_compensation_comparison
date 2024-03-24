### What is this?
EF-Tu (prokaryotic) and EF1a (eukaryotic) are proteins that bind and deliver amino-acid-charged tRNAs to the ribosome for translation.

The Uhlenbeck lab in the 2000s showed that the affinity between a charged tRNA and EF-Tu molecule is determined by a linear combination of the affinity for the amino acid and the innermost three basepairs of the T-arm. In prokaryotes, there is "thermodynamic compensation" with low-affinity T-arm basepairs associated with high-affinity amino acids and vice versa, for a narrow range of affinity between -9.5 and 10.5kcal/mol. This is conserved across different bacteria (Schrader and Uhlenbeck, 2011, doi:10.1093/nar/gkr641). This acts as 1) quality control by preventing translation with egregiously misacylated tRNAs and 2) a roadblock if that "egregious misacylation" was on purpose (biology is fun). 

"Thermodynamic compensation" has not been definitively proven for eukaryotic tRNAs and EF1a, despite several claims that it does, and significant evidence that some joint amino-acid/tRNA-body recognition is required for proper EF1a binding. This is ONLY looking at whether the amino acids and innermost three basepairs of the T-arm follow the same EXACT pattern in eukaryotic tRNAs as prokaryotic. 

### Conclusions
Prokaryotic thermodynamic compensation results in aatRNA/EF-Tu affinities significantly different from what would be achieved by random combinations of amino acid and T-arm basepairs (p=7.6e-8)

eukaryotic aatRNAs do not show a pattern *based on the values of aa and T-arm basepair affinities* (p=0.35), and is significantly different from the prokaryotic values (p=8.2e-182)

### NOT conclusions and other concerns with how I did this
This doesn't rule out thermodynamic compensation in a different way, especially since the eukaryotic tRNA-delivery system is EF1a, not EF-Tu. 

This is based on Schrader and Uhlenbeck, 2018(doi:10.1016/j.cbpa.2018.07.016), with the values compared to phenylalanine. The data does not include threonine's value, and does not have values for several tRNA basepairs. 

### Data?
The tRNA sequences are from GtRNAdb out of UCSC (Chan and Lowe, 2016 doi:10.1093/nar/gkv1309). I took all bacterial and all eukaryotic with a quality score above 56, which is "conservatively" predicted to be an active tRNA (Chan and Lowe, 2019 doi:10.1007/978-1-4939-9173-0_1). This led to ~150k eukaryotic tRNA sequences and 250k prokaryotic sequences. 

The effect of the amino acid and "Uhlenbeck pairs" is relative to properly acylated Phe-tRNAPhe, and the values come from Schrader and Uhlenbeck, 2018 (doi:10.1016/j.cbpa.2018.07.016)

### Approach?
##### Identify the T-arm and compile sequences where identification succeeded. 

I tried doing this based on conserved bases (included as commented segment, for future reference/curiosity), but it worked better to assume the proportions of every tRNA is the same, and just use backwards indexing. In the database, eukaryotic tRNAs do not contain the 3' terminal 'CCA', while prokaryotic often do, and I clip them before indexing. I check if the T-arm is indeed there by checking if the two putatitive T-arm segments are paired in 4/5 of the positions. If I did not successfully get the T-arm, I discard the sequence. ~1.5k and 15k of eukaryotic and prokaryotic tRNAs were abandoned, respectively, mostly from differently-sized T-arm loops. 

##### Using the amino acid and the three innermost T-arm basepairs, calculate the total "ΔΔG" (the different in EF-Tu binding energy compared to Phe-tRNAPhe). 

matching the amino acid and the Uhlenbeck pairs to their values. This step also removes some weird tRNAs (initiator, suppressor), and unfortunately some tRNAs that contain Uhlenbeck pairs I do not have data for (~3k for Eukaryotes and ~4k for Prokaryotes)

##### Evaluate
