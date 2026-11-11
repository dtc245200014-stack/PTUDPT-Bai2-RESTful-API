# Bài 2: RESTful API với ASP.NET Core

## Mục tiêu

Xây dựng RESTful API quản lý danh mục sản phẩm, thực hành các phương thức HTTP, kiểm tra dữ liệu đầu vào và xử lý mã trạng thái HTTP.

## Catalog API

`Catalog.Api` cung cấp danh sách sản phẩm trong bộ nhớ, tra cứu theo ID và tạo sản phẩm mới. Dữ liệu khởi tạo gồm ba sản phẩm; dữ liệu tạo mới chỉ tồn tại trong phiên chạy hiện tại.

## Catalog Client

`Catalog.Client` là ứng dụng console dùng `HttpClient` để đọc danh sách, tạo sản phẩm hợp lệ, đọc chi tiết và gửi dữ liệu không hợp lệ nhằm minh họa phản hồi API.

## Công nghệ

- .NET 10 / ASP.NET Core Minimal API
- C# và `HttpClient`
- HTTP/JSON

## Cấu trúc

```text
PTUDPT-Bai2-RESTful-API/
├── Catalog/
│   ├── src/
│   │   ├── Catalog.Api/
│   │   └── Catalog.Client/
│   ├── CatalogApi.slnx
│   ├── requests.http
│   ├── sp-hop-le.json
│   ├── sp-sai.json
│   └── README.md
├── EduSubmit/
├── .gitignore
└── README.md
```

## Cài đặt và chạy

Cài .NET 10 SDK. Chạy lệnh từ thư mục gốc repository:

```powershell
dotnet restore Catalog/CatalogApi.slnx
dotnet build Catalog/CatalogApi.slnx
dotnet run --project Catalog/src/Catalog.Api/Catalog.Api.csproj --launch-profile http
```

API mặc định chạy tại `http://localhost:5100`. Mở terminal khác để chạy client:

```powershell
dotnet run --project Catalog/src/Catalog.Client/Catalog.Client.csproj
```

Có thể truyền URL API khác làm tham số đầu tiên cho client.

## Endpoint

| Phương thức | Đường dẫn | Mô tả |
|---|---|---|
| GET | `/` | Trạng thái API |
| GET | `/api/products` | Danh sách sản phẩm |
| GET | `/api/products/{id}` | Chi tiết sản phẩm |
| POST | `/api/products` | Tạo sản phẩm |

POST nhận JSON gồm `name`, `description`, `price`; tên không được để trống và giá phải lớn hơn 0.

## Kiểm thử bằng requests.http

Chạy API, sau đó mở `Catalog/requests.http` bằng REST Client của Visual Studio Code hoặc HTTP Client trong IDE. Gửi lần lượt các request để kiểm tra danh sách, chi tiết, ID không tồn tại/không hợp lệ, tạo mới và dữ liệu không hợp lệ. Tệp cũng có ví dụ thiếu Content-Type và phương thức PUT không được hỗ trợ.

## Mã trạng thái HTTP

- `200 OK`: đọc thành công.
- `201 Created`: tạo sản phẩm thành công; header `Location` trỏ tới tài nguyên mới.
- `400 Bad Request`: dữ liệu sản phẩm không hợp lệ.
- `404 Not Found`: không tìm thấy sản phẩm hoặc đường dẫn không khớp.
- `405 Method Not Allowed`: phương thức không được endpoint hỗ trợ.
- `415 Unsupported Media Type`: nội dung POST không có Content-Type JSON phù hợp.

## Kết quả kiểm thử

Chạy `dotnet restore Catalog/CatalogApi.slnx` và `dotnet build Catalog/CatalogApi.slnx` từ thư mục gốc để xác nhận restore và build thành công.
