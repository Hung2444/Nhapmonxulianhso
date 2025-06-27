
**Bài 1: Đọc ảnh**

Dùng thư viện `imageio.v2.imread` để nạp ảnh `scene.png` vào biến `data`. Kết quả là một mảng NumPy ba chiều với kích thước tương ứng (chiều cao, chiều rộng, và 3 kênh màu RGB).

### Tách từng kênh màu:

* **Kênh đỏ (Red):** `rdata = data[:, :, 0]`
* **Kênh lục (Green):** `gdata = data[:, :, 1]`
* **Kênh xanh dương (Blue):** `bdata = data[:, :, 2]`

### Hiển thị từng kênh màu:

Dùng `matplotlib.pyplot.imshow` để hiển thị ảnh từng kênh màu đơn lẻ:

* `rdata` với bảng màu `'Reds'` làm nổi bật màu đỏ.
* `gdata` với bảng màu `'Greens'` làm nổi bật màu lục.
* `bdata` với bảng màu `'Blues'` làm nổi bật màu xanh dương.

**Kết quả:**
Hiển thị từng ảnh tương ứng theo màu nổi bật của kênh.

---

**Bài 2: Hoán đổi các kênh màu**

### Hoán đổi thứ tự các kênh:

* Chuyển từ **RGB → GRB**: `rgb_to_grb = img[:, :, [1, 0, 2]]`
* Chuyển từ **RGB → BGR**: `rgb_to_bgr = img[:, :, [2, 1, 0]]`
* Chuyển từ **RGB → BRG**: `rgb_to_brg = img[:, :, [2, 0, 1]]`

### Lưu ảnh đã hoán đổi:

* **scence\_grb.png:** Đổi vị trí màu đỏ và xanh lục.
* **scence\_bgr.png:** Đổi vị trí màu đỏ và xanh dương.
* **scence\_brg.png:** Màu lần lượt là xanh dương, đỏ, xanh lục.

Hiển thị ảnh `scence_bgr.png` để kiểm tra.

---

**Bài 3: Chuyển đổi RGB → HSV**

### Chuẩn hóa ảnh:

Đọc ảnh `scene.png` và chuẩn hóa giá trị pixel về \[0, 1]:
`img = iio.imread('scene.png') / 255.0`

Loại bỏ kênh Alpha nếu ảnh có 4 kênh:
`if img.shape[-1] == 4: img = img[..., :3]`

### Chuyển sang không gian HSV:

Sử dụng `matplotlib.colors.rgb_to_hsv` để chuyển đổi ảnh.

* Kênh Hue (H): `H = hsv[..., 0]`
* Kênh Saturation (S): `S = hsv[..., 1]`
* Kênh Value (V): `V = hsv[..., 2]`

### Lưu và hiển thị kênh HSV:

Chuyển các kênh về \[0, 255], ép kiểu uint8, và lưu dưới dạng `.png`.
Dùng vòng lặp hiển thị từng kênh màu xám.

**Kết quả:**

* `hue.png`: Thể hiện màu sắc (H).
* `saturation.png`: Mức độ bão hòa (S).
* `value.png`: Độ sáng (V).

---

**Bài 4: Biến đổi HSV**

### Chuyển RGB sang HSV:

Dùng `colorsys.rgb_to_hsv` để chuyển đổi pixel RGB sang HSV bằng `np.vectorize`.
`h, s, v = rgb2hsv(rgb[:, :, 0], rgb[:, :, 1], rgb[:, :, 2])`

### Điều chỉnh kênh:

* Giảm Hue: `h = (1/3) * h`
* Giảm Value: `v = (3/4) * v`
* Dùng `np.clip` để giữ giá trị trong khoảng \[0, 1].

### Chuyển lại RGB:

Dùng `colorsys.hsv_to_rgb` để chuyển HSV về RGB:
`rgb_new = np.stack([r, g, b], axis=2)`

Lưu ảnh đã chỉnh sửa.

**Kết quả:**
Ảnh `hsv_modified.png` sẽ có màu sắc và độ sáng thay đổi.

---

**Bài 5: Làm mờ ảnh**

### Đọc và chuyển ảnh sang grayscale:

Dùng `rgb2gray` chuyển đổi ảnh `baby.jpeg`, `balloons_noisy.png`, và `flower.jpeg` sang ảnh xám.

### Áp dụng bộ lọc trung bình:

Sử dụng kernel 5x5 để làm mờ ảnh:
`k = np.ones((5, 5)) / 25`
`blurred = sn.convolve(img, k)`

Lưu và hiển thị ảnh làm mờ.

**Kết quả:**
Ảnh đầu ra mượt hơn, nhiễu giảm rõ rệt.

---

**Bài 6: Các loại bộ lọc**

### Đọc ảnh và áp dụng các bộ lọc:

* Lọc trung bình (Mean filter): Làm mờ toàn cục.
* Lọc trung vị (Median filter): Loại bỏ nhiễu muối tiêu.
* Lọc giá trị lớn nhất/nhỏ nhất: Làm nổi bật vùng sáng/tối.

Hiển thị ảnh đã lọc để so sánh.

**Kết quả:**
Hiệu quả từng bộ lọc được hiển thị trực quan.

---

**Bài 7: Phát hiện biên cạnh**

### Các bước chính:

1. **Khử nhiễu ảnh:** Dùng `median_filter`.
2. **Tính biên cạnh:** Sử dụng Sobel, Prewitt, và Canny.

### So sánh hiệu quả:

Hiển thị biên cạnh từ từng phương pháp để so sánh.

**Kết quả:**
Canny phát hiện biên rõ nét và ít nhiễu hơn.

---

**Bài 8: Khử nhiễu và thay đổi màu sắc**

### Xử lý từng kênh:

* Lọc trung vị từng kênh R, G, B.
* Nhân mỗi kênh với hệ số ngẫu nhiên để tạo hiệu ứng màu sắc.

**Kết quả:**
Ảnh được làm mịn và có màu sắc mới lạ.

---

**Bài 9: Biến đổi ngẫu nhiên HSV**

### Bước nổi bật:

* Khử nhiễu bằng `median_filter`.
* Chuyển đổi ngẫu nhiên Hue, Saturation, Value.
* Lưu ảnh không trùng lặp bằng cách kiểm tra mã băm.

**Kết quả:**
Tạo ra các ảnh có màu sắc độc đáo từ ảnh gốc.
