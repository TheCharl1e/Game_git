# Caldreth — Notatki / Dev Log

Repo komunikacyjne projektu **Stan_Pierwotny** (robocza nazwa świata: *Caldreth*).
To NIE jest kod gry — kod żyje osobno w repo gry (`E:\Game`, moduł
`Source/Stan_Pierwotny/`). Tutaj trzymamy to, co usprawnia komunikację o projekcie
między sesjami: dziennik postępów i dokumenty projektowe do czytania / burzy mózgów.

## Co tu jest

| Plik | Do czego |
|---|---|
| `MILESTONES.md` | Dziennik kamieni milowych. **Najnowsze na górze.** Każdy wpis: data — co się zmieniło — status. |
| `DESIGN_how_it_works.md` | Jak działają WSZYSTKIE mechaniki (piramida Maslowa NPC L0–L5 + świat Caldreth). Dokument do czytania i burzy mózgów, NIE lista zadań. |
| `TECHNOLOGY_SYSTEM_rama.md` | Rama emergentnego systemu technologii (tagi-właściwości → receptury funkcyjne → graf rośnie sam). Wizja/rama, nie spec do kodowania. |
| `AMBIENT_TEMP_design.md` | Projekt systemu temperatury otoczenia (strefy → ciało). |
| `SLEEP_ENGINE_design.md` | Projekt silnika snu (ETAP 1 — narastanie zmęczenia). |
| `SLEEP_ENGINE_ETAP2_design.md` | Projekt silnika snu (ETAP 2 — skutki: mgła, mikrosen, omdlenie). |

## Gdzie żyją „żywe" dokumenty operacyjne

Te są w repo gry (`E:\Game\Gra_Stan_Pierwotny\`), aktualizowane na bieżąco przy pracy
— NIE duplikujemy ich tutaj, żeby nie rozjeżdżały się dwie wersje:

- `PROJECT_STATE.md` — co istnieje, statusy komponentów, API
- `ROADMAP.md` — zadania, kolejność, zależności
- `MECHANICS.md` — ground-truth wartości zmiennych (do testów)
- `CODE_REGISTRY.md` — spis co istnieje w `Source/` (klasy/struktury/enumy/funkcje)
- `DECISIONS.md` — zatwierdzone decyzje mechaniczne
- `CHANGELOG.md` — historia zmian (każda zmiana + wartości zmiennych)
- `REPORTS/` — szczegółowe raporty per zadanie

## Jak używamy tego repo

1. Po skończonym etapie → dopisz wpis na górze `MILESTONES.md` (data, co, status, commit).
2. Nowy pomysł na mechanikę → najpierw opis w `DESIGN_how_it_works.md` (co robi / jak /
   gdzie się wpina), POTEM zadanie do `ROADMAP.md` w repo gry.
3. To repo = szybka orientacja „gdzie jesteśmy" bez wchodzenia w kod.

## Zasady projektu (skrót)

- Kod/zmienne/komentarze po angielsku, rozmowa po polsku.
- C++ = mózg (matematyka/pamięć/logika), Blueprint = ciało (wizualizacja).
- Zero Event Tick — timery + Behavior Tree + EQS. Cel: 500+ NPC.
- Data-driven (DataTable/DataAsset), zero hardkodu.
- Dostarczanie pionowe (cienki plaster end-to-end), weryfikacja twardymi liczbami z logu.
