---
name: wisemusic-kontrola-kontextu
description: >-
  Použij, když champion kontextové vrstvy ve Wisemusic dělá týdenní kontrolu kontextu: projde asi
  deset skutečných otázek z týdne, položí je Claudovi přes firemní nástroje, zapíše verdikt ke každé
  odpovědi a ohlásí týdenní podíl správných odpovědí se zdroji; a když se vedení ptá, jak si kontext
  vede. Spouštěče: kontrola kontextu, týdenní kontrola, spot check, otestuj odpovědi, zapiš verdikt,
  kolik odpovědí bylo správně, plníme 80 procent, jak jde kontext, pokrytí porad, pokrytí e-mailů,
  úkoly z porad.
---

# Týdenní kontrola kontextu

**Owner:** owner (vedení; kontrolu vede champion kontextové vrstvy). **Used by:** champion, vedení.

Měříme kontextovou vrstvu, ne lidi. Verdikt dává vždy champion (zná správnou odpověď nebo ji ověří u
toho, kdo se ptal), nikdy Claude sám. Odpovídej česky.

1. **Otázky týdne.** Požádej championa o asi deset skutečných otázek z tohoto týdne (metoda níže).
   Ke každé si nech říct, kde je správná odpověď (`answer_source`: meeting, email, document, card,
   not_recorded) a téma (`topic`: artist, booking, release, campaign, merch, task, meeting, other).
   Text otázky si drž jen v tomto rozhovoru; nikam ho nezapisuj.
2. **Odkaz na otázku** (`question_ref`): interní, bez jmen a kontaktů, z id objektu a krátkého
   slugu, například `luna-vlny-2026-12-05-praha:smlouva` nebo `kovar-mc-beton:datum-vydani`. Id objektu
   najdi přes `search`. `check_id` je ISO týden a pořadí: `2026-W43:01` až `2026-W43:10`.
3. **Polož otázku poctivě.** Odpověz na ni přesně tak, jak bys odpověděl kolegovi: `search` a `get`,
   `query_metric` (například `upcoming_bookings`, `artist_activity`, `release_calendar`), `sources`,
   `timeline`, u „co je nového“ postup skillu `wisemusic-co-je-noveho`. Bez nápověd od championa,
   každý fakt se zdrojem a datem. Odpověď ukaž celou a po verdiktu ji neupravuj.
4. **Verdikt od championa:**
   - `correct_with_sources`: správně a s aspoň jedním zdrojem a datem; kolegu by se ptát nemusel;
   - `partly`: něco chybí nebo je nepřesné, nebo je to správně, ale bez zdroje;
   - `wrong_or_not_found`: špatně, nebo odpověď v modelu není.

   `source_cited` je true, když tvoje odpověď uvedla aspoň jeden zdroj s datem. Poznámka (`note`, do
   500 znaků) jen říká, co chybělo, například „rozhodnutí z porady nebylo zachycené“; žádná jména ani
   osobní údaje.
5. **Zapiš každou otázku:** `propose_action` `log_context_check` s {check_id, checked_on, question_ref,
   topic, verdict, source_cited, answer_source, note}. Přečti championovi náhled; schválí si ho sám
   jedním klepnutím v portálu. Zapsáno je, až když `action_status` ukáže executed. Opravu zapiš pod
   stejným check_id.
6. **Týdenní výsledek:** `query_metric` `context_check_weekly` s date_from = 2026-10-19 (základní
   týden) a date_to = dnes. Přečti řádek tohoto týdne tak, jak je: počet otázek, podíl
   `share_correct_with_sources`, `target_met` (aspoň 8 otázek a aspoň 80 % správně se zdroji) a
   `weeks_in_a_row`. Cíl: tři týdny po sobě do 30. 11. 2026.
7. **Kde to chybí:** `query_metric` `context_check_by_answer_source` za tento týden (pondělí až dnes)
   a pokrytí za stejné období: `query_metric` `meeting_capture_lag` (první fakt do 60 minut od
   publikace přepisu), `query_metric` `mail_capture_lag` (e-mail v modelu do jednoho pracovního dne) a
   `query_metric` `meeting_tasks_same_day` (úkoly z porady ještě ten den). Čísla ber jen z výsledků.
8. **Další krok** ke každému minutí: co chybělo (nezachyceno, zachyceno pozdě, nepřiřazeno k objektu,
   nikde nezapsáno) a co s tím: zpracovat poradu (`wisemusic-meeting-to-tasks`), zachytit e-mail
   (`capture-a-decision`), doplnit stránku do KB, nebo přidat otázku do drillů. Nikdy ne kdo za to
   může.

**The answer contains:** u každé otázky check_id, question_ref, odpověď se zdroji, verdikt championa
a stav zápisu; pak řádek týdne z `context_check_weekly` (podíl, target_met, weeks_in_a_row), minutí
podle místa odpovědi, tři čísla pokrytí a další kroky.

**Never:** nedávej verdikt sám, nezapisuj text otázky ani něčí jméno a nečti výsledky jako hodnocení
člověka.

## Metoda (jedna strana)

**Co měříme.** Jestli kdokoli ve Wisemusic dostane od Clauda na skutečnou otázku „co se děje s X“
správnou odpověď se zdroji, aniž by se musel ptát kolegy. Cíl (12. 10. 2026): v týdenní kontrole asi
deseti otázek aspoň 80 % správně se zdroji. Základní týden je týden od 19. 10. 2026; cíl držet tři
týdny po sobě do 30. 11. 2026.

**Pokrytí za tím.** Fakta z nahrané porady jsou v modelu do hodiny od publikace přepisu;
dohody z e-mailu do jednoho pracovního dne; dohodnuté úkoly ještě ten den (dnes jako úkoly v Company
OS, po napojení Todoistu i tam). Tři metriky pokrytí ukazují, kde kontrola padá dřív, než to poznají
lidé.

**Výběr otázek (každý týden, nejpozději ve čtvrtek).** Champion se zeptá každého v týmu: „Na co ses
tento týden musel(a) zeptat kolegy nebo to dlouho hledat?“ Z odpovědí vybere asi deset otázek tak,
aby pokryly booking, vydání, PR a provoz, aspoň tři mířily na porady a aspoň dvě na e-maily. Otázky
jsou skutečné, ne vymyšlené na míru tomu, co Claude umí. Champion si ke každé předem poznamená
správnou odpověď a kde je napsaná; když není napsaná nikde, je to `not_recorded`.

**Jak se ptát.** V novém rozhovoru, formulací kolegy, bez nápověd. Jedna otázka, jedna odpověď; žádné
doptávání, které by kolega sám neudělal.

**Jak hodnotit.** Správně se zdroji, jen když by kolega podle odpovědi jednal a nemusel nikoho
obtěžovat, a když odpověď uvádí zdroj s datem. Správná odpověď bez zdroje je „částečně“. Odpověď,
která si něco vymyslí, je „špatně“, i když zbytek sedí.

**Co se nezapisuje.** Text otázky, kdo se ptal, kdo odpovídal, kdo kontroloval. Jen interní odkaz,
téma, verdikt, zdroj a kde je správná odpověď. Záznamy vidí štábní týmy.

**Co s výsledkem.** V pátek na týdenní poradě: podíl týdne, minutí podle místa odpovědi a jeden
konkrétní krok na příští týden (třeba „porady s umělci se nahrávají a zpracují do hodiny“). Výsledek
je pozorování na malém vzorku, ne důkaz, a nikdy hodnocení člověka.
