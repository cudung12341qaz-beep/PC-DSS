# Kịch bản thuyết trình PC-DSS — Nhóm 11

File nguồn có 19 slide. Thời lượng slide tham khảo: 12 phút 05 giây, thêm 1–2 phút demo.

## Cần xác nhận trước khi trình bày

- Bộ số liệu dùng trong kịch bản theo xác nhận mới nhất ngày 12/10/2026 của nhóm: Manual UI 79/79 Pass, Postman API thủ công 50/50 Pass, Playwright 50/50 Pass. Kết quả Runner/Newman theo PPT: mỗi lần 257 Pass, 0 Fail/Skipped/Errors.
- Đã thay ghi chú cũ 77 Pass/2 Fail bằng kết quả mới nhóm xác nhận. Chuẩn bị workbook và minh chứng retest cho TC-STATE-001, TC-UI-006 nếu cô hỏi lịch sử hai ca này; không tự tạo ngày sửa, Bug ID hoặc chi tiết chạy lại.
- Word cuối đã gửi trước đó vẫn ghi Manual 80 ca, API thủ công 20 Pass/30 chưa chạy và Playwright chưa chạy; cần đồng bộ Word với Excel/report mới nhất trước khi nộp.
- Runner Pass không thay kết quả API thủ công. Playwright Pass không tự thay retest Manual UI. Số lượng testcase khác số assertion.
- Slide 15–16: nhóm đã xác nhận Playwright 50 Pass; cập nhật Word còn ghi chưa chạy và chuẩn bị report thật. Chrome và 2,4 phút vẫn cần đối chiếu report.
- PPT có 19 slide. Vị trí các trang khác bản ảnh cũ: trang 11–14 hiện là nhóm Postman, API thủ công, script và Runner/Newman; Playwright ở trang 15, tổng hợp ở trang 16.

## Slide 1. Trang bìa — 20 giây

Em chào cô và các bạn. Nhóm 11, lớp 23CN2 xin trình bày đề tài kiểm thử thủ công và tự động hệ thống hỗ trợ lựa chọn cấu hình máy tính PC-DSS bằng Postman và Playwright, dưới sự hướng dẫn của cô ThS. Nguyễn Thị Hạnh. Trọng tâm bài trình bày là cách nhóm thiết kế testcase, thực hiện kiểm thử và đánh giá kết quả theo minh chứng.

**Chuyển ý:** Trước hết, em xin giới thiệu bố cục bài trình bày.

**Lưu ý:**
- Không cần đọc lại toàn bộ tên và mã sinh viên. Nói rõ đây là đề tài môn kiểm thử; PC-DSS là đối tượng thực hành.

## Slide 2. Nội dung trình bày — 20 giây

Bài trình bày gồm bốn phần. Phần đầu giới thiệu hệ thống và mục tiêu kiểm thử. Phần hai trình bày yêu cầu và cách thiết kế các ca. Phần ba là quá trình kiểm thử thủ công, API với Postman và giao diện với Playwright. Cuối cùng, nhóm tổng hợp kết quả, giới hạn của bộ kiểm thử và hướng phát triển.

**Chuyển ý:** Em xin bắt đầu với đối tượng và mục tiêu kiểm thử.

**Lưu ý:**
- Giới thiệu mạch bài, không đọc hết các câu hỏi nhỏ trên slide.

## Slide 3. Đối tượng và mục tiêu kiểm thử — 35 giây

PC-DSS hỗ trợ lựa chọn các cấu hình máy tính đã có trong catalog. Người dùng chọn nhu cầu Gaming hoặc Rendering, khoảng ngân sách và số lượng gợi ý Top 1 đến Top 3. Hệ thống lọc các cấu hình đủ điều kiện, dự đoán điểm và xếp hạng kết quả. Nhóm sử dụng hệ thống này để kiểm tra chức năng có đúng đặc tả hay không, phát hiện sai lệch và ghi nhận kết quả có minh chứng. Phần kiểm thử không dùng để chứng minh độ chính xác benchmark của mô hình.

**Chuyển ý:** Để xác định nơi cần kiểm tra, nhóm xem xét kiến trúc hệ thống.

