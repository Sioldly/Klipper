# Klipper
Anycupic S1 Combo print.cfg
# Anycubic Kobra S1 Klipper Configuration Update
這套配置我用了大半年了還行
此專案紀錄了 Anycubic Kobra S1 (S1C) 打印機設定檔 `printer.cfg` 的優化歷程。主要針對自動換料效率、打印品質補償以及硬體驅動進行了深度調整。
主要改了

1.Z軸噪音大

2.電機電流不足

3.首層問題

4.ACE進退料速度

5.調平效率
## 🛠 修改重點概覽
### 1. 核心運動與硬體參數
* ** 驅動器配置 (TMC2209)**：
    * ** 電流提升**：X/Y 軸運行電流由 `1.5A` 提升至 `1.8A`；擠出機由 `0.6A` 提升至 `0.8A`。
* **Z 軸歸位優化**：`homing_speed` 從 `8` 降低至 `6`，並將 `z_hop` 縮減為 `2.0` 以提升效率和降低噪音。

### 2. ACE自動進退料與洗料邏輯
* **進退料速度提升**：
    * ACE進退料`default_unwind_speed` 與 `default_feed_speed` 均從原本的 `20/30` 提升至 **`60`** [cite: 2, 11]。
* **洗料邏輯微調**：
    * [cite_start]`unwind_length_after_triggered` 退料長度由 `1300` 縮減至 `1100` 提升速度。
    * [cite_start]擦除速度 `sweep_speed` 降低至 `7` 以確保噴頭清潔度避免殘留影響調平。

### 3. 打印品質補償與自動化模組
* **床面網格 (Bed Mesh) 升級(這部分是打好完美首層的關鍵)**：
    * 探測點數從 `5x5` 提升至 **`9x9`**。
    * 算法從 `lagrange` 更換為 `bicubic`，並新增了 `fade`。
* **新增功能模組**：
    * **多材質溫度控制**：新增了換料時的溫差控制設定 [cite: 18]。
    * **拋料指令**：新增 `TO_THROW_POSITION` 宏指令，優化拋料流程。
---
**Note:** 本次修改旨在提升 Anycubic S1C 的自動換料穩定度，並透過高密度的床面探測與動態流速補償來追求更高精度的打印結果。
