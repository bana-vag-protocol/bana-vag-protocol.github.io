# Technical Spec: Johannine Scheduling (v0.1)

## Problem Statement
Faith communities often have peak resource availability (volunteers, facilities) and peak demand on different days (e.g., Friday Jumu'ah, Saturday Shabbat, Sunday Service). Traditional siloed scheduling leads to "mountains" of waste and "valleys" of service gaps.

## Objective
Provide a coordinated view of volunteer and facility surges to ensure 24/7 coverage of essential services (e.g., food pantries, shelters) across a city or region.

## Data Model (Non-Sensitive)
- **Surplus Capacity:** Estimated volunteer hours per 4-hour block.
- **Facility Availability:** Binary (Available/Busy) for "Second Coat" spaces.
- **Demand Signals:** Anonymized throughput data from existing services.

## Algorithm: "The Leveling"
1. **Identify Voids:** Identify time blocks where service delivery falls below the 15% safety threshold.
2. **Trigger Surplus Alerts:** Notify partner communities with high capacity during those specific blocks.
3. **Cross-Calendar Optimization:** - Friday/Saturday gaps -> Christian/Secular surge.
   - Sunday/Monday gaps -> Muslim/Jewish surge.
   - Holiday surges (Ramadan/Advent) -> Offset by partners in non-peak seasons.

## Implementation Guardrails
- **Human Approval:** No shift is "assigned" by AI; only "suggested" to human coordinators.
- **Instance-Boundedness:** Scheduling logic is local to the pilot instance (e.g., "Bana Väg Uppsala").
