Get Started
-------------------------
-------------------------

Epcotv2 is a general-purpose foundation model for integrative genomic prediction,
capable of inferring diverse regulatory modalities from minimal input data. Unlike task-specific
models, this architecture unifies transcriptional and chromatin-level outputs within a shared
multi-task framework.

.. image:: overview.png
   :alt: Overview of the multi-task genomic model
   :align: center
   :width: 600px

Model Inputs
------------

The model takes the following as input:

- **DNA sequence**: One-hot encoded sequence centered on each genomic region of interest
- **ATAC-seq signal**: Chromatin accessibility profiles for the same regions

Both inputs are designed to be cell-type specific and jointly encode local cis-regulatory information.

Predicted Modalities
--------------------

The model is trained in a multi-task setting to directly predict a broad range of genomic and epigenomic modalities from DNA sequence and ATAC-seq input. These include:

- **Nascent transcription signals**, such as PRO-seq, GRO-seq, TT-seq, and related strand-specific assays
- **Total and polyA+ RNA-seq**, capturing steady-state expression
- **Chromatin accessibility and histone modifications**, covering a wide panel of epigenomic marks
- **3D chromatin organization**, including Micro-C, Hi-C, and ChIA-PET contact maps
- **Transcription initiation signals**, such as CAGE-seq and GRO-cap
- **Synthetic enhancer activity**, including STARR-seq

A complete list of supported modalities can be found in the repository under ``data/epi_list`` and ``data/extra_tf_list.txt``.

All outputs are aligned to a shared genomic coordinate system, enabling consistent evaluation and downstream analysis.

Cross-Context Generalization
----------------------------

The model is trained across a large number of human cell types and tissues. It generalizes well
to unseen biological contexts, and supports cross-species transfer.

This model can be used for:

- Predicting transcriptional output from accessible chromatin regions
- Characterizing regulatory elements in new tissues with only ATAC-seq and sequence
- Interpreting the potential functional role of non-coding genetic variants
- Reconstructing 3D chromatin architecture in data-limited settings

Installation
-------------------------

To set up the model locally for inference or fine-tuning, follow the steps below:

.. code-block:: bash

    git clone https://github.com/liu-bioinfo-lab/general_AI_model.git
    cd general_AI_model
    # setup environment
    conda create -n epcot python==3.9
    conda activate epcot
    pip install -r requirements.txt

One can refer to **epcotv2_basic_tutorial.ipynb** for the basic usage of this model.
