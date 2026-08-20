# TomatoMTL Bilingual Chapter Exporter

Private unpacked Manifest V3 Chrome extension.

## What it exports

Each TomatoMTL chapter page is loaded once and produces two files.

Chinese:
- title: `chapter_title`
- body: `txt_content`
- matches the content used by TomatoMTL's Raw button

English:
- title: `chapter_title_translated`
- body: cleaned text from `chapter_content_translated`

Both files contain only the chapter title and chapter body. The TomatoMTL footer and source URL are omitted.

## Output layout

Files are saved under Chrome's normal download directory:

```text
TomatoMTL/
└── <book ID>/
    ├── Chinese/
    │   ├── 0001 - <Chinese title>.txt
    │   ├── 0002 - <Chinese title>.txt
    │   └── ...
    └── English/
        ├── 0001 - <English title>.txt
        ├── 0002 - <English title>.txt
        └── ...
```

## Installation

1. Extract this folder somewhere permanent, for example:
   `~/.local/share/tomatomtl-bilingual-exporter`
2. Open Chrome and go to `chrome://extensions`.
3. Enable **Developer mode**.
4. Select **Load unpacked**.
5. Choose the extracted extension directory.
6. Pin the extension if desired.

## Use

1. Open a logged-in TomatoMTL chapter.
2. Open the extension.
3. Choose:
   - current chapter or beginning of book
   - maximum chapter count
   - delay
   - base download folder
4. Press **Start new job**.
5. Keep the TomatoMTL tab open.
6. The popup may be closed while the job continues.

To change the delay or base folder during a saved job,
edit the field and press **Apply settings**.

## Rate-limit behaviour

- One chapter page creates both Chinese and English files.
- Bilingual export therefore does not double chapter requests.
- A single job may span the entire remaining book.
- **All available** is checked by default, meaning all remaining chapters; default delay is 30 seconds.
- Chrome background alarms have a 30-second minimum.
- The extension also pauses after 90 extension-managed chapter loads
  in a rolling hour.
- It does not attempt to bypass TomatoMTL or Cloudflare limits.
- Manual browsing and earlier scripts are not visible to the
  extension's internal request counter.

## Notes

- Starting a new job replaces the extension's saved job state.
- Chrome may create a uniquely named duplicate if a file already exists.
- Keep the unpacked extension directory after loading it.


## Version 0.2.2

- Default delay changed from 45 seconds to 30 seconds.
- Chinese and English downloads no longer include the TomatoMTL footer or source URL.
- Each text file now contains only the chapter title, a blank line, and the chapter body.


## Version 0.2.3

- Adds one `source.txt` file at the book root.
- `source.txt` contains the TomatoMTL source URL.
- Chinese and English chapter files remain footer-free.


## Version 0.2.4

- Removed the 90-chapter per-job ceiling.
- `Maximum chapters = 0` now means all remaining chapters.
- Long books can run as one persistent job.
- The existing rolling-hour safety limiter remains active and automatically pauses/resumes the same job.


## Version 0.2.5

- Replaced the special `Maximum chapters = 0` behavior with an explicit **All available** checkbox.
- **All available** is checked by default.
- When checked, the numeric chapter-limit field is disabled.
- Uncheck it to set a specific maximum chapter count.


## Version 0.2.6

- Replaced the start-position dropdown with a **Start from beginning** checkbox.
- If **Start from beginning** is checked, **All available** is automatically checked.
- While **Start from beginning** remains checked, **All available** is locked on.
- If **Start from beginning** is unchecked, the job starts from the currently open chapter and **All available** can be changed normally.

## Version 0.3.0

- Added a permanent self-hosted Chrome update URL using GitHub Pages.
- This release is intended as the final manual migration before signed in-place updates.
- Future packaged releases must be signed with the same private key generated when 0.3.0 is first packed.
