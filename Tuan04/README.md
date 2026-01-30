# THỊ GIÁC MÁY TÍNH (COMPUTER VISION)

- **Sinh Viên Thực Hiện:** Phạm Thế Hùng
- **MSSV:** 2374802010164
- **Môn Học:** Thị Giác Máy Tính
- **Giảng viên:** TS.Đỗ Hữu Quân

## File 1: 2.4.1_Gemetric_trasfroms_PIL.ipynb

### Công nghệ sử dụng
- **PIL (Pillow)**: Thư viện xử lý ảnh đơn giản, dễ dùng cho các tác vụ cơ bản như mở, chỉnh sửa và lưu ảnh
- **Matplotlib**: Thư viện hiển thị ảnh, dùng để xem ảnh trước và sau khi biến đổi
- **NumPy**: Thư viện tính toán với mảng số, dùng để chuyển ảnh sang mảng và tính toán

## Cách hoạt động
#### Phần 1: Geometric Transformations
**Scaling - Thay đổi kích thước:**
- Dùng hàm `resize()` để thay đổi kích thước ảnh
- Có thể phóng to bằng cách nhân đôi chiều rộng hoặc chiều cao
- Có thể thu nhỏ bằng cách chia đôi chiều rộng hoặc chiều cao
- Ví dụ: nhân đôi chiều rộng sẽ làm ảnh rộng gấp đôi

**Rotation - Xoay ảnh:**
- Dùng hàm `rotate()` với góc quay tính bằng độ
- Ví dụ: xoay 45 độ sẽ quay ảnh theo chiều ngược kim đồng hồ

#### Phần 2: Mathematical Operations

**Array Operations - Phép toán mảng:**
- Chuyển ảnh sang mảng số để tính toán được
- Cộng số vào ảnh: `image + 20` làm ảnh sáng hơn
- Nhân ảnh với số: `10 * image` làm ảnh sáng hơn nữa
- Tạo nhiễu ngẫu nhiên và cộng vào ảnh để tạo hiệu ứng nhiễu
- Nhân ảnh với nhiễu để tạo hiệu ứng khác

**Matrix Operations - Phép toán ma trận:**
- Đọc ảnh xám và chuyển thành ma trận số
- Dùng SVD để tách ảnh thành các phần quan trọng nhất

### Kết quả
**Kết quả biến đổi hình học:**
- Thay đổi kích thước ảnh thành công: phóng to, thu nhỏ theo các tỷ lệ khác nhau
- Xoay ảnh thành công, giữ nguyên chất lượng
- Có thể so sánh ảnh gốc và ảnh đã biến đổi cạnh nhau

**Kết quả phép toán mảng:**
- Làm sáng ảnh bằng cách cộng hoặc nhân với số
- Tạo hiệu ứng nhiễu trên ảnh bằng cách cộng nhiễu ngẫu nhiên
- Các phép toán đều hoạt động tốt

**Kết quả phép toán ma trận:**
- Phân tích SVD thành công, tách được ảnh thành các phần
- Khôi phục được ảnh gốc từ các phần đã tách
- Nén ảnh hiệu quả: chỉ cần 100-200 thành phần đầu tiên là đủ để giữ chất lượng ảnh tốt

## File 2: 2.4.2_Gemetric_trasfroms_OpenCV.ipynb
### Công nghệ sử dụng
- **OpenCV (cv2)**: Thư viện mạnh mẽ cho xử lý ảnh, có nhiều hàm tối ưu. Lưu ý: OpenCV đọc ảnh theo định dạng BGR thay vì RGB
- **Matplotlib**: Thư viện hiển thị ảnh, cần chuyển đổi từ BGR sang RGB trước khi hiển thị
- **NumPy**: Thư viện tính toán với mảng số, dùng để tạo ma trận và tính toán

### Cách hoạt động
#### Phần 1: Geometric Transformations

