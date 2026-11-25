# ACARS Eventhouse Analysis

Notes and KQL queries for analysing and decoding ACARS messages stored in a Microsoft Fabric Eventhouse. The messages were received by an acarshub station near Warsaw Chopin Airport (EPWA). The documents are in Polish.

Polish version: [README.md](README.md).

## Contents

- [`docs/acars_label_examples.md`](docs/acars_label_examples.md): sample message texts grouped by ACARS label, with a readability assessment and a suggested order for using them in decoding work.
- [`docs/acars_label_parsers.kql`](docs/acars_label_parsers.kql): KQL queries that parse fields for specific labels (A9, 21, 17/49, QQ/QP/QR/QS, 83, 16, 38, 8A/8C/8F, 5U, 12/13/14/22, RA/RB, H1).

## Data source

- Eventhouse query URI: `<EVENTHOUSE_QUERY_URI>`
- Database: `ACARSEH`
- Table: `acars_raw` (schema: `Source:string, ReceivedUtc:datetime, Event:string, Payload:dynamic`)

The queries expect the acarshub message JSON in `Payload.msghtml`. To use them, ingest your own acarshub output into a table with this schema.

## Known limitations

- Label `SA` ("Media Advisory" in the acarshub dictionary) is a technical heartbeat/status, not a press message.
- Label `H1` has many internal formats. The parser currently handles only the `POS...` subtype.

## Disclaimer

ACARS messages are unencrypted radio transmissions. The examples are short excerpts kept for format analysis. Do not use this material to track individual aircraft or people. Check the rules on receiving and publishing radio communications in your country. Not an official Microsoft product.

## License

MIT, see [LICENSE](LICENSE).
