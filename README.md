# 1. Cấu trúc mã và các best practices trong Angular  
## Hướng dẫn xây dựng dự án Angular dễ bảo trì và mở rộng

Việc xây dựng các ứng dụng Angular mạnh mẽ và có khả năng mở rộng đòi hỏi cần phải tổ chức mã một cách hợp lý và tuân thủ các best practices. Trong bài viết này, chúng ta sẽ cùng tìm hiểu các hướng dẫn và kỹ thuật quan trọng giúp bạn cấu trúc code Angular hiệu quả hơn. Làm đúng từ đầu sẽ giúp dự án dễ bảo trì, dễ đọc và mở rộng trong tương lai.

## 📦 Tổ chức Module

Nếu bạn sử dụng kiến trúc dựa trên module trong Angular, hãy tổ chức các module một cách hợp lý. Điều này giúp mã nguồn rõ ràng và dễ bảo trì hơn.

**Một số lưu ý:**
- Nhóm các thành phần (component), directive và service liên quan vào cùng một feature module.
- Tạo một `SharedModule` để chứa các thành phần, directive và pipe được dùng chung.
- Dùng **lazy loading** để tải module theo yêu cầu, cải thiện hiệu năng ứng dụng.

👉 Nếu bạn dùng **standalone component**, hãy chú trọng vào kiến trúc tổ chức hợp lý. Standalone giúp bạn linh hoạt hơn, nhưng bạn sẽ phải tự thiết kế cấu trúc. Tổ chức tốt sẽ mang lại khả năng **tái sử dụng code và mở rộng dễ dàng**.


## 🧩 Cấu trúc Component

Component là trung tâm trong Angular. Việc tổ chức component nhất quán giúp tăng tính dễ đọc và khả năng tái sử dụng.

**Best practices:**
- Mỗi file component nên chỉ đảm nhiệm một trách nhiệm (single responsibility).
- Tách riêng class, template và style ra các file khác nhau để dễ quản lý.
- Giữ component nhỏ và chuyên biệt. Khi quá lớn, hãy tách thành nhiều component nhỏ.
- Tận dụng các **lifecycle hooks** của Angular để xử lý khởi tạo và huỷ component.


## 🛠️ Services và Dependency Injection

Service cung cấp logic tái sử dụng và kết nối giữa các component.

**Lưu ý khi sử dụng:**
- Dùng hệ thống **Dependency Injection** của Angular để cung cấp và inject service.
- Service nên tập trung vào một chức năng cụ thể.
- Tránh viết quá nhiều logic trong service – hãy tuân thủ **nguyên lý đơn trách nhiệm (SRP)**.
- Tận dụng **phạm vi cung cấp** để chia sẻ service một cách tối ưu (ví dụ: module-level providers).


## 📁 Quy ước đặt tên file & thư mục

Quy ước đặt tên rõ ràng sẽ cải thiện khả năng đọc và bảo trì code.

**Tips:**
- Đặt tên mô tả cho file, thư mục và biến để dễ hiểu.
- Dùng định dạng nhất quán: `camelCase`, `kebab-case`, v.v.
- Thêm prefix mang ý nghĩa cho component, service, directive để tránh trùng lặp tên.

## 🗂️ Cấu trúc file và thư mục

Một cấu trúc thư mục tốt là nền tảng cho khả năng mở rộng và bảo trì. Dưới đây là ví dụ cấu trúc gợi ý cho ứng dụng Angular dựa trên module:

```
app/
├── core/
│   ├── constants/
│   ├── guards/
│   ├── interceptors/
│   ├── models/
│   └── services/
├── modules/
│   ├── feature1/
│   │   ├── components/
│   │   ├── services/
│   │   └── feature1.module.ts
│   └── feature2/
│       ├── components/
│       ├── services/
│       └── feature2.module.ts
├── shared/
│   ├── components/
│   ├── directives/
│   ├── pipes/
│   └── services/
├── app.component.ts
├── app.module.ts
├── app-routing.module.ts
├── app.component.html
├── app.component.scss
└── main.ts
```


## 🔁 RxJS và Observables

RxJS là thư viện mạnh mẽ để xử lý bất đồng bộ trong Angular. Angular tích hợp sẵn RxJS nên việc tận dụng là rất quan trọng.

**Best practices với RxJS:**
- Dùng các operator như `map`, `filter`, `switchMap` để xử lý stream dữ liệu.
- **Unsubscribe** khi không còn cần thiết để tránh rò rỉ bộ nhớ.
- Dùng **async pipe** trong template để tự động subscribe và unsubscribe.
- Tránh nested observable. Hãy dùng các operator như `switchMap`, `mergeMap`, `concatMap`, `combineLatest` tuỳ theo nhu cầu.

## ✅ Kết luận

Bằng cách áp dụng các nguyên tắc cấu trúc mã và best practices trong dự án Angular, bạn có thể:
- Cải thiện khả năng bảo trì
- Nâng cao tính rõ ràng
- Tăng khả năng mở rộng ứng dụng



# 2. **Cấu trúc file workspace và dự án**  

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
