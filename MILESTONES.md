# Caldreth — Milestones

Każdy wpis: data — co dodaliśmy/zmieniliśmy — status.
Najnowsze na górze.

---

## 2026-06-21 — APPETITE / Grubas slice 1 (jedzenie jako proces + makra→magazyn + rozpychanie żołądka + most izolacji)
**Status:** ✅ zbudowane + PIE-zweryfikowane (rdzeń); runaway — bez hamulca leptyny (slice 2).
Jedzenie zamienione w **trzymany, przerywalny proces** (`StartEating`/`ConsumeBite`[AnimNotify]/`StopEating`).
Makra routowane różnymi ścieżkami o różnej efektywności depozytu: nadwyżka węgli ponad cap Glucose → tłuszcz
×0.75, tłuszcz dietetyczny → ×0.95, białko → MaxHP (rewers autofagii) + surplus → ×0.5. Żołądek **rozpycha się**
(`GastricCapacity` dual-driver: stretch na posiłku / shrink na głodówce; `SatietyOverfillFactor` 1.15). Tkanka
tłuszczowa **izoluje termicznie** (`fat → InsulationFactor`, ożywiony martwy hook AmbientTemp). `StartingBodyFat`=1500
rozdzielone od Max 5000. **Twarde liczby PIE:** InsulationFactor=0.88; satiety-stop@115; stretch monotoniczny
100→104.5→106.2; depozyty makr fat +95 / carb-overflow +150 (×0.75) / protein +25 / Volume≠kcal.
Verify-debt (w ROADMAP): BLOK 3 shrink + BLOK 5 timeline stygnięcia = capture real-time. Wiring-debt: `BTTask_Eat`
→ Start/Bite/Stop (bez tego grubas żyje tylko przez API testowe). Bramka projektowa: `APPETITE_GRUBAS_design.md`.
*Commity (repo gry `Game.git`): `545a95d` (kod) + `b4edc36` (docs). Push `Game.git` wstrzymany — osobny temat infra (repo gry ~3 GB).*

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