**Scaling - Thay đổi kích thước:**
- Dùng `cv2.resize()` với các hệ số:
  - `fx`: hệ số phóng đại ngang fx=2 là nhân đôi chiều rộng
  - `fy`: hệ số phóng đại dọc fy=0.5 là giảm một nửa chiều cao
  - `interpolation`: cách tính pixel mới INTER_CUBIC cho chất lượng tốt hơn
- Có thể chỉ định kích thước cụ thể hoặc dùng hệ số phóng đại
- 
**Translation - Dịch chuyển ảnh:**
- Tạo ma trận dịch chuyển với số pixel muốn dịch:
  - `tx`: dịch ngang (dương = sang phải, âm = sang trái)
  - `ty`: dịch dọc (dương = xuống dưới, âm = lên trên)
- Dùng `cv2.warpAffine()` để dịch ảnh
- Tăng kích thước đầu ra để không bị cắt mất phần ảnh

**Rotation - Xoay ảnh:**
- Tạo ma trận quay với tâm quay, góc quay và tỷ lệ
- Thường quay quanh trung tâm ảnh
- Áp dụng ma trận quay để xoay ảnh

#### Phần 2: Mathematical Operations
**Array Operations - Phép toán mảng:**
- OpenCV đọc ảnh thành mảng số, tính toán trực tiếp được
- Cộng số vào ảnh để làm sáng
- Nhân ảnh với số để làm sáng hơn
- Tạo nhiễu và cộng vào ảnh để tạo hiệu ứng nhiễu
**Matrix Operations - Phép toán ma trận:**
- Đọc ảnh xám trực tiếp không cần chuyển đổi
- Dùng SVD để tách và nén ản
### Kết quả
**Kết quả biến đổi hình học:**
- Thay đổi kích thước ảnh với chất lượng tốt nhờ phương pháp nội suy
- Dịch chuyển ảnh thành công theo các hướng khác nhau mà không bị cắt mất phần ảnh
- Xoay ảnh quanh trung tâm một cách tự nhiên
- Tạo được ảnh mẫu nhỏ để minh họa rõ ràng các phép biến đổi
**Kết quả phép toán mảng:**
- Điều chỉnh độ sáng ảnh thành công
- Tạo hiệu ứng nhiễu trên ảnh một cách tự nhiên
- Các phép toán chạy nhanh và hiệu quả
**Kết quả phép toán ma trận:**
- Phân tích SVD thành công trên ảnh xám
- Khôi phục được ảnh gốc từ các thành phần đã phân tích
- Nén ảnh hiệu quả: chỉ cần 100-200 thành phần là đủ để giữ chất lượng tốt


### SVD là cách tách một ma trận thành ba phần nhỏ hơn nó giống như phân tích một bức ảnh thành các mảnh ghép quan trọng nhất.
**Công thức:** Ảnh = U × S × V
- **U**: Chứa các mẫu hình dạng chính của ảnh
- **S**: Chứa các số quan trọng, được sắp xếp từ lớn đến nhỏ
- **V**: Chứa cách các mẫu hình được sắp xếp
### SVD làm gì với ảnh?
**Ý tưởng:**
- Ảnh xám là một ma trận số, mỗi số là độ sáng của một điểm ảnh
- SVD tách ảnh thành các phần quan trọng nhất
- Các số lớn trong S chứa thông tin quan trọng nhất của ảnh
- Các số nhỏ trong S chứa chi tiết nhỏ, có thể bỏ qua
**Các bước trong code:**
1. **Đọc ảnh xám** và chuyển thành ma trận số
2. **Phân tích SVD** để tách thành ba phần U, S, V
3. **Tạo ma trận S** từ vector s bằng cách đặt các số vào đường chéo
4. **Khôi phục ảnh** bằng cách nhân lại ba ma trận - sẽ được ảnh gốc
5. **Nén ảnh** bằng cách chỉ giữ lại một số thành phần đầu tiên (các số lớn nhất), bỏ đi các thành phần nhỏ - ảnh vẫn nhìn được nhưng dung lượng nhỏ hơn
