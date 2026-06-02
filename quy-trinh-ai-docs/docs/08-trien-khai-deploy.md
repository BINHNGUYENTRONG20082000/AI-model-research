# Giai đoạn 8 — Triển khai (Deploy)

## Mục tiêu
Đưa tính năng AI ra môi trường sản xuất một cách **an toàn, có kiểm soát rủi ro** và **có khả năng quay lui (rollback)** nhanh, đồng thời đo lường tác động thực tế lên KPI.

## Đầu vào
- Hệ thống đã qua QA & UAT (giai đoạn 7).
- Model Card hoàn chỉnh.
- Hạ tầng sản xuất & kế hoạch giám sát (giai đoạn 9 đã chuẩn bị).

## Hoạt động chi tiết
1. **Chuẩn bị hạ tầng sản xuất**
   - Cấu hình tài nguyên (CPU/GPU/RAM), autoscaling, hạn mức (quota).
   - Cấu hình môi trường, secret, biến cấu hình theo môi trường prod.
   - Hoàn tất [Deployment Checklist](../templates/04-deployment-checklist.md).
2. **Chọn chiến lược release**
   - **Shadow / dark launch**: model chạy song song nhận traffic thật nhưng không ảnh hưởng người dùng; dùng để so kết quả an toàn.
   - **Canary**: mở cho một tỉ lệ nhỏ người dùng (ví dụ 5%), tăng dần nếu ổn.
   - **Blue-Green**: chạy song song hai phiên bản, chuyển traffic và rollback nhanh.
   - **A/B test**: so sánh model mới với baseline/phiên bản cũ trên KPI nghiệp vụ với ý nghĩa thống kê.
3. **Triển khai theo từng bước (rollout)**
   - Bật qua feature flag cho nhóm nhỏ → quan sát → mở rộng dần.
   - Theo dõi sát chỉ số kỹ thuật (latency, lỗi) và nghiệp vụ (KPI) ở mỗi bước.
4. **Phê duyệt & truyền thông**
   - Có phê duyệt của người chịu trách nhiệm (release approval).
   - Thông báo cho các bên liên quan; chuẩn bị tài liệu hỗ trợ/CSKH nếu cần.
5. **Sẵn sàng rollback**
   - Định nghĩa rõ điều kiện kích hoạt rollback (ngưỡng lỗi, sụt KPI).
   - Quy trình rollback đã được thử (tắt feature flag hoặc chuyển phiên bản).
6. **Đo tác động & kết luận**
   - Sau khi mở 100%, đánh giá kết quả A/B và tác động lên KPI thực tế.
   - Ghi nhận kết quả và quyết định giữ/điều chỉnh.

## Vai trò (RACI)
| Hoạt động | MLOps/Platform | SRE | PO/BA | Data Scientist |
|---|---|---|---|---|
| Chuẩn bị hạ tầng | A/R | C | I | I |
| Chọn chiến lược release | R | C | A | C |
| Rollout & theo dõi | A/R | R | C | C |
| Phê duyệt release | C | C | A/R | I |
| Rollback | A/R | R | I | C |
| Đánh giá A/B & KPI | C | I | A | R |

## Đầu ra
- Tính năng AI chạy trên sản xuất ở quy mô mục tiêu.
- Deployment Checklist hoàn tất; quy trình rollback đã kiểm chứng.
- Kết quả A/B test và tác động KPI.
- Bản ghi release (phiên bản model, thời điểm, người duyệt).

## Checklist
- [ ] Deployment Checklist hoàn tất và được duyệt.
- [ ] Chiến lược release (shadow/canary/blue-green/A-B) được chọn và cấu hình.
- [ ] Giám sát & cảnh báo đã bật trước khi mở traffic.
- [ ] Điều kiện và quy trình rollback rõ ràng, đã thử.
- [ ] Có phê duyệt release và đã thông báo các bên.
- [ ] Đo được tác động KPI sau khi mở rộng.

## Tiêu chí qua cổng (Gate)
- Tính năng chạy ổn định ở sản xuất, chỉ số kỹ thuật & nghiệp vụ trong ngưỡng.
- Rollback sẵn sàng và đã kiểm chứng.
- Chuyển sang vận hành & giám sát liên tục (giai đoạn 9).
