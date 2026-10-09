# Safetensors Joiner

> A lightweight, client-side web utility to concatenate sharded `.safetensors` model weights into a single, unified `.safetensors` file[cite: 2]. Completely offline, zero dependencies, and runs directly inside your browser[cite: 2].

**[Live Demo](https://www.google.com/search?q=https://your-username.github.io/repository-name/)** • **[Quick Start](https://www.google.com/search?q=%23quick-start)** • **[Features](https://www.google.com/search?q=%23features)** • **[Supported Dtypes](https://www.google.com/search?q=%23supported-data-types)** • **[Browser Notes](https://www.google.com/search?q=%23browser-support--performance)**

---

## Overview

**Safetensors Joiner** is a self-contained, single-file HTML utility designed to merge partitioned deep learning checkpoints (e.g., `model-00001-of-00004.safetensors` to `model-00004-of-00004.safetensors`) into a single consolidated file[cite: 2].

* **Complete Data Privacy:** Processes files entirely on the client side using the HTML5 File API and File System Access API[cite: 2]. No network requests are made, and no weights leave your local machine[cite: 2].
* **Low Memory Footprint:** Uses chunked streaming writes (64 MB buffers) to assemble massive multi-gigabyte models without crashing system memory[cite: 2].
* **Pre-Join Diagnostics:** Audits shard continuity, file integrity, index mappings, and tensor byte offsets before any data is written[cite: 2].

---

## Quick Start

1. Download or clone `safetensors-joiner.html`[cite: 2]:
```bash
git clone https://github.com/your-username/repository-name.git

```


2. Open `safetensors-joiner.html` in any supported desktop web browser (double-click to open)[cite: 2].
3. Import your model shards by using **Choose files…**, selecting a folder via **Choose folder…**, or dragging and dropping the files directly into the drop zone[cite: 2].
4. Verify the **Checks** panel displays *All checks passed*[cite: 2].
5. Click **Join & save…** and pick your destination path[cite: 2].

> **Important:** After generating your combined file, move or delete `model.safetensors.index.json` from the target model folder[cite: 2]. Downstream loaders look for index files first and may attempt to read the non-existent shards if the index remains present[cite: 2].

---

## Features

### 1. Robust Pre-Flight Safety Checks

* **Missing Shard Detection:** Automatically parses shard naming sequences (`-0000N-of-0000M`) and highlights missing shards[cite: 2].
* **Corruption & Truncation Checks:** Identifies incomplete downloads or malformed files before joining starts[cite: 2].
* **Index Cross-Verification:** Validates whether all tensors referenced in `model.safetensors.index.json` are present in the provided shards[cite: 2].
* **Shape & Byte Size Validation:** Re-evaluates each tensor's raw byte payload against its declared data type (`dtype`) and tensor shape[cite: 2].
* **Format Discrimination:** Flags incompatible formats (such as `.bin`, `.pt`, `.ckpt`, and `.gguf`) with descriptive explanations[cite: 2].

### 2. Flexible Merge Configuration

* **Duplicate Tensor Resolution:** Choose to stop execution (default), keep the first instance, retain the last instance, or rename duplicates sequentially (e.g., `name__2`)[cite: 2].
* **Memory-Alignment Modes:**
* *Alignment-safe (Default):* Follows the official Hugging Face safetensors standard, aligning every tensor start offset to boundary requirements for the corresponding dtype[cite: 2].
* *Same as source:* Preserves the raw sequential order of the input shards[cite: 2].


* **Regex Tensor Exclusion:** Filter out specific weight blocks (e.g., `^lm_head\.` or training states) via regular expressions to save storage space[cite: 2].
* **Metadata Aggregation:** Merges `__metadata__` fields across all shards, reports conflicting keys, and supports custom inline JSON edits[cite: 2].
* **Tensor Explorer:** Search, filter, and inspect tensor attributes (dtype, dimensions, source shard) directly in the UI[cite: 2].

### 3. Post-Save File Integrity Verification

Once the combined file is assembled, the tool performs an automatic verification pass[cite: 2]:

* Confirms file length matches computed byte projections[cite: 2].
* Parses the output JSON header structure and total tensor count[cite: 2].
* Performs byte-for-byte spot checks between sampled tensors and their original source shard data[cite: 2].

---

## Supported Data Types

Supports all standard and cutting-edge deep learning dtypes[cite: 2]:

* **Standard Numeric:** `BOOL`, `U8`, `I8`, `I16`, `U16`, `I32`, `U32`, `I64`, `U64`, `F16`, `BF16`, `F32`, `F64`, `C64`[cite: 2]
* **8-bit Floats (FP8):** `F8_E5M2`, `F8_E4M3`, `F8_E4M3FN`, `F8_E8M0`[cite: 2]
* **Sub-Byte Formats:** `F4`, `F6_E2M3`, `F6_E3M2`[cite: 2]

*Unrecognized custom dtypes are transferred as raw bytes with an accompanying UI warning[cite: 2].*

---

## Browser Support & Performance

| Browser | Recommended | Write Mechanism | Performance Notes |
| --- | --- | --- | --- |
| **Google Chrome / Microsoft Edge** | **Yes**[cite: 2] | Direct-to-disk streaming via File System Access API[cite: 2] | Streams in 64 MB chunks[cite: 2]. Low RAM usage; includes active transfer speed and ETA[cite: 2]. |
| **Mozilla Firefox / Apple Safari** | Compatible[cite: 2] | Standard browser blob download[cite: 2] | Saves to default Downloads folder[cite: 2]. Less reliable when joining large multi-gigabyte models[cite: 2]. |

### System Requirements

* Adequate free disk space matching the total size of the final merged model[cite: 2].
* An exFAT or NTFS drive when saving files exceeding **4 GB** (FAT32 file systems do not support single files over 4 GB)[cite: 2].

---

## Important Scope Notes

* **Concatenation vs. Merging:** This utility **joins sharded pieces** of a single segmented checkpoint[cite: 2]. It is not designed to perform model weight arithmetic, LoRA merges, spherical linear interpolations (SLERP), or model soups[cite: 2].
* **Folder Permissions:** When selecting a directory via **Choose folder…**, Chromium-based browsers display a native prompt: *"Upload N files to this site?"*[cite: 2]. This is standard browser phrasing for folder read access—no data is sent over the network[cite: 2].

---

## License

Distributed under the **MIT License**[cite: 2]. See the [LICENSE](https://www.google.com/search?q=LICENSE) file for details[cite: 2].

---

### Recommended GitHub Repository Settings

* **Repository Description:**
> *"Client-side, offline web tool to join sharded .safetensors model files into a single file with zero dependencies and real-time integrity verification."*


* **Repository Topics / Tags:**
`safetensors`, `machine-learning`, `llm`, `deep-learning`, `huggingface`, `model-weights`, `offline-tool`, `vanilla-js`, `file-system-access-api`, `single-file`