**Lưu ý:**
- Dùng “cấu hình PC trong catalog” để tránh hiểu rằng hệ thống tự lắp mọi tổ hợp linh kiện.

## Slide 4. Các thành phần được kiểm thử — 35 giây

Luồng chính đi từ giao diện React đến API ASP.NET Core, sau đó backend sử dụng dữ liệu CSV và tệp mô hình để xử lý. Người dùng thao tác và xem kết quả ở giao diện; API nhận request rồi trả response. Nhóm kiểm thử giao diện bằng tay và Playwright, đồng thời dùng Postman kiểm tra API trực tiếp. Cách tách này giúp kiểm tra cả dữ liệu trả về lẫn cách frontend hiển thị dữ liệu đó.

**Chuyển ý:** Các công nghệ và công cụ có vai trò cụ thể như sau.

**Lưu ý:**
- Chỉ lần lượt theo các mũi tên. Sơ đồ kiến trúc không phải ảnh minh chứng một lần chạy kiểm thử. CSV là dữ liệu; tệp mô hình phục vụ dự đoán khi được backend sử dụng.

## Slide 5. Công nghệ và công cụ sử dụng — 25 giây

React và ASP.NET Core là công nghệ xây dựng hệ thống. CSV và tệp mô hình cung cấp dữ liệu cùng thông tin phục vụ dự đoán. Về kiểm thử, Postman giúp gửi request và kiểm tra response; Newman thực thi Collection bằng dòng lệnh; Playwright điều khiển trình duyệt và kiểm tra các luồng sử dụng. Postman và Playwright là công cụ, còn hộp đen là cách tiếp cận kiểm thử mà nhóm áp dụng chủ yếu.

**Chuyển ý:** Trước khi sử dụng công cụ, nhóm cần xác định kết quả mong đợi.

**Lưu ý:**
- Không đọc từng ô trong bảng. “Xác thực đầu vào” ở đây nên giải thích là kiểm tra tính hợp lệ của dữ liệu, tránh nhầm với đăng nhập/xác thực người dùng.

## Slide 6. Yêu cầu và kết quả mong đợi — 45 giây

Nhóm xác định năm yêu cầu chính để đánh giá đúng sai: nhu cầu, khoảng giá, số lượng gợi ý, thứ tự kết quả và tiền còn lại. Giá PC phải nằm trong khoảng đã chọn. Số kết quả không vượt quá Top và có thể ít hơn nếu không đủ cấu hình hợp lệ. Thứ tự ưu tiên điểm dự đoán giảm dần, sau đó giá thấp hơn khi bằng điểm. Số tiền còn lại phải bằng ngân sách trừ giá máy, tính theo đồng. Đây là căn cứ để viết Expected Result trước khi thực hiện testcase.

**Chuyển ý:** Từ những yêu cầu đó, nhóm lựa chọn phương pháp và chuẩn bị môi trường.

**Lưu ý:**
- Phân biệt quy tắc PcId có trên slide với việc đã kiểm thử nó: báo cáo nêu chưa có fixture riêng cho trường hợp cùng điểm và cùng giá. Không nói bộ test đã bao phủ mọi tie-break.

## Slide 7. Phương pháp và môi trường kiểm thử — 35 giây

Nhóm chủ yếu kiểm thử hộp đen, tức là đưa đầu vào và kiểm tra đầu ra theo đặc tả mà không cần dựa vào đường đi bên trong code. Môi trường được trình bày gồm frontend ở cổng 5173, backend ở cổng 5170 và snapshot 36 PC. Sau khi thực thi, ca đúng kỳ vọng được ghi Pass; sai kỳ vọng được ghi Fail. Blocked dùng khi môi trường hoặc điều kiện trước khiến nhóm chưa thể thực thi hay kết luận ca đó.

**Chuyển ý:** Tiếp theo là các kỹ thuật giúp lựa chọn dữ liệu kiểm thử.

**Lưu ý:**
- 36 PC là số liệu của snapshot, không phải số lượng bắt buộc ở mọi phiên bản. Nếu backend dừng vì lỗi phần mềm đã tái hiện thì cần ghi nhận lỗi; không tự chuyển mọi lỗi backend thành Blocked.

