# Avoid UUID v4 Primary Keys in Postgres

**Source:** [Andy Atkinson](https://andyatkinson.com/avoid-uuid-version-4-primary-keys)
**Tags:** #postgres #database #performance #uuid
**Date Added:** 2026-01-04

---

## TL;DR

**Avoid UUID Version 4 for primary keys in Postgres.** The randomness causes poor performance due to index fragmentation, increased I/O, and worse cache hit ratios. Use integers/bigints, or if you must use UUIDs, use time-ordered UUID v7.

---

## The Core Problem: Randomness

UUID v4 values are **122 random bits**. This randomness destroys database performance:

- **Insert latency**: Random values cause index page splits (not appending to rightmost leaf)
- **Lookup inefficiency**: ~40% more I/O needed compared to integers
- **Poor cache utilization**: Random access patterns evict useful buffers

### Real Numbers (10M rows, 1M updates)
- Integer index: **27,332 buffer hits**
- UUID v4 index: **8,562,960 buffer hits** (31,229% more!)
- That's ~68GB more data accessed, adding **1-3.4 seconds of latency**

---

## Index Density Comparison

| Data Type | Avg Leaf Fill % |
|-----------|-----------------|
| Integer   | 97.64%          |
| UUID v4   | 79.06%          |
| UUID v7   | 90.09%          |

---

## Common Misconceptions

### "UUIDs are secure"
**Wrong.** RFC 4122 explicitly states: *"Do not assume that UUIDs are hard to guess; they should not be used as security capabilities"*

### "I need UUIDs for distributed systems"
**Maybe.** Valid use cases:
- Generating IDs from multiple services/clients
- Microservices with separate databases needing collision-free IDs

**But consider:** You can generate obfuscated codes from integers using XOR + base62 encoding.

---

## Recommendations

### For New Databases
1. **Default choice**: `integer` or `bigint` with identity/sequence
   - 4-byte integer: ~2 billion unique values per table
   - 8-byte bigint: for high-growth apps (social media, telemetry, etc.)

### If You Must Use UUIDs
- **Use UUID v7** (time-ordered) instead of v4
- Available in Postgres 18 (Fall 2025) or via `pg_uuidv7` extension now
- Same `uuid` data type, much better performance

### Mitigations for Existing UUID v4 Databases
1. **Rebuild indexes**: `REINDEX CONCURRENTLY`
2. **Increase memory**: Size `shared_buffers` to fit indexes
3. **Increase work_mem**: For sort-heavy queries
4. **Rails**: Set `implicit_order_column` to `created_at` instead of UUID
5. **Cluster**: On an indexed timestamp column (though requires exclusive lock)

---

## Key Takeaways

- UUID v4 = 16 bytes (2x bigint, 4x integer)
- Random values → index fragmentation → slow reads AND writes
- UUID v7 exists and is much better (timestamp in first 48 bits)
- For obfuscated public IDs, derive them from integers instead
- Don't use `gen_random_uuid()` for primary keys

---

## Related
- [[PostgreSQL Performance]]
- [[Database Design Patterns]]
