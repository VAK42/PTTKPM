%%------------------------------------------------
%% BIỂU ĐỒ USE CASE: CỬA HÀNG TRỰC TUYẾN
%%------------------------------------------------
usecaseDiagram

actor "Khách Truy Cập" as Visitor
actor "Quản Trị Viên" as Admin
actor "Hệ Thống" as System

rectangle "Cửa Hàng Trực Tuyến" {

  %% --- Người Dùng (Visitor) ---
  (Đăng Ký Tài Khoản) as UC1
  (Đăng Nhập) as UC2
  (Duyệt Danh Mục) as UC3
  (Tìm Kiếm Sản Phẩm) as UC4
  (Xem Chi Tiết Sản Phẩm) as UC5
  (Lọc Sản Phẩm) as UC6
  (Thêm Vào Giỏ Hàng) as UC7
  (Cập Nhật Số Lượng) as UC8
  (Xóa Khỏi Giỏ Hàng) as UC9
  (Thanh Toán) as UC10
  (Xem Đơn Hàng) as UC11
  (Hủy Đơn Hàng) as UC12
  (Viết Đánh Giá Sản Phẩm) as UC13
  (Báo Cáo Đánh Giá Vi Phạm) as UC14
  (Quản Lý Tài Khoản) as UC15
  (Quản Lý Địa Chỉ Giao Hàng) as UC16
  (Lưu Phương Thức Thanh Toán) as UC17
  (Đăng Xuất) as UC18
  (Thêm Vào Danh Sách Yêu Thích) as UC19

  %% --- Quản Trị Viên (Admin) ---
  (Cập Nhật Sản Phẩm) as UC20
  (Quản Lý Banner Trang Chủ) as UC21
  (Quản Lý Bộ Sưu Tập) as UC22
  (Quản Lý Trang CMS) as UC23
  (Nhập Kho) as UC24
  (Xuất Kho Theo Đơn) as UC25
  (Điều Chỉnh Tồn Kho) as UC26
  (Quản Lý Nhà Cung Cấp) as UC27
  (Báo Cáo Doanh Thu Theo Thời Gian) as UC28
  (Báo Cáo Sản Phẩm Bán Chạy) as UC29
  (Quản Lý Người Dùng) as UC30
  (Thay Đổi Trạng Thái Đơn Hàng) as UC31
  (Tạo Nhãn Vận Chuyển) as UC32
  (Xác Nhận Giao Hàng) as UC33

  %% --- Quy Trình Tự Động (System) ---
  (Gợi Ý Sản Phẩm Tự Động) as UC34
  (Tính Phí Vận Chuyển Tự Động) as UC35
  (Cập Nhật Trạng Thái Tự Động) as UC36
  (Tạo Nhãn Vận Chuyển Tự Động) as UC37
  (Xác Nhận Giao Hàng Tự Động) as UC38
  (Gửi Email Tự Động) as UC39
}

%% --- Liên Kết Của Khách Truy Cập ---
Visitor --> UC1
Visitor --> UC2
Visitor --> UC3
Visitor --> UC4
Visitor --> UC5
Visitor --> UC6
Visitor --> UC7
Visitor --> UC8
Visitor --> UC9
Visitor --> UC10
Visitor --> UC11
Visitor --> UC12
Visitor --> UC13
Visitor --> UC14
Visitor --> UC15
Visitor --> UC16
Visitor --> UC17
Visitor --> UC18
Visitor --> UC19

%% --- Liên Kết Của Quản Trị Viên ---
Admin --> UC20
Admin --> UC21
Admin --> UC22
Admin --> UC23
Admin --> UC24
Admin --> UC25
Admin --> UC26
Admin --> UC27
Admin --> UC28
Admin --> UC29
Admin --> UC30
Admin --> UC31
Admin --> UC32
Admin --> UC33

%% --- Liên Kết Của Hệ Thống ---
System --> UC34
System --> UC35
System --> UC36
System --> UC37
System --> UC38
System --> UC39
