# HuggingFace Model/Dataset Downloader

Download models, datasets, and spaces from HuggingFace Hub to Google Drive.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/WhoisMonesh/Colab-HuggingFace-Downloader/blob/main/Colab-HuggingFace-Downloader.ipynb)

---

## Quick Start

1. **Open in Colab** (click badge above)
2. **Mount Drive** when prompted
3. **Set `REPO_ID`** in section 3 (e.g. `'mistralai/Mistral-7B-v0.1'`)
4. **Run all cells**

Your model files will appear in your Google Drive under `HuggingFaceModelDownloader/`.

---

## Features

| Feature | Description |
|---|---|
| **Models, Datasets, Spaces** | Supports all HuggingFace Hub repo types |
| **Glob Filtering** | `FILE_PATTERN` to download only specific files (e.g. `*.safetensors`) |
| **Recursive Structure** | Preserves subdirectory structure during zip and Drive move |
| **Sync-safe** | Downloads to local temp, moves to Drive after completion |
| **Keep-Alive** | JavaScript prevents Colab timeout during large model downloads |
| **Auto-Zip** | Uses `shutil.make_archive` for fast recursive zipping |

---

## Where to Put the Repo ID

In section **3. Configuration**, find this line and set your repo:

```python
REPO_ID = 'mistralai/Mistral-7B-v0.1'  # <-- set your repo ID here
```

### Examples

| Type | REPO_ID |
|---|---|
| Model | `'mistralai/Mistral-7B-v0.1'` |
| Dataset | `'datasets/imdb'` (also set `REPO_TYPE = 'dataset'`) |
| Space | `'black-forest-labs/FLUX.1-schnell'` (also set `REPO_TYPE = 'space'`) |

### File Filtering

```python
FILE_PATTERN = '*.safetensors'       # only .safetensors files
FILE_PATTERN = '*.bin'                # only .bin files
FILE_PATTERN = 'config.json'          # single file
FILE_PATTERN = '*'                    # everything (default)
```

---

## All Configuration Options

| Variable | Default | Description |
|---|---|---|
| `SAVE_PATH` | `/content/downloads/HuggingFaceModelDownloader/` | Local temp directory |
| `DRIVE_PATH` | `/content/drive/My Drive/HuggingFaceModelDownloader/` | Final Drive destination |
| `REPO_ID` | `''` | HuggingFace repo ID (e.g. `'mistralai/Mistral-7B-v0.1'`) |
| `REPO_TYPE` | `'model'` | Repo type: `'model'`, `'dataset'`, or `'space'` |
| `FILE_PATTERN` | `'*'` | Glob pattern to filter which files to download |
| `KEEP_ALIVE` | `True` | Prevent Colab timeout |

---

## Technical Details

- Uses `huggingface_hub.snapshot_download` for reliable repo downloading
- Glob filtering via `allow_patterns` parameter (native HF Hub support)
- Recursive file collection via `os.walk` for proper subdirectory handling
- Fast zipping via `shutil.make_archive` (preserves directory structure)
- Downloads to `/content/downloads/` first, then `shutil.move` to Drive (avoids FUSE sync conflicts)
- JavaScript keep-alive prevents Colab session timeout

---

## Fair Use & Legal Notice

This tool downloads publicly available models, datasets, and spaces from HuggingFace Hub for **personal, non-commercial use only**.

**You agree to:**
- Comply with each model/dataset's specific license (e.g. Apache 2.0, MIT, CC-BY, Llama Community License, etc.)
- Respect HuggingFace's terms of service and rate limits
- Use downloaded content in accordance with its intended license
- Attribute model/dataset authors as required by their license

**You may NOT use this tool to:**
- Download content protected by access restrictions or gated repositories (unless you have authorized access)
- Mass-download for commercial purposes without license compliance
- Violate any applicable export control laws or content restrictions
- Redistribute or re-upload downloaded models without license permission

**Disclaimer:** The authors are not responsible for how you use this software. You assume all legal responsibility for the content you download and its subsequent use. This tool is provided for educational purposes only. Always check the license of each model or dataset before downloading.

---

## License

MIT
