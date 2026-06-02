# Model Evaluation Scorecard

> Điền ở giai đoạn 5 để chấm điểm và ra quyết định Go/No-Go. Dùng phần [ML] hoặc [LLM] phù hợp.

## 1. Thông tin
- **Tên model / phiên bản**:
- **Người đánh giá / ngày**:
- **Tập dữ liệu đánh giá (phiên bản)**:
- **Baseline để so sánh**:

## 2A. Chỉ số kỹ thuật — [ML]
### Phân loại
| Chỉ số | Baseline | Model | Ngưỡng tối thiểu | Đạt? |
|---|---|---|---|---|
| Accuracy |  |  |  |  |
| Precision |  |  |  |  |
| Recall |  |  |  |  |
| F1 |  |  |  |  |
| ROC-AUC / PR-AUC |  |  |  |  |

### Hồi quy
| Chỉ số | Baseline | Model | Ngưỡng | Đạt? |
|---|---|---|---|---|
| MAE |  |  |  |  |
| RMSE |  |  |  |  |
| R² |  |  |  |  |

## 2B. Chỉ số chất lượng — [LLM]
| Chỉ số | Baseline | Model | Ngưỡng | Đạt? |
|---|---|---|---|---|
| Độ chính xác tác vụ |  |  |  |  |
| Faithfulness / groundedness (RAG) |  |  |  |  |
| Hallucination rate (thấp hơn tốt hơn) |  |  |  |  |
| Tỉ lệ nội dung không an toàn (thấp hơn tốt hơn) |  |  |  |  |
| Tỉ lệ đúng định dạng đầu ra |  |  |  |  |
| Độ nhất quán khi lặp lại |  |  |  |  |

## 3. Đánh giá theo con người (human eval)
| Tiêu chí | Cỡ mẫu | Điểm trung bình | Ngưỡng | Đạt? |
|---|---|---|---|---|
| Đúng / chính xác |  |  |  |  |
| Hữu ích |  |  |  |  |
| An toàn / phù hợp |  |  |  |  |

## 4. Công bằng & độ bền
| Hạng mục | Kết quả | Đạt? |
|---|---|---|
| Chênh lệch chỉ số giữa các nhóm nhạy cảm |  |  |
| Độ bền với đầu vào nhiễu/biên/OOD |  |  |
| [LLM] Chống prompt injection |  |  |

## 5. Ràng buộc vận hành
| Hạng mục | Đo được | Yêu cầu | Đạt? |
|---|---|---|---|
| Latency p95 / p99 |  |  |  |
| Thông lượng (req/s) |  |  |  |
| Chi phí mỗi request ([LLM]: token) |  |  |  |
| Tài nguyên (CPU/GPU/RAM) |  |  |  |

## 6. Hạn chế đã biết
-

## 7. Quyết định
- [ ] **Go** — đạt tiêu chí, tiến hành tích hợp
- [ ] **No-Go** — quay lại cải tiến (ghi rõ hạng mục chưa đạt)
- [ ] **Go có điều kiện** — kèm biện pháp giảm thiểu rủi ro
- **Lý do / điều kiện**:
- **Người duyệt (Accountable) / ngày**:
