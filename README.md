# Microbiome_2021
Supplementary materials for Berihu et al.\
The input/output files used/generated with code below are all available on Drive: https://volcanicenter-my.sharepoint.com/:f:/g/personal/ofirt_volcani_agri_gov_il/EsPau_uqpolHk37VuXWMqMIB0J-Ey1I-Pstl2gt0k48G8A



# Code for merging MEGAN annotations tables with count tables
We have created a count table using BWA mapping software, and each treatment was run on MEGAN to create functional or taxonomic keys. The count data are presented as a table which reports, for each sample, the number of sequence fragments that have been assigned to the contigs or genes. To merge count table with functional and taxonomic keys, we wrote the following codes written in python:
"get_contig_taxonomy_v3.py" defines the contigs/genes frequent taxonomy and prints the taxonomy rank. The code merges the count table and the new file created from the first code, creating a count table based on the taxonomic level. \
"Prepare_edgeR_input_taxonomy_v2.py" cuts only contigs/genes with EC/KEGG identifiers from MEGAN functional file: "ReadName_to_KeggName". \
"script_1kegg_parser.pl" merges count table and MEGAN file with taxonomy annotation.\
"prepare_edgeR_input_v2.py" merges count table, MEGAN file with taxonomy annotation, and the output file from "script_1kegg_parser.pl" creating a count table based on the functional keys (EC/KEGG) with taxonomic level. \
"prepare_ECcodes_taxonomy_ctable_contigwise_v2.py" generates a list of enzymes dominated by specific taxa. \
"knockout-ecs_interactive_modified.R" uses the output file generated by the code above. input: ECcodes_genus_Countable_NTC_G210.txt, available on the drive https://volcanicenter-my.sharepoint.com/:f:/g/personal/ofirt_volcani_agri_gov_il/EsPau_uqpolHk37VuXWMqMIB0J-Ey1I-Pstl2gt0k48G8A
Output file is available as Additional file 4 in the supplementary material.

# Using edgeR to obtain a list of significantly different contigs/genes using_edgeR_generic_2.R
The edge R script requires 6 parameters. 
    1. Pathway to the input count table used \
    2. Pathway to the metadata file, with at least two columns: one for the samples ID and one assigning each sampe to a group\
    3. Base name for output files (the program generates multiple outputs, this is just the pathway to them and the "base" of the name, such as "edgeR_results"\
    4. Name of the metadata file column dividing the samples into the groups of replicates \
    5. Text file with the contrasts used in the analysis. It is important that the contrast names and the contrast structure (see example files) are separates by ' = '. In the example, we want to compare The conventional israeli group of samples to the organic israeli group and to the average of the american conventional groups.\
    6.  FDR threshold used to establish significance. For our analysis, we used 0.05 Example: Rscript using_edgeR_generic.R. 
Count_Table_Order_NTC.txt sample_metadata.txt Order_0.05_ Tretment_Rootstock contrasts_used.txt 0.05. The script will produce, for each contrast, a table file with the results of the differential analysis and a plot showing the distribution of differentially represented elements.\
Network analysis Code for network construction and visualization was deposited in https://github.com/ot483/NetCom

# Removal Network
The script "Removal_Network_order_1_1.24.py" was used as a reference for community 'knockouts' simulations in which selected taxonomic groups were removed. In each of the removal iterations, all edges -enzymes representing metabolic functions, specifically dominated by a taxonomic group, taxa-dominated enzymes were removed from the original enzyme set. The impact of the removal group was estimated according to differences in the number of metabolites between the network expanded from the truncated enzyme set, and the reference meta-network.\
The four required DB files are available in the Scripts folder.
