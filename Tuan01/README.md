# THỊ GIÁC MÁY TÍNH (COMPUTER VISION)

- **Sinh Viên Thực Hiên:** Phạm Thế Hùng
- **MSSV:** 2374802010164
- **Môn Học:** Thị Giác Máy Tính
- **Giảng viên:** TS.Đỗ Hữu Quân

## File 1: 2.1.1_Images_with_python_library_PIL.ipynb

### Công nghệ sử dụng

- **Pillow (PIL)**: Thư viện xử lý ảnh chính
- **NumPy**: Xử lý mảng đa chiều và chuyển đổi ảnh thành mảng
- **Matplotlib**: Hiển thị và vẽ biểu đồ ảnh
- **OS**: Làm việc với hệ thống file và đường dẫn

### Cách hoạt động

#### 1. Tải và quản lý ảnh
- Sử dụng `Image.open()` từ PIL để tải ảnh từ file
- Làm việc với đường dẫn file sử dụng module `os`
- Hỗ trợ các định dạng ảnh phổ biến: PNG, JPG, JPEG

#### 2. Thông tin ảnh
- `image.size`: Trả về kích thước ảnh (chiều rộng, chiều cao) tính bằng pixel
- `image.mode`: Trả về chế độ màu (RGB, L cho grayscale)

#### 3. Hiển thị ảnh
- Hiển thị trực tiếp trong Jupyter notebook
- Sử dụng `plt.imshow()` để vẽ ảnh với kích thước tùy chỉnh
- Sử dụng `plt.show()` để mở ảnh trong cửa sổ mới

#### 4. Ảnh Grayscale và Quantization
- Chuyển đổi ảnh sang grayscale bằng `ImageOps.grayscale(image)`
- Thực hiện quantization (giảm số lượng mức độ màu) bằng `quantize()`
- So sánh ảnh với các mức quantization khác nhau (256, 128, 64, 32, 16, 8 levels)

#### 5. Kênh màu RGB
- Tách các kênh màu Red, Green, Blue bằng `image.split()`
- Hiển thị từng kênh màu riêng biệt dưới dạng grayscale
- So sánh ảnh gốc với từng kênh màu

#### 6. Chuyển đổi sang NumPy Array
- Sử dụng `np.asarray()` hoặc `np.array()` để chuyển PIL Image thành NumPy array
- Array có shape `(height, width, channels)` - ví dụ: (512, 512, 3) cho ảnh RGB
- Giá trị intensity từ 0 đến 255 (8-bit unsigned integer)

#### 7. Thao tác với Array
- Slicing để cắt ảnh (ví dụ: lấy nửa trên, nửa trái)
- Làm việc với các kênh màu riêng lẻ bằng indexing
- Sử dụng `copy()` để tạo bản sao độc lập, tránh thay đổi ảnh gốc
- Thao tác với kênh màu: đặt các kênh khác về 0 để chỉ hiển thị một kênh

### Kết quả

- **Tải và hiển thị ảnh**: Thành công tải các ảnh mẫu (lenna.png, baboon.png, barbara.png)
- **Chuyển đổi grayscale**: Tạo được ảnh grayscale với mode 'L'
- **Quantization**: Quan sát được sự khác biệt khi giảm số lượng mức màu
- **Tách kênh màu**: Hiển thị được từng kênh RGB riêng biệt
- **NumPy array**: Chuyển đổi thành công PIL Image sang NumPy array với shape (512, 512, 3)
- **Thao tác ảnh**: Thực hiện được các thao tác cắt, chỉnh sửa kênh màu

---

## File 2: 2.1.2_Images_with_python_library_CV.ipynb

### Công nghệ sử dụng

- **OpenCV (cv2)**: Thư viện xử lý ảnh và computer vision
- **NumPy**: Xử lý mảng đa chiều (OpenCV trả về NumPy array trực tiếp)
- **Matplotlib**: Hiển thị và vẽ biểu đồ ảnh
- **OS**: Làm việc với hệ thống file và đường dẫn

### Cách hoạt động

#### 1. Tải ảnh với OpenCV
- Sử dụng `cv2.imread()` để tải ảnh từ file
- Kết quả trả về là NumPy array ngay lập tức (không cần chuyển đổi)
- Hỗ trợ flag `cv2.IMREAD_COLOR` (mặc định) và `cv2.IMREAD_GRAYSCALE`

#### 2. Định dạng màu BGR vs RGB
- **Quan trọng**: OpenCV sử dụng định dạng **BGR** (Blue-Green-Red) thay vì RGB
- Cần chuyển đổi sang RGB khi hiển thị bằng matplotlib: `cv2.cvtColor(image, cv2.COLOR_BGR2RGB)`
- Nếu không chuyển đổi, ảnh sẽ hiển thị sai màu

#### 3. Thông tin ảnh
- `image.shape`: Trả về (height, width, channels) - ví dụ: (512, 512, 3)
- `image.max()` và `image.min()`: Giá trị intensity tối đa và tối thiểu (0-255)
- Array có kiểu dữ liệu 8-bit unsigned integer

#### 4. Hiển thị ảnh
- Sử dụng `plt.imshow()` sau khi chuyển đổi BGR sang RGB

#### 5. Ảnh Grayscale
- Chuyển đổi sang grayscale: `cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)`
- Hiển thị với `cmap='gray'` trong matplotlib

#### 6. Kênh màu BGR
- Tách các kênh màu: `blue, green, red = baboon[:, :, 0], baboon[:, :, 1], baboon[:, :, 2]`
- Lưu ý: Thứ tự là BGR (Blue=0, Green=1, Red=2)
- Ghép các kênh theo chiều dọc: `cv2.vconcat([blue, green, red])`
- Thao tác với kênh màu: đặt các kênh khác về 0 để chỉ hiển thị một kênh

#### 7. Thao tác với Array
- Slicing để cắt ảnh (lấy nửa trên, nửa trái)
- Sử dụng `copy()` để tạo bản sao độc lập
- Indexing để chỉnh sửa các kênh màu cụ thể

### Kết quả

- **Tải ảnh**: Thành công tải ảnh và nhận được NumPy array trực tiếp
- **Chuyển đổi BGR sang RGB**: Hiển thị đúng màu sắc sau khi chuyển đổi
- **Grayscale**: Tạo được ảnh grayscale với shape 2 chiều
- **Tách kênh màu**: Hiển thị được các kênh BGR riêng biệt
- **Thao tác ảnh**: Thực hiện được các thao tác cắt, chỉnh sửa kênh màu
- **Lưu ảnh**: Sử dụng `cv2.imwrite()` để lưu ảnh ở các định dạng khác nhau


### Thư viện Python cần thiết:
```python
- Pillow (PIL)
- OpenCV (cv2)
- NumPy
- Matplotlib
```

### Cài đặt:
```bash
pip install pillow opencv-python numpy matplotlib
```