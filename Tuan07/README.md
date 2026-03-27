## THỊ GIÁC MÁY TÍNH – LAB 04: KEYPOINT DETECTION

- **Sinh viên thực hiện**: Phạm Thế Hùng  
- **MSSV**: 2374802010164  
- **Môn học**: Thị Giác Máy Tính  
- **Giảng viên**: TS. Đỗ Hữu Quân  
## Công nghệ sử dụng

- **NumPy**: Xử lý mảng số (ma trận), biểu diễn ảnh dưới dạng dữ liệu số.  
- **OpenCV (`cv2`)**: Thư viện xử lý ảnh và thị giác máy tính, hỗ trợ đọc/ghi ảnh, phát hiện đặc trưng, ghép ảnh,…  
- **Matplotlib** (`pyplot`/`hung`): Hiển thị và vẽ ảnh, biểu đồ trong Jupyter Notebook.  
- **`skimage.feature.blob_log`**: Phát hiện các blob (vùng tròn) trong ảnh ở nhiều scale khác nhau.  
- **`sklearn.cluster.KMeans`**: Gom cụm các vector đặc trưng để tạo “visual words” trong mô hình Bag-of-Words.  


### 1. Khai báo thư viện ảnh

- **Công nghệ**: `numpy`, `cv2`, `blob_log`, `matplotlib.pyplot`, `KMeans`.  
- **Cách hoạt động**: Import đầy đủ các thư viện để sẵn sàng dùng cho các bước xử lý ảnh, phát hiện đặc trưng, ghép ảnh, Bag-of-Words.  
- **Kết quả**: Môi trường Python đã sẵn sàng với đủ thư viện cần thiết.  

###  Kiểm tra OpenCV đọc ảnh và hiển thị đúng màu

- **Công nghệ**: `cv2.imread`, `matplotlib`.  
- **Cách hoạt động**:
  - Dùng `cv2.imread('image.png')` để đọc ảnh (mặc định BGR).  
  - Dùng `img[:, :, ::-1]` để chuyển BGR → RGB trước khi `hung.imshow(...)`.  
- **Kết quả**: Ảnh được đọc thành công và hiển thị đúng màu trong matplotlib.  

### 3. Harris Corner Detection – tìm keypoint dạng góc

- **Công nghệ**: `cv2.cornerHarris`, `cv2.cvtColor`, `cv2.dilate`, `matplotlib`.  
- **Cách hoạt động**:
  - Chuyển ảnh sang grayscale, đổi sang `float32`.  
  - Dùng `cv.cornerHarris` để tính phản hồi tại các góc.  
  - Dùng `cv.dilate` để làm nổi vùng góc và tô màu đỏ những điểm có phản hồi lớn.  
- **Kết quả**: Các góc trong ảnh được đánh dấu đỏ, cho thấy Harris corner detector tìm được nhiều keypoint.  

### 4. Band-pass filtering bằng Difference of Gaussians (DoG)

- **Công nghệ**: `cv2.GaussianBlur`, phép trừ hai ảnh, `matplotlib`.  
- **Cách hoạt động**:
  - Tạo hai ảnh Gaussian blur với sigma khác nhau.  
  - Lấy hiệu `DoG = blur1 - blur2` để giữ lại vùng biến thiên nhanh (biên/chi tiết).  
- **Kết quả**: Ảnh DoG làm nổi bật biên và chi tiết, nền phẳng bị giảm bớt.  

### 5. Automatic Scale Selection (Gaussian với nhiều sigma)

- **Công nghệ**: `cv2.GaussianBlur`, vòng lặp Python, `matplotlib`.  
- **Cách hoạt động**:
  - Lặp với nhiều giá trị sigma khác nhau, blur ảnh và hiển thị.  
  - So sánh mức độ mờ/giữ chi tiết theo từng sigma.  
- **Kết quả**: Thấy được ảnh hưởng của scale: sigma nhỏ giữ nhiều chi tiết, sigma lớn làm ảnh mờ đi.  

### 6. Scale-Invariant Detection với SIFT

