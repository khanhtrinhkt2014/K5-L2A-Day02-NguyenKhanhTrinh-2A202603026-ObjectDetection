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

[Kết quả chấm nhãn trong repo](../../outputs/annotation_evaluation.json). Bản trên repo tại thời điểm đối chiếu vẫn ghi kết quả lần đầu. Lần đầu, mean IoU của các box đã khớp vượt ngưỡng 0.70, còn F1 thấp hơn ngưỡng 0.80.
- drive_002: 44 box đã vẽ, 13 box gold và 11 box khớp. Ưu tiên rà các box chưa khớp để xem có box trùng, sai lớp, lệch vị trí hoặc ngoài phạm vi hay không.
- drive_041: 24 box gold và 5 box khớp. Ưu tiên rà xe có thể bị sót và các box có thể sai lớp hoặc lệch vị trí.
- Kết quả đã đạt ngưỡng F1 cập nhật của Lab Coach không có rework.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch: Google Colab, GPU Tesla T4 (CUDA:0, 14 913 MiB), Python 3.13.16, Ultralytics 8.4.208 và Torch 2.14.1+cu130.
- Các tham số thay đổi so với notebook nếu có và lý do:
- Đường dẫn best checkpoint trong phiên chạy:
- Mô hình: YOLO26n. Checkpoint dùng để đánh giá: /content/Day2-Lab/outputs/yolo26_runs/vehicle_annotation/weights/best.pt.
- Thư mục kết quả eval trong Colab: /content/Day2-Lab/outputs/yolo26_runs/vehicle_eval.

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision |0.4105|
| Recall |0.2303|
| mAP50 |0.2723|
| mAP50–95 |0.2017|

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.
Đầu ra cần bổ sung từ day2_colab_outputs.zip: [ảnh dự đoán](assets/eval_predictions/) và [kết quả lần chạy YOLO26](assets/yolo26_runs/).

Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa? Lớp có recall thấp nhất: bus. drive_058.jpg
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box? Kiểm tra box dự đoán có bị lệch tâm, quá rộng hoặc quá hẹp so với box chuẩn không. Box có thể khớp ở IoU 0.50 nhưng trượt ở ngưỡng chặt hơn. Rà thêm các cạnh box trên xe bị che hoặc cắt khung.
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét? Trong nhãn người, đã ghi nhận một xe van bị gán nhầm truck. Dấu hiệu cần đối chiếu là khoang sau liền cabin ở van và cấu trúc thùng hàng của xe tải. Trên tập eval, recall của van là 0.0833. Cần xem ảnh dự đoán hoặc ma trận nhầm lẫn để biết mô hình bỏ sót van hay gán sang lớp khác.
4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì? Do cùng tập được dùng để chọn checkpoint, kết quả trên 10 ảnh này chưa phải đánh giá trên một tập test độc lập.

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
|CP5 — Chấm gold lần đầu|F1 = 0.5459, mean IoU = 0.8465.|Đối chiếu số box và số ghép theo ảnh để xác định ảnh cần rà lại.|Đạt theo ngưỡng F1 > 0.50 do Lab Coach thông báo. Chưa có số liệu chấm lại.|

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.

## 8. Công cụ AI và tài liệu tham khảo

Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.
