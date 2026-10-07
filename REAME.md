# Lab 21 - Phân tích rủi ro AI qua case study thực tế

- **Họ và tên:** Lê Duy Bảo
- **Mã học viên:** 2A202602749
- **Lớp:** Track 1 - L34B
- **Ngành đã chọn:** Mobility / autonomous driving - AI trong di chuyển, xe tự hành

### 1. Industry Risk Snapshot

| Nội dung | Đánh giá của tôi và lý do |
| --- | --- |
| Những tác hại chính có thể xảy ra | Người đi bộ, người đi xe đạp và hành khách có thể bị thương khi xe bỏ sót vật cản hoặc di chuyển sai. Chủ xe và chủ tài sản có thể chịu thiệt hại do va chạm; người sử dụng bãi đỗ có thể bị cản trở lối đi. |
| Mức độ high-stakes | **Cao** - AI tham gia điều khiển chuyển động của xe trong không gian có con người và tài sản. Tốc độ đỗ xe thấp không loại trừ nguy cơ gây thương tích nghiêm trọng. |
| Dữ liệu nhạy cảm có thể được sử dụng | Hình ảnh khuôn mặt, biển số và người xung quanh; vị trí nhà ở, tuyến đường đỗ xe đã ghi nhớ và lịch sử sử dụng. |
| Nhu cầu human review | **Cao** - người lái kiểm tra vị trí đỗ, vật cản và điều kiện môi trường trước khi kích hoạt, giám sát theo hướng dẫn của sản phẩm và can thiệp khi bất thường. Đội kỹ thuật kiểm tra log, thử nghiệm tình huống nguy hiểm trước phát hành. Với chế độ không có người lái trong xe, cần xác minh cơ chế dừng an toàn và hỗ trợ từ người thật; human review không thay thế được cơ chế an toàn tức thời. |

### 2. Case study 1 - VinAI Touch2Park: rủi ro bỏ sót vật cản khi đỗ xe bằng camera

#### Brief Case

