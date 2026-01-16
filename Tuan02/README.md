# THỊ GIÁC MÁY TÍNH (COMPUTER VISION)

- **Sinh Viên Thực Hiện:** Phạm Thế Hùng
- **MSSV:** 2374802010164
- **Môn Học:** Thị Giác Máy Tính
- **Giảng viên:** TS.Đỗ Hữu Quân


## File 1: 2.2.1_basic_image_manipulation_PIL.ipynb

### Công nghệ sử dụng

- **Pillow (PIL)**: Thư viện xử lý ảnh chính với các module:
  - `Image`: Đọc, hiển thị và thao tác ảnh cơ bản
  - `ImageOps`: Các phép biến đổi ảnh (lật, xoay)
  - `ImageDraw`: Viết text lên ảnh
  - `ImageFont`: Quản lý font chữ cho text
- **NumPy**: Xử lý mảng đa chiều và chuyển đổi ảnh thành mảng
- **Matplotlib**: Hiển thị và vẽ biểu đồ ảnh

### Cách hoạt động

#### Copying Images
- Sử dụng `copy()` để tạo bản sao độc lập của ảnh
- Sử dụng `id()` để kiểm tra địa chỉ nhớ
- Nếu không dùng `copy()`, thay đổi ảnh gốc sẽ ảnh hưởng đến biến được gán
- Ví dụ: `B = baboon.copy()` tạo bản sao độc lập với địa chỉ nhớ khác

#### Flipping Images
- **Cách thủ công**: Sử dụng vòng lặp để đảo ngược thứ tự các hàng pixel
  - Tạo mảng rỗng cùng kích thước: `array_flip = np.zeros((width, height, C), dtype=np.uint8)`
  - Đảo ngược hàng: `array_flip[width - 1 - i, :, :] = row`
- **Sử dụng PIL**:
  - `ImageOps.flip(image)`: Lật ảnh theo chiều dọc 
  - `ImageOps.mirror(image)`: Lật ảnh theo chiều ngang
  - `Image.FLIP_LEFT_RIGHT`: Lật ngang
  - `Image.FLIP_TOP_BOTTOM`: Lật dọc
  - `Image.ROTATE_90`: Xoay 90 độ
  - `Image.ROTATE_180`: Xoay 180 độ
  - `Image.ROTATE_270`: Xoay 270 độ

#### Cropping an Image
- **Sử dụng mảng numpy**:
  - Cắt theo chiều dọc: `crop_top = array[upper:lower, :, :]`
  - Cắt theo chiều ngang: `crop_horizontal = crop_top[:, left:right, :]`
  - Cắt cả hai chiều: `crop_region = array[upper:lower, left:right, :]`
- **Sử dụng PIL method**:
  - `image.crop((left, upper, right, lower))`: Cắt ảnh theo tọa độ box
  - Tham số theo thứ tự: left (trái), upper (trên), right (phải), lower (dưới)
- Có thể kết hợp với transpose để lật ảnh đã cắt

#### Changing Specific Image Pixels
- Sử dụng array indexing để truy cập và thay đổi giá trị pixel
- Ví dụ: `array_sq[upper:lower, left:right, 1:3] = 0` - đặt kênh màu xanh lá và xanh dương về 0 tạo vùng màu đỏ
- Có thể chỉnh sửa từng kênh màu riêng lẻ (R, G, B)

#### Drawing Shapes and Text
- **Sử dụng ImageDraw module**:
  - Tạo đối tượng vẽ: `image_fn = ImageDraw.Draw(im=image_draw)`
  - Vẽ hình chữ nhật: `image_fn.rectangle(xy=[left, upper, right, lower], fill="red")`
  - Vẽ text: `image_fn.text(xy=(0, 0), text="box", fill=(0, 0, 0))`
  - Sử dụng `ImageFont` để quản lý font chữ
- Thay đổi trên đối tượng `image_fn` sẽ tự động cập nhật `image_draw`
- **Sử dụng NumPy array**: Gán pixel từ ảnh này vào vị trí cụ thể của ảnh khác
  - `array_lenna[upper:lower, left:right, :] = array[upper:lower, left:right, :]`
- **Sử dụng PIL method**:
  - `image_lenna.paste(crop_image, box=(left, upper))`: Dán ảnh đã cắt vào vị trí chỉ định
- Cho phép tạo hiệu ứng composite bằng cách kết hợp nhiều ảnh