## Slide 8. Kỹ thuật thiết kế ca kiểm thử — 45 giây

Phân vùng tương đương giúp nhóm chọn các đại diện cho dữ liệu hợp lệ và không hợp lệ, như Gaming, Rendering so với purpose không được hỗ trợ hoặc null. Phân tích giá trị biên tập trung vào các giới hạn dễ sai, chẳng hạn TopCount hoặc giá PC đúng cận và lệch một đồng. Ví dụ PM-023 đặt hai cận bằng 14.280.000 đồng, bằng giá PC-031; kết quả mong đợi là cấu hình này vẫn được chọn. Các quy tắc lọc và xếp hạng cũng được đối chiếu riêng.

**Chuyển ý:** Sau bước thiết kế, nhóm thực hiện trước các ca trên giao diện.

**Lưu ý:**
- PM-023 trên slide là ví dụ kiểm tra hai cận có tính bao gồm. Chỉ gọi đây là kết quả thực tế nếu minh chứng ca tương ứng xác nhận. Ba kỹ thuật được chọn để minh họa, không phải toàn bộ bộ test chỉ có ba kỹ thuật.

## Slide 9. Kiểm thử giao diện thủ công — 40 giây

Trong kiểm thử giao diện thủ công, người kiểm thử thực hiện các bước như người dùng thật: điều hướng, chọn nhu cầu, khoảng giá, Top và gửi yêu cầu. Sau đó nhóm quan sát kết quả, thông báo lỗi và cách hiển thị để đối chiếu với Expected Result. Kết quả và ảnh minh chứng được ghi theo từng testcase trong Excel. Theo kết quả mới nhất nhóm xác nhận, cả 79 ca đều Pass. Việc lưu theo mã ca giúp truy vết khi có sai lệch và thực hiện retest sau khi sửa.

**Chuyển ý:** Slide tiếp theo minh họa cách nhóm đối chiếu một testcase cụ thể.

**Lưu ý:**
- Nhóm xác nhận mới nhất 79/79 Pass. Chuẩn bị workbook ghi trạng thái từng ca. Với hai ca từng Fail là TC-STATE-001 và TC-UI-006, chuẩn bị minh chứng retest để giải thích sự thay đổi trạng thái; kịch bản không tự tạo ngày sửa, Bug ID hoặc kết quả chạy lại.

## Slide 10. Ví dụ kiểm thử giao diện — 40 giây

Ví dụ này là TC-REC-G-001 với nhu cầu Gaming, khoảng từ 10 đến dưới 15 triệu và Top 3. Ảnh minh chứng cho thấy có 4 cấu hình đủ điều kiện trong snapshot và giao diện hiển thị 3 cấu hình. Người kiểm thử đối chiếu số card, giá và thứ hạng. Giá 14.790.000 đồng và 14.680.000 đồng đều nằm trong khoảng đã chọn; điểm hiển thị lần lượt 8849,3, 6600,3 và 5513,0, được sắp giảm dần. Các điều kiện này là căn cứ đánh giá ca ví dụ.

**Chuyển ý:** Để kiểm tra trực tiếp lớp xử lý phía sau giao diện, nhóm dùng Postman.

**Lưu ý:**
- Chỉ vào số ứng viên, ba card và điểm giảm dần. Một ảnh minh chứng không tự xác nhận toàn bộ bộ Manual UI đã Pass.

## Slide 11. Các nhóm kịch bản Postman — 40 giây

Bộ Postman gồm 50 testcase, từ PM-001 đến PM-050. Nhóm chia theo chức năng: trạng thái API, danh mục PC, dự đoán và gợi ý cấu hình. Trong Recommendation có các ca về khoảng giá, mặc định, Top, biên giá, xếp hạng, tiền còn lại và đầu vào sai. Cách nhóm theo mục tiêu giúp theo dõi phạm vi bộ test và tránh bỏ sót các nhóm điều kiện quan trọng. Cùng bộ 50 ca này được dùng cho cả kiểm thử thủ công và tự động hóa.

