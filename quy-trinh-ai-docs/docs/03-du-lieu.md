# Giai đoạn 3 — Dữ liệu

## Mục tiêu
Chuẩn bị dữ liệu đủ **chất lượng, đại diện và hợp pháp** để huấn luyện và/hoặc đánh giá model. Đây thường là giai đoạn tốn công nhất và quyết định lớn đến chất lượng cuối cùng.

> Nguyên tắc: "Garbage in, garbage out." Chất lượng dữ liệu quan trọng hơn độ phức tạp của model.

## Đầu vào
- Hướng tiếp cận đã chọn (từ giai đoạn 2).
- Yêu cầu về loại dữ liệu, nhãn, khối lượng.
- Ràng buộc quyền riêng tư & pháp lý.

## Hoạt động chi tiết
1. **Thu thập dữ liệu**
   - Xác định nguồn (DB sản xuất, log, bên thứ ba, thu thập mới).
   - Đảm bảo quyền sử dụng dữ liệu (license, hợp đồng, đồng thuận người dùng).
2. **Gán nhãn (labeling)** *(nếu cần học có giám sát)*
   - Định nghĩa hướng dẫn gán nhãn (labeling guideline) rõ ràng, ví dụ minh họa.
   - Đo độ đồng thuận giữa người gán nhãn (inter-annotator agreement).
   - [DL] Gán nhãn chuyên biệt theo tác vụ: bounding box / segmentation mask cho ảnh, nhãn theo khung hình cho video, transcript cho âm thanh; thường cần khối lượng lớn.
   - [LLM] Có thể dùng LLM hỗ trợ gán nhãn sơ bộ rồi người kiểm tra (cẩn trọng với sai lệch).
3. **Làm sạch & tiền xử lý**
   - Xử lý thiếu dữ liệu, trùng lặp, ngoại lệ (outlier), chuẩn hóa định dạng.
   - [ML] Feature engineering, mã hóa, chuẩn hóa thang đo.
   - [DL] Chuẩn hóa/resize ảnh, trích đặc trưng âm thanh (spectrogram), tokenize văn bản; **data augmentation** (xoay/lật/cắt ảnh, nhiễu âm thanh) để tăng dữ liệu và chống overfitting.
   - [LLM] Làm sạch văn bản, chunking tài liệu cho RAG, loại bỏ trùng lặp/nhiễu.
4. **Kiểm tra chất lượng & thiên lệch (bias)**
   - Phân bố lớp/đặc trưng có cân bằng và đại diện cho thực tế không?
   - Có thiên lệch theo nhóm nhạy cảm (giới tính, vùng miền...) không?
   - Phát hiện **rò rỉ dữ liệu (data leakage)**: đặc trưng "nhìn trộm" tương lai/nhãn.
5. **Tách tập dữ liệu**
   - [ML] Chia train/validation/test (ví dụ 70/15/15); với chuỗi thời gian phải chia theo thời gian.
   - Đảm bảo không rò rỉ giữa các tập (cùng người dùng/đối tượng không nằm cả train lẫn test).
   - [DL] Cần lượng dữ liệu lớn; chỉ áp dụng augmentation trên tập train (không trên val/test); đảm bảo ảnh/đoạn của cùng một đối tượng không rơi vào cả train lẫn test.
   - [LLM] Xây **bộ dữ liệu đánh giá (eval set)** đại diện và các ví dụ "vàng" (golden examples); chuẩn bị dữ liệu fine-tune nếu dùng.
6. **Quản trị dữ liệu (data governance)**
   - Ẩn danh/giả danh PII khi cần; kiểm soát truy cập.
   - **Versioning dữ liệu** (ví dụ DVC, hoặc snapshot có ghi nhận) để tái lập thí nghiệm.
   - Ghi nguồn gốc dữ liệu (data lineage) và tài liệu mô tả (data card).

## Vai trò (RACI)
| Hoạt động | Data Engineer | Data Scientist | PO/BA | Security/Legal |
|---|---|---|---|---|
| Thu thập & pipeline | A/R | C | I | C |
| Gán nhãn | C | A/R | C | I |
| Làm sạch & tiền xử lý | R | A/R | I | I |
| Kiểm tra bias/leakage | C | A/R | I | C |
| Quản trị & quyền riêng tư | R | C | I | A/R |

## Đầu ra
- Tập dữ liệu đã làm sạch, có phiên bản, đã tách train/val/test (hoặc eval set cho LLM).
- Tài liệu mô tả dữ liệu (data card): nguồn, kích thước, phân bố, hạn chế, rủi ro bias.
- Hướng dẫn gán nhãn (nếu có).

## Checklist
- [ ] Có quyền hợp pháp sử dụng toàn bộ dữ liệu.
- [ ] PII được xử lý theo quy định; truy cập được kiểm soát.
- [ ] Dữ liệu đại diện cho phân bố thực tế khi vận hành.
- [ ] Đã kiểm tra và xử lý bias, trùng lặp, ngoại lệ.
- [ ] Không có rò rỉ dữ liệu giữa các tập.
- [ ] [ML] Đã tách train/val/test đúng cách; [LLM] có eval set & golden examples.
- [ ] Dữ liệu được đánh phiên bản để tái lập được.

## Tiêu chí qua cổng (Gate)
- Có tập dữ liệu (train/eval) đạt chất lượng, có phiên bản và tài liệu mô tả.
- Đã giải quyết các vấn đề quyền riêng tư/pháp lý.
- Sẵn sàng cho thử nghiệm model ở giai đoạn 4.
