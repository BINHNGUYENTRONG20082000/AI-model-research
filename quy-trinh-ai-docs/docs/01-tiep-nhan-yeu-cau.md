# Giai đoạn 1 — Tiếp nhận & làm rõ yêu cầu

## Mục tiêu
Hiểu đúng **bài toán nghiệp vụ** đằng sau yêu cầu, xác định liệu AI có thực sự là giải pháp phù hợp, và chốt được mục tiêu đo lường được (KPI) cùng các ràng buộc trước khi đầu tư nguồn lực.

> Nguyên tắc: "Không bắt đầu bằng việc chọn model, mà bắt đầu bằng việc hiểu vấn đề." Nhiều yêu cầu có thể giải bằng quy tắc nghiệp vụ (rules) hoặc thống kê đơn giản, rẻ và dễ bảo trì hơn AI.

## Đầu vào
- Yêu cầu từ khách hàng / stakeholder (mô tả vấn đề, mong đợi).
- Bối cảnh sản phẩm, người dùng, quy trình nghiệp vụ hiện tại.
- Ràng buộc đã biết (ngân sách, thời hạn, dữ liệu sẵn có, quy định pháp lý).

## Hoạt động chi tiết
1. **Làm rõ vấn đề nghiệp vụ**
   - Vấn đề thực sự cần giải là gì? Ai là người dùng? Quyết định/hành động nào sẽ thay đổi nhờ AI?
   - Hiện tại đang xử lý thế nào (baseline thủ công/quy tắc)? Chi phí của việc làm sai là gì?
2. **Xác định AI có cần thiết không**
   - Có thể giải bằng rule/heuristic/thống kê không? Nếu có thì cân nhắc làm trước như baseline.
   - Bài toán có tính lặp lại, có dữ liệu, có mẫu (pattern) để học không?
3. **Định nghĩa mục tiêu & KPI**
   - KPI nghiệp vụ (ví dụ: giảm 20% thời gian xử lý, tăng 5% tỉ lệ chuyển đổi).
   - Chỉ số kỹ thuật tương ứng (ví dụ: F1 ≥ 0.85; với LLM: tỉ lệ trả lời đúng ≥ 90%).
   - **Tiêu chí thành công tối thiểu** (ngưỡng để được coi là đáng deploy).
4. **Xác định ràng buộc phi chức năng**
   - **Độ trễ (latency)**: thời gian phản hồi tối đa cho phép.
   - **Chi phí**: ngân sách hạ tầng; [LLM] chi phí token theo lượng dùng.
   - **Bảo mật & quyền riêng tư**: dữ liệu nhạy cảm, PII, nơi xử lý dữ liệu (on-prem/cloud).
   - **Pháp lý & tuân thủ**: quy định ngành, GDPR/nghị định bảo vệ dữ liệu, yêu cầu giải thích được (explainability).
   - **Khối lượng**: số request/ngày, đỉnh tải.
5. **Phân loại bài toán**
   - [ML] Phân loại / hồi quy / xếp hạng / phát hiện bất thường / dự báo chuỗi thời gian.
   - [LLM] Sinh văn bản / hỏi đáp / tóm tắt / trích xuất / phân loại bằng prompt / agent.
6. **Đánh giá rủi ro sơ bộ** — dùng [Risk Assessment](../templates/06-risk-assessment.md): tác hại nếu sai, nhóm bị ảnh hưởng, mức độ tự động hóa quyết định.
7. **Chốt phạm vi (scope)** — phạm vi của phiên bản đầu (MVP) và những gì nằm ngoài phạm vi.

## Vai trò (RACI)
| Hoạt động | PO/BA | Data Scientist | Eng | Security/Legal |
|---|---|---|---|---|
| Làm rõ vấn đề & KPI | A/R | C | C | I |
| Đánh giá tính khả thi sơ bộ | C | R | C | I |
| Ràng buộc bảo mật/pháp lý | C | C | C | A/R |
| Chốt phạm vi MVP | A/R | C | C | I |

## Đầu ra
- **Requirement Brief** đã điền (xem [template](../templates/01-requirement-brief.md)).
- Danh sách KPI & tiêu chí thành công tối thiểu.
- Danh sách ràng buộc phi chức năng.
- Bản đánh giá rủi ro sơ bộ.

## Checklist
- [ ] Vấn đề nghiệp vụ và người dùng được mô tả rõ ràng.
- [ ] Đã cân nhắc giải pháp không-AI (rule/heuristic) làm baseline.
- [ ] KPI nghiệp vụ và chỉ số kỹ thuật đo được, có ngưỡng tối thiểu.
- [ ] Ràng buộc latency/chi phí/bảo mật/pháp lý được ghi nhận.
- [ ] Loại bài toán được phân loại rõ ([ML]/[LLM]).
- [ ] Rủi ro sơ bộ và mức độ tác hại được đánh giá.
- [ ] Phạm vi MVP được chốt và thống nhất với stakeholder.

## Tiêu chí qua cổng (Gate)
- Có **Requirement Brief** được stakeholder phê duyệt.
- Có định nghĩa thành công đo lường được và ràng buộc rõ ràng.
- Quyết định: **dùng AI** (đi tiếp giai đoạn 2) hay **dùng giải pháp khác** (dừng quy trình AI).