**Chuyển ý:** Em xin minh họa cách thực hiện một ca API thủ công.

**Lưu ý:**
- Không đọc toàn bộ chín hàng. API không kiểm tra đủ 14 tổ hợp nhu cầu × khoảng giá: PM-011–017 là Gaming ở 7 khoảng, PM-018 là Rendering ở một khoảng. Không cộng chạy thủ công và tự động thành 100 testcase.

## Slide 12. Kiểm thử API thủ công bằng Postman — 60 giây

Khi kiểm thử API thủ công, người kiểm thử chuẩn bị request, bấm Send, đọc response và tự đối chiếu các điều kiện trước khi ghi Excel. PM-029 kiểm tra công thức tiền còn lại. Với ngân sách 34.999.999 đồng, PC-042 có giá 31.980.000 đồng nên tiền còn lại phải là 3.019.999 đồng, khớp giá trị phản hồi trong ví dụ. Tương tự, PC-045 còn 19.999 đồng và PC-044 còn 6.519.999 đồng. Theo kết quả mới nhất nhóm xác nhận, cả 50 ca API thủ công đều Pass. Kết quả thủ công được ghi nhận riêng, không suy ra từ chạy tự động.

**Chuyển ý:** Nhóm có thể mã hóa chính điều kiện đó để kiểm tra tự động.

**Lưu ý:**
- Chỉ vào ngân sách, giá, tiền còn lại và dòng response của PC-042. Các phép tính trong bảng khớp nhau. Nhóm xác nhận API thủ công 50/50 Pass; chuẩn bị Excel và minh chứng từng ca. Word cuối còn ghi 20 Pass/30 chưa chạy cần đồng bộ theo kết quả mới nhất.

## Slide 13. Tự động hóa kiểm thử API — 50 giây

Đoạn script minh họa chạy sau khi nhận response. Dòng đầu đọc JSON thành dữ liệu. pm.test tạo phép kiểm tra có tên; pm.expect đối chiếu điều kiện. Trước hết script yêu cầu items là một danh sách không rỗng để tránh Pass khi không có kết quả. Sau đó nó duyệt từng cấu hình và so sánh budgetRemainingVnd với ngân sách trừ giá PC. Nếu điều kiện sai, phép kiểm tra báo Fail để nhóm xem thông báo và tìm nguyên nhân. Cách này giúp chạy lại cùng điều kiện nhanh và nhất quán.

**Chuyển ý:** Sau khi viết script, nhóm thực thi Collection và xem báo cáo tổng hợp.

**Lưu ý:**
- Không đọc từng dấu ngoặc. Đoạn code là ví dụ minh họa điều kiện PM-029, không phải ảnh minh chứng một lần chạy mới. Với ca kỳ vọng danh sách rỗng, phải dùng assertion khác; không áp dụng “not.empty” cho mọi request. Một pm.test có thể chứa nhiều phép so sánh; không đếm 257 từ số dòng code trên slide.

## Slide 14. Kết quả Postman Runner và Newman — 45 giây

Collection là bộ request API kèm dữ liệu và script kiểm tra. Nhóm thực thi Collection bằng Runner trong Postman và bằng Newman ở dòng lệnh. Slide tổng hợp hai lần chạy riêng, mỗi lần ghi 257 phép kiểm tra đạt và không có thất bại, bỏ qua hoặc lỗi. Bộ nghiệp vụ vẫn gồm 50 testcase; một testcase có thể kiểm tra nhiều điều kiện. Vì vậy 257 là số phép kiểm tra, không phải số testcase, và hai lần chạy không được cộng thành hai bộ testcase độc lập.

**Chuyển ý:** Bên cạnh API, nhóm xây dựng bộ tự động hóa cho giao diện bằng Playwright.

**Lưu ý:**
- Chuẩn bị report Runner và Newman riêng khi cô yêu cầu. HTTP 400/404/415 vẫn có thể Pass nếu đúng Expected Result. Không cộng 257 + 257 thành 514 testcase; không dùng thời gian một lần chạy làm thời gian của lần khác.

## Slide 15. Kiểm thử giao diện tự động bằng Playwright — 55 giây

