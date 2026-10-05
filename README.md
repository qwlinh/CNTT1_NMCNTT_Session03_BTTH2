## Bài 2 : Phân tích hiệu năng hệ thống và quản lý đường dẫn tệp

---

## PHẦN 1: BÁO CÁO PHÂN TÍCH
1. Nguyên nhân đường dẫn tuyệt đối gây lỗi khi đổi máy
 - Đường dẫn tuyệt đối (Absolute Path) chứa tên ổ đĩa và toàn bộ cây thư mục gốc gắn liền với máy tính của người tạo

 - Khi chuyển sang máy của bạn thân, tên tài khoản người dùng hoặc cấu trúc thư mục gốc hoàn toàn khác, dẫn đến hệ điều hành không tìm thấy đúng vị trí thư mục, gây ra lỗi FileNotFoundError.

2. Luồng IPO từ Storage vào RAM của ứng dụng
Input (Nhập): Người dùng kích hoạt chạy ứng dụng Python. Hệ điều hành đọc mã nguồn và các file tài nguyên (ảnh logo) từ thiết bị lưu trữ Storage (SSD/HDD).

 - Process (Xử lý): CPU nhận lệnh, thực thi các đoạn code Python, nạp dữ liệu hình ảnh và biến trạng thái từ bộ nhớ vào RAM để xử lý tính toán nhanh chóng.

 - Output (Xuất): Giao diện ứng dụng Shopee-Lite hiển thị hoàn chỉnh lên màn hình (Monitor) cho người dùng tương tác.

## PHẦN 2: GIẢI PHÁP KỸ THUẬT
1. Viết lại đường dẫn tương đối sử dụng ký hiệu . và ..
Sử dụng đường dẫn tương đối dựa trên vị trí hiện tại của file code thay vì gắn cứng ổ đĩa:

 - Ký hiệu . đại diện cho thư mục hiện tại.

 - Ký hiệu .. đại diện cho thư mục cha (lùi lại một cấp).

 - Đường dẫn tương đối từ thư mục hiện tại trỏ tới assets/logo.png
logo_path = os.path.join(".", "assets", "logo.png")

2. 3 bước xử lý giảm lag dựa trên Task Manager (RAM 98%)
   
B1. **Buộc dừng các tiến trình ngốn RAM:** Mở **Task Manager** (Ctrl + Shift + Esc), chọn tab *Processes*, tìm các ứng dụng chạy ngầm chiếm nhiều tài nguyên

B2. **Khởi động lại môi trường lập trình:** Tắt hoàn toàn IDE để giải phóng vùng nhớ RAM đang bị giữ bởi tiến trình Python chạy treo trước đó.

B3. **Tối ưu hóa dung lượng tài nguyên:** Nén lại kích thước/độ phân giải của các file ảnh logo trong thư mục `assets` để giảm tải lượng RAM tiêu thụ khi ứng dụng nạp dữ liệu.
