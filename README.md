# TMbed: Unofficial Google Colab Interface

<div align="center">

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1lUawtexMQaoCt6UWQN56P3MyvOTIsMBE?usp=sharing)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Paper](https://img.shields.io/badge/BMC_Bioinformatics-10.1186/s12859--022--04873--x-red.svg)](https://doi.org/10.1186/s12859-022-04873-x)
[![bioRxiv](https://img.shields.io/badge/bioRxiv-2022.06.12.495804-red.svg)](https://doi.org/10.1101/2022.06.12.495804)

</div>

## Overview

This Google Colab notebook provides an easy-to-use interface for **TMbed**, a transmembrane protein prediction tool developed by Bernhofer et al. (2022) that uses ProtT5-XL-U50 language model embeddings to predict transmembrane beta barrel and alpha helical proteins, segment positions and orientations, and signal peptides. This implementation is simply a user-friendly Colab wrapper that makes the original TMbed model accessible through a streamlined notebook interface.

**🚀 [Click here to open the TMbed Colab notebook](https://colab.research.google.com/drive/1lUawtexMQaoCt6UWQN56P3MyvOTIsMBE?usp=sharing)**

> **Note**: This is an unofficial Google Colab implementation. All credit for the TMbed model, methodology, and scientific contributions goes to the original authors. This notebook simply provides a convenient interface for running their published model.

## Key Features of This Interface

- **🧬 Access to TMbed**: Easy access to state-of-the-art transmembrane protein prediction
- **⚡ Simplified Workflow**: Run TMbed through a user-friendly 3-cell notebook interface
- **📁 FASTA Upload**: Simple file upload with automatic processing and .gz decompression support
- **🏷️ Custom Prefixes**: Add custom prefixes to output files for better organization
- **☁️ Google Drive Integration**: Optional automatic upload of results to your Google Drive
- **🔧 Multiple Output Formats**: Choose from 5 different output formats with automatic GFF conversion for all formats
- **📊 Comprehensive Results**: Prediction files with GFF format for downstream analysis (all formats supported)
- **🔄 Fallback Download**: Automatic fallback to local download if Google Drive unavailable

## Input Methods

### FASTA File Upload
Upload protein sequences in FASTA format for batch processing with:
- Automatic file validation and processing
- Support for multi-sequence FASTA files
- **Automatic .gz decompression**: Upload compressed FASTA files and they'll be automatically decompressed
- **Custom file prefixes**: Add prefixes like "experiment1_" to organize output files
- Clean filename handling (removes Colab duplicate numbering)

## Configuration Options

### Output Format Selection
Choose from 5 different TMbed output formats:

- **Format 0** (default): 3-line format with directed segments (B/b for beta strands, H/h for alpha helices)
- **Format 1**: 3-line format with undirected segments and inside/outside annotation
- **Format 2**: Tabular format with directed segments and probabilities
- **Format 3**: Tabular format with undirected segments and probabilities  
- **Format 4**: 3-line format with directed segments and explicit inside/outside prediction

### Google Drive Integration
- **Optional Connection**: Choose whether to connect to Google Drive
- **Custom Folder**: Specify Google Drive folder name for organized storage
- **Automatic Fallback**: Downloads files normally if Google Drive connection fails
- **Smart Upload**: Uploads both prediction files and converted GFF files when applicable

## Workflow

1. **Configuration**: Upload FASTA file, select output format, and configure Google Drive settings
2. **Installation**: Run the installation cell to set up TMbed and dependencies  
3. **Prediction & Results**: Execute prediction and automatically process results with upload/download

## Output Files

Each prediction generates:
- **Prediction file**: TMbed output in selected format (`.pred` extension)
- **GFF file**: Converted GFF3 format for ALL formats (for genome browsers and annotation tools)
- **Google Drive upload**: Automatic cloud storage when enabled
- **Local download**: Fallback download when Google Drive unavailable

**Example file naming (input: `RLPs.fasta`, prefix: `experiment1_`)**:
- `experiment1_RLPs.pred` (prediction file)
- `experiment1_RLPs.gff` (GFF annotation file)

### Format Examples

**Format 0 (3-line directed)**:
```
>sequence_id
MKTVRQERLKSIVRIL...
SSSSSS.......HHHHHHHHHHHhhhhhhhhhh....
```

**Format 2 (tabular with probabilities)**:
```
>sequence_id
AA  PRD P(B)    P(H)    P(S)    P(i)    P(o)
M   S   0.00    0.00    0.94    0.05    0.00
K   S   0.00    0.00    0.98    0.02    0.00
```

**GFF3 (converted from all formats using universal converter)**:
```
##gff-version 3
sequence_id	TMbed	signal_peptide	1	6	.	.	.	ID=sequence_id_signal_peptide-1;Name=signal_peptide
sequence_id	TMbed	outside	7	19	.	.	.	ID=sequence_id_outside-1;Name=outside
sequence_id	TMbed	TMhelix	20	42	.	.	.	ID=sequence_id_TMhelix-1;Name=TMhelix
sequence_id	TMbed	inside	43	60	.	.	.	ID=sequence_id_inside-1;Name=inside
```

## System Requirements

- **Platform**: Google Colab with GPU runtime (recommended)
- **Memory**: GPU runtime recommended for faster processing
- **Runtime**: T4, V100, or A100 GPUs supported
- **Internet**: Required for model downloads and Google Drive integration

## TMbed Prediction Classes

### Residue Classes
- **B/b**: Transmembrane beta strand (B = IN→OUT, b = OUT→IN)
- **H/h**: Transmembrane alpha helix (H = IN→OUT, h = OUT→IN)  
- **S**: Signal peptide
- **. / i**: Inside/non-transmembrane (inside)
- **o**: Outside/non-transmembrane (outside)

### Applications
- **Membrane protein identification**: Screen proteomes for transmembrane proteins
- **Topology prediction**: Determine segment orientation and position
- **Signal peptide detection**: Identify secretion signals
- **Genome annotation**: Generate GFF files for genome browsers
- **Structural analysis**: Complement structure prediction workflows

## Citation

If you use this notebook in your research, please cite the TMbed papers:

**TMbed: transmembrane proteins predicted through language model embeddings**  
Bernhofer, M., Littmann, M., Heinzinger, M., Weissenow, K., Hirsch-Hoffmann, J., Henkel, T., & Rost, B. (2022)  
*BMC Bioinformatics* [https://doi.org/10.1186/s12859-022-04873-x](https://doi.org/10.1186/s12859-022-04873-x)

**TMbed: transmembrane proteins predicted through language model embeddings**  
Bernhofer, M., Littmann, M., Heinzinger, M., Weissenow, K., Hirsch-Hoffmann, J., Henkel, T., & Rost, B. (2022)  
*bioRxiv* [https://doi.org/10.1101/2022.06.12.495804](https://doi.org/10.1101/2022.06.12.495804)

**ProtTrans: Towards Cracking the Language of Life's Code Through Self-Supervised Deep Learning and High Performance Computing**  
Elnaggar, A., Heinzinger, M., Dallago, C., Rihawi, G., Wang, Y., Jones, L., Gibbs, T., Feher, T., Angerer, C., Bhowmik, D., & Rost, B. (2021)  
*IEEE Transactions on Pattern Analysis and Machine Intelligence* [https://doi.org/10.1109/TPAMI.2021.3095381](https://doi.org/10.1109/TPAMI.2021.3095381)

<details>
<summary>BibTeX format</summary>

```bibtex
@article{bernhofer2022tmbed,
    title={TMbed: transmembrane proteins predicted through language model embeddings},
    author={Bernhofer, Michael and Littmann, Maria and Heinzinger, Michael and Weissenow, Konstantin and Hirsch-Hoffmann, Joachim and Henkel, Tobias and Rost, Burkhard},
    journal={BMC bioinformatics},
    volume={23},
    number={1},
    pages={1--20},
    year={2022},
    publisher={Springer},
    doi={10.1186/s12859-022-04873-x}
}

@article{bernhofer2022tmbed_preprint,
    title={TMbed: transmembrane proteins predicted through language model embeddings},
    author={Bernhofer, Michael and Littmann, Maria and Heinzinger, Michael and Weissenow, Konstantin and Hirsch-Hoffmann, Joachim and Henkel, Tobias and Rost, Burkhard},
    journal={bioRxiv},
    year={2022},
    doi={10.1101/2022.06.12.495804}
}

@article{elnaggar2021prottrans,
    title={ProtTrans: Towards Cracking the Language of Life's Code Through Self-Supervised Deep Learning and High Performance Computing},
    author={Elnaggar, Ahmed and Heinzinger, Michael and Dallago, Christian and Rihawi, Ghalia and Wang, Yu and Jones, Llion and Gibbs, Tom and Feher, Tamas and Angerer, Christoph and Bhowmik, Debsindhu and Rost, Burkhard},
    journal={IEEE Transactions on Pattern Analysis and Machine Intelligence},
    year={2021},
    doi={10.1109/TPAMI.2021.3095381}
}
```

</details>

## Disclaimer

This Google Colab notebook is an independent implementation created to make the TMbed model more accessible. All scientific credit, model development, and methodological contributions belong to the original TMbed team. This notebook serves purely as a user interface wrapper around their published work and does not represent any original research or model development.

For the official TMbed implementation and latest updates, please visit the [official TMbed repository](https://github.com/BernhoferM/TMbed).

## Troubleshooting

**Common Issues:**
- **GPU Memory**: Reduce batch size if encountering memory issues
- **Runtime Errors**: Use "Factory reset runtime" in Google Colab  
- **Upload Issues**: Ensure proper FASTA formatting and file extensions
- **Google Drive Connection**: Check authentication and folder permissions
- **Download Problems**: Verify browser allows downloads from Colab

**File Format Requirements:**
- FASTA files must have `.fasta`, `.fa`, or `.fas` extensions (`.gz` compression supported)
- Sequences should contain only standard amino acid codes
- Headers should start with `>` followed by sequence identifier
- Compressed files (.gz) are automatically decompressed after upload

## Related Resources

- [Official TMbed Repository](https://github.com/BernhoferM/TMbed)
- [TMVisDB - Precomputed Predictions](https://tmvisdb.predictprotein.org)
- [ProtT5 Model](https://huggingface.co/Rostlab/prot_t5_xl_half_uniref50-enc)
- [bio_embeddings Integration](https://github.com/sacdallago/bio_embeddings)
- [LambdaPP Web Interface](https://embed.predictprotein.org/)
- [Original TMbed Colab](https://colab.research.google.com/drive/1FbT2rQHYT67NNHCrGw4t0WMEHCY9lqR2?usp=sharing)

---

**Author**: Jiorgos Kourelis  
**Last Updated**: July 24, 2025