Bộ Playwright gồm 50 testcase: 8 ca nền tảng cho trang chủ, điều hướng, nhu cầu, dữ liệu nhập và trạng thái; 42 ca còn lại tạo từ 2 nhu cầu, 7 khoảng giá và 3 lựa chọn Top. Playwright điều khiển trình duyệt thực hiện lựa chọn, gửi yêu cầu qua giao diện và kiểm tra kết quả theo kịch bản. Theo kết quả mới nhất nhóm xác nhận, cả 50 ca đều Pass. Bộ này tự động hóa một phần tình huống Manual UI và mở rộng các tổ hợp, nên không ánh xạ một-một với toàn bộ bộ thủ công.

**Chuyển ý:** Sau các hình thức thực hiện, nhóm tổng hợp kết quả riêng từng bộ.

**Lưu ý:**
- Nhóm đã xác nhận Playwright đã chạy và 50 ca đều Pass trong lượt làm việc này. Chuẩn bị report PC-DSS thật để minh chứng và cập nhật Word đang ghi “chưa chạy”. Chrome và 2,4 phút cần đối chiếu report trước khi nói. Report 6 ca example.spec.js không chứng minh bộ 50 ca PC-DSS. Chỉ khẳng định kịch bản đối chiếu request/response nếu đã đối chiếu script thực tế.

## Slide 16. Tổng hợp kết quả kiểm thử — 45 giây

Theo kết quả mới nhất nhóm xác nhận, Manual UI có 79 ca Pass; API thủ công có 50 ca Pass; Playwright có 50 ca Pass. Runner và Newman thực thi cùng bộ 50 ca API, mỗi lần ghi 257 phép kiểm tra đạt. Nhóm báo riêng từng bộ vì chúng có những tình huống liên quan hoặc trùng nhau. Kết quả thủ công lấy từ ghi nhận riêng; số testcase không được cộng với số assertion. Các kết quả Pass xác nhận điều kiện đã kiểm tra trong phiên bản và dữ liệu đang xét, không chứng minh hệ thống hoàn toàn không còn lỗi.

**Chuyển ý:** Tiếp theo là giới hạn của các kết quả và hướng mở rộng.

**Lưu ý:**
- Số liệu sử dụng theo xác nhận mới nhất của nhóm: Manual UI 79/79 Pass, API thủ công 50/50 Pass, Playwright 50/50 Pass. Đã thay ghi chú cũ 77 Pass/2 Fail. Cần đồng bộ Word và chuẩn bị Excel/report; chưa xác minh trực tiếp các nguồn kết quả mới trong lượt soạn này. Không nói đã retest hoặc đóng Bug ID cụ thể nếu chưa có minh chứng tương ứng.

## Slide 17. Hạn chế và hướng phát triển — 30 giây

Kết quả hiện tại gắn với phiên bản, catalog và mô hình tại thời điểm kiểm thử. Phạm vi chủ yếu là chức năng; nhóm chưa có minh chứng cho kiểm thử tải, bảo mật chuyên sâu hoặc bao phủ mã nguồn. Hướng phát triển là mở rộng trình duyệt, kích thước màn hình, tình huống kết nối và tải đồng thời; đồng thời dùng bộ test để kiểm thử hồi quy khi hệ thống thay đổi. API và giao diện Pass cũng không chứng minh điểm dự đoán chính xác so với benchmark thực tế.

**Chuyển ý:** Từ quá trình thực hiện, nhóm rút ra các kết luận sau.

**Lưu ý:**
- Nếu chưa có report trình duyệt, đổi “mới chạy trên Chrome” thành “cần mở rộng và xác nhận môi trường trình duyệt”. Các hướng mở rộng là kế hoạch, chưa phải kết quả đã làm.

## Slide 18. Kết luận — 30 giây

Qua đề tài, nhóm vận dụng kiến thức thiết kế testcase vào một hệ thống thực tế, kết hợp quan sát thủ công với các phép kiểm tra tự động. Postman hỗ trợ kiểm tra API, còn Playwright hỗ trợ kiểm tra luồng sử dụng trên trình duyệt. Bài học quan trọng là phải xác định kỳ vọng trước, ghi kết quả thực tế và giữ minh chứng có thể truy vết. Pass xác nhận những điều kiện đã kiểm tra trong lần chạy đó, không bảo đảm hệ thống hoàn toàn không còn lỗi.

