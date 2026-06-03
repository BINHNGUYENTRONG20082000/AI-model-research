# Giai đoạn 4 — Thử nghiệm & lựa chọn model

## Mục tiêu
Thử nghiệm có hệ thống nhiều ứng viên (model/cấu hình/prompt) để chọn ra phương án tốt nhất theo KPI và ràng buộc, đồng thời đảm bảo **tái lập được (reproducibility)**.

## Đầu vào
- Tập dữ liệu đã chuẩn bị (train/val hoặc eval set).
- Baseline và kết quả PoC.
- KPI, ràng buộc latency/chi phí.

## Hoạt động chi tiết
1. **Thiết lập môi trường thí nghiệm**
   - Cố định seed, phiên bản dữ liệu, phiên bản thư viện để tái lập.
   - Thiết lập **theo dõi experiment** (ví dụ MLflow, Weights & Biases, hoặc bảng ghi chép có cấu trúc): ghi lại tham số, dữ liệu, chỉ số, artefact.
2. **Thử nghiệm các ứng viên**
   - [ML]
     - Thử nhiều thuật toán (ví dụ: hồi quy logistic, gradient boosting, mạng nơ-ron) từ đơn giản đến phức tạp.
     - Tinh chỉnh siêu tham số (hyperparameter tuning) trên tập validation; dùng cross-validation khi dữ liệu ít.
     - Theo dõi overfitting/underfitting.
   - [DL]
     - Chọn kiến trúc mạng phù hợp tác vụ (CNN cho ảnh, RNN/LSTM cho chuỗi, Transformer cho NLP/đa phương thức).
     - Ưu tiên **transfer learning / fine-tune** mô hình tiền huấn luyện thay vì train từ đầu khi dữ liệu hạn chế.
     - Tinh chỉnh learning rate, batch size, số epoch, optimizer; dùng **regularization** (dropout, weight decay), **early stopping**, learning-rate schedule.
     - Theo dõi đường cong loss/accuracy theo epoch trên train và validation; quản lý tài nguyên GPU và checkpoint.
   - [LLM]
     - So sánh các model ứng viên (kích thước/nhà cung cấp khác nhau).
     - **Prompt engineering** có hệ thống (few-shot, hướng dẫn rõ ràng, định dạng đầu ra).
     - Nếu dùng **RAG**: thử nghiệm chiến lược chunking, embedding, top-k, reranking.
     - Cân nhắc **fine-tune** khi prompt/RAG chưa đủ và có đủ dữ liệu.
3. **Đo trên tập độc lập**
   - Đánh giá ứng viên trên validation/eval set (chưa đụng tới test set cuối cùng).
   - So với baseline và với ràng buộc latency/chi phí.
4. **Phân tích lỗi (error analysis)**
   - Xem các trường hợp sai để hiểu giới hạn model; phân nhóm lỗi.
   - Đây là nguồn gợi ý cải tiến (thêm dữ liệu, đổi đặc trưng, sửa prompt).
5. **Lập danh sách rút gọn (shortlist)** 1–2 ứng viên tốt nhất để đánh giá kỹ ở giai đoạn 5.

## Vai trò (RACI)
| Hoạt động | Data Scientist | ML Engineer | PO/BA |
|---|---|---|---|
| Thiết lập theo dõi experiment | C | A/R | I |
| Thử nghiệm ứng viên | A/R | C | I |
| Phân tích lỗi | A/R | C | C |
| Chọn shortlist | A/R | C | C |

## Đầu ra
- Bảng so sánh các ứng viên (chỉ số trên validation/eval, latency, chi phí).
- Experiment được ghi lại (tham số, dữ liệu, kết quả, artefact model).
- Shortlist ứng viên + phân tích lỗi.

## Checklist
- [ ] Thí nghiệm được ghi lại và tái lập được (seed, version dữ liệu/thư viện).
- [ ] Đã thử nhiều phương án và so với baseline.
- [ ] Đo trên tập độc lập, chưa dùng test set cuối.
- [ ] [ML] Đã tinh chỉnh siêu tham số, kiểm soát overfitting.
- [ ] [LLM] Đã thử prompt/RAG/fine-tune một cách có hệ thống.
- [ ] Có phân tích lỗi để hiểu giới hạn model.

## Tiêu chí qua cổng (Gate)
- Có 1–2 ứng viên vượt baseline và tiệm cận KPI, thỏa ràng buộc latency/chi phí.
- Thí nghiệm tái lập được, sẵn sàng cho đánh giá toàn diện ở giai đoạn 5.
