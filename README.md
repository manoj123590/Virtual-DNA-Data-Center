# Virtual DNA Data Center — GreenDNA AI Framework for Sustainable Data Storage

**Author:** Manoj M  
**Project type:** Software-only research prototype / educational simulation  
**Core idea:** Simulate a DNA-inspired archival storage pipeline in software, from lossless compression and binary-to-nucleotide encoding to retrieval, integrity verification, and illustrative sustainability estimates.

> **Important:** This project is a computational model only. It does not synthesize, contain, or use biological DNA. Sustainability figures are illustrative simulation estimates, not measured real-world savings.

## Overview

GreenDNA AI models a Virtual DNA Data Center using a reversible two-bit-to-nucleotide mapping:

| Binary pair | Nucleotide |
|---|---|
| `00` | `A` |
| `01` | `C` |
| `10` | `G` |
| `11` | `T` |

The prototype compresses input data with Python's `zlib` (DEFLATE, level 9), converts the compressed bytes to bits, computes a SHA-256 checksum, maps each pair of bits to a nucleotide, and stores the resulting sequence as a virtual record. Retrieval reverses the process and verifies the recovered data.

## Key Features

- Accepts demonstration data and common text/structured inputs (the paper describes text, CSV and JSON).
- Profiles input data, including size, byte distribution, repeated patterns, entropy and estimated compressibility.
- Uses lossless compression before encoding.
- Converts compressed bytes into a binary bit stream.
- Maps every 2 bits to one of `A`, `C`, `G`, or `T`.
- Tracks padding and metadata needed for exact decoding.
- Uses SHA-256 to detect changes to the checksummed bit stream.
- Supports simulated nucleotide mutations to demonstrate integrity failure.
- Retrieves virtual records by storage ID (session-only in the described prototype).
- Produces sustainability estimates labelled **Illustrative Simulation Estimate**.

## Workflow

1. Receive and validate input.
2. Analyze the input and estimate compressibility.
3. Compress the data losslessly.
4. Convert compressed bytes to binary.
5. Calculate and store a SHA-256 checksum.
6. Add a padding bit if required.
7. Encode bit pairs as nucleotides.
8. Store the sequence, ID, metadata, checksum, padding and timestamp in virtual storage.
9. Retrieve a record by its ID.
10. Validate nucleotide symbols and check integrity.
11. Decode the sequence, remove padding and decompress.
12. Compare the recovered content and report success or failure.
13. Generate illustrative energy, cooling and water scenario estimates.

## Prototype Results Reported in the Paper

The paper reports that all six synthetic test inputs were reconstructed exactly and all simulated mutations in its tests were detected. Examples include:

| Input | Original size | Compressed size | Reported reduction | DNA sequence length |
|---|---:|---:|---:|---:|
| Repetitive text | 3,960 bytes | 94 bytes | 97.6% | 376 nt |
| Synthetic prose | 19,732 bytes | 6,575 bytes | 66.7% | 26,300 nt |
| JSON records | 30,417 bytes | 2,886 bytes | 90.5% | 11,544 nt |
| CSV records | 10,437 bytes | 2,584 bytes | 75.2% | 10,336 nt |
| Random bytes | 4,000 bytes | 4,011 bytes | -0.3% | 16,044 nt |
| Single character | 1 byte | 9 bytes | -800.0% | 36 nt |

These are results reported for the paper's synthetic prototype inputs, not guarantees for arbitrary files. Compression can increase the size of very small or high-entropy inputs.

## Technology

- **Language:** Python 3
- **Compression:** `zlib` (DEFLATE, level 9)
- **Integrity:** `hashlib` / SHA-256
- **Encoding:** Python dictionary mapping binary pairs to nucleotide symbols

The PDF describes the research and includes a reference implementation of the core pipeline. The full application/repository file structure, user interface, dependency list and exact run commands are not specified in the paper; add or update these sections once the actual code files are in the repository.

## Repository Structure (Suggested)

```text
virtual-dna-data-center/
├── README.md
├── docs/
│   └── research-paper.pdf
├── src/
│   └── greendna.py
├── tests/
│   └── test_pipeline.py
├── examples/
│   └── sample-input.json
├── LICENSE
└── .gitignore
```

This is a suggested structure, not a claim about the files currently in your GitHub repository. Keep only folders and files that actually exist.

## Getting Started

The paper specifies Python 3 and uses standard-library modules (`zlib` and `hashlib`) for its core pipeline. If you have saved the implementation as a Python file, run it using your installed Python 3 environment:

```bash
python --version
python src/greendna.py
```

Change the file path/command to match the actual filename in your repository. The PDF does not define a complete command-line or web-app entry point, so the command above is a template rather than a verified run command.

## Example: Core Mapping

The character `A` is ASCII byte `01000001`.

```text
Binary:       01 | 00 | 00 | 01
Nucleotides:   C |  A |  A |  C
Encoded:      CAAC
```

Decoding `CAAC` with the reverse mapping returns `01000001`, which represents `A`.

## Sustainability and Responsible Interpretation

The sustainability module uses assumptions for storage power, cooling overhead, water use and storage duration. Its results must always be labelled **Illustrative Simulation Estimate**. They are not measurements from an actual data center, and the paper does not establish real-world energy or water savings.

The virtual DNA store is an in-memory software simulation. It is not a replacement for physical storage or a real DNA archive.

## Limitations

- The simple mapping does not enforce real-DNA constraints such as GC balance or limits on long repeated bases.
- SHA-256 detects changes to the checksummed data but does not repair them.
- Compression may increase the size of small or random inputs.
- The analysis engine is rule-based / AI-inspired; the paper does not describe a trained machine-learning model.
- Sustainability outputs depend on user-provided assumptions.
- The reported tests use small synthetic data; large real-world archives were not evaluated.
- Records are session-only in the described prototype.
- The paper's appendix notes that changing only the final padding bit may not be detected because the checksum is computed before padding.

## Planned Future Work

The paper proposes:
1. Constrained nucleotide coding to reduce long runs and balance GC content.
2. Error-correcting codes to repair errors rather than only detect them.
3. Type-specific compression for text, JSON and CSV.
4. A learned model for compression selection.
5. Skipping compression for tiny or high-entropy inputs.
6. Persistent storage and storage-ID indexing.
7. Random-access indexing across many records.
8. Better-calibrated sustainability assumptions based on published data.
9. A web dashboard with charts and a mutation demo.
10. An encryption layer before encoding.

## Research Paper

Add the PDF to a folder such as `docs/` in your repository and link it here, updating the path to match the uploaded filename:

- **Research paper:** [`docs/research-paper.pdf`](docs/research-paper.pdf)

## References

The paper's reference list includes foundational work on DNA data storage, compression, hashing and information theory:

1. Church, G. M., Gao, Y., & Kosuri, S. (2012). “Next-generation digital information storage in DNA.” *Science*, 337(6102), 1628.
2. Goldman, N., et al. (2013). “Towards practical, high-capacity, low-maintenance information storage in synthesized DNA.” *Nature*, 494, 77–80.
3. Grass, R. N., et al. (2015). “Robust chemical preservation of digital information on DNA in silica with error-correcting codes.” *Angewandte Chemie International Edition*, 54(8), 2552–2555.
4. Erlich, Y., & Zielinski, D. (2017). “DNA Fountain enables a robust and efficient storage architecture.” *Science*, 355(6328), 950–954.
5. Organick, L., et al. (2018). “Random access in large-scale DNA data storage.” *Nature Biotechnology*, 36, 242–248.
6. Ziv, J., & Lempel, A. (1977). “A universal algorithm for sequential data compression.” *IEEE Transactions on Information Theory*, 23(3), 337–343.
7. National Institute of Standards and Technology. (2015). *Secure Hash Standard (SHS)*, FIPS PUB 180-4.
8. Shannon, C. E. (1948). “A mathematical theory of communication.” *Bell System Technical Journal*, 27, 379–423 and 623–656.

## Author

**Manoj M**  
B.Sc. Computer Science with Data Science  
DRBCCC Hindu College, Chennai

---

If you use or extend this work, please cite the research paper and clearly distinguish software simulation results from physical DNA-storage performance.
