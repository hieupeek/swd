# EOF-OMS Context Diagram - Đánh giá ảnh cũ và bản chuẩn

> Hệ thống trung tâm: `EOF-OMS`
> Ảnh cũ: `OMSupdate5.jpg` / `[Image 1]`
> Quy ước: không dùng stereotype theo confirm của thầy, chỉ xét actor + flow + chiều + từ ngữ.

---

## I. Những thiếu sót của ảnh cũ

### 1. Tên actor sai ngữ pháp, không nhất quán

- `System Schedule` -> sai. `Schedule` là thời khóa biểu / động từ. Phải là `System Scheduler`.
- `Administrator` -> quá chung. Phải là `System Administrator` để phân biệt với `Accountant, Warehouse Operator`.
- `POS / Sales Software` -> sai thuật ngữ. `Software` không đếm được, không đặt tên hệ thống là Software. Phải là `Web Storefront / POS System` (thống nhất với báo cáo II.1) hoặc `POS / Sales System`.
- Cách viết slash không nhất quán: `POS / Sales Software` (cách 2 bên), `Accounting System/ ERP` (thiếu 1 cách), `Cancellation/Return Request` (dính liền).

### 2. Viết hoa lung tung

- `COD payment update, COD payment request, COD payment Information, Payment report` - lúc thường lúc hoa.
- Chuẩn phải Title Case hết: `COD Payment Update`, `COD Payment Request`, `COD Payment Information`, `Payment Report`.

### 3. Một tên dùng cho 2 việc khác nhau

- `Payment Request` vừa `Customer -> OMS` vừa `OMS -> Payment Gateway`. Việc 2 là OMS nhờ gateway trừ tiền, phải là `Payment Authorization Request`.
- `Payment Result` quá chung. Phải là `Payment Authorization Result`.
- `Order Request` (Customer) vs `Sales Order Request` (POS, Sales Staff): 3 tên cho cùng 1 khái niệm. Phải thống nhất là `Sales Order Request`, riêng Sales Staff là `Assisted Sales Order Request`.
- `System Setting Information` xuất hiện 2 lần cả chiều vào và ra Administrator. Không phân biệt request / trả về. Một chiều phải là `System Setting Request`.
- `Order Status Information` lặp ở 3 nơi (Customer, POS, Sales Staff) gây rối.

### 4. Gộp sai nghiệp vụ

- `Cancellation/Return Request`: Cancel trước giao và Return sau giao là 2 quy trình khác nhau (BR2 vs BR14), kho - kế toán xử lý khác nhau. Không gộp bằng `/`. Phải tách `Order Cancellation Request` và `Return Request`.
- `Order Information` vs `Order Status Information` vs `Order Update Request` của Sales Staff: 3 nhãn chung chung, không rõ khác nhau chỗ nào.

### 5. Từ quá chung, không kiểm chứng được

- `Delivery Order` phải là `Delivery Order Manifest` mới là chứng từ.
- `Shipment Request` không rõ xin gì. Phải là `Shipment Dispatch Request`.
- `Accounting Information` không rõ là gì. Phải là `Sales and Delivery Accounting Data`.
- `Inventory Information (OMS -> Warehouse Operator)` ngược logic và quá chung. Kho mới là người biết tồn. OMS chỉ gửi `Inventory Availability Update`, kho gửi lên `Inventory Audit Result`, không phải `Stock Check Information`.
- `Invoice Request / Invoice Information / Payment Information / COD payment Information` ở cụm Accountant: 4-5 nhãn chồng nghĩa, không phân biệt hóa đơn bán hàng vs đối soát COD.
- `Goods Receipt Confirmation` nên chuẩn hóa thành `Goods Receipt Confirmation` giữ nguyên hoặc `Stock Inbound Confirmation` cho rõ nhập kho.

### 6. Sai / thiếu chiều so với nghiệp vụ EOF-OMS

- `Payment report` đang vẽ chiều `Accounting System/ERP -> OMS`. Ngược. OMS mới là bên phát sinh đơn và giao hàng, phải gửi `Payment Report / Invoice` sang ERP. Chiều về nếu có phải là `Reconciliation Report`.
- `Payment Timeout Signal` của Scheduler: timeout cái gì? Trong hệ thống là hết hạn giữ chỗ 15 phút cho prepaid (BR8, BR37). Phải là `Order Expiration Signal`.
- Thiếu chiều về cho Customer: có `Cancellation/Return Request` đi mà không có `Return Authorization / Refund Status` về. Hiện chỉ có `Order Confirmation, Payment Status Information, Shipment Tracking Information`.
- Cụm Accountant 5 mũi tên chập vào nhau, không đọc được. Cần gom còn 2 chiều: đi `Invoice Generation Request, COD Reconciliation Request`, về `Sales Invoice, COD Settlement Data`.
- POS chỉ có vào/ra order, thiếu luồng đồng bộ `Inventory Availability Update` cho bán omni-channel.

### 7. Trình bày khó nhìn

- 4 mũi tên Customer -> OMS chập 1 điểm trên đỉnh vòng tròn, 5 mũi tên Accountant chập 1 điểm dưới đáy, nhãn đè nhau.
- Nhãn đặt xa mũi tên (cụm Administrator 4 đường song song, cụm 3PL, ERP), không biết nhãn nào của mũi tên nào.
- Thiếu luồng về cho Return, thừa luồng trùng lặp cho Order Status.

---

## II. Context chuẩn (dạng liệt kê, thay cho hình)

### 1. Customer

- Customer -> EOF-OMS:
  - Sales Order Request
  - Order Cancellation Request
  - Return Request
- EOF-OMS -> Customer:
  - Order Confirmation
  - Payment Status Information
  - Shipment Tracking Information
  - Refund Status Information

### 2. Web Storefront / POS System

- Web Storefront / POS System -> EOF-OMS:
  - Sales Order Request
- EOF-OMS -> Web Storefront / POS System:
  - Order Status Information
  - Inventory Availability Update

### 3. Sales Staff

- Sales Staff -> EOF-OMS:
  - Assisted Sales Order Request
- EOF-OMS -> Sales Staff:
  - Order Status Information

### 4. Warehouse Operator

- Warehouse Operator -> EOF-OMS:
  - Goods Receipt Confirmation
  - Goods Issue Confirmation
  - Inventory Audit Result
- EOF-OMS -> Warehouse Operator:
  - Delivery Order Manifest
  - Inventory Availability Update

### 5. Payment Gateway

- EOF-OMS -> Payment Gateway:
  - Payment Authorization Request
- Payment Gateway -> EOF-OMS:
  - Payment Authorization Result

### 6. System Scheduler

- System Scheduler -> EOF-OMS:
  - Order Expiration Signal
- EOF-OMS -> System Scheduler:
  - (không có)

### 7. System Administrator

- System Administrator -> EOF-OMS:
  - System Status Request
  - System Setting Request
- EOF-OMS -> System Administrator:
  - System Status Information
  - System Setting Update

### 8. 3PL Carrier System

- EOF-OMS -> 3PL Carrier System:
  - Shipment Dispatch Request
- 3PL Carrier System -> EOF-OMS:
  - Shipment Tracking Update
  - Delivery and COD Collection Confirmation

### 9. Accountant

- Accountant -> EOF-OMS:
  - Invoice Generation Request
  - COD Reconciliation Request
- EOF-OMS -> Accountant:
  - Sales Invoice
  - COD Settlement Data

### 10. Accounting / ERP System

- EOF-OMS -> Accounting / ERP System:
  - Sales and Delivery Accounting Data
- Accounting / ERP System -> EOF-OMS:
  - Reconciliation Report
