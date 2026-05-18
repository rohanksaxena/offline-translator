# Changelog

All notable changes to the Offline Translator plugin will be documented here.

---

## [1.0.1] — 2026

### Fixed
- Model downloader now downloads all required files including 
  vocab.json and shared_vocabulary.json which are needed by 
  CTranslate2 for translation
- Added retry logic (up to 4 attempts) for intermittent SSL 
  connection errors when downloading from HuggingFace
- Added manual download instructions in error message if all 
  retries fail

## [1.0.0] — 2026

### Added
- Initial release
- 12 language pairs: English ↔ German, French, Spanish, Italian, Russian, Polish
- Sentence and paragraph translation modes
- Synchronous and asynchronous translation nodes
- Game Instance Subsystem API for full control
- BP Library API for quick one-liner translation
- Project Settings panel with model management
- Console commands: `OfflineTranslator.DownloadModel`, `OfflineTranslator.DeleteModel`
- Model status indicator in Project Settings
- Smart language swap when same language selected for source and target
- Package Models With Game toggle
- Windows 64-bit support
- Unreal Engine 5.7

