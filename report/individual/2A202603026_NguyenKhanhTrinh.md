# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên: Nguyễn Khánh Trình
- MSSV: 2A202603026
- Email: 26ai.trinhnk@vinuni.edu.vn
- Lớp: 2A-LAB-E402
- Link repo bài làm: https://github.com/khanhtrinhkt2014/K5-L2A-Day02-NguyenKhanhTrinh-2A202603026-ObjectDetection.git
- Link Colab đã chạy: https://colab.research.google.com/github/khanhtrinhkt2014/K5-L2A-Day02-NguyenKhanhTrinh-2A202603026-ObjectDetection/blob/main/notebooks/day2_annotation_to_yolo.ipynb

## 2. Schema và mini guideline

Theo [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md), bốn lớp là car = 0, truck = 1, bus = 2 và van = 3. Mỗi xe nhận diện được có một box ôm sát phần nhìn thấy. Nếu xe bị cắt khung, cạnh box phía bị cắt chạm mép ảnh. Khi nhiều xe che nhau, xét riêng từng xe và cho phép các box chồng lên nhau.

## 3. Annotation và self-QC

- Số file nhãn train: 50
- Kết quả checker và lỗi đã xử lý: 50/50 file nhãn hợp lệ về cấu trúc. Trên Windows, lệnh python3 không được nhận diện. Chạy lại bằng python tools/check_yolo_labels.py thì checker báo đạt.
- Danh sách ít nhất 10 ảnh đã rà bằng mắt:drive_001.jpg, drive_002.jpg, drive_009.jpg, drive_010.jpg, drive_011.jpg, drive_015.jpg, drive_020.jpg, drive_029.jpg, drive_030.jpg, drive_031.jpg
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa: drive_001.jpg — Xe ở [sát trái gần cổng] bị gán nhầm truck. Đã đổi nhãn thành van vì xe có thân liền dạng hộp và khoang sau liền với cabin. Giữ nguyên box vì box đã ôm sát phần xe nhìn thấy.
- Commit khóa nhãn ban đầu:38918c4d2e6be97f8518d5dcbb3a98f64f8fd41c

## 4. Gold QC và rework

| Chỉ số | Trước sửa | Sau sửa nếu có |
|---|---:|---:|
| TP |458| |
| FP |567| |
| FN |195| |
| Precision |0.4468| |
| Recall |0.7014| |
| F1 |0.5459| |
| mean_iou_of_matches |0.8465| |
| passed |false| |

Dẫn tới `outputs/annotation_evaluation.json` trong repo. Nếu rework, ghi ảnh, lỗi đã kiểm, quyết định sửa/giữ và lý do. Không suy nguyên nhân chỉ từ FP/FN. Không có rework thì ghi rõ.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch:
- Các tham số thay đổi so với notebook nếu có và lý do:
- Đường dẫn best checkpoint trong phiên chạy:

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision | |
| Recall | |
| mAP50 | |
| mAP50–95 | |

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa?
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét?
4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| | | | |

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.

## 8. Công cụ AI và tài liệu tham khảo

Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.
