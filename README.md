# spaced_hgvs_patch

## Overview

This tool processes an input [JSON Lines](https://jsonlines.org/) (`jsonl`) file with the following format:

```jsonl
{"hgvs":"NC_000010.11:g.79347326_79347330delinsCTCAG","ca_id":"_:CA"}
{"hgvs":"NC_000010.11:g.79347306_79347310delinsAGCCA","ca_id":"_:CA"}
{"hgvs":"NC_000010.11:g.79347301_79347305delinsCCCTT","ca_id":"_:CA"}
{"hgvs":"NC_000010.11:g.79347301_79347304delinsCTCA","ca_id":"_:CA"}
{"hgvs":"NC_000010.11:g.79347351_79347354delinsCAGT","ca_id":"_:CA"}
{"hgvs":"NC_000010.11:g.79347296_79347300delinsAACCC","ca_id":"_:CA"}
{"hgvs":"NC_000010.11:g.79347481_79347484delinsCTCA","ca_id":"_:CA"}
{"hgvs":"NC_000010.11:g.79347441_79347444delinsCGCC","ca_id":"_:CA"}
{"hgvs":"NC_000010.11:g.79347341_79347345delinsCAGTC","ca_id":"_:CA"}
{"hgvs":"NC_000010.11:g.79347341_79347345delinsGTGCA","ca_id":"_:CA"}
```

## Output

The output is a `jsonl` file of identical length, where each object has an ArangoDB `_key` added:

```jsonl
{"hgvs":"NC_000010.11:g.79347326_79347330delinsCTCAG","ca_id":"_:CA", "_key": "key1"}
{"hgvs":"NC_000010.11:g.79347306_79347310delinsAGCCA","ca_id":"_:CA", "_key": "key2"}
{"hgvs":"NC_000010.11:g.79347301_79347305delinsCCCTT","ca_id":"_:CA", "_key": "key3"}
{"hgvs":"NC_000010.11:g.79347301_79347304delinsCTCA","ca_id":"_:CA", "_key": "key4"}
{"hgvs":"NC_000010.11:g.79347351_79347354delinsCAGT","ca_id":"_:CA", "_key": "key5"}
{"hgvs":"NC_000010.11:g.79347296_79347300delinsAACCC","ca_id":"_:CA", "_key": "key6"}
{"hgvs":"NC_000010.11:g.79347481_79347484delinsCTCA","ca_id":"_:CA", "_key": "key7"}
{"hgvs":"NC_000010.11:g.79347441_79347444delinsCGCC","ca_id":"_:CA", "_key": "key8"}
{"hgvs":"NC_000010.11:g.79347341_79347345delinsCAGTC","ca_id":"_:CA", "_key": "key9"}
{"hgvs":"NC_000010.11:g.79347341_79347345delinsGTGCA","ca_id":"_:CA", "_key": "key10"}
```

## Key Generation

- The `_key` is generated using the [SPDI](https://www.ncbi.nlm.nih.gov/variation/spdi/) representation.
- If the SPDI string is longer than 254 characters, a [VRS](https://github.com/ga4gh/vrs-python/tree/2.1.2) digest of the allele is used as the `_key`.

---