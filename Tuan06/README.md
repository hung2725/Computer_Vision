# THỊ GIÁC MÁY TÍNH (COMPUTER VISION)

- **Sinh Viên Thực Hiện:** Phạm Thế Hùng
- **MSSV:** 2374802010164
- **Môn Học:** Thị Giác Máy Tính
- **Giảng viên:** TS.Đỗ Hữu Quân

## File 1: 2.5.1_Spatial_Filtering-PIL.ipynb

### Công nghệ sử dụng

- **PIL (Pillow)**
- **Matplotlib**
- **NumPy**

### Cách hoạt động

**Spatial Filtering - Lọc không gian:**
- Sử dụng một ma trận nhỏ (gọi là kernel hoặc mask) trượt qua từng điểm ảnh (pixel) trên ảnh gốc để tính toán giá trị mới cho điểm ảnh đó.
- **Custom Kernels (Bộ lọc tự định nghĩa):** Tự tạo ma trận trọng số (ví dụ kernel 3x3) để thực hiện các phép biến đổi tùy ý như làm mờ, sắc nét.
- **Predefined Filters (Bộ lọc có sẵn trong PIL):**
  - **Làm mờ (Blur / GaussianBlur):** Lấy trung bình cộng các pixel xung quanh để làm ảnh mịn hơn, giảm nhiễu.
  - **Lọc trung vị (Median Filter):** Thay pixel bằng giá trị trung vị của các pixel xung quanh, rất hiệu quả để xóa nhiễu hạt dưa (salt and pepper noise).
  - **Tìm biên (Edge Detection):** Dùng bộ lọc như Sobel hoặc FIND_EDGES để tìm sự thay đổi độ sáng đột ngột, làm nổi đường viền.

### Kết quả

- Làm mờ ảnh thành công ở các mức độ khác nhau.
- Xóa sạch được nhiễu muối tiêu (chấm trắng/đen) giữ nguyên độ nét của cạnh nhờ lọc trung vị.
- Tách được các đường nét, viền vật thể ra khỏi nền nhờ các bộ lọc phát hiện cạnh.


## File 2: 2.5.2_Spatial_Filtering.ipynb

### Công nghệ sử dụng

- **OpenCV (cv2)**
- **Matplotlib**
- **NumPy**

### Cách hoạt động

**Lọc không gian với OpenCV:**
- **Lọc tùy biến (`cv2.filter2D`):** Cho phép áp dụng bất kỳ ma trận kernel (chẳng hạn 3x3, 5x5) tự tạo nào lên ảnh để làm mờ hoặc sắc nét.
- **Làm mờ trung bình (Averaging - `cv2.blur`):** Dùng một kernel hình vuông có các giá trị bằng nhau, giúp làm mờ đều ảnh.
- **Làm mờ Gaussian (`cv2.GaussianBlur`):** Trọng số ở giữa kernel cao hơn và giảm dần ra ngoài, giúp ảnh mờ mịn và tự nhiên hơn so với lọc trung bình.
- **Lọc trung vị (`cv2.medianBlur`):** Lấy giá trị trung vị trong vùng lân cận, thay vì lấy trung bình cộng.

### Kết quả

- Áp dụng các bộ lọc làm mờ cực kỳ tối ưu và tốc độ chạy nhanh nhờ OpenCV.
- Phân biệt được sự khác biệt giữa làm mờ bằng trung bình cộng (ảnh hơi vuông vức) và Gaussian (ảnh mờ mịn, tự nhiên).
- Loại bỏ xuất sắc nhiễu muối tiêu bằng lọc trung vị mà không làm nhòe các cạnh của ảnh bằng OpenCV.


## File 3: 2374802010164_PhamTheHung_CV0101_Lab03.ipynb

### Công nghệ sử dụng

- **OpenCV (cv2) & NumPy**
- **Matplotlib (nhập với tên `hung`)**
- **SciPy (`scipy.fft`)**
- **Scikit-Image (`skimage.filters`, `skimage.data`)**

### Cách hoạt động

**Lọc trong không gian gốc (Spatial Domain):**
- Tiếp tục thực hành các kỹ thuật lọc ảnh cơ bản (làm mờ, cường điệu cạnh) trên ảnh đầu vào, so sánh kết quả.

**Lọc trong miền tần số (Frequency Domain):**
- Thay vì trượt ma trận, biến đổi toàn bộ ảnh sang miền tần số bằng Fast Fourier Transform (`fftn`, `fftshift`).
- Sử dụng các bộ lọc dạng cửa sổ (như cửa sổ `hann`) che đi hoặc giữ lại các tần số nhất định (tần số thấp giúp làm mờ, tần số cao chứa thông tin cạnh).
- Biến đổi ngược lại ảnh về hệ không gian ban đầu để thấy kết quả.

**Difference of Gaussians (DoG):**
- Dùng hàm `difference_of_gaussians` làm mờ ảnh hai lần bằng Gaussian với 2 mức độ (sigma) khác nhau.
- Trừ 2 kết quả này cho nhau. Kết quả còn lại chính là các đường viền và chi tiết nổi bật của ảnh.

### Kết quả

- Trực tiếp biến đổi Fourier trên ảnh, minh họa rõ ràng các thành phần tần số của ảnh.
- Áp dụng thành công tính lọc trong không gian tần số và chuyển ngược về ảnh gốc.
- Sử dụng được kỹ thuật tinh vi như DoG để trích xuất đặc trưng cạnh một cách rõ nét và ít nhiễu.
