# Giai đoạn 7 — Kiểm thử & QA

## Mục tiêu
Đảm bảo tính năng AI và toàn bộ hệ thống xung quanh model hoạt động **đúng, ổn định, an toàn và đủ hiệu năng** trước khi triển khai cho người dùng thật.

## Đầu vào
- Dịch vụ model đã tích hợp trên staging (giai đoạn 6).
- Hợp đồng API, Model Card, tiêu chí thành công.
- Eval/test set và các kịch bản nghiệp vụ.

## Hoạt động chi tiết
1. **Kiểm thử chức năng (functional)**
   - Unit test cho tiền/hậu xử lý và logic nghiệp vụ.
   - Integration test cho luồng end-to-end (request → model → phản hồi → UI).
   - Kiểm thử fallback: mô phỏng model lỗi/timeout để chắc chắn hệ thống xử lý đúng.
2. **Kiểm thử dữ liệu biên & bất thường**
   - Đầu vào rỗng, quá dài, sai định dạng, ký tự đặc biệt, đa ngôn ngữ.
   - Trường hợp ngoài phân bố (out-of-distribution).
3. **Kiểm thử chất lượng model trong sản phẩm**
   - Chạy lại bộ eval trên dịch vụ đã tích hợp để xác nhận chỉ số không suy giảm so với giai đoạn 5 (do khác biệt môi trường/tiền xử lý).
   - **Regression test cho AI**: bộ ví dụ "vàng" phải luôn cho kết quả đạt ngưỡng.
4. **An toàn & bảo mật**
   - [LLM] **Red-teaming**: thử prompt injection, jailbreak, dụ rò rỉ dữ liệu/khóa, sinh nội dung độc hại.
   - Kiểm thử xác thực/ủy quyền, rate limiting, rò rỉ PII trong log/phản hồi.
5. **Kiểm thử hiệu năng & tải**
   - Load test ở tải dự kiến và đỉnh; đo latency p95/p99 và tỉ lệ lỗi.
   - Kiểm tra hành vi khi quá tải (degradation, fallback, hàng đợi).
   - [LLM] Kiểm tra ứng xử với rate limit của nhà cung cấp.
6. **Kiểm thử chấp nhận (UAT)**
   - Người dùng/PO xác nhận tính năng đáp ứng yêu cầu nghiệp vụ và KPI.

## Vai trò (RACI)
| Hoạt động | QA | Software Eng | Data Scientist | Security |
|---|---|---|---|---|
| Functional & integration test | A/R | C | I | I |
| Kiểm thử biên & regression AI | A/R | C | C | I |
| Red-teaming & bảo mật | C | C | C | A/R |
| Load/performance test | R | A/R | I | I |
| UAT | R | I | I | I |

## Đầu ra
- Báo cáo kiểm thử: kết quả functional, biên, regression, bảo mật, hiệu năng.
- Bộ test tự động (gồm regression AI) đưa vào CI.
- Danh sách lỗi/khuyết tật đã xử lý hoặc chấp nhận rủi ro.
- Kết quả UAT được ký duyệt.

## Checklist
- [ ] Unit/integration test phủ luồng chính và fallback.
- [ ] Đã kiểm thử dữ liệu biên/bất thường.
- [ ] Chỉ số model trên dịch vụ tích hợp khớp với giai đoạn 5.
- [ ] Có regression test với golden examples trong CI.
- [ ] [LLM] Đã red-teaming prompt injection/jailbreak/nội dung độc hại.
- [ ] Load test đạt ngưỡng latency/tỉ lệ lỗi ở tải đỉnh.
- [ ] UAT được PO/người dùng chấp nhận.

## Tiêu chí qua cổng (Gate)
- Không còn lỗi nghiêm trọng (blocker/critical) chưa xử lý.
- Đạt ngưỡng chất lượng, an toàn và hiệu năng đã định.
- UAT được duyệt → sẵn sàng triển khai ở giai đoạn 8.
