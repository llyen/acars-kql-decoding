# Przykłady komunikatów ACARS wg etykiety (label) — z Eventhouse ACARSEH.acars_raw

Źródło: acarshub, stacja EPWA. Dane pobrane 2026-07-24.
Kolumny źródłowe: Payload.msghtml.{label, label_type, text, tail, flight}

---

## Ranking wg czytelności tekstu

### 🏆 Pełny czytelny tekst (naturalny język)

**A9 — Deliver ATIS Information** (3 rekordy, śr. 130 znaków)
```
E VACATING RWY
WIND 290 12 KT
VIS 10KM
OVC 2200 FT
T17 DP13
QNH 1014
TEMPO CLD BKN 1400FT
BIRD INTENSITY HIGH AROUND THE AIRPORT
END OF ATIS H
5600
```
```
 INPR. CTN BIRD ACT. AFTER DEP 132.050. SIMUL INDEPENDENT DUAL PARL OPS INPR.

END OF ATIS Z
F351
```
```
B 2900 FT, CLD SCT
3300 FT.
T 20.
DP 13.
QNH 1013.
TREND TEMPO VIS 3000 M, MOD
SHRA.
CAUTION. BIRD ACT.
END OF EPWA ARR LA93D
```
→ Pełne komunikaty ATIS (informacja lotniskowa/pogodowa). Najlepszy kandydat na przykłady NLP/free-text.

---

**21 — Takeoff Data Calculation** (11 rekordów — najliczniejsza grupa czytelnego tekstu)
```
/TXT/ARINC DIRECT|||FLIGHT PLAN A0361 (EPWA - EPGD) FOR TAIL SPXXX IS AVAILABLE FOR RECALL
```
→ Ten sam wzorzec powtórzony wielokrotnie (różne tail/flight w innych rekordach). Format: `/TXT/<system>|||<treść>`.

---

**RB / RA — Command/Response** (harmonogramy i METAR/TREND)
```
ZZ1234567/~2
0729 HECAUUDD 0723-0729/    -
0714 OLBAHECA 0253-0257/0358-0408
0713 HECAOLBA 0056-0101/0157-0202
---- -------- 2008-2016/2146-2201
0723 HECALGAV 1703-1704/1838-1844
```
```
/16 Q1008
     RESHRA NOSIG=
```
```
LO0045 YYZ 1500 G21N      Y4   OK
LO0389 BER 1500 G33       Y2   OK
LO0253 LUX 1515 G44       Y1   OK
```
→ Tabele lotów (kod lotniska + czasy) oraz skrócone dane METAR/TREND.

---

### 📊 Ustrukturyzowany, skrótowy tekst (kody + wartości)

**H1 — Message To/From Terminal** (156 rekordów — największa próbka!)
```
POSN52026E020545,NAVUR,103411,350,SUTIK,103944,SUWGI,M50,01269,1432491
,0793/X70288,E0209,N521,064,014,0112,0792/
```
→ Dane pozycyjne/nawigacyjne (POS + waypointy + czasy + poziom lotu). Bardzo zróżnicowany format wewnętrzny (są też surowe binarne fragmenty CMU/loadsheet).

**17 — Northwest Airlines Position/Weather Report** (7 rekordów)
```
01DCAPLOT5N     /241039KJFKEPWA
1656  146.2 +19.0
```
→ nr raportu + linia + trasa + czas + kurs/prędkość + temperatura.

**49 — Status Reports** (3 rekordy)
```
01TOIC    LOT6NY/241036EPWAKJFK
+  412177.2+ 22.7
```
→ kod zdarzenia (TOIC=Take-Off, ICCL=In-Climb) + lot + trasa + czas + dane lotu.

**QQ/QP/QR/QS — klasyczne OOOI (OFF/OUT/ON/IN Report)**
```
QQ OFF: EPMOLBBG10351025
QP OUT: EPMOLBBG1025 233
QR ON:  LIRAEPMO0901
QS IN:  LIRAEPMO0906  80
```
→ para lotnisk (odjazd/przylot) + znacznik czasu HHMM.

**16 — General Aviation Weather Request**
```
103553,28768,1041,  92,N 52.545 E 20.794
```
→ czas, wysokość(?), kurs, prędkość, współrzędne.

**8A/8C/8F — Airline Defined / SAS Out/On Report**
```
092026,C,EPMO
```
→ czas, status (C/O), kod lotniska.

**83 — Airline Defined**
```
KEWR,EPWA,241045, 52.11,  21.17, 6378,221, 143.7,  7700
```
→ trasa (departure,arrival), data/czas, współrzędne, dystans, kurs, prędkość, wysokość.

**38 — Unknown Message Label** (ale czytelny wzorzec)
```
/AY1472/240726/E 20.869/N 52.042/34983/-------/      /- 49/ 1268/ 68
/65/
```
→ lot/data/współrzędne/wysokość/temperatura — prawdopodobnie pozycyjny raport Finnair.

**B6 — Provide ADS Report**
```
/JEDAAYA.ADS.A7-BHI1424DFB870EA89C3E87A1F0D269BF8677709C404EA26F6E0656149C400C869
```
→ zakodowany (hex) raport ADS-C, nieczytelny bez dodatkowego dekodera.

**5U — Downlink Weather Request**
```
SA EPWA,LKMT
```
→ krótkie żądanie danych pogodowych dla lotnisk.

**22, 12, 13, 14 — OFF/ON/CMU loadsheet raporty**
```
OFF01LO0135/24241122EPWALTFM11220084
ONN01LOT5N     /24241041KJFKEPWA 1041 107
```
→ kod zdarzenia (OFF/ON/INN) + lot + trasa + data/czas.

**15 — General Aviation Position Report**
```
REQPOS
```
→ samo żądanie pozycji, brak danych.

**2F — Unknown Message Label**
```
PACEPOSREQ
```
→ żądanie pozycji (Pace/ACARS).

**1L — Unknown Message Label** (dane binarne)
```
00145209293MQO887W232+K:IM8K1,1K,0GGM)OCF*THBBJ49II6BV9T55(+WYD+
```
→ nieczytelne, prawdopodobnie skompresowane/binarne dane.

---

### ❌ Brak treści / techniczne bez tekstu
- `SQ` — Ground Station Squitter Message (dane radiowe, nie treść)
- `_d` — No Information To Transmit
- `Q0` — ACARS Link Test
- `5V` — VDL Switch Advisory
- `SA` — Media Advisory (patrz wcześniejsza analiza — heartbeat/status, nie tekst)

---

## Rekomendacja kolejności do trenowania Copilota w Fabric
1. **A9** (ATIS) — pełny naturalny język, najlepszy start
2. **21** (Flight Plan free text) — duża, spójna próbka
3. **RB/RA** (harmonogramy/METAR)
4. **H1** (pozycja/nawigacja) — największa próbka, ale zróżnicowana wewnętrznie — warto podzielić na podtypy wg długości/wzorca
5. **17/49/QQ/QP/QR/QS** (OOOI i status) — krótkie, wysoce ustrukturyzowane, dobre do regexów
6. Pozostałe (83, 8A/8C/8F, 38, 5U, 16) — niskoczęstotliwościowe, ale przydatne do uzupełnienia słownika kodów
