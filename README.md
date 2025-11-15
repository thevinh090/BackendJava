API Backend E-commerce (Spring Boot)
Dự án này là một hệ thống API RESTful hoàn chỉnh cho một trang web thương mại điện tử, được xây dựng bằng Java và Spring Boot.

Hệ thống bao gồm các chức năng cốt lõi như quản lý người dùng, xác thực (JWT), quản lý sản phẩm, danh mục, giỏ hàng, đặt hàng và các chức năng quản trị (Admin).

🚀 Tính năng chính
Dự án được phân chia rõ ràng thành các module chức năng:

👤 Xác thực & Người dùng (Authentication)
Đăng ký tài khoản người dùng mới.

Đăng nhập với JWT (JSON Web Token) để xác thực.

Phân quyền dựa trên vai trò (ROLE_USER và ROLE_ADMIN).



📦 Quản lý Sản phẩm & Danh mục (Products & Categories)
Public:

Lấy tất cả sản phẩm (có phân trang/bộ lọc).

Lấy chi tiết một sản phẩm.

Tìm kiếm sản phẩm theo tên hoặc mô tả.

Lọc sản phẩm theo danh mục hoặc khoảng giá.


Lấy tất cả danh mục.

Admin:

Thêm, sửa, xóa sản phẩm.


Thêm, sửa, xóa danh mục.


🛒 Giỏ hàng (Shopping Cart)
Lấy giỏ hàng của người dùng hiện tại.

Thêm sản phẩm vào giỏ hàng.

Cập nhật số lượng sản phẩm trong giỏ.

Xóa một sản phẩm khỏi giỏ.

Xóa toàn bộ giỏ hàng.

💳 Đặt hàng (Orders)
Tạo đơn hàng mới từ giỏ hàng.

Lấy lịch sử đơn hàng của người dùng.

Lấy chi tiết một đơn hàng cụ thể.

Hủy đơn hàng (nếu trạng thái là "PENDING").

⭐ Đánh giá (Reviews)
Người dùng đã mua hàng có thể tạo đánh giá (rating + comment) cho sản phẩm.

Lấy tất cả đánh giá của một sản phẩm.

👑 Quản trị (Admin Dashboard)
Xem thống kê tổng quan (tổng doanh thu, số người dùng, số đơn hàng).

Quản lý tất cả đơn hàng (xem và cập nhật trạng thái, ví dụ: PENDING -> CONFIRMED).

Quản lý tất cả người dùng (xem, cập nhật thông tin, xóa).


📁 Tải file (File Upload)
Endpoint để tải ảnh sản phẩm/danh mục lên server.

🛠️ Công nghệ sử dụng
Ngôn ngữ: Java 21 (dựa trên pom.xml)


Framework: Spring Boot 3.5.7 (bao gồm Spring Web, Spring Data JPA, Spring Security) 


Bảo mật: Spring Security & JSON Web Token (JWT) 



Cơ sở dữ liệu: MySQL (sử dụng mysql-connector-j) & Spring Data JPA 





API: RESTful API

Build: Apache Maven

Tiện ích: Lombok, Jakarta Validation

⚙️ Cài đặt và Khởi chạy
1. Yêu cầu
JDK 21

Maven

Một CSDL MySQL đang chạy (ví dụ: qua XAMPP, MySQL Workbench, hoặc Docker)

2. Clone dự án
Bash

git clone <URL_REPO_CUA_BAN>
cd BackendJava
3. Cấu hình CSDL
Tạo một file application.properties trong thư mục src/main/resources.

Nội dung file application.properties:

Properties

# Cấu hình kết nối MySQL
spring.datasource.url=jdbc:mysql://localhost:3306/ten_database_cua_ban
spring.datasource.username=root
spring.datasource.password=mat_khau_mysql_cua_ban

# Cấu hình JPA/Hibernate
# Dùng 'update' để tự động cập nhật schema CSDL khi khởi chạy
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true

# Cấu hình JWT (BẮT BUỘC)
# Thay 'YourVeryStrongSecretKey...' bằng một chuỗi bí mật dài và ngẫu nhiên
jwt.secret=YourVeryStrongSecretKeyForGeneratingTokensMustBeLongEnough
jwt.expiration=86400000 # 24 giờ (tính bằng mili-giây)

# Cấu hình thư mục tải file (tùy chọn)
# Mặc định là thư mục 'uploads' ngang hàng với file .jar
file.upload-dir=uploads
4. Chạy ứng dụng
Bạn có thể chạy bằng Maven hoặc trực tiếp từ IDE của mình.

Dùng Maven:

Bash

mvn spring-boot:run
Ứng dụng sẽ khởi chạy tại http://localhost:8080.

5. ⭐️ Lấy quyền Admin
Đăng ký một tài khoản bình thường qua API POST /api/auth/register.

Mở CSDL của bạn (ví dụ: dùng MySQL Workbench).

Truy cập bảng users và tìm bản ghi của user bạn vừa tạo.

Sửa cột role từ "USER" thành "ADMIN".


Đăng nhập lại, token của bạn bây giờ sẽ có quyền Admin.


🗺️ Danh sách API Endpoints
Dưới đây là các API endpoint chính của dự án.

Authentication (/api/auth)

POST /register: Đăng ký tài khoản mới.


POST /login: Đăng nhập lấy token JWT.

Products (/api/products)

GET /: Lấy tất cả sản phẩm.


GET /{id}: Lấy chi tiết sản phẩm.


GET /category/{categoryId}: Lấy sản phẩm theo danh mục.


GET /search: Tìm kiếm sản phẩm (ví dụ: ?keyword=áo).


GET /filter: Lọc theo giá (ví dụ: ?minPrice=100&maxPrice=500).


POST /: (Admin) Tạo sản phẩm mới.


PUT /{id}: (Admin) Cập nhật sản phẩm.


DELETE /{id}: (Admin) Xóa sản phẩm.

Categories (/api/categories)

GET /: Lấy tất cả danh mục.


GET /{id}: Lấy chi tiết danh mục.


POST /: (Admin) Tạo danh mục mới.


PUT /{id}: (Admin) Cập nhật danh mục.


DELETE /{id}: (Admin) Xóa danh mục.

Cart (/api/cart) - (Yêu cầu USER Token)

GET /: Lấy giỏ hàng.


POST /items: Thêm item vào giỏ.


PUT /items/{itemId}: Cập nhật số lượng item (ví dụ: ?quantity=3).


DELETE /items/{itemId}: Xóa item khỏi giỏ.


DELETE /: Xóa sạch giỏ hàng.

Orders (/api/orders) - (Yêu cầu USER Token)

POST /: Tạo đơn hàng (checkout).


GET /: Lấy lịch sử đơn hàng của user.


GET /{orderId}: Lấy chi tiết 1 đơn hàng.


PUT /{orderId}/cancel: Hủy đơn hàng.

Reviews (/api/reviews)

POST /: (User) Gửi đánh giá.


GET /product/{productId}: (Public) Lấy đánh giá của sản phẩm.

File Upload (/api/files)

POST /upload: Tải file (ảnh) lên.

Admin (/api/admin) - (Yêu cầu ADMIN Token)

GET /statistics/dashboard: Lấy thống kê dashboard.


GET /orders: Lấy tất cả đơn hàng.


PUT /orders/{orderId}/status: Cập nhật trạng thái đơn hàng (ví dụ: ?status=CONFIRMED).


GET /users: Lấy tất cả người dùng.


PUT /users/{id}: Cập nhật thông tin người dùng.


DELETE /users/{id}: Xóa người dùng.