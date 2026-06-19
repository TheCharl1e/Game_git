# Caldreth — Milestones

Każdy wpis: data — co dodaliśmy/zmieniliśmy — status.
Najnowsze na górze.

---

## 2026-06-19 — Warstwa doby: DayNightTempOffset (dokumentacja + weryfikacja)
**Status:** ✅ udokumentowane i zweryfikowane względem kodu.
Offset temperatury dzień/noc spięty z `BP_DayNightCycle` (źródło: SunIntensity/MaxSunIntensity).
Wymaga postawienia zegara na mapie Caldreth. Naprawia też „jeden zegar" snu (fallback znika).
*Commity: kod `8dba663`, docs `ca76f6b`.*

## 2026-06-19 — AmbientTemp (rdzeń strefowy)
**Status:** ✅ zbudowane i zweryfikowane.
Temperatura otoczenia ożywiła 3 martwe od początku systemy temperatury.
Zmienne/elementy: `FZoneDef.BaseTemp`, cache stref, sprzężenie otoczenie→ciało (3 reżimy),
hipotermia stopniowa, cold-burn split.
*Commit: `e2dd851`.*

## 2026-06-18 — Silnik snu ETAP 2 (skutki zmęczenia)
**Status:** ✅ zbudowane (scalenie A+B).
Mgła liniowa (spadek wydajności), mikrosen, omdlenie (ragdoll) z blokadą AI;
`StartSleep`/`StopSleep`/reset/`Rested` scalone; 2 bugi naprawione.
*Commit: `8326f14`. Projekt: `SLEEP_ENGINE_ETAP2_design.md`.*

## (wcześniej) — Silnik snu ETAP 1 (narastanie zmęczenia)
**Status:** ✅ zbudowane.
Narastanie `HoursAwake`/zmęczenia, drabina stanów `FatigueState`.
*Projekt: `SLEEP_ENGINE_design.md`.*

---

### Następne w kolejce (z ramy projektu)
- Postawienie zegara dobowego na mapie Caldreth (domknięcie warstwy doby + „jeden zegar").
- Caldreth spawner (zaludnienie wyspy NPC + NavMesh).
- **NPCRegistry** — keystone pod warstwy społeczne L3/L4/L5 + cache stref.
- Pierwszy pionowy plaster systemu technologii: głód → polowanie → porażka → eksperyment
  (kamień o kamień) → ostry kamień → udane polowanie.
