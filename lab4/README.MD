Họ tên: Lê Minh Hùng
MSSV: 2174802010063
Lớp: 71ITAI40803
GVHD: Nguyễn Thái Anh

THƯ MỤC
exercise/ : chứa ảnh gốc colorful-ripe-tropical-fruits.jpg để xử lý
BÀI 1: DI CHUYỂN LÁT KIWI SANG PHẢI 30 PIXEL
Quy trình thực hiện:
Đọc ảnh:
Dùng thư viện imageio.v2 để đọc ảnh RGB từ thư mục exercise/.
Chọn vùng kiwi:
Xác định lát kiwi nằm ở góc trên bên trái, gần quả cam và nho tím.
Tọa độ: y = 180 → 270, x = 230 → 320.
Cắt lát kiwi:
Dùng slicing của NumPy để trích xuất lát kiwi.
Dán lát kiwi sang phải 30 pixels:
Gán lát kiwi vào vị trí mới (x + 30).
Xóa kiwi gốc (nếu muốn):
Có thể dùng result[y1:y2, x1:x2] = 0 để đặt vùng gốc thành màu đen.
Hiển thị ảnh kết quả bằng matplotlib.pyplot.
Cấu trúc code:
numpy: xử lý mảng ảnh.
imageio: đọc ảnh RGB.
matplotlib.pyplot: hiển thị ảnh sau xử lý.
Kết quả:
Ảnh sau xử lý hiển thị lát kiwi ở vị trí mới, cách chỗ cũ 30 pixels theo trục hoành.
Ảnh gốc vẫn giữ nguyên nếu không xóa lát kiwi cũ.
Gợi ý mở rộng:
Cho phép người dùng chọn vùng ảnh bằng chuột.
Áp dụng thao tác di chuyển nhiều lát khác nhau.
Kết hợp với hiệu ứng hoặc hoạt ảnh chuyển động.
BÀI 2 : ĐỔI MÀU TRÁI CÂY THEO VÙNG
Quy trình thực hiện:
Đọc ảnh:

Sử dụng imageio để đọc ảnh màu từ thư mục exercise/.
Chuyển đổi ảnh sang định dạng BGR để xử lý với OpenCV.
Đổi màu đu đủ:

Cắt vùng ảnh chứa quả đu đủ theo tọa độ:
y = 340 → 790, x = 100 → 650
Chuyển vùng ảnh sang HSV.
Gán giá trị Hue = 60 → màu xanh lá cây.
Chuyển lại BGR và gán vào ảnh gốc.
Đổi màu dưa hấu:

Cắt vùng ảnh chứa dưa hấu theo tọa độ:
y = 300 → 1000, x = 1660 → 3500
Chuyển vùng ảnh sang HSV.
Gán giá trị Hue = 120 → màu xanh dương.
Chuyển lại BGR và gán vào ảnh gốc.
Hiển thị kết quả:

Chuyển ảnh từ BGR sang RGB.
Dùng matplotlib.pyplot để hiển thị kết quả.
Cấu trúc code:
Sử dụng imageio.v2 để đọc ảnh.
Dùng OpenCV (cv2) để chuyển đổi không gian màu và xử lý ảnh.
Dùng matplotlib để hiển thị ảnh kết quả.
Kết quả:
Quả đu đủ trong ảnh gốc được đổi thành xanh lá cây.
Quả dưa hấu được đổi sang xanh dương toàn vùng đã chọn.
Các vùng khác trong ảnh không bị ảnh hưởng.
BÀI 3: XOAY ĐỐI TƯỢNG TRONG ẢNH
Quy trình thực hiện:
Đọc ảnh:

Dùng imageio.v2 để đọc ảnh quang_ninh.jpg.
Xử lý ngọn núi:

Cắt ngọn núi từ ảnh với tọa độ:
y = 80 → 390, x = 520 → 790
Dùng scipy.ndimage.rotate để xoay 45° với reshape=True.
Lưu kết quả vào file mountain_rotated.jpg.
Xử lý con thuyền:

Cắt con thuyền từ ảnh với tọa độ:
y = 450 → 600, x = 420 → 640
Xoay góc 45° bằng rotate.
Lưu kết quả vào file boat_rotated.jpg.
Hiển thị kết quả (tuỳ chọn):

Dùng matplotlib.pyplot để hiển thị hai ảnh đã xoay.
Cấu trúc code:
imageio: đọc và lưu ảnh.
scipy.ndimage.rotate: thực hiện phép xoay ảnh.
numpy: thao tác mảng.
matplotlib.pyplot: hiển thị ảnh kết quả.
Kết quả:
Tách riêng được 2 đối tượng (núi và thuyền) từ ảnh gốc.
Mỗi đối tượng được xoay đúng 45° và lưu thành 2 ảnh mới:
mountain_rotated.jpg
boat_rotated.jpg
BÀI 4: PHÓNG TO VÙNG NGÔI CHÙA
Quy trình thực hiện:
Đọc ảnh:

Dùng imageio.v2 để đọc ảnh pagoda.jpg.
Cắt vùng ngôi chùa:

Sử dụng slicing để lấy vùng ảnh có chứa ngôi chùa:
Tọa độ: y = 100 → 300, x = 220 → 370
Phóng to ảnh:

Dùng cv2.resize() với các hệ số:
fx = 5, fy = 5 (tăng kích thước 5 lần theo cả hai chiều)
Sử dụng nội suy INTER_LINEAR để ảnh được phóng nét hơn.
Lưu ảnh kết quả:

Ảnh sau khi phóng được lưu dưới tên:
pagoda_upscaled.jpg
Hiển thị (nếu cần):

Có thể dùng matplotlib.pyplot để hiển thị ảnh kết quả.
Cấu trúc code:
imageio.v2: dùng để đọc và lưu ảnh.
cv2: dùng để thay đổi kích thước ảnh (resize).
matplotlib.pyplot: dùng để hiển thị ảnh (nếu thêm import matplotlib.pyplot as plt).
Kết quả:
Vùng ngôi chùa trong ảnh được phóng lớn lên 5 lần.
Chất lượng phóng tốt nhờ nội suy tuyến tính (INTER_LINEAR).
BÀI 5: CHƯƠNG TRÌNH XỬ LÝ ẢNH ĐA CHỨC NĂNG
Quy trình thực hiện:
Quét thư mục exercise/ để lấy danh sách các ảnh đầu vào.
Hiển thị menu lựa chọn chức năng cho người dùng.
Người dùng chọn ảnh và thao tác cần thực hiện.
Áp dụng xử lý ảnh tương ứng với lựa chọn.
Hiển thị ảnh kết quả bằng matplotlib.
Lưu ảnh kết quả cùng tên với tiền tố result_.

Tên file kết quả sẽ có dạng: result_ten_anh_goc.jpg
