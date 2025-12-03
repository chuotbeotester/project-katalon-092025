# 🚀 AUTOMATION TESTING FINAL PROJECT

![Status](https://img.shields.io/badge/Status-Active-success)
![Type](https://img.shields.io/badge/Type-Hybrid%20Framework-blue)
![Target](https://img.shields.io/badge/Target-WebUI%20%26%20API-orange)

Dự án này là bài tập cuối khóa, tập trung vào việc xây dựng Framework Automation Test kết hợp giữa **API Testing** và **WebUI Testing**. Dự án áp dụng mô hình Data-Driven và tổ chức Test Case theo cấu trúc khoa học, dễ bảo trì.

## 🌐 Hệ thống kiểm thử (AUT)

* **Website:** [https://book.anhtester.com/](https://book.anhtester.com/) 
* **Mô tả:** Hệ thống quản lý sách (Book Management).

---

## 📂 Yêu cầu Kỹ thuật (Requirements)

Dự án tuân thủ nghiêm ngặt các tiêu chuẩn sau:

1.  **Cấu trúc Project:** Tổ chức khoa học, rõ ràng. Phân chia Test Case thành 2 loại folder riêng biệt:
    * 📂 **Function Test Case:** Chứa các bước thực thi hành động.
    * 📂 **Assertion Test Case:** Chứa các bước kiểm tra (Verify/Assert).
    * **NOTE** : 2 loại test case trên chỉ là tối thiểu phải có, có thể tạo thêm folder loại test case khác nếu cần 
2.  **Data-Driven:** Sử dụng dữ liệu động. Mỗi lần thực thi (execute) là một bộ dữ liệu độc lập, không tái sử dụng dữ liệu cũ.
3.  **Execution:** File thực thi chính phải là **Test Suite Collection**.

---

## 🧪 Danh sách Kịch bản kiểm thử (Test Scenarios)

### 🟢 Test Suite 01: Tạo tài khoản & Thay đổi thông tin
*Mục tiêu: Kiểm tra luồng tạo mới và cập nhật thông tin người dùng (Avatar, Phone, Address).*

| ID | Loại | Mô tả Test Case | Chi tiết |
|:---|:---:|:---|:---|
| **TC1** | `API` | **Tạo tài khoản mới** | Endpoint: `/api/register`. Tạo dữ liệu với 3 trường bắt buộc. |
| **TC2** | `WebUI` | **Đăng nhập** | Đăng nhập thành công với tài khoản vừa tạo ở TC1. |
| **TC3** | `WebUI` | **Bổ sung thông tin** | Cập nhật 3 thông tin: Avatar image, Phone, Address (Division, Ward, Address). |
| **TC4** | `WebUI` | **Kiểm tra hiển thị** | 1. Check màn hình *User Management*: Hiển thị đúng Name (gồm name & email), Phone, Address.<br>2. Check Avatar: Vào `File` -> `$avatar-image` -> `<email>` -> Rename ảnh giống tên file upload -> Copy đường dẫn ảnh. |
| **TC5** | `API` | **Verify thông tin** | Endpoint: `/api/me`. Kiểm tra response khớp với data đã đổi (name, email, avatarUrl, phone, address). |

### 🟡 Test Suite 02: Inactive tài khoản người dùng
*Mục tiêu: Kiểm tra chức năng khóa tài khoản và hiển thị trạng thái.*

| ID | Loại | Mô tả Test Case | Chi tiết |
|:---|:---:|:---|:---|
| **TC1** | `API` | **Tạo dữ liệu mẫu** | Endpoint: `/api/register`. Tạo 03 tài khoản mới (chỉ 3 trường bắt buộc). |
| **TC2** | `API` | **Lấy AccessToken** | Endpoint: `/api/login`. Đăng nhập để lấy token chuẩn bị cho TC3. |
| **TC3** | `API` | **Lấy ID tài khoản** | Endpoint: `/api/me`. Kiểm tra thông tin và lấy `id` của các account vừa tạo. |
| **TC4** | `API` | **Khóa tài khoản** | Endpoint: `/api/user/{id}` (Method: `PATCH`). Đổi `isActive = false` cho 2/3 tài khoản. |
| **TC5** | `API` | **Check Đăng nhập** | Endpoint: `/api/login`. Thử đăng nhập lại với 3 tài khoản để kiểm tra chặn/cho phép truy cập. |
| **TC6** | `WebUI` | **Verify hiển thị** | Màn hình *User Management*: Kiểm tra 2 trường Name (name & email) và trạng thái **Active** của các tài khoản. |

### 🔵 Test Suite 03: Thay đổi mật khẩu
*Mục tiêu: Đảm bảo chức năng đổi mật khẩu hoạt động đúng trên cả Web và API.*

| ID | Loại | Mô tả Test Case | Chi tiết |
|:---|:---:|:---|:---|
| **TC1** | `API` | **Tạo tài khoản** | Endpoint: `/api/register`. Tạo dữ liệu với 3 trường bắt buộc. |
| **TC2** | `WebUI` | **Đăng nhập** | Đăng nhập thành công với tài khoản vừa tạo. |
| **TC3** | `WebUI` | **Đổi mật khẩu** | Thực hiện chức năng Change Password trên giao diện. |
| **TC4** | `API` | **Verify mật khẩu** | Endpoint: `/api/login`. Kiểm tra đăng nhập với 2 mật khẩu (Cũ & Mới) để xác nhận kết quả. |

---