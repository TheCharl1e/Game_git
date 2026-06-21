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
*Kod slice 1 jest teraz w **`573830d`** (repo `Game.git` przebudowane orphanem 2026-06-22 → lekkie kod+docs, jedna czysta historia, Private, push OK). Oryginalne commity slice 1 `545a95d`/`b4edc36` — oraz wszystkie pozostałe hashe sprzed 2026-06-22 z tej listy (NPCRegistry/OCEAN/most #1 itd.) — zachowane wyłącznie w archiwum `E:\Game-history-2026-06-21.bundle` (3.1 GB, pełna stara historia). Bramka: `APPETITE_GRUBAS_design.md`.*

## 2026-06-20 — Most Maslow→BT, plaster #1 (pragnienie): C++ steruje wyborem akcji
**Status:** ✅ zbudowane + PIE-zweryfikowane.
`GetActionableNeed()` deleguje do sędziego `EvaluateCurrentNeed` i mapuje poziom→konkret; serwis BT pisze
JEDEN klucz `CurrentNeed`; zapis klucza w BP `EvaluateNeeds` zamrożony (odpięty). Dowód: zepsucie C++ Hydration
(BP `ThirstLevel` nietknięty) → `CurrentNeed=Thirst` → BT wchodzi w Handle Thirst (FindWater). Rozplątuje dwa
równoległe systemy potrzeb — C++ Maslow został mózgiem, BP cienkim ciałem.
*Commity: `32c6b81` (most), `2a381d5` (recon TRASH_: „reset stanu" to artefakt pomiaru, nie re-init; TECH-09 zamknięte).*

## 2026-06-20 — OCEAN slice #1: Neurotyczność → szansa paniki L0
**Status:** ✅ zbudowane + PIE-zweryfikowane (killer-demo).
`FOceanProfile` (Wielka Piątka per-NPC) na `UNPCIdentityComponent`; Neurotyczność przesuwa SZANSĘ paniki
(stochastyczny rzut na kadencji metabolizmu, latch `bIsInPanic`, histereza wyjścia). Sędzia tylko CZYTA latch —
zero RNG w środku. Killer-demo: ta sama rana (HP%=0.35) → C1 N=0.9 PanicChance 0.25 → panika; C2 N=0.1 → 0.00 → spokój.
*Commity: `48e1a73` (slice), `8951d65` (korekta misdiagnozy TECH-08 — żadnego pinu HP nie ma).*

## 2026-06-20 — NPCRegistry (L3-01) ⭐ keystone: int32 ID → żywy NPC
**Status:** ✅ zbudowane + PIE-zweryfikowane.
`UNPCRegistrySubsystem` (Register/Unregister/GetNPCById/GetRegisteredCount; ID nie-recyklowane, O(1), bez Tick)
+ `UNPCIdentityComponent` (rejestracja w `BeginPlay` / wyrejestrowanie w `EndPlay`). PIE: ID 1/2, nowy NPC→ID 3
(nie-recykling), `EndPlay`→„ID retired", count→0. Odblokowuje P2P (L3-05), reputację (L4-01), detektywa (L5-01).
*Commit: `ba9c092`.*

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
- Pierwszy pionowy plaster systemu technologii: głód → polowanie → porażka → eksperyment
  (kamień o kamień) → ostry kamień → udane polowanie.
