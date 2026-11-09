# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` (0) | Xe con, SUV, taxi và xe bán tải. | UAZ dáng Jeep/SUV thuộc `car`. |
| `truck` (1) | Xe tải chở hàng và xe đầu kéo. | Xe tải thùng hoặc xe đầu kéo thuộc `truck`. Với xe có thùng hở, kiểm tra kiểu thân để phân biệt xe tải với bán tải. |
| `bus` (2) | Xe buýt và minibus chở khách. | Khi khó phân biệt minibus với van chở người, ghi lại ca để hỏi giảng viên. |
| `van` (3) | Xe van và minivan chở hàng hoặc chở người. | Thân cao, dáng hộp và khoang sau liền với cabin là dấu hiệu để xem xét cùng các chi tiết khác của thân xe. |

## Quy tắc chung

- **Box bám sát vật thể.** Vẽ một box cho mỗi xe thuộc bốn lớp. Đặt bốn cạnh sát phần xe nhìn thấy và tránh lấy thêm nền hoặc xe bên cạnh.
- **Vật thể bị che khuất.** Nếu phần lộ ra đủ để xác định lớp, vẽ box quanh phần nhìn thấy. Khi nhiều xe che nhau, xét từng xe riêng. Các box có thể chồng lên nhau.
- **Vật thể bị cắt bởi rìa ảnh.** Nếu vẫn xác định được lớp, vẽ box quanh phần xe còn trong ảnh. Cạnh box phía bị cắt chạm đúng mép ảnh.
- **Vật thể rất nhỏ hoặc mơ hồ.** Nếu chưa đủ căn cứ để xác định không gán.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

> Thay các tên ảnh mẫu bằng tên ảnh gốc trong CVAT. Chỉ giữ các tình huống đúng với ảnh đã quan sát và cập nhật quyết định sau khi xác nhận.

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_003.jpg` | Xe trắng nhỏ, thân cao và dáng hộp. Ảnh che khuất nên khó phân biệt `car` với `van`. | Chờ giảng viên xác nhận. | Thân cao và đuôi đứng gợi ý `van`, nhưng chi tiết nhìn thấy chưa đủ để chốt lớp. |
| `drive_005.jpg` | Xe UAZ thân vuông, dễ nhầm giữa SUV và xe tải nhỏ. | Gán `car` nếu ảnh xác nhận xe có kiểu thân Jeep/SUV. | Schema xếp SUV vào `car`. Dựa vào kiểu thân xe để phân lớp. |
| `drive_006.jpg` | Nhiều xe che nhau. Một xe phía sau chỉ lộ đầu và cabin. | Vẽ một box riêng nếu phần lộ ra đủ để xác định lớp. Ghi lớp cụ thể sau khi đối chiếu ảnh. | Mỗi xe nhận diện được có một box sát phần nhìn thấy, kể cả khi các box chồng lên nhau. |
