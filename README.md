# Anycubic Kobra S1 Klipper Configuration Update

This configuration has been battle-tested for over six months and has proven to be highly stable. This project documents the optimization process of the `printer.cfg` for the Anycubic Kobra S1 Combo(S1C), primarily focusing on multi-material switching efficiency, print quality compensation, and hardware driver tuning.

## 🚀 Main Improvements
* **Z-axis Noise**: Reduced excessive mechanical resonance during homing and movement.
* **Motor Current**: Addressed insufficient torque during high-speed printing.
* **First Layer Issues**: Improved bed adhesion and consistency for a perfect start.
* **ACE Feeding Speed**: Significantly reduced material switching time.
* **Leveling Efficiency**: Optimized the probing process for faster preparation and higher precision.

---

## 🛠 Key Optimization Highlights

### 1. Core Motion & Hardware Parameters
* **Driver Configuration**:
    * **Current Boost**: Increased X/Y axis `run_current` from `1.5A` to `1.8A`.
    * **Extruder Boost**: Increased extruder `run_current` from `0.6A` to `0.8A` to ensure consistent extrusion and prevent slipping.
* **Z-Axis Homing Optimization**:
    * Reduced `homing_speed` from `8` to `6` to lower noise and improve origin precision.
    * Decreased `z_hop` to `2.0` for better efficiency and reduced mechanical impact.

### 2. ACE Auto-Loading & Purge Logic
* **Feeding Speed Increase**:
    * ACE `default_unwind_speed` and `default_feed_speed` increased from `20/30` to **`65`**[cite: 2].
* **Wiping & Purging Refinement**:
    * Reduced `unwind_length_after_triggered` from `1300` to `1100` to accelerate material swaps[cite: 3].
    * Lowered `sweep_speed` to `7` to ensure a cleaner nozzle and prevent residue from affecting the leveling process[cite: 2].

### 3. Print Quality Compensation & Automation
* **Bed Mesh Upgrade (Critical for a Perfect First Layer)**:
    * Increased probe density from `5x5` to **`9x9`**.
    * Switched algorithm from `lagrange` to **`bicubic`** for smoother interpolation.
    * Enabled `fade` mechanism to gradually phase out compensation as height increases.
    * Adjusted `horizontal_move_z` to `2` for faster travel between probe points.
* **New Functional Modules**:
    * **Multi-Material Temp Control**: Added temperature differential settings for material changes.
    * **Purge Command**: Added `TO_THROW_POSITION` to optimize the filament purging workflow.

---

**Note:** These modifications are designed to enhance the stability of the Anycubic S1C's automatic material switching system while achieving high-precision results through high-density bed probing and dynamic flow compensation.
