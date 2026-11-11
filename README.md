# Bài 2: RESTful API với ASP.NET Core

Repository gồm hai phần thực hành độc lập: Catalog API quản lý sản phẩm và EduSubmit API quản lý bài tập/lượt nộp. Cả hai dùng ASP.NET Core Minimal API, .NET 10 và dữ liệu trong bộ nhớ.

## Catalog

`Catalog/` cung cấp Minimal API và console client. API quản lý danh sách sản phẩm trong bộ nhớ, tra cứu theo ID và tạo sản phẩm mới. Dữ liệu khởi tạo gồm ba sản phẩm; dữ liệu tạo mới chỉ tồn tại trong phiên chạy hiện tại. Client dùng `HttpClient` để đọc danh sách, tạo sản phẩm hợp lệ, đọc chi tiết và gửi dữ liệu không hợp lệ.

### Endpoint Catalog

| Phương thức | Đường dẫn | Mô tả |
|---|---|---|
| GET | `/` | Trạng thái API |
| GET | `/api/products` | Danh sách sản phẩm |
| GET | `/api/products/{id}` | Chi tiết sản phẩm |
| POST | `/api/products` | Tạo sản phẩm |

POST nhận JSON gồm `name`, `description`, `price`; tên không được để trống và giá phải lớn hơn 0.

### Chạy Catalog

Cài .NET 10 SDK. Chạy lệnh từ thư mục gốc repository:

```powershell
dotnet restore Catalog/CatalogApi.slnx
dotnet build Catalog/CatalogApi.slnx
dotnet run --project Catalog/src/Catalog.Api/Catalog.Api.csproj --launch-profile http
```

Catalog API mặc định chạy tại `http://localhost:5100`. Mở terminal khác để chạy client:

```powershell
dotnet run --project Catalog/src/Catalog.Client/Catalog.Client.csproj
```

Có thể truyền URL API khác làm tham số đầu tiên cho client. Mở `Catalog/requests.http` bằng REST Client của VS Code hoặc HTTP Client trong IDE để kiểm tra các trường hợp thành công và lỗi. Xem thêm [Catalog/README.md](Catalog/README.md).

## EduSubmit

`EduSubmit/` là phần Client - Server của bài thực hành. Minimal API cung cấp danh sách bài tập và tạo/đọc/xóa lượt nộp; console client dùng `HttpClient`. Dữ liệu lượt nộp chỉ lưu trong List RAM của tiến trình API.

```powershell
dotnet restore EduSubmit/RestfulClientServer.slnx
dotnet build EduSubmit/RestfulClientServer.slnx
dotnet run --project EduSubmit/src/Submission.Api/Submission.Api.csproj --urls http://localhost:5000
```

API chạy tại `http://localhost:5000`. Mở PowerShell khác để chạy Client:

```powershell
dotnet run --project EduSubmit/src/Submission.Client/Submission.Client.csproj
```

Hướng dẫn đầy đủ, hợp đồng API, curl/PowerShell và các thử nghiệm xem [EduSubmit/README.md](EduSubmit/README.md). Mở `EduSubmit/requests.http` bằng REST Client/HTTP Client để gửi request mẫu.
