# Klipper
Anycupic S1 Combo print.cfg
# Anycubic Kobra S1 Klipper Configuration Update
這套配置我用了大半年了還行

此專案紀錄了 Anycubic Kobra S1 (S1C) 打印機設定檔 `printer.cfg` 的優化歷程。主要針對自動換料效率、打印品質補償以及硬體驅動進行了深度調整。

## 🛠 修改重點概覽

### 1. 核心運動與硬體參數
* **驅動器配置 (TMC2209)**：
    * [cite_start]**電流提升**：X/Y 軸運行電流由 `1.5A` 提升至 `1.8A`；擠出機由 `0.6A` 提升至 `0.8A`。
* [cite_start]**Z 軸歸位優化**：`homing_speed` 從 `8` 降低至 `6`，並將 `z_hop` 縮減為 `2.0` 以提升效率。

### 2. ACE自動進退料與洗料邏輯
* **進退料速度提升**：
    * [cite_start]`default_unwind_speed` 與 `default_feed_speed` 均從原本的 `20/30` 提升至 **`60`** [cite: 2, 11]。
* **洗料邏輯微調**：
    * [cite_start]`cutter_position` (切刀偏移) 從 `1.0` 增加到 `1.5` [cite: 2, 11]。
    * [cite_start]`unwind_length_after_triggered` 退料長度由 `1300` 縮減至 `1100` [cite: 3, 12]。
    * [cite_start]擦除速度 `sweep_speed` 降低至 `7` 以確保噴頭清潔度 [cite: 3, 12]。

### 3. 打印品質補償與自動化模組
* [cite_start]**新增流量校正 [flow_calibration]**：加入了針對不同溫度 (210°C~250°C) 與速度 (100~400mm/s) 的動態壓力超前 (Dynamic PA) 補償矩陣 [cite: 14]。
* **床面網格 (Bed Mesh) 升級**：
    * [cite_start]探測點數從 `5x5` 提升至 **`9x9`** [cite: 6, 17]。
    * [cite_start]算法從 `lagrange` 更換為 `bicubic` [cite: 6, 17][cite_start]，並新增了 `fade` (淡出) 機制 [cite: 17]。
* **新增功能模組**：
    * [cite_start]**異物檢測 [foreign_object_detect]**：設定檢測坐標為 `0, 245.0` [cite: 18]。
    * **多材質溫度控制**：新增了換料時的溫差控制設定 [cite: 18]。
    * [cite_start]**拋料指令**：新增 `TO_THROW_POSITION` 宏指令，優化拋料流程 [cite: 21]。

### 4. 環境與冷卻設定
* **風扇優化**：
    * [cite_start]`controller_fan` 新增 `idle_timeout: 30` 節能設定 [cite: 17]。
    * 主噴嘴風扇開啟 `hardware_pwm: True` 並將 `cycle_time` 調整為 `0.005` [cite: 7, 17]。
* [cite_start]**安全溫度調整**：`heater_bed` 的最低安全溫度從 `45` 降至 `35`，提升環境適應性 [cite: 4, 16]。

---
**Note:** 本次修改旨在提升 Anycubic S1C 的自動換料穩定度，並透過高密度的床面探測與動態流速補償來追求更高精度的打印結果。
