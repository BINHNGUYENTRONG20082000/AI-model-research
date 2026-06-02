# Giai đoạn 2 — Nghiên cứu & đánh giá khả thi

## Mục tiêu
Khảo sát các hướng giải pháp, xây dựng **baseline** và **Proof of Concept (PoC)** để xác nhận bài toán **khả thi về kỹ thuật, chi phí và dữ liệu** trước khi cam kết xây dựng đầy đủ.

## Đầu vào
- Requirement Brief đã duyệt (từ giai đoạn 1).
- KPI, ràng buộc, loại bài toán.
- Hiểu biết sơ bộ về dữ liệu sẵn có.

## Hoạt động chi tiết
1. **Khảo sát giải pháp & state-of-the-art**
   - Tìm hiểu cách bài toán tương tự đã được giải (paper, blog, sản phẩm, thư viện).
   - Liệt kê các hướng tiếp cận khả dĩ và ưu/nhược điểm.
2. **Quyết định hướng xây dựng (build vs buy)**
   - [ML] Tự train model: cần dữ liệu gán nhãn, hạ tầng train, chuyên môn.
   - [LLM] Dùng API có sẵn (closed-source) vs model mở (self-host) vs fine-tune vs **RAG** (truy hồi tri thức) vs chỉ prompt engineering.
   - Cân nhắc: chi phí, kiểm soát dữ liệu, độ trễ, khả năng tùy biến, khóa nhà cung cấp (vendor lock-in).
3. **Xây dựng baseline**
   - Baseline đơn giản nhất (rule, model nhỏ, hoặc prompt cơ bản) để có mốc so sánh.
   - Mọi cải tiến về sau phải vượt baseline mới đáng giá.
4. **Làm PoC nhanh**
   - [ML] Train thử trên tập dữ liệu nhỏ, đo chỉ số sơ bộ.
   - [LLM] Thử vài prompt/model trên một bộ ví dụ đại diện (10–50 mẫu), đánh giá định tính + định lượng nhanh.
   - Mục tiêu PoC: trả lời "có khả thi đạt KPI không?", **không** phải tối ưu hoàn chỉnh.
5. **Ước lượng chi phí & nguồn lực**
   - Chi phí train/suy luận (inference), hạ tầng, lưu trữ.
   - [LLM] Ước lượng chi phí token: (số request × token vào/ra × đơn giá). Cân nhắc caching.
   - Nhân lực và thời gian.
6. **Đánh giá rủi ro kỹ thuật & dữ liệu**
   - Có đủ dữ liệu chất lượng không? Có vấn đề bias/quyền riêng tư không?
   - Rủi ro về độ trễ, độ chính xác, khả năng giải thích.
7. **Khuyến nghị Go/No-Go cho giai đoạn xây dựng đầy đủ.**

## Vai trò (RACI)
| Hoạt động | PO/BA | Data Scientist | Eng/MLOps | Security/Legal |
|---|---|---|---|---|
| Khảo sát giải pháp | C | A/R | C | I |
| Build vs buy | C | R | C | C |
| Baseline & PoC | I | A/R | C | I |
| Ước lượng chi phí | C | R | C | I |
| Khuyến nghị Go/No-Go | A | R | C | C |

## Đầu ra
- Báo cáo nghiên cứu khả thi: các hướng tiếp cận, lựa chọn đề xuất + lý do.
- Kết quả baseline & PoC (chỉ số sơ bộ).
- Ước lượng chi phí & nguồn lực.
- Khuyến nghị Go/No-Go.

## Checklist
- [ ] Đã khảo sát ≥ 2 hướng tiếp cận và so sánh.
- [ ] Đã quyết định build/buy (train, API, fine-tune, RAG, hay prompt).
- [ ] Có baseline để làm mốc so sánh.
- [ ] PoC cho thấy khả năng đạt (hoặc tiệm cận) KPI.
- [ ] Có ước lượng chi phí vận hành ([LLM] gồm chi phí token).
- [ ] Rủi ro dữ liệu/kỹ thuật được nhận diện.

## Tiêu chí qua cổng (Gate)
- PoC chứng minh bài toán **khả thi** và có đường đạt KPI.
- Chi phí ước lượng nằm trong ngân sách cho phép.
- Có quyết định **Go** để chuyển sang chuẩn bị dữ liệu / xây dựng đầy đủ.
