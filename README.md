# Magento 2 CMS Import/Export — utrzymywany fork (SISL)

**Przenoszenie bloków i stron CMS między środowiskami** Magento 2 (dev → staging → produkcja).
Eksportuje wybrane strony i bloki CMS do jednego pliku **ZIP** (razem z powiązanymi obrazami z
galerii mediów), który importujesz na innej instancji. Koniec z ręcznym kopiowaniem treści przez
panel albo dumpami tabel `cms_page` / `cms_block`.

- **Eksport** z panelu: zaznacz strony/bloki → *Export* → dostajesz `.zip`.
- **Import**: wgraj `.zip` na docelowej instancji (albo z CLI: `bin/magento cms:import plik.zip`).
- Zachowuje treść, layout, meta, przypisania do widoków sklepu i **załączone obrazy**.

To utrzymywany fork porzuconego `msp/cmsimportexport` z **MageSpecialist Security Suite / CMS tools**
(ostatni commit 2023; jedyny publiczny fork to zwykły mirror, nie modernizacja). Oryginał nie ma
przypiętego `magento/framework` i nie był testowany pod nowsze wydania. Ten fork doprecyzowuje
zależności, aktualizuje komendę CLI do Symfony Console 7 (z 2.4.9) i jest **zweryfikowany na
Magento 2.4.9 / PHP 8.4** realnym testem round-trip (eksport strony → ZIP → import → weryfikacja).

## Zgodność
- Magento **2.4.4 – 2.4.9** (Open Source / Adobe Commerce)
- PHP **8.1 – 8.4**
- Wymaga `msp/common` (nasz fork — dociąga się automatycznie)

## Instalacja
```bash
composer config repositories.sisl-msp-common vcs https://github.com/SISL-source/magento2-msp-common
composer config repositories.sisl-cmsie vcs https://github.com/SISL-source/magento2-cms-import-export
composer require msp/cmsimportexport:dev-main
bin/magento module:enable MSP_Common MSP_CmsImportExport
bin/magento setup:upgrade
bin/magento setup:di:compile   # tryb produkcyjny
```

## Użycie
- **Eksport (panel):** Content → Pages / Blocks → zaznacz wiersze → akcja masowa *Export*. Pobierze się ZIP.
- **Import (panel):** wejście importu w sekcji CMS → wgraj ZIP.
- **Import (CLI):**
  ```bash
  bin/magento cms:import /sciezka/do/cms_export.zip
  ```

## Typowy scenariusz
Redaktor przygotował landing i bloki na **stagingu** → eksport do ZIP → import na **produkcji**
jednym ruchem, z zachowaniem obrazów i przypisań do store view. Wersjonowalne (ZIP w repo/artefaktach).

## Licencja
OSL-3.0 / AFL-3.0 (jak oryginał). Fork utrzymywany przez [SISL](https://sisl.pl).
