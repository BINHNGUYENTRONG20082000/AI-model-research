# Giai đoạn 5 — Đánh giá model (Evaluation)

## Mục tiêu
Đánh giá toàn diện ứng viên model trên dữ liệu chưa từng thấy, theo cả **chỉ số kỹ thuật**, **chất lượng theo con người**, **công bằng/an toàn** và **ràng buộc vận hành**, để ra quyết định **Go/No-Go** có căn cứ.

## Đầu vào
- Shortlist model/cấu hình (từ giai đoạn 4).
- Test set độc lập / eval set (chưa dùng để tinh chỉnh).
- KPI và tiêu chí thành công tối thiểu.

## Hoạt động chi tiết

### 1. Đánh giá offline theo chỉ số kỹ thuật
- **[ML] Phân loại**: Accuracy, Precision, Recall, **F1**, ROC-AUC, PR-AUC, confusion matrix. Lưu ý chọn chỉ số phù hợp khi dữ liệu mất cân bằng (ưu tiên F1/PR-AUC hơn accuracy).
- **[ML] Hồi quy**: MAE, RMSE, MAPE, R².
- **[ML] Xếp hạng/gợi ý**: Precision@k, Recall@k, NDCG, MAP.
- **[ML] Hiệu chỉnh xác suất (calibration)** nếu cần xác suất tin cậy.
- **[DL] Theo tác vụ**:
  - Thị giác: Top-1/Top-5 accuracy (phân loại), **mAP**/IoU (phát hiện đối tượng), Dice/IoU (phân vùng).
  - NLP: F1/Exact Match, **BLEU**/**ROUGE** (sinh/dịch), perplexity.
  - Âm thanh: **WER** (nhận dạng giọng nói).
  - Kiểm tra độ bền với nhiễu/biến đổi đầu vào và tấn công đối nghịch (adversarial).
- **[LLM]**:
  - **Chất lượng tác vụ**: độ chính xác trả lời, độ đúng trích xuất, điểm tương đồng (ví dụ với tham chiếu).
  - **Faithfulness / groundedness** (đặc biệt RAG): câu trả lời có bám sát nguồn không.
  - **Hallucination rate**: tỉ lệ bịa đặt.
  - **An toàn**: tỉ lệ nội dung độc hại/không phù hợp, tuân thủ chính sách.
  - **Tính ổn định**: độ nhất quán khi lặp lại (do tính ngẫu nhiên).
  - Có thể dùng **LLM-as-a-judge** để chấm tự động, nhưng cần hiệu chỉnh với đánh giá của con người.

### 2. Đánh giá theo con người (human evaluation)
- Lấy mẫu đại diện, để chuyên gia/người dùng chấm theo tiêu chí (đúng, hữu ích, an toàn, phù hợp).
- Đặc biệt quan trọng với [LLM] và các bài toán khó đo tự động.

### 3. Kiểm thử công bằng & độ bền (fairness & robustness)
- So sánh chỉ số giữa các nhóm nhạy cảm để phát hiện thiên lệch.
- Kiểm thử với đầu vào nhiễu/đối nghịch, dữ liệu biên, ngoài phân bố (out-of-distribution).
- [LLM] Thử prompt injection, đầu vào gây hiểu nhầm.

### 4. Đánh giá ràng buộc vận hành
- Đo **latency** (p50/p95/p99) và thông lượng ở tải dự kiến.
- **Chi phí** mỗi request; [LLM] chi phí token thực tế.
- Kích thước model, yêu cầu tài nguyên (CPU/GPU/RAM).

### 5. Tổng hợp & quyết định Go/No-Go
- Điền [Model Evaluation Scorecard](../templates/02-model-evaluation-scorecard.md).
- So sánh với baseline và tiêu chí tối thiểu.
- Ghi nhận hạn chế đã biết; ra quyết định **Go / No-Go / quay lại cải tiến**.

## Vai trò (RACI)
| Hoạt động | Data Scientist | QA | PO/BA | Security/Legal |
|---|---|---|---|---|
| Đánh giá offline | A/R | C | I | I |
| Human evaluation | R | C | A | I |
| Fairness & robustness | A/R | C | C | C |
| Đo latency/chi phí | R | C | C | I |
| Quyết định Go/No-Go | R | C | A | C |

## Đầu ra
- **Model Evaluation Scorecard** đã điền.
- Báo cáo đánh giá: chỉ số, kết quả human eval, fairness/robustness, latency/chi phí.
- Quyết định Go/No-Go có ghi lý do.
- (Nếu Go) **Model Card** bản nháp (xem [template](../templates/03-model-card.md)).

## Checklist
- [ ] Đánh giá trên test/eval set độc lập, không bị rò rỉ.
- [ ] Dùng chỉ số phù hợp bài toán (không chỉ accuracy khi mất cân bằng).
- [ ] [LLM] Đo faithfulness/hallucination/an toàn, có human eval.
- [ ] Đã kiểm thử công bằng giữa các nhóm và độ bền với đầu vào bất thường.
- [ ] Đã đo latency (p95/p99) và chi phí ở tải dự kiến.
- [ ] Scorecard hoàn tất, so với baseline & tiêu chí tối thiểu.
- [ ] Hạn chế đã biết được ghi lại.

## Tiêu chí qua cổng (Gate)
- Model **đạt hoặc vượt** tiêu chí thành công tối thiểu và baseline.
- Thỏa ràng buộc latency/chi phí/an toàn.
- Có quyết định **Go** kèm Model Card nháp để tiến hành tích hợp; nếu **No-Go**, quay lại giai đoạn 2/3/4.
