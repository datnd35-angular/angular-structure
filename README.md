

**Cấu trúc file workspace và dự án**  

### **Workspace và dự án trong Angular**  
Bạn phát triển ứng dụng trong một **workspace Angular**. Workspace chứa các file cho một hoặc nhiều dự án. Một **dự án** là tập hợp các file tạo thành một ứng dụng hoặc một thư viện có thể chia sẻ.  

Lệnh `ng new` của Angular CLI sẽ tạo một workspace:  
```bash
ng new my-project
```  
Khi chạy lệnh này, CLI sẽ cài đặt các gói npm cần thiết cho Angular và các phụ thuộc khác vào một workspace mới, với một ứng dụng cấp gốc có tên là `my-project`.  

Theo mặc định, lệnh `ng new` tạo một ứng dụng khung xương ban đầu ở cấp gốc của workspace cùng với các bài kiểm thử end-to-end. Ứng dụng khung xương này là một ứng dụng chào mừng đơn giản, sẵn sàng để chạy và dễ dàng chỉnh sửa. Ứng dụng cấp gốc có cùng tên với workspace và các file nguồn nằm trong thư mục con `src/` của workspace.  

Hành vi mặc định này phù hợp với phong cách phát triển "multi-repo", nơi mỗi ứng dụng nằm trong một workspace riêng. Người mới bắt đầu và người dùng ở cấp trung bình được khuyến khích sử dụng lệnh `ng new` để tạo một workspace riêng cho từng ứng dụng.  

Angular cũng hỗ trợ workspace với nhiều dự án. Kiểu môi trường phát triển này phù hợp với những người dùng nâng cao đang phát triển các thư viện có thể chia sẻ và với các doanh nghiệp sử dụng phong cách phát triển "monorepo", với một kho lưu trữ duy nhất và cấu hình toàn cục cho tất cả các dự án Angular.  

Để thiết lập workspace dạng monorepo, bạn nên bỏ qua việc tạo ứng dụng cấp gốc. Xem phần **Thiết lập workspace đa dự án** bên dưới.

---

### **Các file cấu hình của Workspace**  
Tất cả các dự án trong một workspace sẽ dùng chung cấu hình. Mức cao nhất của workspace chứa các file cấu hình toàn workspace, cấu hình cho ứng dụng cấp gốc và các thư mục con chứa file nguồn cũng như file kiểm thử cho ứng dụng cấp gốc.

| **File cấu hình**         | **Mục đích**                                                                                     |
|---------------------------|--------------------------------------------------------------------------------------------------|
| `.editorconfig`            | Cấu hình cho các trình chỉnh sửa mã nguồn. Xem chi tiết tại [EditorConfig](https://editorconfig.org/). |
| `.gitignore`               | Chỉ định các file không cần theo dõi mà Git sẽ bỏ qua.                                          |
| `README.md`                | Tài liệu hướng dẫn cho workspace.                                                              |
| `angular.json`             | Cấu hình CLI cho tất cả dự án trong workspace, bao gồm cách build, serve và test từng dự án.   |
| `package.json`             | Cấu hình các gói npm mà tất cả dự án trong workspace đều có thể sử dụng.                       |
| `package-lock.json`        | Cung cấp thông tin phiên bản của các gói đã cài đặt vào `node_modules` bởi npm.                |
| `src/`                     | Chứa các file nguồn cho dự án cấp gốc.                                                         |
| `public/`                  | Chứa hình ảnh và các file tài nguyên khác được phục vụ dưới dạng file tĩnh.                    |
| `node_modules/`            | Các gói npm được cài đặt cho toàn bộ workspace. Các phụ thuộc ở đây đều có thể dùng cho mọi dự án. |
| `tsconfig.json`            | File cấu hình TypeScript cơ bản cho các dự án trong workspace. Tất cả file cấu hình khác kế thừa từ đây. |

---

### **Các file của dự án ứng dụng**  
Theo mặc định, lệnh `ng new my-app` tạo một thư mục workspace có tên "my-app" và tạo một ứng dụng khung xương mới trong thư mục `src/` ở cấp cao nhất của workspace. Ứng dụng mới tạo sẽ chứa các file nguồn cho một module gốc, với một component và template gốc.

Khi cấu trúc file của workspace đã được thiết lập, bạn có thể sử dụng lệnh `ng generate` trên dòng lệnh để thêm tính năng và dữ liệu vào ứng dụng. Ứng dụng cấp gốc ban đầu này sẽ là ứng dụng mặc định cho các lệnh CLI (trừ khi bạn thay đổi ứng dụng mặc định sau khi tạo thêm các ứng dụng khác).

---

### **Các file nguồn của ứng dụng**  
Các file ở mức cao nhất của thư mục `src/` hỗ trợ chạy ứng dụng. Các thư mục con chứa mã nguồn và cấu hình dành riêng cho ứng dụng.

| **File hỗ trợ ứng dụng**    | **Mục đích**                                                                                   |
|----------------------------|------------------------------------------------------------------------------------------------|
| `app/`                      | Chứa các file component định nghĩa logic và dữ liệu của ứng dụng.                             |
| `favicon.ico`               | Biểu tượng sử dụng cho ứng dụng khi hiển thị trên thanh đánh dấu trang.                       |
| `index.html`                | Trang HTML chính được phục vụ khi truy cập vào ứng dụng.                                      |
| `main.ts`                   | Điểm vào chính của ứng dụng.                                                                  |
| `styles.css`                | CSS toàn cục áp dụng cho toàn bộ ứng dụng.                                                   |

---

### **Cấu trúc file cho workspace đa dự án**  
Một workspace đa dự án phù hợp với tổ chức sử dụng một kho lưu trữ và cấu hình toàn cục cho nhiều dự án Angular (mô hình "monorepo"). Workspace đa dự án cũng hỗ trợ phát triển thư viện.

---

Nếu cần thêm chi tiết hoặc chỉnh sửa phần nào, cứ nói nhé!
