# AI Prompt Log - Xây dựng Tech Blog & Chiến lược Atomic Commit

## 1. Brainstorm: Chiến lược Atomic Commit & Quy chuẩn Conventional Commits
* **Câu hỏi của học viên:** 
  > *"Tôi đang xử lý file mã nguồn thô của Tech Blog (chứa các thẻ `div` phân vùng tổng quát). Hãy tư vấn chiến lược chia nhỏ tiến trình refactor thành các commit nguyên tử (Atomic Commits) độc lập, có ý nghĩa và tuân thủ chặt chẽ quy chuẩn Conventional Commits để tối ưu hóa khả năng kiểm soát lịch sử mã nguồn."*
* **Phản hồi từ AI & Đề xuất giải pháp:** 
  - **Phân tách các bước (Granularity):** Chia tiến trình thành 5 mốc rõ rệt: Khởi tạo mã nguồn thô (`init`), cấu trúc hóa phần đầu trang (`refactor(header)`), cấu trúc hóa phần nội dung chính (`refactor(main/section/article)`), cấu trúc chân trang (`refactor(footer)`), và tài liệu hóa (`docs`).
  - **Quy chuẩn Conventional Commits:** Sử dụng cấu trúc tiền tố rõ ràng `type: description` (ví dụ: `init:`, `refactor:`, `docs:`) giúp dễ dàng đọc hiểu lịch sử thay đổi và tự động hóa sinh tài liệu changelog.

---

## 2. Phản biện kỹ thuật: Vai trò của Snapshot Gốc & Staging Area
* **Câu hỏi của học viên:** 
  > *"Tại sao quy trình yêu cầu bắt buộc phải khởi tạo `git init` và thực hiện một commit thô ban đầu trước khi tiến hành sửa đổi? Hơn nữa, cơ chế của Staging Area (`git add`) hỗ trợ gì cho chiến lược Atomic Commit thay vì commit thẳng mọi thứ một lúc?"*
* **Phản hồi từ AI & Phân tích chuyên sâu:** 
  - **Snapshot Gốc (Base Baseline):** Cung cấp một điểm neo (checkpoint) sạch sẽ chứa mã nguồn legacy ban đầu, cho phép lập trình viên dễ dàng so sánh sự khác biệt (`git diff`) hoặc thực hiện lệnh quay lui (`git checkout / git reset`) khi cấu trúc mới phát sinh lỗi.
  - **Staging Area (`git add`):** Đóng vai trò là "bộ lọc trung gian", cho phép lập trình viên chủ động lựa chọn chính xác những dòng code hoặc tệp tin nào thuộc về logic thay đổi nào để đưa vào gói commit, đảm bảo tính nguyên tử (mỗi commit chỉ giải quyết một nhiệm vụ duy nhất).

---

## 3. Phân tích ngữ nghĩa: Phân định rạch ròi `<section>` và `<article>`
* **Câu hỏi của học viên:** 
  > *"Trong trang Tech Blog, cấu trúc chứa danh sách các bài viết bên trong một khối nội dung chính. Làm thế nào để phân định chính xác thời điểm nào nên sử dụng thẻ `<section>` và thời điểm nào nên sử dụng thẻ `<article>` để đảm bảo tính ngữ nghĩa (Semantics) và khả năng truy cập (Accessibility) đạt chuẩn W3C?"*
* **Phản hồi từ AI & Tiêu chuẩn kỹ thuật:** 
  - **Thẻ `<article>`:** Đại diện cho một khối nội dung độc lập, tự thân (self-contained composition), có thể phân phối hoặc tái sử dụng độc lập (mỗi bài đăng `.post` là một `<article>` hoàn chỉnh bao gồm tiêu đề, metadata và nội dung).
  - **Thẻ `<section>`:** Đại diện cho một vùng gom nhóm nội dung có chung chủ đề (thematic grouping of content), thường chứa một tiêu đề (`h1`-`h6`) bên trong. Khối bọc ngoài danh sách các bài viết chính là một `<section>` hoàn hảo.

---

## 4. Kiểm định chất lượng (QA) & Nghiên cứu mở rộng: Thẻ `<aside>` và W3C Validation
* **Câu hỏi của học viên:** 
  > *"Sau khi hoàn tất cấu trúc semantic, làm thế nào để thực hiện kiểm tra QA (Quality Assurance) tính hợp lệ của mã nguồn HTML? Ngoài ra, nếu trong tương lai tôi muốn tích hợp một thanh bên (sidebar) chứa các bài viết liên quan hoặc widget quảng cáo, tôi nên áp dụng thẻ ngữ nghĩa nào?"*
* **Phản hồi từ AI & Các bước kiểm thử:** 
  - **Quy trình QA HTML:** Kiểm tra tính toàn vẹn của cây phân cấp tiêu đề (Heading hierarchy từ `<h1>` đến `<h3>` không bị nhảy cóc bậc), kiểm tra các thẻ đóng/mở hợp lệ, và sử dụng công cụ W3C Markup Validation Service.
  - **Mở rộng với `<aside>`:** Thẻ `<aside>` được định nghĩa dành riêng cho các nội dung có liên quan gián tiếp hoặc phụ trợ so với nội dung chính xung quanh nó (như sidebar, mục lục, quảng cáo, author bio), giúp công cụ tìm kiếm và trình đọc màn hình hiểu rõ cấu trúc trang web hơn."