demoFL
======


This document outlines the step-by-step workflow for the analysis of follicular lymphoma using the `dds_analysis` package. Each step is described along with the corresponding bash code.

Step 1: Map mutation blocks to genomic regions
----------------------------------------------

The `map_block2genome` module from the `dds_analysis` package is used to map mutation blocks to predefined genomic regions.

.. code-block :: bash

   dds_analysis map_block2genome --in_sortedBlock_file $IN_BLOCK_FILE --in_genomicRegion_file $GENOMIC_REGION_FILE --in_reference_genome $REFERENCE_GENOME_FILE --out_folder $OUTPUT_FOLDER

Step 2: Map mutation blocks to chromatin segments
-------------------------------------------------

The `map_block2chromSegment` module from the `dds_analysis` package is used to map mutation blocks to chromatin segments.

.. code-block :: bash

   dds_analysis map_block2chromSegment --in_sortedBlock_file $IN_BLOCK_FILE --in_chromatinSegment_folder $CHROMATIN_SEGMENT_FOLDER --out_folder $OUTPUT_FOLDER

Step 3: Map mutation blocks to differentially methylated regions (DMRs)
-----------------------------------------------------------------------

The `map_block2dmr` module from the `dds_analysis` package is used to map mutation blocks to DMRs after adding flank regions.

.. code-block :: bash

   dds_analysis map_block2dmr --in_sortedBlock_file $IN_BLOCK_FILE --in_dmr_file $DMR_FILE --flank_region_size $FLANK_REGION_SIZE --out_folder $OUTPUT_FOLDER

Step 4: Combine genomic regions with mutation block information and find differentially expressed genes
-------------------------------------------------------------------------------------------------------

The `find_geneExp4block` module from the `dds_analysis` package is used to combine genomic regions with mutation block information and identify differentially expressed genes.

.. code-block :: bash

   dds_analysis find_geneExp4block --in_blocks_genome_folder $BLOCKS_GENOME_FOLDER --in_sortedBlock_file $IN_BLOCK_FILE --in_de_genes_file $DE_GENES_FILE --in_feature_list $FEATURE_LIST --out_folder $OUTPUT_FOLDER

Step 5: Find patient IDs for each mutation block
------------------------------------------------

The `find_block_patientID` module from the `dds_analysis` package is used to find patient IDs associated with each mutation block.

.. code-block :: bash

   dds_analysis find_block_patientID --in_block_summary_file $BLOCK_SUMMARY_FILE --in_block_folder $BLOCK_FOLDER

Step 6: Combine DMRs, differentially expressed genes (DEGs), and mutation block information
-------------------------------------------------------------------------------------------

The `combine_dmr_deg2block` module from the `dds_analysis` package is used to combine DMRs, DEGs, and mutation block information.

.. code-block :: bash

   dds_analysis combine_dmr_deg2block --in_sortedBlock_patient_file $SORTED_BLOCK_PATIENT_FILE --in_dmr_file $DMR_FILE --in_deg_folder $DEG_FOLDER --deg_file_suffix $DEG_FILE_SUFFIX --out_folder $OUTPUT_FOLDER

Step 7: Filter blocks based on DMR or DEG information
-----------------------------------------------------

The `filter_blocks` module from the `dds_analysis` package is used to filter blocks based on DMR or DEG information.

.. code-block :: bash

   dds_analysis filter_blocks --in_combined_dmr_deg_block_file $COMBINED_DMR_DEG_BLOCK_FILE

Step 8: Collect unique gene names from predicted blocks after filtering
-----------------------------------------------------------------------

The `collect_gene_names4blocks` module from the `dds_analysis` package is used to collect unique gene names from predicted blocks.

.. code-block :: bash

   dds_analysis collect_gene_names4blocks --in_filtered_block_file $FILTERED_BLOCK_FILE --out_gene_file $GENE_FILE

Step 9: Perform gene expression analysis for selected genes
-----------------------------------------------------------

The `gene_expression_analysis` module from the `dds_analysis` package is used to perform gene expression analysis for selected genes.

.. code-block :: bash

   dds_analysis gene_expression_analysis --in_gene_file $GENE_FILE --in_expression_file $EXPRESSION_FILE --out_folder $OUTPUT_FOLDER

Step 10: Perform functional enrichment analysis for selected genes
------------------------------------------------------------------

The `functional_enrichment_analysis` module from the `dds_analysis` package is used to perform functional enrichment analysis for selected genes.

.. code-block :: bash

   dds_analysis functional_enrichment_analysis --in_gene_file $GENE_FILE --in_annotation_file $ANNOTATION_FILE --out_folder $OUTPUT_FOLDER

Step 11: Find enhancer target genes
-----------------------------------

The `find_enhancer_target_genes` module from the `dds_analysis` package is used to find enhancer target genes by overlapping predicted enhancers with selected mutation blocks and a predicted target gene.

.. code-block :: bash

   dds_analysis find_enhancer_target_genes --in_enhancer_folder $ENHANCER_FOLDER --in_dds_file $DDS_FILE --in_gene_file $GENE_FILE --out_folder $OUTPUT_FOLDER

