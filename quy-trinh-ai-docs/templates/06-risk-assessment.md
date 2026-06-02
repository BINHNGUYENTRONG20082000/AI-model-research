# Risk Assessment — Đánh giá rủi ro AI

> Bắt đầu ở giai đoạn 1 và rà soát lại ở giai đoạn 5 và định kỳ khi vận hành.

## 1. Thông tin
- **Dự án / tính năng**:
- **Người đánh giá / ngày**:
- **Mức độ tự động hóa quyết định**: gợi ý cho người / hỗ trợ / tự động hoàn toàn

## 2. Ma trận rủi ro
> Mức = Khả năng xảy ra (Thấp/Trung/Cao) × Mức tác động (Thấp/Trung/Cao).

| # | Rủi ro | Loại | Khả năng | Tác động | Mức | Biện pháp giảm thiểu | Người phụ trách |
|---|---|---|---|---|---|---|---|
| 1 |  | An toàn |  |  |  |  |  |
| 2 |  | Công bằng / bias |  |  |  |  |  |
| 3 |  | Quyền riêng tư / PII |  |  |  |  |  |
| 4 |  | Bảo mật (rò rỉ, lạm dụng) |  |  |  |  |  |
| 5 |  | Pháp lý / tuân thủ |  |  |  |  |  |
| 6 |  | Chất lượng / độ chính xác |  |  |  |  |  |
| 7 |  | Vận hành / phụ thuộc bên thứ ba |  |  |  |  |  |
| 8 |  | Chi phí |  |  |  |  |  |

## 3. Các nhóm rủi ro cần xem xét
- **An toàn**: tác hại tới người dùng/bên thứ ba khi model sai.
- **Công bằng & bias**: chênh lệch tác động giữa các nhóm; dữ liệu thiên lệch.
- **Quyền riêng tư**: xử lý PII, lưu trữ, đồng thuận, ẩn danh.
- **Bảo mật**: rò rỉ dữ liệu/khóa, lạm dụng; [LLM] prompt injection, jailbreak.
- **Pháp lý / tuân thủ**: quy định ngành, yêu cầu giải thích được, lưu vết.
- **Phụ thuộc bên thứ ba**: thay đổi/ngừng dịch vụ, rate limit, đổi phiên bản model.

## 4. Biện pháp kiểm soát chung
- [ ] Fallback / con người giám sát ở quyết định rủi ro cao.
- [ ] Lọc & ẩn PII đầu vào/đầu ra; kiểm soát truy cập.
- [ ] [LLM] Bộ lọc nội dung và phòng vệ prompt injection.
- [ ] Giám sát chất lượng/an toàn và cảnh báo (xem Monitoring Runbook).
- [ ] Tài liệu hóa & phê duyệt với rủi ro cao.

## 5. Kết luận
- **Rủi ro tồn dư chấp nhận được?** Có / Không
- **Điều kiện kèm theo**:
- **Người phê duyệt (Accountable) / ngày**:
