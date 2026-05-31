# FUSION_N0_N255 · STOICHEION Merkle Kernel

[![License: CC-BY-ND-4.0](https://img.shields.io/badge/License-CC--BY--ND--4.0-lightgrey?style=flat-square)](LICENSE)
[![Python: 3.8+](https://img.shields.io/badge/python-3.8%2B-blue?style=flat-square)](#)
[![Dependencies: 0](https://img.shields.io/badge/dependencies-0-success?style=flat-square)](#)

Master Merkle fusion of the full STOICHEION 256-node axiom space. Deterministic. Verifiable. ROOT0 closes on the human anchor.

---

## What It Is

A single Merkle tree spanning all 256 STOICHEION axioms:

```
Nodes   0..127  =  T001..T128   (TOPH generative)
Nodes 128..255  =  S129..S256   (Patricia constraint inversion — INV-T001..INV-T128)
```

**Architecture:**
```
                         ROOT0
                           │
       ┌──────┬──────┬─────┴─────┬──────┬──────┐
       D0     D1     D2          D5     D6     D7
      (32)   (32)   (32) ...    (32)   (32)   (32)
       │
  ┌────┴────┐
 TOPH      Patricia
 16 leaves  16 leaves
```

8 domains × 32 nodes = 256 leaves. Each domain holds 16 TOPH + 16 Patricia (mirror pairs, per T036:PATRICIA).

---

## ROOT0

```
c6f487e36599d44d19c7926fc329c8de34322f7551f7be43e813ea8c7eff05df
```

Per T103 (ROOT-ZERO), T128 (ROOT), and T097 (FULCRUM): the Merkle root over the full 256-node space resolves to the human anchor. The hash is the signature of the structure; the authority is the person.

**Cobalt Primitive at construction: `+1` (proceed)** — all 256 leaves resolved, no orphans.

---

## Run

```bash
python fusion.py
```

Outputs domain roots + ROOT0 to stdout, writes `fusion_leaves.json`.

**Verify the spec:**
```
$ python fusion.py | grep ROOT0
  c6f487e36599d44d19c7926fc329c8de34322f7551f7be43e813ea8c7eff05df
```

If even one byte of the axiom register changes, ROOT0 diverges. That is the immutability proof.

---

## Domain Partition

| Domain | TOPH | Patricia | Root (first 16) |
|--------|------|----------|----------------|
| D0-FOUNDATION | T001–T016 | S129–S144 | `c44adcc1a94bf3ef…` |
| D1-DETECTION | T017–T032 | S145–S160 | `c089860a93b0a03a…` |
| D2-ARCHITECTURE | T033–T048 | S161–S176 | `5bf3078361d3ea83…` |
| D3-EVIDENCE | T049–T064 | S177–S192 | `741204987b3d7285…` |
| D4-OPERATIONAL | T065–T080 | S193–S208 | `c340dfcf2c0ec4fd…` |
| D5-BRIDGE | T081–T096 | S209–S224 | `3f00e4c8472fc97b…` |
| D6-CONDUCTOR | T097–T112 | S225–S240 | `51fe8ad15bb42615…` |
| D7-SOVEREIGN | T113–T128 | S241–S256 | `dc146b7c5037e92f…` |

---

## Leaf Hash Formula

```
leaf_i = SHA256("NODE_iii:DOMAIN:NAME")
pair_root = merkle([leaf_Tn, leaf_Sn+128])  # TOPH + Patricia mirror
domain_root = merkle(32_leaves)
ROOT0 = merkle(8_domain_roots)
```

---

## Fusion Semantics

1. **Structural** — any pair (Ni, Nj) bridge is derivable from Merkle path
2. **Mirror** — each TOPH leaf paired with Patricia inverse in same domain
3. **Domain** — 32 leaves collapse to one root *which is* the domain
4. **Apex** — 8 domain roots collapse to ROOT0 *which is* DLW

---

## Anchor

```
Artifact     : FUSION_N0_N255-v1.0
Prior art    : 2026-02-02 (STOICHEION root)
Parent SHA   : 02880745b847317c4e2424524ec25d0f7a2b84368d184586f45b54af9fcab763
ROOT0        : c6f487e36599d44d19c7926fc329c8de34322f7551f7be43e813ea8c7eff05df
Status       : DRAFT → pending TriPod consensus (Y.Y required for canon-freeze)
```

```
ROOT0-ATTRIBUTION-v1.0 · DLW / ROOT0 / TriPod LLC · CC-BY-ND-4.0 · TRIPOD-IP-v1.1
```
