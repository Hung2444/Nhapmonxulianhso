# Nhapmonxulianhso 
BÁO CÁO XỬ LÝ ẢNH ( BÀI 1 -5)
Họ và Tên: Lê Minh Hùng
MSSV: 2174802010063
Lớp: NhapMonXuLyAnhSo-243_71ITAI40803_0101 
GVHD: Nguyễn Thái Anh

Ngôn ngữ: Python 3 Thư viện: PIL, numpy, matplotlib, scipy, skimage,...

-Bài 1: Tách màu RGB Tách ảnh thành 3 ảnh chỉ hiển thị màu Đỏ (R), Xanh Lá (G), và Xanh Dương (B).
import các thư viện cần thiết như PIL.Image, numpy, matplotlib.pyplot
Bước 1: Đọc ảnh đầu vào (img = Image.open('hinh1.jpg')
Bước 2: Tách kênh màu RGB (r, g, b = img.split() )
Bước 3: Tạo ảnh giữ lại từng kênh (red_img = Image.merge("RGB", (r, Image.new("L", r.size), Image.new("L", r.size))) )
Bước 4: Lưu kết quả:
  red_img.save("red.jpg")
  green_img.save("green.jpg")
  blue_img.save("blue.jpg")
Bước 5: hiển thị ảnh ( plt.figure(figsize=(12, 4)) )

-Bài 2: 
Bước 1: Mở ảnh (img = Image.open("hinh1.jpg"))
Bước 2: Tách màu (r, g, b = img.split() )
Bước 3: Hoán đổi kênh R và B ( swapped = Image.merge("RGB", (b, g, r)) )
Bước 4: Lưu ảnh kết quả ( swapped.save("swapped.jpg") )
Bước 5: Hiển thị ảnh trước và sau biến đổi ( plt.figure(figsize=(10, 4)) )

- Bài 3
Bước 1: Đọc ảnh và chuyển hóa giá trị RGB
img = Image.open("hinh1.jpg")
arr = np.array(img).astype("float32") / 25
Bước 2: Khởi tạo mảng HSV rỗng
(hsv = np.zeros_like(arr))

Bước 3: Chuyển đổi từng pixel từ RGB sang HSV 
( for i in range(arr.shape[0]):
    for j in range(arr.shape[1]):
        hsv[i, j] = colorsys.rgb_to_hsv(*arr[i, j])
)

Bước 4: Tách và chuyển đổi các kênh H, S, V
( h = (hsv[:, :, 0] * 255).astype('uint8')
s = (hsv[:, :, 1] * 255).astype('uint8')
v = (hsv[:, :, 2] * 255).astype('uint8')
)

Bước 5: Lưu ảnh từng kênh 
( Image.fromarray(h).save("hue.jpg")
Image.fromarray(s).save("saturation.jpg")
Image.fromarray(v).save("value.jpg")
)
 
Bước 6: Hiển thị từng kênh
( plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(h, cmap='gray')
plt.title("Hue (H)")
plt.axis("on")
)

Vẽ ảnh Hue (tông màu), sử dụng cmap='gray' để hiển thị dưới dạng ảnh xám.
 ( plt.subplot(1, 3, 2)
plt.imshow(s, cmap='gray')
plt.title("Saturation (S)")
plt.axis("on")

plt.subplot(1, 3, 3)
plt.imshow(v, cmap='gray')
plt.title("Value (V)")
plt.axis("on")

plt.tight_layout()
plt.show()
)

-Bài 4:
Bước 1: mở ảnh và chuẩn hóa
Bước 2: Chuyển ảnh RGB sang HSV 
(hsv = np.zeros_like(arr)
for i in range(arr.shape[0]):
    for j in range(arr.shape[1]):
        hsv[i, j] = colorsys.rgb_to_hsv(*arr[i, j]) )

Bước 3: Biến đổi màu sắc và độ sáng
( hsv[:, :, 0] /= 3         # Giảm hue
hsv[:, :, 2] *= 0.75      # Giảm độ sáng
)

Bước 4: Chuyển HSV → RGB
( rgb = np.zeros_like(hsv)
for i in range(arr.shape[0]):
    for j in range(arr.shape[1]):
        rgb[i, j] = colorsys.hsv_to_rgb(*hsv[i, j])
)

Bước 5: Lưu ảnh mới
(rgb_img = Image.fromarray((rgb * 255).astype('uint8'))
rgb_img.save("hsv_doimau.jpg")
)

Bước 6: Hiển thị ảnh gốc và ảnh đã biến đổi
plt.figure(figsize=(10, 4))

plt.subplot(1, 2, 1)
plt.imshow(img)
plt.title("Ảnh gốc")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(rgb_img)
plt.title("Ảnh đổi màu HSV")
plt.axis("off")

plt.tight_layout()
plt.show()


-Bài 5:
Bước 1: tạo thư mục chứa ảnh gốc
folder = "C:\XULYANHSO\Exercise_MeanFiltered"
output_folder = "Exercise_MeanFiltered"
os.makedirs(output_folder, exist_ok=True)

Bước 2: Duyệt qua từng ảnh trong thư mục
for filename in os.listdir(folder):
    if filename.lower().endswith((".png", ".jpg", ".jpeg")):

Bước 3: Đọc ảnh và chuyển thành mảng NumPy
path = os.path.join(folder, filename)
img = Image.open(path)
arr = np.array(img)

Bước 4: Áp dụng mean filter
blur = uniform_filter(arr, size=(3, 3, 1))

Bước 5: Lưu ảnh sau khi lọc
blur_img = Image.fromarray(blur.astype("uint8"))
out_path = os.path.join(output_folder, f"mean_{filename}")
blur_img.save(out_path)

Bước 6: Hiển thị 3 ảnh một lần
 if len(images_to_show) == 3:
            plt.figure(figsize=(12, 4))
            for i, (img_show, title) in enumerate(images_to_show):
                plt.subplot(1, 3, i + 1)
                plt.imshow(img_show)
                plt.title(title)
                plt.axis("off")
            plt.tight_layout()
            plt.show()
            images_to_show = []

Bài 6:
Bước 1: Tạo thư mục
Bước 2: Lặp qua các ảnh trong thư mục
Bước 3: Sử dụng bộ lọc 
mean_img = uniform_filter(arr, size=(3, 3, 1))
mean_img = Image.fromarray(mean_img.astype("uint8"))
mean_img.save(os.path.join(output_folder, f"mean_{filename}"))

Bước 4:Hiển thị kết quả


Bài 7:
Bước 1: Tạo thư mục
Bước 2: Lặp qua các ảnh trong thư mục input
Bước 3: Đọc ảnh và xử lý nhiễu
( img = Image.open(input_path)
arr = np.array(img)
denoised = median_filter(arr, size=(3, 3, 1))
)
Bước 4: chuyển đổi ảnh sang màu xám
( gray = rgb2gray(denoised) )
Bước 5: áp dụng Sobel filter để phát hiện biên
( plt.imsave(output_path, edges, cmap="gray") )
Bước 6 : hiển thị kết quả


Bài 8: 
Bước 1: tạo thư mục
Bước 2: xử lý ảnh trong thư mục input
Bước 3: làm mượt và xáo trộn tên màu
(
denoised = uniform_filter(arr, size=(3, 3, 1))
ch = [0, 1, 2]
random.shuffle(ch)
shuffled = denoised[:, :, ch]
)
Bước 4: lưu kết quả
Bước 5: hiển thị ảnh theo nhóm
(
images_to_show.append((shuffled, f"RGB random {filename}"))

if len(images_to_show) == 3:
    plt.figure(figsize=(12, 4))
    for i, (img_show, title) in enumerate(images_to_show):
        plt.subplot(1, 3, i + 1)
        plt.imshow(img_show)
        plt.title(title)
        plt.axis("off")
    plt.tight_layout()
    plt.show()
    images_to_show = []
)


Bài 9:
Bước 1: tạo thư mục
Bước 2:tạo hàm sinh hue duy nhất
(
used_hues = []

def generate_unique_hue():
    """Sinh hue ngẫu nhiên không trùng với các hue đã sử dụng"""
    while True:
        new_hue = np.random.rand()  # Sinh hue ngẫu nhiên từ 0 đến 1
        if all(abs(new_hue - h) > 0.05 for h in used_hues):  # Đảm bảo không trùng lặp
            used_hues.append(new_hue)
            return new_hue
)

Bước 3: Lặp qua các ảnh trong thư mục input
Bước 4: Khử nhiễu và chuyển sang HSV
(
denoised = median_filter(arr, size=(3, 3, 1))

hsv = np.zeros_like(denoised)
for i in range(denoised.shape[0]):
    for j in range(denoised.shape[1]):
        hsv[i, j] = colorsys.rgb_to_hsv(*denoised[i, j])
)

Bước 5: Thay đổi hue và chuyển lại RGB
(
unique_hue = generate_unique_hue()
hsv[:, :, 0] = unique_hue

rgb = np.zeros_like(hsv)
for i in range(hsv.shape[0]):
    for j in range(hsv.shape[1]):
        rgb[i, j] = colorsys.hsv_to_rgb(*hsv[i, j])
)

Bước 6: lưu kết quả và hiển thị kết quả




  