- **Công nghệ**: `cv2.SIFT_create`, `detectAndCompute`, `cv2.drawKeypoints`.  
- **Cách hoạt động**:
  - Chuyển ảnh sang grayscale.  
  - Dùng SIFT để tìm keypoint và descriptor.  
  - Vẽ keypoint lên ảnh bằng `cv2.drawKeypoints` và hiển thị.  
- **Kết quả**: Ảnh hiển thị nhiều keypoint SIFT ổn định theo tỉ lệ (scale-invariant).  

### 7. Scale-space Blob Detector (blob_log)

- **Công nghệ**: `blob_log` (scikit-image), `cv2.circle`, `matplotlib`.  
- **Cách hoạt động**:
  - Dùng `blob_log` để phát hiện blob (vùng tròn) ở nhiều scale.  
  - Vẽ vòng tròn tại vị trí blob trên bản sao ảnh gốc.  
- **Kết quả**: Các blob trong ảnh được khoanh tròn, minh họa phát hiện vùng tròn ở nhiều kích thước.  

### 8. Ghép ảnh Image Panoramas

- **Công nghệ**: `cv2.Stitcher_create`, `stitcher.stitch`, `matplotlib`.  
- **Cách hoạt động**:
  - Đọc 2 ảnh chồng lấn vùng nhìn.  
  - Dùng `cv2.Stitcher` để tự động ghép thành panorama.  
- **Kết quả**: Tạo được ảnh panorama rộng hơn từ 2 ảnh đầu vào.  

### 9. Ghép ảnh Automatic Mosaicing

- **Công nghệ**: `cv2.Stitcher_create`, `stitcher.stitch`, `matplotlib`.  
- **Cách hoạt động**:
  - Đọc 3 ảnh của cùng cảnh.  
  - Dùng `stitcher.stitch(images)` để ghép thành một ảnh mosaic.  
- **Kết quả**: Có được ảnh ghép tự động từ 3 ảnh, cho cái nhìn tổng quát hơn về cảnh.  

### 10. Wide Base-line Stereo (so khớp đặc trưng giữa 2 ảnh)

- **Công nghệ**: SIFT, `cv2.BFMatcher`, `knnMatch`, `cv2.drawMatches`.  
- **Cách hoạt động**:
  - Tính SIFT keypoint + descriptor cho 2 ảnh.  
  - Dùng BFMatcher + Lowe’s ratio test để lọc các match tốt.  
  - Vẽ các đường nối giữa điểm tương ứng trên 2 ảnh.  
- **Kết quả**: Thấy rõ các cặp điểm tương ứng giữa hai ảnh khác góc nhìn (wide baseline).  

### 11. CBIR – Content-Based Image Retrieval bằng histogram màu

- **Công nghệ**: `cv2.calcHist`, `cv2.normalize`, `cv2.compareHist`, `matplotlib`.  
- **Cách hoạt động**:
  - Tính histogram màu 3D cho ảnh truy vấn và các ảnh trong tập.  
  - So sánh bằng `compareHist` (CORREL) để đo độ giống.  
  - Hiển thị ảnh truy vấn và ảnh so sánh kèm điểm số.  
- **Kết quả**: Xác định được ảnh nào giống ảnh truy vấn hơn về màu sắc, minh họa nguyên lý CBIR.  

### 12. Bag-of-Words với SIFT + Histogram

- **Công nghệ**: SIFT, `KMeans`, `numpy.bincount`, `matplotlib`.  
- **Cách hoạt động**:
  - Dùng SIFT để lấy toàn bộ descriptor của ảnh.  
  - Dùng KMeans để gom cụm descriptor thành `k` visual words.  
  - Đếm số lần xuất hiện mỗi visual word để tạo histogram Bag-of-Words.  
  - Hiển thị ảnh keypoint SIFT và biểu đồ histogram.  
- **Kết quả**: Ảnh được biểu diễn dưới dạng vector Bag-of-Words, có thể dùng cho phân loại và tìm kiếm ảnh theo nội dung.  

