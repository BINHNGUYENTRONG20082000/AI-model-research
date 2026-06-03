# Giai đoạn 9 — Giám sát & vận hành (MLOps / LLMOps)

## Mục tiêu
Đảm bảo model duy trì **chất lượng, độ tin cậy, an toàn và chi phí hợp lý** theo thời gian khi vận hành thực tế; phát hiện sớm suy giảm (drift) và sự cố để xử lý kịp thời.

> Khác biệt với phần mềm thông thường: chất lượng model **suy giảm theo thời gian** do dữ liệu/thế giới thay đổi, dù code không đổi.

## Đầu vào
- Tính năng AI đã chạy sản xuất (giai đoạn 8).
- [Monitoring Runbook](../templates/05-monitoring-runbook.md) đã thiết lập.
- Ngưỡng KPI và SLO.

## Hoạt động chi tiết
1. **Giám sát hệ thống (operational)**
   - Latency (p50/p95/p99), throughput, tỉ lệ lỗi, uptime/SLO.
   - Tài nguyên (CPU/GPU/RAM), hàng đợi; [DL] giám sát mức sử dụng GPU/bộ nhớ GPU và chi phí GPU; [LLM] số token, rate limit, lỗi nhà cung cấp.
2. **Giám sát chất lượng model (model performance)**
   - Theo dõi chỉ số chất lượng khi có nhãn thực tế (ground truth) trở về (có thể trễ).
   - Khi chưa có nhãn ngay: dùng proxy (tỉ lệ người dùng chấp nhận, tỉ lệ chuyển sang con người, phản hồi tiêu cực).
   - [LLM] Theo dõi hallucination/an toàn qua lấy mẫu + chấm (người hoặc LLM-judge), tỉ lệ phản hồi sai định dạng.
3. **Phát hiện drift**
   - **Data drift**: phân bố đầu vào thay đổi so với lúc train.
   - **Concept drift**: quan hệ giữa đầu vào và nhãn thay đổi → chất lượng giảm.
   - **Prediction drift**: phân bố đầu ra thay đổi bất thường.
   - Đặt ngưỡng cảnh báo cho từng loại.
4. **Giám sát chi phí**
   - Theo dõi chi phí hạ tầng/inference; [LLM] chi phí token theo ngày/tuần, phát hiện tăng bất thường.
5. **Logging, truy vết & phản hồi**
   - Log request/response (đã ẩn PII) để gỡ lỗi và phân tích; bật tracing.
   - Thu thập phản hồi người dùng làm tín hiệu chất lượng và dữ liệu cải tiến.
6. **Cảnh báo & on-call**
   - Thiết lập alert theo ngưỡng (lỗi, latency, drift, chi phí, sụt KPI).
   - Phân công on-call và runbook xử lý sự cố (gồm khi nào rollback).
7. **Vòng phản hồi dữ liệu**
   - Lưu các trường hợp khó/sai để bổ sung vào tập dữ liệu/eval cho lần cải tiến sau (chú ý quyền riêng tư).

## Vai trò (RACI)
| Hoạt động | MLOps | SRE/On-call | Data Scientist | PO/BA |
|---|---|---|---|---|
| Giám sát hệ thống | A/R | R | I | I |
| Giám sát chất lượng & drift | R | C | A/R | C |
| Giám sát chi phí | A/R | C | C | C |
| Cảnh báo & on-call | A/R | R | C | I |
| Xử lý sự cố | R | A/R | C | I |

## Đầu ra
- Dashboard giám sát (hệ thống + chất lượng + chi phí).
- Cảnh báo theo ngưỡng và phân công on-call.
- Monitoring Runbook đang vận hành; nhật ký sự cố.
- Kho dữ liệu trường hợp khó/sai phục vụ cải tiến.

## Checklist
- [ ] Dashboard theo dõi latency/lỗi/throughput/chi phí.
- [ ] Theo dõi chất lượng model (trực tiếp hoặc proxy).
- [ ] Phát hiện data/concept/prediction drift với ngưỡng cảnh báo.
- [ ] [LLM] Giám sát token, an toàn, hallucination qua lấy mẫu.
- [ ] Logging ẩn PII, có tracing.
- [ ] Cảnh báo và on-call được thiết lập; runbook sẵn sàng.
- [ ] Có vòng thu thập dữ liệu/phản hồi để cải tiến.

## Tiêu chí qua cổng (Gate)
- Hệ thống giám sát đầy đủ, cảnh báo hoạt động, on-call sẵn sàng.
- Có dữ liệu vận hành để đánh giá nhu cầu cải tiến (chuyển sang giai đoạn 10 khi cần).
