---
title: "Event 4 - FCAJ Community Day"
date: 2026-10-31
weight: 4
chapter: false
pre: "<b>4.4.</b>"
---

# AWS First Cloud AI Journey Community Day

## Thông tin sự kiện

- **Tên sự kiện:** AWS First Cloud AI Journey Community Day.
- **Thời gian:** Thứ Bảy, ngày 31/10/2026.
- **Vai trò của tôi:** Người tham dự.

Ngày 31/10/2026, tôi tham gia Community Day của cộng đồng First Cloud AI Journey. Các phần chia sẻ giúp tôi có thêm góc nhìn về cách học AWS, tổ chức quy trình phát triển phần mềm với AI và xây dựng ứng dụng trên nền tảng Serverless.

Các phần chia sẻ tại sự kiện giúp tôi liên hệ kiến thức AWS với quá trình xây dựng và vận hành sản phẩm thực tế.

## 1. New to AWS? Where Should You Start?

Một phần chia sẻ tập trung vào câu hỏi người mới nên bắt đầu học AWS từ đâu. Nội dung giới thiệu các nguồn học, lộ trình tiếp cận và cơ hội AWS credit phục vụ việc thực hành.

### Lộ trình học được gợi ý

Slide **A Suggested AWS Learning Order** trình bày bốn bước:

1. **Foundations:** xây dựng kiến thức nền tảng về cloud, Region, Availability Zone, IAM và bảo mật.
2. **Hands-on:** thực hành các bài lab để hiểu cách sử dụng dịch vụ.
3. **Take Notes:** ghi lại khái niệm, lỗi gặp phải và cách giải quyết.
4. **Connect:** kết nối với cộng đồng để trao đổi và tiếp tục học hỏi.

Ngoài slide, tôi còn được xem phần giới thiệu trực tiếp giao diện nguồn học và cộng đồng AWS. Điều tôi rút ra là cần kết hợp đọc tài liệu, thực hành và ghi chú, thay vì chỉ xem qua nhiều dịch vụ mà chưa hiểu cách sử dụng.

## 2. Lessons Learned from Building Software Factories

Anh **Henry (Duc) Bui**, Head of Engineering tại **CloudThinker**, chia sẻ kinh nghiệm qua chủ đề **Lessons Learned from Building Software Factories**.

Phần này giúp tôi hình dung cách một đội ngũ tổ chức công việc khi sử dụng coding agent: chuẩn bị ngữ cảnh, quản lý các repository, kiểm tra thay đổi và cung cấp bằng chứng để người review đánh giá kết quả.

### Một thư mục điều phối chung

Slide **One folder runs everything** giới thiệu một thư mục `control` làm điểm bắt đầu cho các phiên làm việc. Thư mục này chứa ghi chú, skills và hướng dẫn về môi trường; từ đó agent tiếp cận repository ứng dụng, hạ tầng, tài liệu và các máy cần sử dụng.

Theo cách tôi hiểu, điểm đáng chú ý là tổ chức thông tin để agent có nơi tìm lại ngữ cảnh và hướng dẫn, thay vì mỗi phiên bắt đầu với thông tin rời rạc.

### Merge request cần có bằng chứng về thay đổi

Một slide khác minh họa việc đính kèm ảnh trước và sau thay đổi, ở giao diện sáng và tối, màn hình rộng và hẹp. Nhờ đó, người review có thể nhìn thấy kết quả giao diện ngay trong merge request.

Điều này khá gần với giai đoạn tôi đang dựng UI cho dự án. Tôi ghi lại ý tưởng lưu ảnh kết quả và mô tả rõ phần đã chỉnh sửa để việc kiểm tra thuận tiện hơn.

### Chia sẻ kết quả kiểm thử giữa nhiều phiên

Phần **Many sessions, one shared test cache** trình bày cách nhiều phiên coding dùng chung bộ nhớ đệm kết quả kiểm thử và bộ chạy kiểm tra. Slide mô tả việc tái sử dụng kết quả khi mã liên quan không thay đổi và chạy lại khi có thay đổi.

Qua đó, tôi có thêm góc nhìn về tối ưu quy trình phát triển: bên cạnh tốc độ viết mã, thời gian chờ kiểm tra và cách dùng lại kết quả cũng ảnh hưởng đến hiệu quả làm việc.

## 3. Xây dựng ứng dụng game với Serverless

Một phần khác chia sẻ về việc xây dựng ứng dụng game với Serverless, từ cách lựa chọn dịch vụ đến tổ chức các thành phần trong hệ thống. Slide **Why Serverless?** nhấn mạnh việc giảm công việc quản lý máy chủ, khả năng mở rộng và cách tính phí theo sử dụng trong mô hình được trình bày.

Tôi cũng chú ý đến dòng về trách nhiệm chia sẻ: bên cạnh phần hạ tầng do AWS vận hành, phía xây dựng ứng dụng vẫn cần quan tâm đến mã nguồn, IAM và dữ liệu.

