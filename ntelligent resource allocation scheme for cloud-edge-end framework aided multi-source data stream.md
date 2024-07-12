# 智能資源分配方案（Intelligent Resource Allocation Scheme）

## 目錄

1. [摘要](#摘要)
2. [介紹](#介紹)
3. [系統模型](#系統模型)
4. [問題表述](#問題表述)
5. [解決方案](#解決方案)
6. [模擬結果](#模擬結果)
7. [結論](#結論)

## 摘要

- 多源數據流
- 邊緣計算
- 協同卸載
- 近端策略優化（PPO）

## 介紹

- 5G 及物聯網的發展
- MCC 的缺點
  - 高延遲
- MEC 的優勢
  - 低延遲，高帶寬
- 動態網絡環境下的挑戰
  - 無線通道時變
  - 數據流特性變化
- 研究目的
  - 提出動態卸載和資源分配策略
  - 保障設備的經濟預算約束

## 系統模型

### 傳輸模型

- 設備到 CAP 的無線上行通道
  - $r_{CAP}^{m,n} = w_{CAP}^{m,n} \log_2 \left(1 + \frac{p_{trans}^{m} |h_{m,n}|^2}{\sigma^2} \right)$
- CAP 到雲端的無線上行通道
  - $r_{c}^{m,n} = w_{c}^{m,n} \log_2 \left(1 + \frac{p_{trans}^{n} |g_{m,n}|^2}{\sigma^2} \right)$
- 頻寬限制
  - $\sum_{m=1}^{M} w_{CAP}^{m,n} \leq W_{CAP}^{n}$
  - $\sum_{m=1}^{M} w_{c}^{m,n} \leq W_{c}$

### 計算模型

- 本地計算延遲
  - $T_{local}^{m} = \frac{l_{local}^{m} \omega \kappa}{f_{l}^{m}}$
- CAP 計算延遲
  - $T_{CAP}^{m,n} = \frac{l_{CAP}^{m,n} \omega \kappa}{f_{CAP}^{m,n}}$
- 雲端計算延遲
  - $T_{c}^{m,n} = \frac{l_{c}^{m,n} \omega \kappa}{f_{c}^{m}}$

### 價格模型

- 基礎服務費用
  - $\tau_{m} = \zeta_1 (\alpha_{m} l_{m}) + \zeta_2 (\beta_{m} \alpha_{m} l_{m})$
- 計算服務費用
  - $\pi_{m} = \eta_1 (f_{CAP}^{m,n}) + \eta_2 (f_{c}^{m})$
- 總費用
  - $U_{m} = \tau_{m} + \pi_{m}$
- 預算約束
  - $U_{m} \leq U_{max}^{m}$

## 問題表述

### 目標

- 最小化總系統延遲
- 優化卸載策略、帶寬資源管理和計算資源分配

### 約束條件

- 卸載比例約束
  - $\alpha_{m} \in [0, 1], \beta_{m} \in [0, 1], \forall m \in M$
- 帶寬資源約束
  - $\sum_{m=1}^{M} w_{CAP}^{m,n} \leq W_{CAP}^{n}, \forall n \in N$
  - $\sum_{m=1}^{M} w_{c}^{m,n} \leq W_{c}, \forall n \in N$
- 計算資源約束
  - $\sum_{m=1}^{M} f_{CAP}^{m,n} \leq F_{CAP}^{n}, \forall n \in N$
  - $\sum_{m=1}^{M} f_{c}^{m} \leq F_{c}, \forall m \in M$
- 預算約束
  - $U_{m} \leq U_{max}^{m}, \forall m \in M$

## 解決方案

### 深度強化學習（DRL）

- DRL 簡介
  - DRL 結合了深度學習和強化學習的優勢，適用於解決複雜的決策問題。
  - 強化學習的目標是找到一個策略，使得智能體在與環境互動過程中獲得最大化的累積獎勵。
  - 深度學習使用神經網絡來處理和分析大量數據，學習複雜的特徵表示。
- 在本研究中的應用
  - 使用 DRL 來決定多源數據流的卸載策略。
  - 針對不同的網絡狀況和資源約束，動態調整卸載決策，優化系統性能。

### 擴展協同學習近端策略優化（ECC-PPO）

- ECC-PPO 簡介
  - PPO（Proximal Policy Optimization）是深度強化學習中的一種策略優化方法，以其穩定性和高效性而著稱。
  - ECC-PPO 在 PPO 的基礎上進行了擴展，專門針對多源數據流的資源分配問題。
- 具體實現
  - 將整個資源分配問題分為卸載決策和資源分配兩個部分。
  - 首先，使用 DRL 進行卸載策略分配，即決定每個設備的數據流是否卸載到邊緣計算節點或雲端。
  - 然後，使用凸優化方法進行帶寬和計算資源的分配，以達到總系統延遲最小化的目標。
- 優勢
  - 將 DRL 和凸優化結合，充分利用兩者的優勢。
  - DRL 能夠處理動態和不確定性的環境，凸優化能夠提供精確和高效的資源分配。

## 模擬結果

- ECC-PPO 的性能驗證
- 模擬數據顯示該方案在動態網絡中表現良好
- 可以提高多源數據流應用的性能

## 結論

- 提出了一種新的資源分配方案
- 動態環境下的有效性驗證
- 對多源數據流應用的發展具有重要意義

✨ **備註**：以上內容均來自《Intelligent resource allocation scheme for cloud-edge-end framework aided multi-source data stream》文件。
