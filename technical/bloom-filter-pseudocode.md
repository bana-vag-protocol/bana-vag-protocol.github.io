# Technical Implementation: Local Bloom Filter Pseudocode (v0.1)

## Purpose
This document provides a reference implementation for local community nodes. The goal is to transform sensitive individual data (e.g., a ID number or name) into a non-reversible "bit-signature" that can be shared with the protocol's aggregate dashboard.

## Logic Overview
1. **Input:** A unique identifier for the beneficiary.
2. **Salt:** A pilot-specific secret key (to prevent rainbow table attacks).
3. **Hash:** Multiple hash functions to map the input to the bit array.
4. **Output:** A bit-position list to be shared.

## Pseudocode

```python
# Constants (Agreed upon by all pilot participants)
FILTER_SIZE = 1000000  # Size of the bit array
NUM_HASHES = 7         # Number of hash functions
PILOT_SALT = "BanaVag_Uppsala_2025_Q1" # Rotated per pilot

def get_bit_positions(individual_id):
    """
    Converts an ID into a list of bit positions in the Bloom Filter.
    """
    # 1. Combine ID with the Salt for privacy
    secure_id = individual_id + PILOT_SALT
    
    positions = []
    for i in range(NUM_HASHES):
        # 2. Use a standard cryptographic hash (e.g., SHA-256) 
        # with an incrementing seed for each hash iteration
        hash_value = cryptographic_hash(secure_id + str(i))
        
        # 3. Map the large hash value to a position in our filter
        bit_position = hash_value % FILTER_SIZE
        positions.append(bit_position)
        
    return positions

# --- Usage in a local node ---

def record_service_rendered(person_id):
    # This stays LOCAL to the church/mosque/synagogue
    bit_indices = get_bit_positions(person_id)
    
    # Send ONLY these indices to the shared protocol dashboard
    # dashboard.report_indices(bit_indices)
    print(f"Sharing bit indices: {bit_indices}")