- Tổ chức / sản phẩm AI: VinAI / Touch2Park, thuộc nhóm SurroundSense.
- Thời gian, địa điểm / bối cảnh: Sản phẩm được VinAI giới thiệu trong thông cáo tại Hà Nội tháng 10/2024. Tình huống phân tích từ tài liệu được cung cấp là đỗ xe tại gara tối hoặc chỗ đỗ hẹp.
- AI được dùng để làm gì: Nhận biết không gian xung quanh và hỗ trợ tự động đỗ vào vị trí người lái chọn trên màn hình.
- Vấn đề hoặc sự kiện đáng chú ý: Mục A.1–A.2 của Problems Final Content.docx nêu nguy cơ sai lệch khoảng cách, điểm mù và suy giảm nhận biết khi thiếu sáng, chói sáng hoặc camera bị che bẩn. Đây là phân tích nguy cơ; các ví dụ người dùng trong tài liệu không có nguồn gốc đủ để xác nhận là sự cố Touch2Park.
- Số liệu có nguồn: VinAI công bố Touch2Park sử dụng 4 camera mắt cá, cung cấp góc nhìn 360°, theo thông cáo tháng 10/2024; đây là cấu hình liên quan trực tiếp đến rủi ro phụ thuộc hình ảnh, không phải tỷ lệ an toàn. Trong VinAI_Autoparking_CompareChart.xlsb.xlsx, sheet Performance_Safety, ô H60 và H62 đặt mục tiêu phát hiện đúng ≥90% và bỏ sót chỗ đỗ phù hợp <10% trong điều kiện môi trường kém. Đây là mục tiêu nhận biết chỗ đỗ, không phải kết quả thử nghiệm hay tỷ lệ bỏ sót người đi bộ; chưa có thời gian đo hoặc cỡ mẫu.
- **Nguồn:** [VinAI Wins “Smart Parking Innovation of the Year” For Touch2Park In 2024 AutoTech Breakthrough Awards Program](https://www.vinai.io/vinai-wins-smart-parking-innovation-of-the-year-for-touch2park-in-2024-autotech-breakthrough-awards-program/) - VinAI - ngày hiển thị 21/10/2024, nội dung thông cáo ghi 22/10/2024.
- Phân biệt bằng chứng và nhận định: Nguồn chính thức xác nhận cấu hình camera → suy luận nguy cơ va chạm nếu nhận biết thất bại và người lái không can thiệp. Chưa có bằng chứng sản phẩm đã gây va chạm, chưa chứng minh camera kém an toàn hơn cảm biến siêu âm.

#### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | Người lái kích hoạt đỗ xe trong gara thiếu sáng; một người hoặc vật cản ở gần quỹ đạo xe không được nhận biết kịp thời và xe tiếp tục di chuyển. |
| Stakeholder bị ảnh hưởng | Người đi bộ, trẻ em, người lái, hành khách, chủ xe bên cạnh, đơn vị vận hành bãi đỗ và VinAI/OEM tích hợp sản phẩm. |
| Failure mode | Over-reliance: người lái tin hệ thống quan sát toàn cảnh nên bỏ kiểm tra hoặc can thiệp chậm. Bỏ sót vật cản là lỗi nhận biết, không đủ căn cứ là hallucination. |
| Layer bắt đầu lỗi | Chưa đủ dữ liệu để đánh giá. Giả thuyết Model nếu nhận biết vật cản thất bại trong điều kiện ảnh kém; UX nếu giao diện khiến người lái hiểu sai mức độ an toàn. Chưa có log, dữ liệu thử nghiệm hoặc nghiên cứu UX để xác định lớp bắt đầu lỗi. |
| Harm xảy ra là gì? | Người đi bộ có thể bị thương khi xe tiếp tục di chuyển dù có người trên quỹ đạo; chủ xe hoặc chủ tài sản có thể chịu thiệt hại khi va chạm vật cản. Đây là nguy cơ, chưa có hậu quả thực tế của Touch2Park được xác minh trong nguồn. |
| Harm lens | Injury - tổn hại thể chất; kèm thiệt hại tài sản và chi phí khắc phục. |
| Severity | Critical đối với kịch bản va chạm gây thương tích nghiêm trọng; đây là mức hậu quả tiềm ẩn, không phải mức của một sự cố đã ghi nhận. |
| Scale | Chưa đủ dữ liệu để đánh giá. Một lần thao tác có thể ảnh hưởng người và tài sản quanh xe; nguồn không cung cấp số xe dùng Touch2Park hoặc số người bị ảnh hưởng. |
| Probability | Chưa đủ dữ liệu để đánh giá. Mục tiêu nhận biết chỗ đỗ trong bảng tính không cho phép suy ra xác suất va chạm hoặc bỏ sót người. |
| Frequency | Chưa đủ dữ liệu để đánh giá; không có số lần lỗi trên tổng số lần đỗ, số giờ vận hành hoặc khoảng thời gian quan sát. |
| Vì sao? | Chuyển động của xe có thể gây thương tích nên tôi đánh giá hậu quả tiềm ẩn ở mức Critical. Mục  tình huống ảnh kém và điểm mù; yêu cầu dự phòng khi phát hiện người. |

### 3. Case study 2 - VinAI Memorized Parking Assist: rủi ro khi môi trường khác tuyến đã ghi nhớ

#### Brief Case

- Tổ chức / sản phẩm AI: VinAI / Memorized Parking Assist.
- Thời gian, địa điểm / bối cảnh: Sản phẩm được nhắc trong thông cáo VinAI tháng 10/2024. Tình huống phân tích từ tài liệu là quay lại lối vào gara hoặc bãi đỗ quen thuộc sau khi có vật cản mới; không có thời gian, địa điểm của sự cố thực tế được xác minh.
- AI được dùng để làm gì: Ghi nhớ tuyến đỗ và tự động đi tới chỗ đỗ quen thuộc.
- Vấn đề hoặc sự kiện đáng chú ý:  nguy cơ khi xuất hiện xe đạp, xe đẩy hoặc thay đổi bố trí bãi đỗ trên tuyến đã lưu. Câu hỏi rủi ro là xe có dừng an toàn và yêu cầu người thật xử lý khi môi trường không còn phù hợp hay không.
- Số liệu có nguồn: Theo thông cáo VinAI tháng 10/2024, tuyến có thể được ghi nhớ sau 1 lần người lái thực hiện thủ công; số lần này mô tả bước học tuyến, không phải số thử nghiệm an toàn.
- Nguồn: [VinAI Wins “Smart Parking Innovation of the Year” For Touch2Park In 2024 AutoTech Breakthrough Awards Program](https://www.vinai.io/vinai-wins-smart-parking-innovation-of-the-year-for-touch2park-in-2024-autotech-breakthrough-awards-program/) - VinAI - ngày hiển thị 21/10/2024, nội dung thông cáo ghi 22/10/2024, Memorized Parking Assist.
- Phân biệt bằng chứng và nhận định: Nguồn chính thức xác nhận chức năng học tuyến → suy luận việc nhớ tuyến không đủ để bảo đảm tuyến vẫn an toàn ở lần sau. Chưa xác minh sự cố, khả năng tránh vật cản thực tế, cơ chế chuyển cho người lái hoặc việc sản phẩm phụ thuộc GPS.

#### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | Xe đi theo tuyến vào gara đã ghi nhớ, nhưng một trẻ em hoặc xe đạp vừa xuất hiện trên tuyến; hệ thống tiếp tục thao tác thay vì dừng an toàn khi không thể xác nhận đường đi còn phù hợp. |
| Stakeholder bị ảnh hưởng | Trẻ em, người đi bộ, người đi xe đạp, chủ xe, người nhà, chủ tài sản gần tuyến và đơn vị triển khai sản phẩm. |
| Failure mode | Escalation failure: giả thuyết hệ thống tiếp tục xử lý khi cần dừng và yêu cầu người thật can thiệp. Over-reliance: người dùng tin tuyến quen thuộc luôn an toàn nên giảm giám sát. |
| Layer bắt đầu lỗi | Chưa đủ dữ liệu để đánh giá. Giả thuyết Safety nếu hệ thống không dừng khi điều kiện vượt phạm vi vận hành; Model nếu nhận biết hoặc định vị thất bại trước đó. |
| Harm xảy ra là gì? | Trẻ em hoặc người đi bộ có thể bị thương khi xe tiếp tục chạy trên tuyến có vật cản mới; chủ xe có thể chịu hư hỏng khi xe va chạm xe đạp hoặc tài sản. Chưa có sự cố Memorized Parking Assist được xác minh trong nguồn. |
| Harm lens | Injury - tổn hại thể chất; kèm thiệt hại tài sản và chi phí sửa chữa. |
| Severity | Critical đối với tình huống xe va chạm hoặc chèn ép người. |
| Scale | Chưa đủ dữ liệu để đánh giá. Phạm vi trực tiếp là người và tài sản trên tuyến của từng xe; chưa có số xe triển khai, số tuyến hoặc số người bị ảnh hưởng. |
| Probability | Chưa đủ dữ liệu để đánh giá; không có tỷ lệ xử lý thành công vật cản mới hoặc tỷ lệ thất bại khi môi trường thay đổi. |
| Frequency | Chưa đủ dữ liệu để đánh giá; nguồn không có log số lần chạy tuyến, số lần yêu cầu can thiệp hay số sự cố trong một khoảng thời gian. |
| Vì sao? | Thay đổi môi trường là tình huống cần kiểm thử; mục tiêu dừng khi ra ngoài ODD, phù hợp với nguy cơ tiếp tục tự động hóa khi điều kiện không còn bảo đảm. Hậu quả có thể Critical nhưng không gán mức cao cho scale, probability hoặc frequency khi thiếu dữ liệu. |
