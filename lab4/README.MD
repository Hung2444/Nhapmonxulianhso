Họ tên: Lê Minh Hùng
MSSV: 2174802010063
Lớp: 71ITAI40803  
GVHD: Nguyễn Thái Anh  

## THƯ MỤC 
- `exercise/` : chứa ảnh gốc `dalat.jpg` để xử lý  
- `lang_biang.jpg` : ảnh kết quả sau xử lý  

## BÀI 1: PHÂN NGƯỠNG OTSU × 0.3 & DỊCH ẢNH SANG PHẢI 100 PIXELS

### Quy trình thực hiện:

1. **Đọc ảnh**:  
   - Dùng `PIL.Image` để đọc ảnh RGB từ thư mục `exercise/`.

2. **Cắt vùng ảnh LangBiang**:  
   - Vị trí: góc trên bên trái.  
   - Kích thước: `H / 2`, `W / 3`.

3. **Chuyển sang grayscale**:  
   - Dùng `.convert('L')` để chuyển vùng ảnh sang ảnh xám.

4. **Tính ngưỡng Otsu và nhân 0.3**:  
   - Dùng `threshold_otsu()` từ `skimage.filters`.  
   - Nhân kết quả với 0.3 để tạo ngưỡng tùy chỉnh.

5. **Tạo ảnh nhị phân**:  
   - Dựa trên ngưỡng tùy chỉnh, tạo ảnh trắng đen (`True/False`).

6. **Dịch ảnh sang phải 100 pixels**:  
   - Tạo ảnh mới có chiều rộng lớn hơn 100 pixels.  
   - Gán vùng ảnh nhị phân vào vị trí mới (bắt đầu từ cột 100).

7. **Hiển thị và lưu ảnh kết quả**:  
   - Hiển thị bằng `matplotlib.pyplot`.  
   - Lưu kết quả với tên `lang_biang.jpg`.



## BÀI 2: NHỊ PHÂN ẢNH HỒ XUÂN HƯƠNG & XOAY 45 ĐỘ

### Quy trình thực hiện:

1. **Đọc ảnh**:  
   - Dùng `PIL.Image` để đọc ảnh RGB từ thư mục `exercise/`.

2. **Cắt vùng ảnh Hồ Xuân Hương**:  
   - Nằm giữa hàng trên (giữa ảnh gốc).  
   - Tọa độ: `y = 0 → h`, `x = w → 2w`.

3. **Chuyển sang grayscale**:  
   - Dùng `rgb2gray()` từ `skimage.color`.

4. **Tính ngưỡng và phân nhị phân**:  
   - Tính trung bình toàn ảnh xám → chọn những pixel có giá trị **nhỏ hơn trung bình** để tạo ảnh nhị phân (`True` nếu tối hơn).  
   - (Có thể dùng `threshold_local()` nếu ảnh sáng/tối không đều.)

5. **Tạo ảnh RGB từ ảnh nhị phân**:  
   - Dùng `np.stack()` để nhân ảnh nhị phân thành 3 kênh.

6. **Xoay ảnh 45 độ**:  
   - Dùng `rotate(45, expand=True, fillcolor=(0, 0, 0))`.

7. **Hiển thị và lưu ảnh kết quả**:  
   - Hiển thị bằng `matplotlib.pyplot`.  
   - Lưu kết quả với tên `ho_xuan_huong.jpg`.



## BÀI 3: BIẾN DẠNG ẢNH & LÀM MỊN (CLOSING) – QUẢNG TRƯỜNG LÂM VIÊN

### Quy trình thực hiện:

1. **Đọc ảnh**:  
   - Dùng `PIL.Image` để đọc ảnh từ thư mục `exercise/`.

2. **Cắt vùng ảnh Quảng trường Lâm Viên**:  
   - Vị trí: hàng trên, cột phải (1 trong 6 vùng).  
   - Tọa độ: `y = 0 → h`, `x = 2w → 3w`.

3. **Chuyển sang grayscale**:  
   - Dùng `rgb2gray()` từ `skimage.color`.

4. **Tạo ảnh nhị phân**:  
   - Dùng ngưỡng cố định `0.6` để chọn vùng tối hơn.

5. **Biến dạng ảnh (geometric distortion)**:  
   - Dùng hàm `geometric_transform()` với công thức biến đổi tọa độ:  
     ```python
     a = 10 * cos(y / 10) + y  
     b = 10 * sin(x / 10) + x
     ```

6. **Làm mịn bằng closing**:  
   - Áp dụng `binary_closing()` để kết nối các điểm gần nhau.

7. **Hiển thị và lưu ảnh kết quả**:  
   - Hiển thị bằng `matplotlib.pyplot`.  
   - Lưu với tên `quan_truong_lam_vien.jpg`.



## BÀI 4: MENU XỬ LÝ ẢNH – CHỌN VÀ KẾT HỢP HÀM BIẾN ĐỔI


### Quy trình thực hiện:

1. **Hiển thị menu**:  
   - Người dùng được chọn:
     - **1 thao tác** (biến đổi hình học hoặc phân đoạn).
     - **2 thao tác liên tiếp** (1 hình học → 1 phân đoạn).

2. **Các lựa chọn xử lý ảnh**:  
   - **Geometric transformation**:  
     - a. `coordinate_mapping`: Lật ảnh theo chiều ngang.  
     - b. `rotate`: Xoay ảnh 45 độ.  
     - c. `scale`: Phóng to ảnh theo tỉ lệ 1.5.  
     - d. `shift`: Dịch ảnh sang phải 100 pixels.

   - **Segmentation**:  
     - e. `adaptive_thresholding`: Dùng ngưỡng cố định để tạo ảnh nhị phân.  
     - f. `binary_dilation`: Giãn nở vùng trắng trong ảnh nhị phân.  
     - g. `binary_erosion`: Co lại vùng trắng trong ảnh nhị phân.  
     - h. `otsu`: Phân ngưỡng tự động bằng thuật toán Otsu.

3. **Áp dụng lựa chọn**:  
   - Hàm `apply_option()` sẽ nhận mã lựa chọn (`a` → `h`) và gọi hàm tương ứng.
   - Có thể kết hợp 2 thao tác liên tiếp: ví dụ `rotate` → `otsu`.

4. **Hiển thị và lưu kết quả**:  
   - Dùng `matplotlib.pyplot` để hiển thị ảnh.
   - Lưu ảnh kết quả thành `output.jpg`.

