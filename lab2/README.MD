Họ tên: Lê Minh Hùng MSSV: 2174802010063 Lớp: 71ITAI40803 GVHD: Nguyễn Thái Anh

 Câu 1 – Biến đổi ảnh cơ bản (phím I, G, L, H, C) Mục tiêu: Thực hiện các phép biến đổi cơ bản trên ảnh xám (grayscale).

Phím Phép biến đổi Giải thích ngắn gọn I Inverse (âm bản) Đổi màu mỗi pixel thành 255 - pixel. G Gamma Correction Tăng/giảm độ sáng theo công thức phi tuyến. L Log Transformation Làm sáng vùng tối, nén vùng sáng. H Histogram Equalization Cân bằng độ sáng, tăng tương phản tổng thể. C Contrast Stretching Co giãn độ tương phản dựa trên ngưỡng 2%-98%.

Các phương pháp hỗ trợ:

I: Inverse → Đảo ngược ảnh: 255 - pixel
G: Gamma Correction → Làm sáng hoặc tối ảnh theo công thức: c * pixel^γ
L: Log Transformation → Nén độ tương phản ảnh sáng: c * log(1 + pixel)
H: Histogram Equalization → Cân bằng độ sáng toàn ảnh
C: Contrast Stretching → Kéo dãn độ tương phản bằng nội suy tuyến tính

Câu 2 – Biến đổi ảnh tần số (phím F, L, H) Mục tiêu: Biến đổi ảnh sang miền tần số với Fourier và lọc Butterworth.

Phím Phép biến đổi Giải thích ngắn gọn F Fast Fourier Transform (FFT) Hiển thị biên độ phổ tần số của ảnh. L Butterworth Lowpass Filter Giữ vùng tần số thấp (ảnh mịn hơn). H Butterworth Highpass Filter Giữ vùng tần số cao 
Các lựa chọn:

F: Fast Fourier Transform → Biểu diễn phổ tần số bằng log-magnitude
L: Butterworth Lowpass → Làm mờ ảnh, giữ chi tiết lớn, loại bỏ nhiễu
H: Butterworth Highpass → Giữ chi tiết sắc nét, loại bỏ vùng đồng đều
Cấu trúc code:

Dùng numpy.fft.fft2 và fftshift để đưa ảnh về miền tần số
Áp dụng mặt nạ lọc Butterworth (tùy loại)
Biến đổi ngược bằng ifft2 → lấy phần thực để tạo ảnh kết quả
Hiển thị và lưu ảnh


Câu 3 – Hoán đổi RGB + Biến đổi cơ bản ngẫu nhiên Mục tiêu:


Quy trình:

Đọc ảnh RGB
Hoán đổi thứ tự màu (ví dụ: RGB → BGR, BRG, GRB,...)
Ngẫu nhiên chọn 1 phép biến đổi từ Bài 1 để áp dụng
Hiển thị và lưu kết quả


Câu 4 – Hoán đổi RGB + Biến đổi tần số ngẫu nhiên + Lọc nâng cao Mục tiêu:


Quy trình:

Đọc ảnh RGB và hoán đổi màu
Ngẫu nhiên chọn 1 phép biến đổi từ Bài 2
Nếu:
Là Lowpass → áp dụng thêm Min Filter
Là Highpass → áp dụng thêm Max Filter
Biến đổi ảnh, hiển thị và lưu kết quả
Giải thích các bộ lọc:

Min Filter: làm mượt ảnh, giảm nhiễu
Max Filter: giữ lại biên và chi tiết mạnh
