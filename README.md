# Hệ thống Quản Lý Nhân Sự - Kiến trúc 3 Tầng (ADO.NET)

Ứng dụng quản lý nhân sự dành cho doanh nghiệp, xây dựng trên nền tảng **Windows Forms (.NET 8)** theo kiến trúc **3 tầng (3-Tier Architecture)**, sử dụng **ADO.NET** để tương tác trực tiếp với cơ sở dữ liệu SQL Server. Đây là đồ án cuối kỳ của Nhóm 16.

---

## Kiến trúc hệ thống

Ứng dụng được tổ chức theo mô hình 3 tầng tách biệt rõ ràng:

```
┌─────────────────────────────────────┐
│         Presentation Layer          │  ← Windows Forms (UI)
│  frmDangNhap, frmQuanLyNV, ...      │
├─────────────────────────────────────┤
│         Business Logic Layer        │  ← BS Layer/
│  Xử lý nghiệp vụ, validation        │
├─────────────────────────────────────┤
│         Data Access Layer           │  ← DB Layer/
│  ADO.NET - SqlCommand, SqlAdapter   │
└─────────────────────────────────────┘
              ↕
      SQL Server Database
```

---

## Tính năng

**Quản lý nhân sự**
- Quản lý thông tin nhân viên (thêm, sửa, xóa, tìm kiếm)
- Quản lý phòng ban và chức vụ
- Quản lý hợp đồng lao động

**Chấm công & Lương**
- Chấm công theo tháng
- Tính lương nhân viên tự động
- Thống kê lương và xuất báo cáo (RDLC Report)
- Quản lý thưởng / phạt

**Nghỉ phép & Bảo hiểm**
- Đăng ký và duyệt nghỉ phép
- Quản lý bảo hiểm nhân viên

**Hệ thống tài khoản**
- Đăng nhập với 3 vai trò: Quản trị viên, Trưởng phòng, Nhân viên
- Phân quyền menu theo vai trò
- Cập nhật mật khẩu
- Quản lý thông báo nội bộ

---

## Công nghệ sử dụng

| Thành phần | Công nghệ |
|---|---|
| Ngôn ngữ | C# |
| Framework | .NET 8 (Windows) |
| UI | Windows Forms |
| Truy cập dữ liệu | ADO.NET (SqlConnection, SqlCommand, SqlDataAdapter) |
| Cơ sở dữ liệu | SQL Server |
| Báo cáo | RDLC Report |

---

## Yêu cầu hệ thống

- Windows 10 trở lên
- .NET 8 Runtime
- SQL Server 2019 trở lên (hoặc SQL Server Express)
- Visual Studio 2022 (nếu build từ source)

---

## Hướng dẫn cài đặt

### 1. Clone repository

```bash
git clone https://github.com/ventdejanvier/QuanLyNhanSu_3Tang_ADO.NET.git
cd QuanLyNhanSu_3Tang_ADO.NET
```

### 2. Tạo cơ sở dữ liệu

Mở SQL Server Management Studio (SSMS), sau đó chạy file script:

```
QuanLyNhanSu.sql
```

Hoặc restore từ file backup:

```
QuanLyNhanSu.bak
```

### 3. Cấu hình chuỗi kết nối

Mở file cấu hình trong tầng **DB Layer** và cập nhật connection string phù hợp với SQL Server của bạn:

```csharp
string connectionString = "Server=TEN_SERVER;Database=QuanLyNhanSu;Integrated Security=True;";
```

### 4. Build và chạy ứng dụng

Mở file `QuanLyNhanSu_3Tang_ADO.sln` bằng Visual Studio 2022, build solution và chạy.

---

## Cấu trúc thư mục

```
.
├── BS Layer/                  # Business Logic Layer - xử lý nghiệp vụ
├── DB Layer/                  # Data Access Layer - truy vấn ADO.NET
├── Properties/                # Cấu hình project
├── Resources/                 # Tài nguyên (hình ảnh, icon)
├── frm*.cs                    # Các form giao diện (Presentation Layer)
├── QuanLyNhanSu.sql           # Script tạo database
├── QuanLyNhanSu.bak           # File backup database
└── QuanLyNhanSu_3Tang_ADO.sln # Solution file
```

---

## Tài khoản mặc định

| Vai trò | Tên đăng nhập | Mật khẩu |
|---|---|---|
| Quản trị viên | admin | *(xem trong database)* |
| Trưởng phòng | *(xem trong database)* | *(xem trong database)* |
| Nhân viên | *(xem trong database)* | *(xem trong database)* |

---

## So sánh với phiên bản Entity Framework

Repo này sử dụng **ADO.NET** — tức là viết trực tiếp câu lệnh SQL thủ công. Xem phiên bản sử dụng **Entity Framework** (ORM, code-first/database-first) tại:
[hr-management-winforms-ef](https://github.com/ventdejanvier/hr-management-winforms-ef)

| Tiêu chí | ADO.NET (repo này) | Entity Framework |
|---|---|---|
| Kiểm soát SQL | Toàn quyền | Tự động sinh |
| Hiệu năng | Cao hơn với query phức tạp | Tốt cho CRUD đơn giản |
| Khối lượng code | Nhiều hơn | Ít hơn |
| Độ linh hoạt | Cao | Trung bình |
