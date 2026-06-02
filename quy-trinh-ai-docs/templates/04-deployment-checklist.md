# Deployment Checklist

> Hoàn tất ở giai đoạn 8. Đánh dấu trước/trong/sau khi deploy.

## Thông tin release
- **Model / phiên bản**:
- **Môi trường**: staging / production
- **Chiến lược release**: shadow / canary / blue-green / A-B
- **Người phụ trách / người duyệt**:
- **Ngày & giờ dự kiến**:

## Trước khi deploy (Pre-deploy)
- [ ] QA & UAT đã được duyệt (giai đoạn 7).
- [ ] Model Card hoàn chỉnh.
- [ ] Scorecard đạt tiêu chí, có quyết định Go.
- [ ] Hạ tầng prod sẵn sàng (tài nguyên, autoscaling, quota).
- [ ] Secret/khóa API cấu hình an toàn theo môi trường.
- [ ] Feature flag sẵn sàng để bật/tắt nhanh.
- [ ] Giám sát & cảnh báo (giai đoạn 9) đã bật.
- [ ] Điều kiện rollback được định nghĩa; quy trình rollback đã thử.
- [ ] Đã thông báo các bên liên quan / CSKH.
- [ ] Backup / phiên bản trước được giữ để quay lui.

## Trong khi deploy (During)
- [ ] Bật cho nhóm nhỏ (shadow/canary %) trước.
- [ ] Theo dõi latency, tỉ lệ lỗi, log trong thời gian thực.
- [ ] Theo dõi KPI nghiệp vụ / kết quả A-B.
- [ ] Tăng dần traffic theo kế hoạch khi ổn định.

## Sau khi deploy (Post-deploy)
- [ ] Xác nhận chỉ số kỹ thuật & nghiệp vụ trong ngưỡng.
- [ ] Ghi nhận kết quả A/B và tác động KPI.
- [ ] Cập nhật bản ghi release (changelog, phiên bản, người duyệt).
- [ ] Đóng hoặc theo dõi các vấn đề phát sinh.

## Kế hoạch Rollback
- **Điều kiện kích hoạt** (ngưỡng lỗi / sụt KPI):
- **Cách rollback** (tắt feature flag / chuyển phiên bản):
- **Người quyết định rollback**:
- **Thời gian rollback mục tiêu**:
