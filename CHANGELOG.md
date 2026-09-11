# Changelog

## [Unreleased] — fork SISL (2026-09)
- Zgodność z Magento **2.4.9 / PHP 8.4** (di:compile + realny test round-trip: eksport strony CMS → ZIP → import z ZIP → import z array → weryfikacja).
- `composer.json`: `php ~8.1.0 || … || ~8.5.0`, `magento/framework >=103.0.4 <104` (oryginał: brak pinu php i framework); usunięto legacy `magento/magento-composer-installer`.
- `Command/ImportPage.php` (komenda `cms:import`): dodane `execute(): int` + `Cli::RETURN_SUCCESS` (Symfony Console 7 z 2.4.9 — bez tego fatal).

## Oryginał (msp/cmsimportexport) — MageSpecialist, porzucone 2023.