**Chuyển ý:** Nhóm xin chuyển sang phần minh họa và nhận câu hỏi.

**Lưu ý:**
- Không dùng câu notes cũ khẳng định hai lỗi vẫn mở: nhóm đã xác nhận kết quả mới là toàn bộ ca Pass. Nếu cô hỏi lịch sử lỗi, trả lời theo Bug Log và retest thực tế, không tự tạo chi tiết.

## Slide 19. Demo và hỏi đáp — 30 giây

Nhóm xin kết thúc phần trình bày. Nếu thời gian cho phép, nhóm minh họa PM-029: gửi request, xem ngân sách và giá PC, tính số tiền còn lại rồi đối chiếu với response. Cảm ơn cô và các bạn đã lắng nghe. Nhóm xin nhận câu hỏi và góp ý.

**Lưu ý:**
- Dành khoảng 1–2 phút cho demo. Chuẩn bị backend, Collection và request trước khi trình bày. Giữ input ngân sách 34.999.999 đồng nếu muốn đối chiếu bảng trên slide; kiểm tra lại giá thực tế khi dữ liệu đã thay đổi. Không cam kết luôn trả cùng PC ID khi snapshot khác.

## Câu hỏi thường gặp

**Collection là gì?**
Là bộ request API được gom cùng dữ liệu và script kiểm tra. Runner hoặc Newman thực hiện các request và tổng hợp kết quả của script.

**Vì sao 50 testcase có 257 phép kiểm tra?**
Một testcase có thể kiểm tra nhiều điều kiện. Testcase và assertion là hai đơn vị khác nhau; 257 được lấy từ thống kê của lần chạy.

**Runner và Newman khác nhau thế nào?**
Runner chạy Collection trong Postman; Newman chạy Collection bằng dòng lệnh, thuận tiện đưa vào quy trình tự động. Hai lần chạy của nhóm dùng cùng bộ testcase.

**HTTP 400 hoặc 404 có phải Fail không?**
Chỉ Fail khi khác kỳ vọng. Nếu ca yêu cầu hệ thống từ chối dữ liệu sai hoặc PC không tồn tại bằng mã đó thì ca có thể Pass khi cả mã và nội dung đều đúng.

**Viết script có phải kiểm thử hộp trắng?**
Không mặc định. Nhóm chủ yếu kiểm tra đầu vào và đầu ra theo đặc tả; script tự động hóa cách đối chiếu đó nên vẫn có thể là kiểm thử hộp đen.

**Playwright có thay hết Manual UI không?**
Không. Bộ Playwright tự động hóa một phần và mở rộng các tổ hợp. Một kết quả Pass không thay trạng thái Fail của ca khác; muốn đóng lỗi phải retest đúng tình huống.

**Có chứng minh mô hình dự đoán đúng không?**
Bộ test chức năng xác nhận dữ liệu và hành vi đã đặc tả. Đánh giá độ chính xác mô hình cần đối chiếu với benchmark thực tế và phương pháp đánh giá riêng.

**Vì sao không cộng 79/80 + 50 + 50?**
Có thể cộng số dòng quản lý để mô tả quy mô nếu đã kiểm đếm, nhưng các bộ có tình huống trùng hoặc liên quan. Nhóm báo riêng từng bộ để tránh hiểu là tất cả nghiệp vụ đều khác nhau.


## Chuẩn bị demo PM-029

- Khởi động backend và kiểm tra /health trước giờ trình bày.
- Mở sẵn request PM-029: purpose Gaming, minBudget 25.000.000, budget 34.999.999, topCount 3.
- Gửi request, chỉ mã HTTP và một item có giá PC cùng budgetRemainingVnd; tính bằng số thực tế của response.
- Nếu môi trường không chạy, dùng ảnh/response đã lưu và nói rõ đó là minh chứng lần chạy trước. Không trình bày như demo trực tiếp vừa thành công.