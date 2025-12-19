# Technical Deep Dive: Privacy-Preserving Fruit Verification

## Purpose: The "One Coat per Person" Problem
In Phase 1 pilots (e.g., Food Security), we need to report the total "fruit" (unique individuals served) to demonstrate efficiency. However, the Johannine-Advent Ethic forbids creating a centralized "master database" of vulnerable people. 

**The Challenge:** How do we know if a person receiving a coat from Community A is the same person who received one from Community B, without sharing their identity?

## Solution: Distributed Bloom Filters
We use a probabilistic data structure called a **Bloom Filter**. This allows us to test set membership ("Have we seen this person before?") without ever storing or transmitting the actual identity.

### 1. The Hashing Process (Local/Private)
Each community uses a local, salted hashing function on a consistent identifier (e.g., a combination of partial name, birth year, or a government ID if appropriate):
- `ID` -> `Hash_Func(ID + Local_Secret_Salt)` -> `Bit_Indices`

### 2. The Shared Filter (Pooled/Public)
- Communities do not share the Hash or the ID.
- They share only the **Bit Indices** into a collective Bloom Filter (a large array of zeros and ones).
- If Community A serves a person, they flip certain bits to `1`.
- When Community B serves a person, they check the filter. 
    - If the bits are already `1`, the person is **probabilistically** already served by the protocol (avoiding double-counting in shared metrics).
    - If the bits are `0`, this is a unique "New Fruit" for the collective.

### 3. Theological Alignment: "No More Than Required"
- **Luke 3:13:** "Collect no more than required."
- This technical approach collects exactly zero identity data, only the "bit-signature" of the service rendered.
- It prevents the "Prince" (centralized authority) from emerging through data accumulation.

## False Positives and "Graceful Error"
Bloom filters can have false positives (saying someone was served when they weren't), but **never false negatives**. 
- In our context, a false positive simply means we *under-report* our success slightly. 
- This is a "Graceful Error": it is better to slightly under-count the fruit than to over-identify the person.

## Implementation Guardrails
- **Salt Management:** Salts should be rotated per pilot to ensure **Instance-Boundedness**.
- **Transparency:** The hash function and filter size must be documented in the pilot's technical annex to ensure the metrics are "Publicly Intelligible".
