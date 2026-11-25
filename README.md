# ACARS Eventhouse Analysis

Wersja angielska: [README.en.md](README.en.md).

Analiza i dekodowanie komunikatów ACARS przechowywanych w Fabric Eventhouse
(`ACARSEH.acars_raw`, źródło: acarshub, stacja EPWA).

## Zawartość

- [`docs/acars_label_examples.md`](docs/acars_label_examples.md) — przykłady tekstu komunikatów
  pogrupowane wg etykiety ACARS (`label`), z oceną czytelności i rekomendowaną kolejnością
  wykorzystania do trenowania/dekodowania (np. w Copilot w Fabric).
- [`docs/acars_label_parsers.kql`](docs/acars_label_parsers.kql) — zweryfikowane zapytania KQL
  parsujące pola dla poszczególnych etykiet (A9, 21, 17/49, QQ/QP/QR/QS, 83, 16, 38, 8A/8C/8F,
  5U, 12/13/14/22, RA/RB, H1).

## Źródło danych

- Cluster URI: `<EVENTHOUSE_QUERY_URI>`
- Database: `ACARSEH`
- Table: `acars_raw` (schema: `Source:string, ReceivedUtc:datetime, Event:string, Payload:dynamic`)

## Znane ograniczenia

- Etykieta `SA` ("Media Advisory" w słowniku acarshub) to techniczny heartbeat/status,
  nie treść komunikatu prasowego — format opisany w `docs/acars_label_examples.md`.
- Etykieta `H1` ma wysoką wariancję wewnętrznego formatu (pozycja/nawigacja vs. surowe
  dane binarne CMU/loadsheet) — parser w `acars_label_parsers.kql` obsługuje na razie
  tylko podtyp `POS...`.
