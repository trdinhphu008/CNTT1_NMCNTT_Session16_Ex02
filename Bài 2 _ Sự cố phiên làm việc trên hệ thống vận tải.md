# PHẦN 1. PHÂN TÍCH

### 1. So sánh Cache và Cookies

-   **Cache:** Là nơi lưu hình ảnh, CSS, JavaScript và các tài nguyên của website. Dung lượng thường từ MB đến GB, giúp trang web tải nhanh hơn.
    
-   **Cookies:** Là những mẩu dữ liệu nhỏ, thường khoảng 4KB, dùng để lưu thông tin đăng nhập và nhận diện người dùng.
    

**Sự khác biệt:**

-   Cache lưu dữ liệu giúp tăng tốc độ tải trang.
    
-   Cookies lưu thông tin để ghi nhớ người dùng và duy trì trạng thái đăng nhập.
    

**Kết luận:** Em chọn Persistent Cookies để ghi nhớ đăng nhập và giỏ hàng thay vì lưu toàn bộ dữ liệu vào Cookies.

# PHẦN 2. TRIỂN KHAI

### 1. Sử dụng Persistent Cookies

Em đề xuất sử dụng Persistent Cookies để trình duyệt vẫn ghi nhớ người dùng kể cả khi đóng rồi mở lại trình duyệt.

Cấu trúc Cookie đề xuất:

`Set-Cookie: sessionToken=abc123; Max-Age=604800; HttpOnly; Secure; SameSite=Lax`

Ý nghĩa:

-   **sessionToken:** Mã định danh phiên đăng nhập của shipper.
    
-   **Max-Age=604800:** Cookie tồn tại trong 7 ngày.
    
-   **HttpOnly:** Ngăn JavaScript phía Client đọc Cookie.
    
-   **Secure:** Chỉ gửi Cookie qua kết nối HTTPS.
    
-   **SameSite=Lax:** Hạn chế gửi Cookie trong một số yêu cầu từ website bên ngoài.
    

**Cách hoạt động:**

1.  Shipper đăng nhập thành công.
    
2.  Server tạo Token và gửi Cookie về trình duyệt.
    
3.  Trình duyệt lưu Cookie trong 7 ngày.
    
4.  Khi shipper mở lại website, trình duyệt gửi Token lên Server.
    
5.  Server kiểm tra Token và khôi phục trạng thái đăng nhập.
    

Giỏ hàng nên được lưu trong cơ sở dữ liệu phía Server, liên kết với tài khoản shipper, không nên lưu toàn bộ trong Cookie.

# PHẦN 3. KIỂM THỬ

### 1. Cách Hard Reload để xóa Cache

Nếu shipper thay đổi giao diện nhưng trình duyệt vẫn hiện màu cũ, có thể do trình duyệt đang sử dụng Cache cũ.

Em thực hiện như sau:

1.  Mở website trên trình duyệt.
    
2.  Nhấn F12 để mở Developer Tools.
    
3.  Nhấn giữ hoặc nhấp chuột phải vào nút Reload.
    
4.  Chọn Empty Cache and Hard Reload.
    
5.  Trình duyệt sẽ tải lại trang và lấy các tài nguyên mới từ Server.
    

**Kết luận:** Hard Reload giúp xóa Cache cũ và tải lại giao diện mới. Cookies đăng nhập không bị xóa chỉ vì thực hiện Hard Reload.
