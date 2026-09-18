# Magento 2 CMS Import/Export — maintained fork (SISL)

**Move CMS blocks and pages between Magento 2 environments** (dev → staging → production). Exports
selected CMS pages and blocks to a single **ZIP** file (together with the related images from the
media gallery), which you import on another instance. No more copying content by hand through the
admin or dumping the `cms_page` / `cms_block` tables.

- **Export** from the admin: select pages/blocks → *Export* → you get a `.zip`.
- **Import**: upload the `.zip` on the target instance (or from the CLI: `bin/magento cms:import file.zip`).
- Preserves content, layout, meta, store-view assignments and **attached images**.

This is a maintained fork of the abandoned `msp/cmsimportexport` from the **MageSpecialist Security
Suite / CMS tools** (last commit 2023; the only public fork is a plain mirror, not a
modernisation). The original pins no `magento/framework` and was never tested against newer
releases. This fork tightens the dependencies, updates the CLI command to Symfony Console 7
(shipped with 2.4.9) and is **verified on Magento 2.4.9 / PHP 8.4** with a real round-trip test
(export page → ZIP → import → verification).

## Compatibility
- Magento **2.4.4 – 2.4.9** (Open Source / Adobe Commerce)
- PHP **8.1 – 8.4**
- Requires `sisl-source/magento2-msp-common` (our fork — pulled in automatically)

## Installation

```bash
composer require sisl-source/magento2-cms-import-export
bin/magento module:enable MSP_Common MSP_CmsImportExport
bin/magento setup:upgrade
bin/magento setup:di:compile   # production mode
```

## Usage
- **Export (admin):** Content → Pages / Blocks → select rows → mass action *Export*. A ZIP is downloaded.
- **Import (admin):** the import entry in the CMS section → upload the ZIP.
- **Import (CLI):**
  ```bash
  bin/magento cms:import /path/to/cms_export.zip
  ```

## A typical scenario
A content editor prepared a landing page and blocks on **staging** → export to ZIP → import on
**production** in one move, keeping images and store-view assignments. Versionable (ZIP in the
repo/artifacts).

## License
OSL-3.0 / AFL-3.0 (same as upstream). Fork maintained by [SISL](https://sisl.pl).

---

### Maintained by SISL

Maintained fork by **[SISL](https://sisl.pl)** — [Magento 2 development and modules](https://sisl.pl/moduly-magento). More self-hosted plugins: [SISL Marketplace](https://sisl.pl/sklep).