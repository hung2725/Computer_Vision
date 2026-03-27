# THỊ GIÁC MÁY TÍNH – LAB 05 & LAB 06: PHÂN ĐOẠN ẢNH & NHẬN DIỆN KHUÔN MẶT

- **Sinh viên thực hiện**: Phạm Thế Hùng  
- **MSSV**: 2374802010164  
- **Môn học**: Thị Giác Máy Tính  
- **Giảng viên**: TS. Đỗ Hữu Quân  


## LAB 05: PHÂN ĐOẠN ẢNH

### Công nghệ sử dụng

- **NumPy**: Xử lý mảng số (ma trận), biểu diễn ảnh dưới dạng dữ liệu số.  
- **OpenCv**: Thư viện xử lý ảnh và thị giác máy tính, hỗ trợ đọc/ghi ảnh, phân đoạn ảnh, xử lý hình thái học
- **Matplotlib**: Hiển thị và vẽ ảnh, biểu đồ trong Jupyter Notebook.  

### Cách hoạt động

#### 1. Thresholding để phân đoạn ảnh

Phân đoạn ảnh bằng cách phân chia các pixel thành các vùng dựa trên giá trị cường độ

**Thuật toán Otsu (Otsu's Thresholding)**:
- Đọc ảnh dưới dạng ảnh xám (grayscale).
- Áp dụng thuật toán Otsu để tự động tìm ngưỡng tối ưu phân chia foreground và background.
- Sử dụng hàm `cv2.threshold()` với tham số `cv2.THRESH_BINARY + cv2.THRESH_OTSU`.

```python
ret_otsu, thresh_otsu = cv2.threshold(fingerprint_img, 0, 255, cv2.THRESH_BINARY + cv2.THRESH_OTSU)
print(f"Ngưỡng Otsu tự động tìm được là: {ret_otsu}")
```

#### 2. Region Growing (Phát triển vùng)

Phân đoạn ảnh dựa trên sự phát triển từ một điểm mầm (seed point).

**FloodFill (Mô phỏng Region Growing)**:
- Xác định điểm bắt đầu lan truyền (`seed_point`).
- Thiết lập dung sai trên/dưới (`lo_diff`, `up_diff`) để xác định điều kiện lan truyền.
- Sử dụng hàm `cv2.floodFill()` để thực hiện lan truyền vùng.

```python
seed_point = (50, 50)   # Tọa độ điểm bắt đầu lan truyền
new_value  = 255        # Màu của vùng mới (Trắng)
lo_diff    = 10         # Dung sai dưới
up_diff    = 10         # Dung sai trên

img_floodfill = img_rg.copy()
cv2.floodFill(img_floodfill, mask, seed_point, new_value, lo_diff, up_diff)
```

#### 3. Connected Components (Thành phần liên thông)

Phân tích cấu trúc các vùng liên kết trong ảnh nhị phân.
- Sử dụng `cv2.connectedComponentsWithStats()` để gán nhãn và thống kê các thành phần liên thông.
- Mỗi thành phần liên thông được tô màu khác nhau để dễ phân biệt.

### Kết quả

- **Otsu Thresholding**: Tự động xác định ngưỡng phân chia ảnh vân tay thành foreground/background.
- **Region Growing (FloodFill)**: Lan truyền màu từ điểm seed, tô vùng liền kề có cường độ tương tự.
- **Connected Components**: Gán màu riêng biệt cho từng thành phần liên thông trong ảnh nhị phân.


## LAB 06: NHẬN DIỆN KHUÔN MẶT

### Công nghệ sử dụng

- **OpenCV**: Thư viện xử lý ảnh và thị giác máy tính, cung cấp các bộ phân lớp Haar Cascade cho nhận diện đối tượng.  
- **Matplotlib**: Hiển thị ảnh kết quả trong Jupyter Notebook.  
- **Haar Cascade Classifiers**:  
  - `haarcascade_frontalface_default.xml` – Nhận diện khuôn mặt chính diện  
  - `haarcascade_eye.xml` – Nhận diện mắt  
  - `haarcascade_smile.xml` – Nhận diện nụ cười  

### Cách hoạt động

#### Pipeline nhận diện

1. **Đọc và chuẩn bị ảnh**  
   - Đọc ảnh đầu vào bằng `cv2.imread()`.  
   - Chuyển đổi sang ảnh xám (`cv2.COLOR_BGR2GRAY`) để phát hiện, đồng thời giữ bản RGB (`cv2.COLOR_BGR2RGB`) để hiển thị.

2. **Tải bộ phân lớp Haar Cascade**  
   ```python
   face_cascade  = cv2.CascadeClassifier('haarcascade_frontalface_default.xml')
   eye_cascade   = cv2.CascadeClassifier('haarcascade_eye.xml')
   smile_cascade = cv2.CascadeClassifier('haarcascade_smile.xml')
   ```

3. **Nhận diện khuôn mặt**  
   ```python
   faces = face_cascade.detectMultiScale(img_gray, scaleFactor=1.1, minNeighbors=5, minSize=(30, 30))
   ```

4. **Nhận diện mắt và nụ cười trong từng ROI khuôn mặt**  
   Với mỗi khuôn mặt phát hiện được:  
   - Trích xuất ROI (Region of Interest).  
   - Phát hiện mắt bên trong ROI với `minNeighbors=10`.  
   - Phát hiện nụ cười bên trong ROI với `scaleFactor=1.7, minNeighbors=20` (tham số cao hơn để giảm false positive).

5. **Vẽ kết quả lên ảnh**  
   - **Khuôn mặt**: khung chữ nhật màu **xanh lá** (0, 255, 0).  
   - **Mắt**: khung chữ nhật màu **xanh dương** (0, 0, 255).  
   - **Nụ cười**: khung chữ nhật màu **đỏ** (255, 0, 0).

#### Tham số tinh chỉnh

- **`scaleFactor`**: Tỷ lệ thu nhỏ ảnh qua mỗi tầng; giá trị nhỏ hơn → chính xác hơn nhưng chậm hơn.
- **`minNeighbors`**: Số lần phát hiện tối thiểu để xác nhận khuôn mặt; giá trị cao hơn → ít false positive.
- **`minSize`**: Kích thước tối thiểu của đối tượng cần phát hiện.

### Kết quả

- **Khuôn mặt** – khung màu xanh lá (0, 255, 0): phát hiện trên toàn bộ ảnh xám.
- **Mắt** – khung màu xanh dương (0, 0, 255): chỉ tìm bên trong ROI khuôn mặt.
- **Nụ cười** – khung màu đỏ (255, 0, 0): chỉ tìm bên trong ROI khuôn mặt; cần tham số cao hơn để tránh nhận diện nhầm.

Kết quả hiển thị ảnh đầu vào với các khung bao quanh từng đối tượng được phát hiện, kèm tiêu đề Face, Eye, and Smile Detection.