## File 2: 2.2.2_basic_image_manipulation_open_CV.ipynb

### Công nghệ sử dụng

- **OpenCV (cv2)**: Thư viện xử lý ảnh và computer vision
- **NumPy**: Xử lý mảng đa chiều (OpenCV trả về NumPy array trực tiếp)
- **Matplotlib**: Hiển thị và vẽ biểu đồ ảnh

### Cách hoạt động

#### Tải ảnh với OpenCV
- Sử dụng `cv2.imread()` để tải ảnh từ file
- Kết quả trả về là NumPy array ngay lập tức (không cần chuyển đổi từ PIL Image)
- Hỗ trợ các flag: `cv2.IMREAD_COLOR`, `cv2.IMREAD_GRAYSCALE`

#### Định dạng màu BGR vs RGB
- **Quan trọng**: OpenCV sử dụng định dạng **BGR** (Blue-Green-Red) thay vì RGB
- Cần chuyển đổi sang RGB khi hiển thị bằng matplotlib: `cv2.cvtColor(image, cv2.COLOR_BGR2RGB)`
- Nếu không chuyển đổi, ảnh sẽ hiển thị sai màu (kênh đỏ và xanh dương bị đảo)

#### Copying Images
- Sử dụng `copy()` tương tự NumPy array
- Sử dụng `id()` để kiểm tra địa chỉ nhớ
- `B = baboon.copy()` tạo bản sao độc lập với địa chỉ nhớ khác
- Thay đổi ảnh gốc không ảnh hưởng đến bản sao nếu đã dùng `copy()`

#### Flipping Images
- **Cách thủ công**: Sử dụng vòng lặp để đảo ngược thứ tự các hàng pixel
  - Tạo mảng rỗng: `array_flip = np.zeros((width, height, C), dtype=np.uint8)`
  - Đảo ngược hàng: `array_flip[width - 1 - i, :, :] = row`
- **Sử dụng OpenCV**:
  - `cv2.flip(image, 0)`: Lật dọc (xung quanh trục x - flipcode = 0)
  - `cv2.flip(image, 1)`: Lật ngang (xung quanh trục y - flipcode > 0)
  - `cv2.flip(image, -1)`: Lật cả hai chiều (flipcode < 0)

- Sử dụng `cv2.rotate()` function với các tham số:
  - `cv2.ROTATE_90_CLOCKWISE`: Xoay 90 độ theo chiều kim đồng hồ
  - `cv2.ROTATE_90_COUNTERCLOCKWISE`: Xoay 90 độ ngược chiều kim đồng hồ
  - `cv2.ROTATE_180`: Xoay 180 độ
- Tham số là integer constant, không phải góc độ

#### Cropping an Image
- Sử dụng NumPy array slicing (tương tự PIL):
  - Cắt theo chiều dọc: `crop_top = image[upper:lower, :, :]`
  - Cắt theo chiều ngang: `crop_horizontal = crop_top[:, left:right, :]`
  - Cắt cả hai chiều: `crop_region = image[upper:lower, left:right, :]`
- OpenCV không có method `crop()` riêng, phải dùng array slicing

#### Changing Specific Image Pixels
- Sử dụng array indexing để truy cập và thay đổi giá trị pixel
- Ví dụ: `array_sq[upper:lower, left:right, :] = 0` - đặt vùng cắt thành màu đen
- Có thể chỉnh sửa từng kênh màu BGR riêng lẻ
- **Vẽ hình chữ nhật**:
  - `cv2.rectangle(image, pt1=(left, upper), pt2=(right, lower), color=(0, 255, 0), thickness=3)`
  - `pt1`: Tọa độ góc trên-trái (x₀, y₀)
  - `pt2`: Tọa độ góc dưới-phải (x₁, y₁)
  - `color`: Tuple màu theo định dạng BGR `(blue, green, red)` - **Lưu ý**: `(0, 255, 0)` là màu xanh lá, không phải đỏ!
  - `thickness`: Độ dày đường viền (pixel)

- Sử dụng `cv2.putText()` với các tham số:
  - `img`: Image array
  - `text`: Chuỗi text cần vẽ
  - `org`: Tọa độ góc dưới-trái của text `(x, y)`
  - `fontFace`: Kiểu font
  - `fontScale`: Tỷ lệ font (float)
  - `color`: Màu text theo BGR `(blue, green, red)`

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

