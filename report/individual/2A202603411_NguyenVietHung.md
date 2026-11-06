# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

> Đổi tên file này thành `MSSV_HoTen.md` của bạn, ví dụ `2A20260000_NguyenVanAn.md`, rồi điền từng mục. Xoá các dòng hướng dẫn in nghiêng khi xong.

- **MSSV: 2A202603411
- **Họ và tên:Nguyen Viet Hung
- **SEED** (in ở ô đầu notebook): 6605

## 1. Bằng chứng

| Tệp | Có? |
| 3 | 3 |
| [`day01_lab.ipynb`](day01_lab.ipynb) 
| [`lab1_report.json`](lab1_report.json) 
| [`hand_calc.jpg`](hand_calc.jpg) 

## 2. Kết quả chính

                                 precision  recall  F1 (test)  F1 (SUB 40)  \
1. BoW + LogReg (tự code)            1.000    0.81      0.895        0.974   
2. BoW + MLP (deep learning)         0.979    0.93      0.954        0.974   
3a. Encoder (MiniLM) + kNN           0.825    0.94      0.879        0.927   
3b. Encoder (MiniLM) + LogReg        0.941    0.96      0.950        0.950   
3c. Encoder (MiniLM) + MLP head      0.941    0.96      0.950        0.950   
4a. LLM nhỏ zero-shot                0.000    0.00      0.000        0.000   
4b. LLM lớn zero-shot                0.000    0.00      0.000        0.000   
4c. LLM nhỏ few-shot                 0.000    0.00      0.000        0.000   

                                 train (s)  tin/s (cả lô)  p50 ms/tin  \
1. BoW + LogReg (tự code)            3.688      24453.660       0.061   
2. BoW + MLP (deep learning)         6.039      33528.346       0.191   
3a. Encoder (MiniLM) + kNN          79.793         25.709      53.269   
3b. Encoder (MiniLM) + LogReg       80.239         39.028      27.695   
3c. Encoder (MiniLM) + MLP head     81.230         39.865      29.183   
4a. LLM nhỏ zero-shot                0.000          1.186     778.842   
4b. LLM lớn zero-shot                0.000          0.968     993.406   
4c. LLM nhỏ few-shot                 0.000          1.128     784.675   

                                 p95 ms/tin  USD / 1k tin  
1. BoW + LogReg (tự code)             0.174         0.000  
2. BoW + MLP (deep learning)          0.275         0.000  
3a. Encoder (MiniLM) + kNN           71.180         0.000  
3b. Encoder (MiniLM) + LogReg        40.482         0.000  
3c. Encoder (MiniLM) + MLP head      46.834         0.000  
4a. LLM nhỏ zero-shot              1096.179         0.005  
4b. LLM lớn zero-shot              1509.622         0.052  
4c. LLM nhỏ few-shot               1454.645         0.016  
• Hàng LLM chỉ đo trên SUB (40 tin) → so sánh chất lượng công bằng bằng cột 'F1 (SUB 40)'.
• SUB chỉ 40 tin: 1 tin sai đổi F1 vài điểm. Chênh < ~0.05 F1 coi như HOÀ — đừng xếp hạng theo số lẻ.
• Inference đo TỪ VĂN BẢN THÔ → NHÃN (gồm cả vectorize / encode). p50/p95 = gọi từng tin một, như một request thật.
• train (s) của 3a/3b/3c = thời gian encoder MiniLM encode tập train (+ train đầu LogReg / MLP); LLM = 0 vì không train. Số đo phụ thuộc CPU/GPU của Colab.


## 3. Dự đoán và thực tế

*Chọn 3 dự đoán `predict(...)` lệch nhiều nhất so với kết quả. Mỗi cái: bạn đoán gì, ra gì, vì sao lệch.*

## 4. Phân tích 50 case khó

*Model nào tụt nhiều nhất, ở nhóm case nào? Nêu 2 case cụ thể và cơ chế khiến model sai.*

## 5. Thử thách cá nhân

*Đề theo SEED của bạn, cách làm, kết quả, giải thích.*

## 6. Phương án cho sản phẩm thật

*đề xuất BoW + MLP làm mô hình phân loại SMS chính.
Yêu cầu	Kết quả
116 tin/giây	Đạt
p95 dưới 50 ms	Đạt
F1 SUB 40 cao	0.974
Recall cao	0.93
Chi phí inference API	0 USD
Phải đánh đổi chủ yếu ở Precision, khả năng giải thích mô hình và độ phức tạp huấn luyện.

## 7. AI log và điều đã học

*Mỗi lần dùng AI: hỏi gì, nhận gì, bạn sửa gì. Sau đó 2–3 câu: điều bạn hiểu ra hôm nay mà trước đó chưa hiểu.*
