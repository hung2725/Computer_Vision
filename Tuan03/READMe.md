# THỊ GIÁC MÁY TÍNH (COMPUTER VISION)

- **Sinh Viên Thực Hiện:** Phạm Thế Hùng
- **MSSV:** 2374802010164
- **Môn Học:** Thị Giác Máy Tính
- **Giảng viên:** TS.Đỗ Hữu Quân

----

## File 1: Histograms and Intensity Transformations.ipynb

### Công nghệ sử dụng
- **OpenCV (cv2)**: Xử lý và phân tích ảnh
- **Matplotlib**: Hiển thị ảnh và biểu đồ
- **NumPy**: Tính toán ma trận và mảng

### Cách hoạt động
- **Histogram**: Đếm số lần xuất hiện của các giá trị cường độ pixel (0-255)
- **Image Negatives**: Đảo ngược cường độ ảnh (s = 255 - r)
- **Brightness & Contrast**: Điều chỉnh độ sáng và độ tương phản bằng công thức `g(x,y) = αf(x,y) + β`
- **Histogram Equalization**: Cân bằng histogram để tăng độ tương phản tự động
- **Thresholding**: Phân đoạn ảnh bằng cách đặt ngưỡng để tách đối tượng khỏi nền

### Kết quả
- Hiển thị ảnh gốc và ảnh sau khi biến đổi
- Vẽ histogram để phân tích phân bố cường độ pixel
- Áp dụng các kỹ thuật trên ảnh y tế (mammogram) và ảnh thông thường (cameraman, goldhill, zelda)


## File 2: Consumption.ipynb
### Công nghệ sử dụng
- **Pandas**: Xử lý và phân tích dữ liệu CSV
- **Matplotlib & Seaborn**: Vẽ biểu đồ và heatmap
- **Folium**: Tạo bản đồ tương tác
- **Geopy**: Tính khoảng cách địa lý
- **SciPy**: Kiểm định thống kê (t-test)

### Cách hoạt động
Phân tích dữ liệu chuyến đi Uber tháng 7/2014:
1. **Đọc dữ liệu**: Load file CSV chứa 796,121 chuyến đi với thông tin thời gian, tọa độ (Lat/Lon)
2. **Phân  gian**: 
   - Nhóm dữ liệu theo giờ và ngày trong tuần
   - Tính số chuyến đi trung bình cho mỗi giờ/ngày
   - Tạo heatmap hiển thị mật độ chuyến đi
3. **Phân tích địa lý**:
   - Tính khoảng cách từ mỗi điểm đến các điểm quan tâm (sử dụng công thức Haversine)
   - Điểm quan tâm: Đại học Văn Lang (tọa độ: 10.827489, 106.700059)
4. **Mapping Data with Folium**:
   - Tạo bản đồ tương tác với Folium, tập trung tại Đại học Văn Lang (10.827489, 106.700059)
   - Thêm điểm đánh dấu để hiển thị vị trí các chuyến đi
   - Tạo bản đồ nhiệt hiển thị mật độ chuyến đi trên bản đồ
   - Tạo bản đồ nhiệt theo thời gian để quan sát sự thay đổi mật độ theo từng giờ
5. **Phân tích xu hướng**:
   - So sánh xu hướng giữa ngày trong tuần và cuối tuần
   - Kiểm định thống kê để xác định sự khác biệt

### Kết quả
- Biểu đồ đường thể hiện xu hướng chuyến đi theo giờ
- Heatmap 2D hiển thị mật độ chuyến đi theo giờ và ngày trong tuần
- **Bản đồ tương tác với Folium**:
  - Bản đồ với các điểm đánh dấu (markers) hiển thị vị trí chuyến đi
  - Bản đồ nhiệt (heatmap) cho thấy khu vực có nhiều chuyến đi
  - Bản đồ nhiệt theo thời gian (HeatMapWithTime) cho phép xem sự thay đổi mật độ theo từng giờ
- Phân tích cho thấy sự khác biệt rõ ràng giữa ngày làm việc và cuối tuần

