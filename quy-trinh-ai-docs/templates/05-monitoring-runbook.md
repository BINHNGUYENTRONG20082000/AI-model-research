# Monitoring Runbook

> Thiết lập ở giai đoạn 9. Cẩm nang giám sát và xử lý sự cố cho tính năng AI.

## 1. Thông tin
- **Tính năng / model & phiên bản**:
- **Chủ sở hữu / đội on-call**:
- **Dashboard (link)**:
- **Kênh cảnh báo (link)**:

## 2. Chỉ số & ngưỡng cảnh báo
| Nhóm | Chỉ số | Ngưỡng cảnh báo | Mức (warning/critical) | Hành động |
|---|---|---|---|---|
| Hệ thống | Latency p95 |  |  |  |
| Hệ thống | Tỉ lệ lỗi (error rate) |  |  |  |
| Hệ thống | Uptime / SLO |  |  |  |
| Chất lượng | Chỉ số chính / proxy (vd tỉ lệ chấp nhận) |  |  |  |
| Chất lượng | [LLM] Hallucination / nội dung không an toàn |  |  |  |
| Drift | Data drift |  |  |  |
| Drift | Prediction drift |  |  |  |
| Chi phí | Chi phí/ngày ([LLM]: token) |  |  |  |

## 3. Quy trình xử lý sự cố
1. **Xác nhận cảnh báo** — kiểm tra dashboard, phạm vi ảnh hưởng.
2. **Phân loại mức độ** — warning theo dõi tiếp; critical xử lý ngay.
3. **Giảm thiểu nhanh** — bật fallback / giảm traffic / **rollback** nếu vượt ngưỡng (xem điều kiện trong Deployment Checklist).
4. **Chẩn đoán nguyên nhân** — log, tracing, thay đổi gần đây, drift dữ liệu, lỗi nhà cung cấp.
5. **Khắc phục** — sửa cấu hình/prompt, chuyển phiên bản, hoặc lên kế hoạch retrain.
6. **Ghi nhận & hậu kiểm (postmortem)** — nguyên nhân gốc, hành động phòng ngừa.

## 4. Kịch bản thường gặp
| Triệu chứng | Nguyên nhân khả dĩ | Xử lý |
|---|---|---|
| Latency tăng đột biến |  |  |
| Tỉ lệ lỗi tăng |  |  |
| Chất lượng/độ chính xác giảm dần | Drift / dữ liệu thay đổi | Điều tra drift → lên lịch retrain |
| Chi phí token tăng bất thường |  |  |
| [LLM] Tăng nội dung sai/độc hại |  |  |

## 5. Liên hệ & leo thang (escalation)
- **On-call cấp 1**:
- **Leo thang cấp 2 / chủ sở hữu model**:
- **Liên hệ nhà cung cấp (nếu dùng API)**:

## 6. Vòng phản hồi
- **Nơi lưu trường hợp khó/sai để cải tiến**:
- **Tần suất rà soát mẫu chất lượng**:
