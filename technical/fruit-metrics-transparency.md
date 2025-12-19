# Technical Spec: Privacy-Preserving Fruit Metrics (v0.1)

## Purpose
To provide "publicly intelligible" proof of impact (fruit) while strictly protecting the privacy of vulnerable beneficiaries and the autonomy of faith communities.

## The "Fruit Dashboard" Architecture
1. **Local Collection (Input):** Each community tracks its own service delivery (e.g., meals served, debts relieved) using their existing tools.
2. **Aggregated Hashing (Processing):** Only anonymized, aggregated totals are sent to the shared protocol layer.
3. **Proof of Fruit (Output):** A public-facing dashboard displaying:
   - Total meals provided by the coordination (not by specific mosque/church).
   - Efficiency gains (percentage reduction in waste).
   - Cumulative debt relieved.

## Technical Safeguard: No Master Identity
The protocol explicitly forbids the creation of a cross-community "beneficiary ID" database. Instead, it uses **Bloom Filters** or **Zero-Knowledge Proofs** to prevent double-counting of services without identifying the individual receiving help.

## Verification
Independent auditors (from participating traditions) can verify local records against the aggregated hash to ensure "no more is collected than required" (Luke 3:13).
