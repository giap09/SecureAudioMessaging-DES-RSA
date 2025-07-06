🎧 Hệ Thống Truyền Tệp Âm Thanh Bảo Mật Qua Mạng LAN
[![Uploading image.png…]()](https://github.com/giap09/SecureAudioMessaging-DES-RSA/blob/main/486643036_1189777543149102_27833471534785857_n.jpg)

Ứng dụng Flask + Crypto để gửi và nhận file âm thanh qua mạng LAN với mã hóa và xác thực an toàn.

🛡️ Giới thiệu
Hệ thống cho phép gửi và nhận file âm thanh (MP3/WAV) giữa hai máy tính thông qua kết nối TCP, kết hợp với các kỹ thuật mã hóa và xác thực hiện đại:

Bảo mật nội dung: Dữ liệu được mã hóa từng đoạn bằng Triple DES

Xác thực & toàn vẹn: Mỗi đoạn đều kèm chữ ký số SHA-512 + RSA

Kiểm soát luồng truyền: Gửi từng chunk, nhận phản hồi xác nhận

Hệ thống hoạt động không cần máy chủ, chạy độc lập trên hai thiết bị trong cùng mạng LAN.

📌 Tính năng chính
Nhóm chức năng	Mô tả chi tiết
🔐 Mã hóa & giải mã	Dùng RSA để mã hóa khóa phiên, Triple DES để mã hóa từng đoạn
✍️ Chữ ký số	SHA‑512 kết hợp RSA để xác thực metadata và từng chunk
📦 Chia & kiểm dữ liệu	Tệp âm thanh được chia 3 đoạn, xử lý độc lập
🌐 Kết nối mạng nội bộ	Sử dụng socket TCP thuần để truyền dữ liệu
💻 Giao diện web thân thiện	Giao diện HTML + CSS trực quan, có nhật ký, trạng thái, phát file

🧱 Kiến trúc hệ thống
markdown

+----------------+      TCP Socket      +------------------+
|  Giao diện gửi | <------------------> | Giao diện nhận   |
|  Flask + HTML  |                      | Flask + HTML     |
+----------------+                      +------------------+

1. Sender gửi Hello
2. Receiver trả lời Ready
3. Gửi metadata + chữ ký số
4. Gửi từng phần nội dung (chunk)
5. Mỗi chunk được xác minh và phản hồi bằng chữ ký
6. Receiver ghép file & lưu
🧰 Công nghệ sử dụng
Công nghệ	Vai trò
Flask	Giao diện web và server cục bộ
PyCryptodome	Thư viện mã hóa RSA, DES3, SHA-512
HTML/CSS/JS	Giao diện frontend hiện đại
Socket (Python)	Giao tiếp TCP giữa hai ứng dụng
Threading	Cho phép xử lý song song khi lắng nghe dữ liệu

⚙️ Cài đặt & chạy thử
1. Cài thư viện cần thiết
pip install flask pycryptodome
2. Tạo cặp khóa RSA

# Cho bên gửi
openssl genpkey -algorithm RSA -out sender_private.pem -pkeyopt rsa_keygen_bits:2048
openssl rsa -pubout -in sender_private.pem -out sender_public.pem

# Cho bên nhận
openssl genpkey -algorithm RSA -out receiver_private.pem -pkeyopt rsa_keygen_bits:2048
openssl rsa -pubout -in receiver_private.pem -out receiver_public.pem
3. Khởi động hệ thống
Terminal 1 – Máy nhận:

bash
Sao chép
Chỉnh sửa
python receiver_web.py
# Giao diện tại: http://localhost:5001
Terminal 2 – Máy gửi:

python sender_web.py
# Giao diện tại: http://localhost:5000
🖼️ Một số giao diện
Người gửi
Nhập IP máy nhận

Chọn file âm thanh (.mp3, .wav)

Gửi file qua TCP socket


Người nhận
Nhấn "Bắt đầu lắng nghe"

Xem nhật ký, kiểm tra trạng thái kết nối

Tự động lưu file nếu hợp lệ


🧪 Kiểm tra môi trường
Bạn có thể kiểm tra quyền ghi file bằng:

bash
Sao chép
Chỉnh sửa
python test_file_write.py
👥 Tác giả
👨‍💻 Nguyễn Đào Nguyên Giáp

👨‍💻 Khổng Minh Hoài 

👨‍💻 Trịnh Việt Hưng

🏫 Trường Đại học Đại Nam

🗓️ Dự án thực hiện trong kỳ Thực tập học kỳ năm 2025
