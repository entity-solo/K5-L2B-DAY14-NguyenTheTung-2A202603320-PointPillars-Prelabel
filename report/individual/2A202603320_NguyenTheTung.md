# Báo cáo Day 14 — Nguyễn Thế Tùng — 2A202603320

- Mã học viên dùng với `--student`: `2A202603320`
- `seed_tag` trong `frames_A.txt`: `82ac3100fd`

## 1. Dự đoán trước sweep (bước 5b)

- Tham số tôi nghĩ giảm công sửa nhiều nhất: **`score_thr=0.4`, `min_points=10`**.
- Vì sao (nhìn ảnh BEV tập A: box thừa nhiều hay box sót nhiều?): Ảnh BEV và ảnh camera cho thấy **box thừa nhiều hơn box sót rõ rệt**. Phần lớn box thừa nằm trong dải cây/bụi rậm và quanh biển báo, nhiều box vẫn có `score` cao (0.3–0.5) nên chỉ nâng ngưỡng lên 0.2–0.3 sẽ không cắt được. Tôi dự đoán nâng `score_thr` lên **0.4** sẽ loại phần lớn nhóm này, còn `min_points=10` bỏ thêm các box chỉ có vài điểm LiDAR ở xa. Tôi không chọn `score_thr=0.5` vì bắt đầu sót xe thật; mỗi box sót tốn 1.0 điểm, trong khi xóa box thừa chỉ tốn 0.3 điểm. Với nhãn tham chiếu vừa sửa, cấu hình gốc đang có 34 box thừa, 6 box sót và 2 box cần sửa (chi phí 17.2), nên ưu tiên cắt box thừa là hợp lý.

## 2. Tập A: sửa tay và tune

| Cấu hình | Xóa | Thêm | Sửa | Chi phí |
|---|---:|---:|---:|---:|
| Gốc | | | | |
| `best_config.json` | | | | |

- Tham số đã đổi trong `best_config.json`: ...
- Kết quả leave-one-out (dán các dòng `scripts/pp_sweep.py` in ra): ...
- Cấu hình có ổn định trên từng frame không? Vì sao tôi vẫn chọn (hoặc không chọn) nó: ...

## 3. Trước/sau (bước 8)

![so sánh](../../d14_2A202603320/compare/<frame>.jpg)

- `scripts/pp_compare.py` báo giảm (hoặc tăng) ...% công sửa trên tập A.
- Dự đoán ở mục 1 đúng hay sai? Giải thích bằng số box xóa/thêm/sửa: ...

## 4. Tập B

Số đo từ `scripts/pp_prelabel.py --frames d14_2A202603320/frames_B.txt --config d14_2A202603320/best_config.json --gt d14_2A202603320/ref_B.json`:

| Xóa | Thêm | Sửa | Chi phí |
|---:|---:|---:|---:|
| | | | |

- Loại box tốn công sửa nhất ở tập B: ...

## 5. Giới hạn

- Nêu ít nhất 2 giới hạn (ví dụ: chỉ 3 frame tune; model KITTI không có Truck/Bus; chi phí là công thức, chưa phải thời gian sửa thật): ...
