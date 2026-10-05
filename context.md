Kết luận: Actor đủ, nhưng từ ngữ + chiều luồng chưa chuẩn. Chưa dùng được.
1. Tên actor sai ngữ pháp
1. System Schedule -> sai. Schedule là thời khóa biểu / động từ xếp lịch. Phải là System Scheduler - hệ thống lập lịch.
2. Administrator -> quá chung. Trong hệ thống của bạn là System Administrator phân biệt với Accountant, Warehouse Operator. Để Administrator sẽ bị hỏi là admin gì.
3. POS / Sales Software -> sai thuật ngữ:
- Software không đếm được, không ai đặt tên hệ thống ngoài là Software. Phải là System.
- Không nhất quán cách viết slash: POS / Sales Software có 2 dấu cách, Accounting System/ ERP thiếu 1 dấu cách.
4. Accountant người vs Accounting System/ ERP máy để cạnh nhau nhưng tên gần giống nhau, dễ nhầm. Giữ nguyên được nhưng trong báo cáo phải định nghĩa rõ.
2. Từ ngữ, ngữ pháp của luồng
a. Viết hoa lung tung:
- COD payment update , COD payment request , COD payment Information , Payment report - lúc thường lúc hoa. Chuẩn phải Title Case hết: COD Payment Update, Payment Report.
- Cancellation/Return Request viết dính /, các chỗ khác viết  /  có cách.
b. Một tên dùng cho 2 việc khác nhau:
- Payment Request: vừa Customer -> OMS vừa OMS -> Payment Gateway. Hai việc khác nhau hoàn toàn: customer muốn trả tiền vs OMS nhờ gateway trừ tiền. Cái thứ 2 phải là Payment Authorization Request.
- Payment Result: quá chung. Phải là Payment Authorization Result.
- Order Request của Customer vs Sales Order Request của POS vs Sales Order Request của Sales Staff: 3 tên cho cùng 1 khái niệm. Phải thống nhất là Sales Order Request, hoặc tách rõ Assisted Sales Order Request cho Sales Staff.
- Order Status Information xuất hiện 3 lần: về Customer, về POS, về Sales Staff. Ở context được phép trùng, nhưng đang để 3 nhãn rời rạc gây rối.
- System Setting Information xuất hiện 2 lần chiều vào/ra Administrator. Không biết cái nào là request, cái nào là trả về. Một cái phải là System Setting Request.
c. Gộp sai nghiệp vụ:
- Cancellation/Return Request: Cancel trước giao hàng và Return sau giao hàng là 2 quy trình khác nhau, kho - kế toán xử lý khác nhau. Không được gộp bằng /.
- Order Information vs Order Status Information vs Order Update Request của Sales Staff: 3 nhãn chung chung, không biết khác nhau chỗ nào.
d. Từ quá chung, không kiểm được với hệ thống:
- Accounting Information, Inventory Information, Payment Information, Invoice Information, Order Information, Shipment Request, Delivery Order:
- Delivery Order phải là Delivery Order Document / Manifest mới là chứng từ.
- Shipment Request là xin gì? Phải là Shipment Dispatch Request.
- Accounting Information là gì? Phải là Sales and Delivery Accounting Data.
- Inventory Information OMS -> Warehouse Operator ngược logic: kho là người biết tồn kho, OMS phải gửi Inventory Availability Update, kho gửi lên Stock Audit Result chứ không phải Stock Check Information.
3. Không phù hợp với EOF-OMS
1. Payment report đang vẽ chiều Accounting System/ERP -> OMS. Ngược: OMS mới là bên phát sinh đơn, giao hàng, phải gửi Payment Report / Invoice sang ERP. Nếu ERP trả về thì phải là Reconciliation Report.
2. Payment Timeout Signal của Scheduler: timeout cái gì? Trong hệ thống bạn là hết hạn giữ chỗ 15 phút cho prepaid. Phải là Order Expiration Signal.
3. Thiếu chiều về cho Customer: có Cancellation/Return Request đi mà không có Return Authorization / Refund Status về. Chỉ có Order Confirmation, Payment Status Information, Shipment Tracking Information.
4. Cụm Accountant ở dưới 5 mũi tên chập vào nhau: Invoice Request, COD payment request đi lên, Invoice Information, Payment Information, COD payment Information đi xuống. Không phân biệt được hóa đơn bán hàng vs đối soát COD. Thực tế cần chỉ 2 luồng: Invoice Generation Request -> và <- Sales Invoice & COD Settlement Data.
5. POS chỉ có vào/ra order, thiếu luồng đồng bộ tồn kho / catalog cho bán omni-channel.
Sửa tối thiểu: System Schedule -> System Scheduler, Administrator -> System Administrator, thống nhất POS / Sales System, viết hoa lại 4 nhãn COD..., Payment report, tách Cancellation/Return, đổi Payment Request OMS->Gateway thành Payment Authorization Request, đổi Delivery Order thành Delivery Order Manifest, sửa chiều + tên Payment report, tách 2 nhãn System Setting Information trùng nhau.