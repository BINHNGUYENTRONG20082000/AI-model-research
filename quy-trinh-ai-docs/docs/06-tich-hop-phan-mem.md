# Giai đoạn 6 — Tích hợp vào phần mềm

## Mục tiêu
Đưa model đã được duyệt thành một thành phần phần mềm **ổn định, có phiên bản, an toàn** và tích hợp vào sản phẩm với hợp đồng API rõ ràng cùng cơ chế dự phòng (fallback).

## Đầu vào
- Model đã được duyệt Go (giai đoạn 5) + Model Card.
- Ràng buộc latency/chi phí/bảo mật.
- Kiến trúc sản phẩm hiện tại.

## Hoạt động chi tiết
1. **Đóng gói model thành dịch vụ (serving)**
   - [ML] Đóng gói model + tiền/hậu xử lý thành service (REST/gRPC) hoặc batch job; container hóa (Docker).
   - [LLM] Tạo lớp dịch vụ bao quanh API/model: quản lý prompt template, RAG retriever, cấu hình tham số (temperature...).
2. **Định nghĩa hợp đồng API (API contract)**
   - Schema đầu vào/đầu ra rõ ràng, có versioning (ví dụ `/v1/predict`).
   - Quy ước mã lỗi, định dạng phản hồi, giới hạn kích thước.
3. **Xử lý lỗi & fallback**
   - Timeout, retry có kiểm soát, circuit breaker.
   - **Fallback** khi model lỗi/độ tin cậy thấp: trả về giá trị mặc định, chuyển sang quy tắc, hoặc bàn giao cho con người.
   - [LLM] Xử lý rate limit của nhà cung cấp, lỗi nội dung, đầu ra sai định dạng (validate & retry).
4. **Quản lý phiên bản & cấu hình**
   - **Model registry**: lưu model theo phiên bản, gắn với dữ liệu/experiment.
   - Tách cấu hình khỏi code; quản lý secret/khóa API an toàn.
   - **Feature flag** để bật/tắt tính năng AI mà không cần deploy lại.
5. **Tối ưu suy luận (inference)**
   - [ML] Batch, lượng tử hóa (quantization), caching kết quả.
   - [LLM] Caching theo prompt, streaming phản hồi, kiểm soát độ dài đầu ra để giảm chi phí/độ trễ.
6. **Bảo mật khi tích hợp**
   - Xác thực/ủy quyền cho endpoint; rate limiting.
   - [LLM] Phòng prompt injection, lọc PII đầu vào/đầu ra, không log dữ liệu nhạy cảm.
7. **Tích hợp UI/UX**
   - Thể hiện độ tin cậy/giải thích khi phù hợp; cho phép người dùng phản hồi (feedback) để thu thập tín hiệu cải tiến.

## Vai trò (RACI)
| Hoạt động | ML/MLOps Eng | Software Eng | Data Scientist | Security |
|---|---|---|---|---|
| Đóng gói serving | A/R | C | C | I |
| Hợp đồng API | R | A/R | C | I |
| Fallback & xử lý lỗi | R | A/R | C | I |
| Model registry & cấu hình | A/R | C | C | C |
| Bảo mật tích hợp | C | R | I | A/R |

## Đầu ra
- Dịch vụ model có phiên bản, container hóa, có hợp đồng API tài liệu hóa.
- Cơ chế fallback & xử lý lỗi.
- Cấu hình feature flag và quản lý secret.
- Model đã đăng ký trong registry.

## Checklist
- [ ] Model được đóng gói và phục vụ qua API có version.
- [ ] Hợp đồng API (schema, mã lỗi) được tài liệu hóa.
- [ ] Có fallback khi model lỗi hoặc độ tin cậy thấp.
- [ ] Secret/khóa API được quản lý an toàn, không hardcode.
- [ ] Có feature flag để bật/tắt tính năng AI.
- [ ] [LLM] Có phòng vệ prompt injection và validate đầu ra.
- [ ] Có kênh thu thập phản hồi người dùng.

## Tiêu chí qua cổng (Gate)
- Dịch vụ model chạy ổn định trong môi trường staging với hợp đồng API rõ ràng.
- Có fallback, versioning và bảo mật cơ bản.
- Sẵn sàng cho kiểm thử & QA ở giai đoạn 7.
