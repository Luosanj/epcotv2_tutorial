Tutorials for predicting human and mouse data modalities using EPCOT v2.
========================================================================

Introduction
------------
EPCOT v2 predicts diverse molecular modalities for the central 500kb regions extracted from 600kb segments across the entire genome.

Human Data Prediction
---------------------
(1) **Input file preparation.** The initial file, which is a BAM file, is pre-processed to become the input for EPCOT v2. The name of the generated .bigWig file is formatted as '{cell_line_name}_atac'.**Note** The detailed locations (chrom id, start pos, end pos) of each 600kb region is stored in file "input_region_600kb.bed", which can be found on Github. There are 11,123 600kb regions across the whole human genome.

.. code-block:: bash

    ## Generate the .bigWig file
    bamCoverage --bam input.bam -o ${cell_line}_atac.bigWig --outFileFormat bigwig --normalizeUsing RPGC \
    --effectiveGenomeSize 2913022398 --Offset 1 --binSize 1 --numberOfProcessors 12 \
    --blackListFileName ../data/black_list.bed
    ## Run atac_process.py to generate the .pickle file which is the required input format of EPCOT v2.
    python atac_process.py ${cell_line}_atac.bigWig

(2) **Prediction.** Please confirm the directories of input ${cell_line}_atac.pickle file and the output ${cell_line}.pickle file. You can specify which modality you want to predict in file "tt_pred_gw.py" by modifying variable "pred_modalities".

 .. code-block:: bash

     ## Run the model execution file tt_pred_gw.py to predict desired molecular modalities. 
     python tt_pred_gw.py

(3) Extraction of each predicted modality. Assume the output file is called 'spleen.pickle'. 

.. code-block:: python

    import pickle
    with open('/nfs/turbo/umms-drjieliu/usr/luosanj/spleen.pickle', 'rb') as file:
        spleen_pickle = pickle.load(file)
    ## All predicted modalities
    spleen_pickle['epi']
    spleen_pickle['rna'] # expected shape: (11123, 500, 3)
    spleen_pickle['bru'] # expected shape: (11123, 500, 3)
    spleen_pickle['microc']  # expected shape: (11123, 500, 2)
    spleen_pickle['hic'] # expected shape: (11123, 500, 3)
    spleen_pickle['intacthic'] # expected shape: (11123, 500, 2)
    spleen_pickle['rna_strand'] # expected shape: (11123, 500, 2)
    spleen_pickle['external_tf'] 
    spleen_pickle['tt'] # expected shape: (11123, 500, 2)
    spleen_pickle['groseq'] # expected shape: (11123, 500, 2)
    spleen_pickle['grocap'] # expected shape: (11123, 500, 4)
    spleen_pickle['proseq'] # expected shape: (11123, 500, 3)
    spleen_pickle['netcage'] # expected shape: (11123, 500, 2)
    spleen_pickle['starr'] # expected shape: (11123, 500, 1)

Here is the explanation of each modality that can be predicted:
(1) Epigenomic features. The list of epigenomic features can be found on Github in a file named "epigenomes.txt".
(2) RNA-seq. 1. CAGE-seq 2. Total RNA-seq 3. PolyA+ RNA-seq
(3) Bru-seq. 1. Bru-seq 2. BruUV-seq 3. BruChase-seq
(4) Micro-c. 1. O/E normalized Micro-C 2. KR normalized Micro-C
(5) Hi-C. 1. CTCF ChIA-PET 2. RNApol2 ChIA-PET 3. Hi-C
(6) Intact Hi-C. 1. O/E normalized intact Hi-C 2. KR normalized intact Hi-C
(7) RNA Strand. 1. Total RNA-seq (forward) 2. Total RNA-seq (reverse)
(8) Additional TFs. The list of additional TFs can be found on Github in a file named unseeen_tf.txt
(9) TT-seq. 1. TT-seq (forward) 2. TT-seq (reverse)
(10) GRO-seq. 1. GRO-seq (forward) 2. GRO-seq (reverse)
(11) GRO-cap. 1. GRO-cap (forward) 2. GRO-cap (reverse) 3. GRO-cap_wTAP (forward) 4. GRO-cap_wTAP(reverse)
(12) PRO-seq. 1. PRO-seq (forward) 2. PRO-seq (reverse) 3. PRO-cap
(13) NET-CAGE. 1. NET-CAGE (forward) 2. NET-CAGE (reverse)
(14) STARR-seq. 1. STARR-seq

Mouse Data Prediction
---------------------
(1) Input file preparation.

(2) Prediction.

(3) Extraction of each predicted modality.
