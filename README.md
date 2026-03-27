<<<<<<< HEAD
# Computer_Vision
=======
# THỊ GIÁC MÁY TÍNH – LAB 08: NHẬN DIỆN ĐỐI TƯỢNG TRONG VIDEO

- **Sinh viên thực hiện**: Phạm Thế Hùng  
- **MSSV**: 2374802010164  
- **Môn học**: Thị Giác Máy Tính  
- **Giảng viên**: TS. Đỗ Hữu Quân  


## LAB 08: NHẬN DIỆN ĐỐI TƯỢNG TRONG VIDEO

### Công nghệ sử dụng

- **PyTorch & Torchvision**: Nền tảng Deep Learning cốt lõi, sử dụng để triển khai và chạy mô hình `RetinaNet` (với backbone `ResNet50` kết hợp `FPN` - Feature Pyramid Network) đã được huấn luyện sẵn (pre-trained) qua tệp trọng số `retinanet_resnet50_fpn_coco-eeacb38b.pth`.  
- **OpenCV (cv2)**: Thư viện xử lý thị giác máy tính, dùng để đọc xuất video (`VideoCapture`, `VideoWriter`), xử lý từng khung hình ảnh và vẽ hộp giới hạn lên đối tượng.  
- **NumPy**: Thư viện dùng để tính toán và xử lý mảng dữ liệu ảnh nhiều chiều khi chuyển giao giữa OpenCV và PyTorch Tensor.  

### Cách hoạt động

#### Pipeline nhận diện đối tượng trong video

1. **Khởi tạo và Load Mô hình**  
   - Tải kiến trúc mô hình RetinaNet dựa trên `ResNet50_FPN` trong thư viện `torchvision.models.detection`.
   - Nạp file trọng số `retinanet_resnet50_fpn_coco-eeacb38b.pth` (có khả năng nhận diện 91 lớp đối tượng quen thuộc trong bộ dữ liệu COCO như người, xe máy, ô tô...).
   - Đặt mô hình ở chế độ suy luận inference (`model.eval()`) và chuyển tính toán sang GPU (nếu có) để xử lý nhanh hơn

2. **Đọc và xử lý Video**  
   - Dùng OpenCV mở file video đầu vào là `video_predetect.mp4`
   - Khởi tạo bộ ghi luồng video sử dụng định dạng codec tương thích để xuất kết quả ra tệp `video_detected.mp4`
   - Tại vòng lặp duyệt từng frame ảnh trong video: 
     - Đọc frame, chuyển màu sắc từ hệ `BGR` (OpenCV) sang hệ `RGB`
     - Chuyển ma trận ảnh thành dạng Tensor tính toán của PyTorch và đưa giá trị pixel về dải màu chuần `[0.0, 1.0]`

3. **Dự đoán và Vẽ kết quả**  
   - Đưa Tensor của từng frame vào mô hình để dự đoán và nhận về các thông số: tọa độ viền ranh giới (`boxes`), nhãn phân loại (`labels`) và điểm độ tin cậy (`scores`)
   - Loại bỏ các vật thể có độ tin cậy thấp (thiết lập một ngưỡng `confidence threshold`, ví dụ > 0.5) để hạn chế nhận diện nhầm lỗi
   - Đối với các đối tượng nhận diện được:
     - Giải mã nhãn lớp từ giá trị số sang tên văn bản thực
     - Sử dụng `cv2.rectangle()` để vẽ bounding boxes quanh vật thể trên khung hình gốc
     - Sử dụng `cv2.putText()` để in hiển thị số liệu tỷ lệ tự tin và nhãn tên lên khung ảnh
   - Ghi frame ảnh đã vẽ đè lên vào Video mới

### Kết quả

- **Phát hiện đối tượng mạnh mẽ**: Mô hình RetinaNet hoạt động hiệu quả để theo vết, bắt dính các vật thể chuyển động có trong video `video_predetect.mp4`.
- **Đầu ra Video**: Video kết quả `video_detected.mp4` được sinh ra thể hiện các khung màu hiển thị chính xác vị trí nhận dạng và tên của các đối tượng liên tục trên từng khung hình một cách mượt mà và trực quan.
#### Video chưa được nhận diện
<video src="video_predetect.mp4" controls width="400"></video>
[![Watch]](video_predetect.mp4)

#### Video đã được nhận diện
<video src="2374802010164_PhamTheHung_0101_Lab08.mp4" controls width="400"></video>
>>>>>>> db0bce1 (upload with LFS)
