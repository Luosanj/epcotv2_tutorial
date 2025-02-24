Tutorials for predicting human and mouse data modalities using EPCOT v2.
========================================================================

Introduction
------------
EPCOT v2 predicts diverse molecular modalities for the central 500kb regions extracted from 600kb segments across the entire genome.

Human Data Prediction
---------------------
(1) **Input file preparation.** The initial file, which is a BAM file, is pre-processed to become the input for EPCOT v2.

.. code-block:: console

   ## Generate the .bigWig file
   bamCoverage --bam input.bam -o ${cell_line}_atac.bigWig --outFileFormat bigwig --normalizeUsing RPGC \
   --effectiveGenomeSize 2913022398 --Offset 1 --binSize 1 --numberOfProcessors 12 \
   --blackListFileName ../data/black_list.bed
   ## Run atac_process.py to generate the .pickle file which is the required input format of EPCOT v2.
   python atac_process.py ${cell_line}_atac.bigWig

(2) **Prediction.**

(3) Extraction of each predicted modality.

Mouse Data Prediction
---------------------
(1) Input file preparation.

(2) Prediction.

(3) Extraction of each predicted modality.
