---
title: "Event 3 - FCAJ Mini Meeting"
date: 2026-10-24
weight: 3
chapter: false
pre: "<b>4.3.</b>"
---

# FCAJ Mini Meeting: Voice AI, AWS RAM, Security Agent và AgentCore

## Thông tin sự kiện

- **Tên sự kiện:** FCAJ Mini Meeting.
- **Thời gian:** Thứ Bảy, ngày 24/10/2026.
- **Vai trò của tôi:** Người tham dự.

Ngày 24/10/2026, tôi tham gia buổi mini meeting của cộng đồng First Cloud AI Journey. Buổi chia sẻ có nhiều chủ đề, từ xây dựng Voice AI cho tiếng Việt đến chia sẻ tài nguyên giữa các tài khoản AWS, bảo mật ứng dụng web và kiến trúc AI Agent.

Bài viết ghi lại những nội dung tôi tiếp thu từ buổi meeting, dựa trên ghi chú và hình ảnh chụp các slide trình bày.

## 1. Hear, Think, Speak — Chia sẻ của anh Kiệt Trần

Anh Kiệt Trần, AI Engineer tại Revve AI, trình bày chủ đề **Hear, Think, Speak: Building a Vietnamese voice-AI contact center on AWS**. Tôi được nghe về nền tảng Voice AI, các ứng dụng liên quan đến phỏng vấn và contact center, cùng những vấn đề khi đưa hội thoại bằng giọng nói vào hệ thống thực tế.

Điểm tôi chú ý là một cuộc hội thoại không chỉ cần câu trả lời đúng. Hệ thống còn phải nhận biết người dùng nói xong, xử lý nội dung và phản hồi với độ trễ phù hợp để cuộc trao đổi diễn ra tự nhiên.

### Ba hướng xây dựng Voice Agent

Trong phần trình bày, anh Kiệt giới thiệu ba hướng tiếp cận:

- **Cascade:** chia quá trình thành các bước ASR → LLM → TTS, từ nhận dạng giọng nói thành văn bản, xử lý văn bản đến tạo giọng nói phản hồi.
- **Speech-to-Speech (S2S):** xử lý đầu vào và đầu ra bằng âm thanh qua mô hình giọng nói.
- **Full Duplex S2S:** hướng đến tương tác nghe và nói đồng thời, giúp hội thoại gần hơn với cách con người trao đổi.

Theo phần chia sẻ, đội ngũ vẫn chọn **Cascade cho hệ thống đang vận hành**, trong khi tiếp tục thử nghiệm và theo dõi các hướng S2S. Với bài toán tiếng Việt của đội ngũ, cách này cho phép lựa chọn từng thành phần phù hợp và kiểm soát nội dung qua bước văn bản ở giữa.

Tôi hiểu thêm rằng lựa chọn kiến trúc cần dựa vào yêu cầu thực tế: chất lượng tiếng Việt, khả năng kiểm tra nội dung, ghi log và thay thế từng thành phần khi cần.

### Luồng xử lý một cuộc gọi và kiến trúc trên AWS

Slide về luồng cuộc gọi cho thấy nhiều thành phần phối hợp: SIP server, media server, khử nhiễu, nhận biết lượt nói, chuyển giọng nói thành văn bản, LLM kết hợp flow engine và tạo giọng nói trả lời.

Phần kiến trúc Revve trên AWS giới thiệu mô hình triển khai trong một Region và trong tài khoản của khách hàng. Tôi được xem cách các thành phần phục vụ web, cuộc gọi, mô hình và dữ liệu được kết nối trong cùng hệ thống.

Anh Kiệt cũng chia sẻ một POC cho ngân hàng Việt Nam, với các tình huống như tiếp nhận yêu cầu, xác minh, xác định ý định và xử lý qua API hoặc chuyển sang nhân viên. Qua ví dụ này, tôi thấy rõ hơn vai trò của luồng nghiệp vụ và cơ chế chuyển tiếp cho con người trong một ứng dụng Voice AI.

## 2. AWS Resource Access Manager — Chia sẻ của anh Long Huỳnh

Phần tiếp theo là **AWS Resource Access Manager (AWS RAM)** do anh Long Huỳnh trình bày. Chủ đề bắt đầu từ bài toán quản lý nhiều tài khoản AWS và nhu cầu sử dụng chung tài nguyên giữa các tài khoản.

Các nội dung tôi ghi lại gồm:

- **The Multi-account Challenge:** những khó khăn khi quản lý tài nguyên trong môi trường nhiều tài khoản.
- **What is AWS RAM:** giới thiệu vai trò của AWS RAM trong việc chia sẻ tài nguyên.
- **Anatomy of a Resource Share:** các thành phần của một resource share, gồm tài nguyên, đối tượng được chia sẻ và quyền sử dụng.
- **How Sharing Works End to End:** luồng chia sẻ từ phía tài khoản sở hữu đến phía tài khoản sử dụng.
- **Regions, Global and AZ IDs:** những điểm cần chú ý về phạm vi tài nguyên và định danh Availability Zone.
- **RAM in the Landing Zone:** cách đặt bài toán chia sẻ tài nguyên trong môi trường doanh nghiệp.

Theo ghi chú tại buổi chia sẻ, diễn giả đề cập khả năng chia sẻ tài nguyên thuộc hơn 40 dịch vụ. Điều tôi nhớ nhất là việc chia sẻ cần xác định rõ tài nguyên nào được dùng chung, tài khoản nào được sử dụng và quyền được cấp đến đâu.

Phần này giúp tôi có góc nhìn ban đầu về tổ chức hạ tầng nhiều tài khoản, thay vì chỉ làm việc với từng dịch vụ trong một tài khoản riêng lẻ.

## 3. AWS Security Agent — Chia sẻ của anh Thịnh

Anh Thịnh chia sẻ chủ đề **Securing Your Web Apps With AWS Security Agent**. Tôi được giới thiệu cách tiếp cận bảo mật ứng dụng web với sự hỗ trợ của agent và những yếu tố cần cân nhắc khi áp dụng vào dự án.

Một nội dung đáng chú ý là **Design Security Review**. Slide trình bày việc sử dụng tài liệu Markdown hoặc mã Terraform làm đầu vào để xem xét thiết kế theo các bộ yêu cầu bảo mật được cấu hình.

Qua đó, tôi hiểu thêm rằng việc xem xét bảo mật có thể bắt đầu từ tài liệu và thiết kế hệ thống, không chỉ đến khi ứng dụng đã hoàn thành.

Ngoài tính năng, anh Thịnh còn đề cập đến chi phí thông qua phần **The Pricing Reality**. Bài học tôi ghi lại là cần xem xét phạm vi kiểm tra và thời gian agent thực hiện công việc khi đánh giá chi phí sử dụng.

## 4. Amazon Bedrock AgentCore — Chia sẻ của anh Xuân An

Anh Xuân An trình bày về **Amazon Bedrock AgentCore**, tập trung vào Runtime và Memory Architecture. Nội dung mở đầu giới thiệu AI Agent, Agentic AI và Agentic System, sau đó đi vào các phần AgentCore Runtime và AgentCore Memory.

Ở phần Memory, tôi được nghe về cách tổ chức tương tác thành các event và những khái niệm như Memory ID, Actor ID, Session ID, Payload, Timestamp và Branch. Slide giúp tôi hình dung rõ hơn cách thông tin của một phiên trao đổi có thể được lưu và sắp xếp.

Tôi cũng ghi chú thêm các nội dung **Kiro Crew** và **App & Extensibility** được nhắc đến trong buổi chia sẻ. Đây là những chủ đề tôi cần tìm hiểu thêm để hiểu rõ cách ứng dụng vào quá trình phát triển dự án.

## 5. Kết quả và bài học rút ra

Sau buổi mini meeting, tôi có thêm những hiểu biết ban đầu:

- Phân biệt ba hướng xây dựng Voice Agent và hiểu lý do đội ngũ lựa chọn Cascade cho bài toán tiếng Việt được trình bày.
- Hình dung được một hệ thống Voice AI cần phối hợp xử lý âm thanh, mô hình, luồng nghiệp vụ và hạ tầng.
- Biết thêm về AWS RAM và bài toán chia sẻ tài nguyên giữa nhiều tài khoản.
- Nhận thức rõ hơn việc xem xét bảo mật từ giai đoạn thiết kế và cân nhắc chi phí khi sử dụng công cụ hỗ trợ.
- Làm quen với AgentCore Runtime, Memory và cách tổ chức thông tin trong một phiên tương tác.

Ở giai đoạn dự án của tôi đang bắt đầu dựng UI và khung Backend, các phần chia sẻ giúp tôi biết thêm những thành phần cần tìm hiểu về sau. Tôi xem đây là kiến thức tham khảo để hiểu cấu trúc hệ thống, chưa phải những công nghệ đã được triển khai đầy đủ trong dự án.

## Cảm nhận cá nhân

Phần tôi thấy gần với quá trình làm dự án nhất là cách mỗi hệ thống được chia thành các thành phần có vai trò rõ ràng. Từ Voice AI đến AI Agent, việc chọn mô hình chỉ là một phần; tôi còn cần hiểu dữ liệu đi qua đâu, xử lý như thế nào và cách quản lý phiên tương tác.

Buổi meeting giúp tôi có thêm định hướng học tập, đồng thời có cơ hội gặp gỡ và nghe kinh nghiệm thực tế từ các anh chị trong cộng đồng FCAJ.

## Hình ảnh tham gia sự kiện

![Phần mở đầu Hear, Think, Speak của anh Kiệt Trần](/images/4-EventParticipated/4.3-Event3/hear-think-speak.png)

![Phần chia sẻ AWS Resource Access Manager của anh Long Huỳnh](/images/4-EventParticipated/4.3-Event3/aws-ram.png)

![Chủ đề bảo mật ứng dụng web với AWS Security Agent](/images/4-EventParticipated/4.3-Event3/security-agent.png)

![Phần giới thiệu Amazon Bedrock AgentCore của anh Xuân An](/images/4-EventParticipated/4.3-Event3/agentcore.png)