### So sánh kiến trúc trước và sau

Hai slide **Architecture — Then** và **Architecture — Now** cho thấy kiến trúc ứng dụng ở hai giai đoạn. Các sơ đồ trình bày nhiều thành phần như giao diện, xác thực, API, xử lý bằng Lambda, lưu trữ dữ liệu và giám sát.

Tôi chưa đi sâu vào từng đường kết nối trong sơ đồ, nhưng phần so sánh giúp tôi thấy kiến trúc có thể thay đổi khi luồng xử lý và nhu cầu của ứng dụng rõ hơn. Đây là một ví dụ để tôi học cách xác định vai trò của từng thành phần trước khi lựa chọn dịch vụ cho dự án.

### Dự án Chrono Genesis TCG

Phần chia sẻ về dự án **Chrono Genesis TCG** giới thiệu chức năng **Host Private Duel** để tạo phòng đấu riêng. Giao diện hiển thị phần tạo phòng riêng, mã phòng và trạng thái chờ đối thủ tham gia.

Việc xem sản phẩm cùng sơ đồ kiến trúc giúp tôi liên hệ rõ hơn giữa một thao tác trên UI và các thành phần phía Backend cần hỗ trợ cho thao tác đó.

## 4. Lambda Web Functions: Native HTTP Engine

Một slide trong buổi chia sẻ có chủ đề **Lambda Web Functions: Native HTTP Engine**, với ba nhóm nội dung: Native HTTP Socket, Full Container Support và Direct Framework Routing.

Từ phần giới thiệu này, tôi ghi lại hướng tìm hiểu về cách ứng dụng web và framework Backend được đóng gói, tiếp nhận HTTP request và triển khai trong môi trường Lambda. Đây là nội dung tôi mới làm quen tại sự kiện và cần đọc thêm tài liệu trước khi áp dụng vào dự án.

## 5. AWS SQS: Asynchronous Systems

Phần trình bày của **Luong Cam Dao (FCAJ)** có chủ đề **AWS SQS: Asynchronous Systems**.

Chủ đề này gợi cho tôi hướng tìm hiểu về hàng đợi và xử lý bất đồng bộ: cách tách việc tiếp nhận yêu cầu khỏi phần xử lý phía sau. Ở giai đoạn hiện tại, tôi ghi nhận đây là một nội dung cần học thêm để hiểu cách tổ chức Backend khi dự án có các tác vụ cần xử lý riêng.

## 6. Kết quả và bài học rút ra

Sau Community Day, tôi ghi lại một số điểm:

- Có lộ trình học AWS rõ hơn: kiến thức nền tảng, thực hành, ghi chú và kết nối cộng đồng.
- Biết thêm cách tổ chức ngữ cảnh và tài liệu khi làm việc với coding agent.
- Hiểu giá trị của ảnh minh chứng và thông tin kiểm tra trong quá trình review thay đổi.
- Có góc nhìn ban đầu về việc chia sẻ kết quả kiểm thử giữa nhiều phiên phát triển.
- Hình dung rõ hơn mối liên hệ giữa giao diện sản phẩm và kiến trúc Backend qua dự án game sử dụng Serverless.
- Ghi lại các chủ đề Lambda và SQS để tiếp tục tìm hiểu.

## Cảm nhận cá nhân

Ở thời điểm tham gia sự kiện, dự án của tôi chủ yếu đang dựng UI, khởi tạo Backend và tìm hiểu cấu trúc cần có. Vì vậy, điều tôi thấy hữu ích nhất là cách tổ chức công việc và chia hệ thống thành các phần có nhiệm vụ rõ ràng.

Tôi có thể bắt đầu từ những việc nhỏ như sắp xếp mã nguồn, ghi chú luồng xử lý và lưu lại kết quả giao diện. Các nội dung về Serverless, Lambda hay hàng đợi là hướng học tiếp theo khi yêu cầu dự án rõ hơn.

Community Day cũng là dịp để tôi gặp gỡ các thành viên FCAJ và tiếp cận kinh nghiệm thực tế từ những người đang xây dựng sản phẩm.

## Hình ảnh tham gia sự kiện

![Phần giới thiệu lộ trình học AWS cho người mới](/images/4-EventParticipated/4.4-Event4/aws-learning.png)

![Phần chia sẻ của anh Henry Duc Bui về Software Factories](/images/4-EventParticipated/4.4-Event4/software-factories.png)

![Kiến trúc ứng dụng ở giai đoạn sau](/images/4-EventParticipated/4.4-Event4/architecture-now.png)

![Slide Lambda Web Functions: Native HTTP Engine tại sự kiện](/images/4-EventParticipated/4.4-Event4/lambda-web.png)

![Phần giới thiệu AWS SQS: Asynchronous Systems của Luong Cam Dao](/images/4-EventParticipated/4.4-Event4/sqs.png)
