# Offline Translator — Unreal Engine Plugin

**Offline neural machine translation for Unreal Engine 5.6 and 5.7**  
Translate text between 12 language pairs with no internet connection required.  
Powered by [CTranslate2](https://github.com/OpenNMT/CTranslate2) and [Opus-MT](https://github.com/Helsinki-NLP/Opus-MT) models.

---

## Features

- **100% Offline** — No internet required at runtime. Models run entirely on CPU.
- **12 Language Pairs** — English ↔ German, French, Spanish, Italian, Russian, Polish
- **Blueprint Ready** — Simple nodes usable in any Blueprint
- **Two APIs** — Quick one-liner via BP Library, or full control via Game Instance Subsystem
- **Async Support** — Non-blocking translation that keeps your game running smoothly
- **Sentence & Paragraph modes** — Optimized for both short NPC dialogue and long text
- **Fast** — 365–620ms per translation on CPU (oneDNN accelerated)
- **Lightweight** — ~80MB per language pair, load only what you need

---

## Supported Language Pairs

| Source | Target | Model Size |
|--------|--------|------------|
| English | German | ~80MB |
| German | English | ~80MB |
| English | French | ~80MB |
| French | English | ~80MB |
| English | Spanish | ~80MB |
| Spanish | English | ~80MB |
| English | Italian | ~89MB |
| Italian | English | ~89MB |
| English | Russian | ~80MB |
| Russian | English | ~80MB |
| English | Polish | ~79MB |
| Polish | English | ~79MB |

---

## Installation

### 1. Purchase and Install from Fab
Purchase the plugin from the [Fab Marketplace](#) and install it to your engine via the Epic Games Launcher. The plugin will appear under **Edit → Plugins → Offline Translator**.

### 2. Enable the Plugin
Open your project in Unreal Engine, go to **Edit → Plugins**, search for **Offline Translator** and enable it. Restart the editor when prompted.

### 3. Update DefaultGame.ini
Add the following to your project's `Config/DefaultGame.ini` to ensure models are staged correctly in packaged builds:

```ini
[/Script/UnrealEd.ProjectPackagingSettings]
+DirectoriesToAlwaysStageAsNonUFS=(Path="OfflineTranslatorModels")
```

### 4. Download Models
Open the Unreal console (backtick) and run:
```
OfflineTranslator.DownloadModel English German
```

Replace `English` and `German` with your desired language pair. Available languages:
`English`, `German`, `French`, `Spanish`, `Italian`, `Russian`, `Polish`

To delete a model:
```
OfflineTranslator.DeleteModel English German
```

---

## Quick Start

### Option 1 — BP Library (Simple)

The quickest way to translate:

1. Call **Initialize Translator** at game start (e.g. Event BeginPlay)
2. Wait for **On Ready** callback
3. Call **Quick Translate** anywhere in your Blueprint

### Option 2 — Subsystem (Full Control)

For games that need persistent translation state:

1. **Get Offline Translator Subsystem** — gets the subsystem reference
2. **Initialize Translator** — loads model into memory (~1-3 seconds, async)
3. **Translate Sentence Async** — translate without blocking game thread
4. **Shutdown Translator** — unload model and free memory when done

---

## Blueprint Nodes Reference

### Initialization
| Node | Description |
|------|-------------|
| `Initialize Translator` | Load a language model into memory. Call once before translating. |
| `Shutdown Translator` | Unload model and free ~300MB RAM. |
| `Is Translator Ready` | Returns true if model is loaded and ready. |

### Translation
| Node | Description |
|------|-------------|
| `Translate Sentence` | Translate a single sentence. Blocks game thread briefly. |
| `Translate Sentence Async` | Translate without blocking. Result via callback. |
| `Translate Paragraph` | Translate multi-sentence text. Better structure preservation. |
| `Translate Paragraph Async` | Non-blocking paragraph translation. |
| `Quick Translate` | One-liner: translate without managing subsystem. |

### Utility
| Node | Description |
|------|-------------|
| `Is Language Pair Supported` | Check if a pair has a model available. |
| `Get Backend Name` | Returns compute backend (e.g. oneDNN). |
| `Get Offline Translator` | Get subsystem reference from anywhere. |

---

## Sentence vs Paragraph Mode

**Sentence mode** — treats the entire input as one sentence. Best for short single-line NPC dialogue.

**Paragraph mode** — splits input into individual sentences, translates each separately, then joins them. Best for multi-line dialogue, item descriptions, quest text, and subtitles. Produces more faithful translations of structured text.

---

## Project Settings

Go to **Project Settings → Plugins → Offline Translator**:

| Setting | Description |
|---------|-------------|
| Source Language | Default language to translate FROM |
| Target Language | Default language to translate TO |
| Models Directory | Where models are stored (default: Content/OfflineTranslatorModels) |
| Model Status | Shows if the selected model is downloaded |
| CPU Threads | Number of threads (1 recommended, 0 = auto) |
| Beam Size | Translation quality vs speed (4 recommended) |
| Package Models With Game | Include models in packaged builds |

---

## Use Cases

- **Localization testing** — Quickly test your game in multiple languages during development
- **Dynamic NPC dialogue** — Translate procedurally generated NPC lines at runtime
- **Player-generated content** — Translate player chat or input text
- **Subtitle generation** — Translate cutscene dialogue on the fly
- **Debug logging** — Translate debug output without internet access

---

## Licensing

| Component | License |
|-----------|---------|
| Plugin source code | MIT |
| CTranslate2 | Apache 2.0 |
| SentencePiece | Apache 2.0 |
| Opus-MT models (EN↔DE/FR/ES/IT/RU) | CC-BY 4.0 |
| Opus-MT models (EN↔PL) | Apache 2.0 |
| oneDNN | Apache 2.0 |
| OpenBLAS | BSD 3-Clause |

---

## Support

- **Bug reports and feature requests:** [GitHub Issues](https://github.com/rohanksaxena/offline-translator/issues)
- **Models:** [HuggingFace](https://huggingface.co/rohanksaxena)
