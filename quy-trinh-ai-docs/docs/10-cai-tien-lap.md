# Giai đoạn 10 — Cải tiến lặp (Iteration)

## Mục tiêu
Liên tục cải thiện model và tính năng dựa trên dữ liệu vận hành và phản hồi, duy trì chất lượng trước sự thay đổi của dữ liệu/thế giới, và kiểm soát nợ kỹ thuật.

## Đầu vào
- Dữ liệu giám sát, cảnh báo drift, phản hồi người dùng (giai đoạn 9).
- Trường hợp khó/sai đã thu thập.
- KPI thực tế so với mục tiêu.

## Hoạt động chi tiết
1. **Phân tích & ưu tiên cải tiến**
   - Xác định nguyên nhân suy giảm/lỗi (drift, dữ liệu mới, thay đổi nghiệp vụ).
   - Ưu tiên cải tiến theo tác động tới KPI và chi phí.
2. **Cập nhật dữ liệu & retrain/refresh**
   - [ML] **Retrain** với dữ liệu mới (định kỳ hoặc theo trigger drift); bổ sung trường hợp khó.
   - [LLM] Cập nhật prompt, làm mới kho tri thức RAG, hoặc fine-tune lại; cập nhật khi nhà cung cấp đổi phiên bản model.
3. **Đánh giá lại trước khi phát hành**
   - Chạy lại quy trình giai đoạn 5 (evaluation) cho phiên bản mới.
   - **So sánh với phiên bản đang chạy** để chắc chắn không hồi quy (regression).
   - Cập nhật [Model Card](../templates/03-model-card.md) và scorecard.
4. **Phát hành phiên bản mới**
   - Theo lại chiến lược release an toàn ở giai đoạn 8 (canary/A-B/shadow) + rollback.
5. **Quản lý phiên bản & nợ kỹ thuật**
   - Versioning model/dữ liệu/prompt; ghi changelog.
   - Dọn dẹp model/cờ tính năng cũ; cập nhật thư viện và vá lỗ hổng bảo mật.
   - Rà soát định kỳ chi phí và hiệu quả; cân nhắc gỡ bỏ tính năng nếu không còn giá trị.
6. **Khép vòng quản trị**
   - Định kỳ rà soát rủi ro, công bằng, tuân thủ (đặc biệt khi dữ liệu/luật thay đổi).
   - Lưu lại bài học và cập nhật chính tài liệu quy trình này.

## Vai trò (RACI)
| Hoạt động | Data Scientist | MLOps | PO/BA | Security/Legal |
|---|---|---|---|---|
| Phân tích & ưu tiên | R | C | A | I |
| Retrain/refresh | A/R | C | I | I |
| Đánh giá lại & chống hồi quy | A/R | C | C | I |
| Phát hành phiên bản mới | C | A/R | C | I |
| Quản lý nợ kỹ thuật | C | A/R | I | C |
| Rà soát rủi ro/tuân thủ | C | I | C | A/R |

## Đầu ra
- Phiên bản model/tính năng cải tiến đã đánh giá và phát hành (hoặc quyết định giữ nguyên).
- Model Card & scorecard cập nhật; changelog phiên bản.
- Lịch retrain/refresh và tiêu chí trigger.
- Cập nhật bài học vào quy trình.

## Checklist
- [ ] Đã phân tích nguyên nhân và ưu tiên cải tiến theo tác động.
- [ ] Phiên bản mới được đánh giá lại như giai đoạn 5.
- [ ] Đã so sánh và xác nhận không hồi quy so với bản đang chạy.
- [ ] Phát hành theo chiến lược an toàn, có rollback.
- [ ] Model/dữ liệu/prompt được đánh phiên bản, có changelog.
- [ ] Rủi ro/tuân thủ được rà soát định kỳ.

## Tiêu chí qua cổng (Gate)
- Mỗi vòng cải tiến phải **vượt hoặc bằng** phiên bản hiện tại theo KPI và an toàn mới được thay thế.
- Vòng lặp được duy trì: dữ liệu vận hành → cải tiến → đánh giá → phát hành → giám sát.
