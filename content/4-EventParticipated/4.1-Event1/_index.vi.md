---
title: "Event 1 - FCAJ Buildrathon Kickoff"
date: 2026-09-26
weight: 1
chapter: false
pre: "<b>4.1.</b>"
---

# FCAJ Buildrathon Kickoff

## Giới thiệu sự kiện

Ngày 26/09/2026, tôi tham gia buổi kickoff của First Cloud AI Journey tại văn phòng AWS Hồ Chí Minh.

Buổi event gồm các phần chính:

- Giới thiệu về First Cloud AI Journey
- Kickoff Buildrathon
- Phần giao lưu và giới thiệu từ CMC Global
- Phần chia sẻ của anh Trường về dự án chatbot
- Giới thiệu kiến trúc của Market Slack Bot

---

## 1. Giới thiệu về First Cloud AI Journey

Phần đầu tiên của buổi event là giới thiệu về First Cloud AI Journey.

Ở phần này, tôi được giới thiệu lại về chương trình FCAJ, cách chương trình hoạt động và những nội dung các thành viên sẽ tham gia trong thời gian tới.

Qua phần này, tôi hiểu rõ hơn về chương trình mình đang tham gia và những hoạt động sẽ diễn ra trong Buildrathon.

---

## 2. Kickoff Buildrathon

Sau phần giới thiệu FCAJ là phần kickoff chính thức của Buildrathon.

Ban tổ chức giới thiệu về chương trình Buildrathon và cách các team sẽ tham gia trong thời gian tới.

Qua phần này, tôi hiểu rõ hơn về quá trình tham gia chương trình cũng như cách các team sẽ cùng làm project.

---

## 3. Phần giao lưu từ CMC Global

Tiếp theo là phần giao lưu với CMC Global.

Ở phần này, phía CMC Global giới thiệu về công ty và một số thông tin liên quan đến đơn vị của họ.

Sau phần giới thiệu là hoạt động giao lưu với các thành viên tham gia chương trình.

CMC Global cũng có phần tặng quà cho các bạn tham gia event.

Phần này chủ yếu giúp tôi biết thêm về CMC Global và tạo không khí giao lưu trong buổi kickoff.

---

## 4. Phần chia sẻ của anh Trường về dự án chatbot

Phần tôi quan tâm nhất trong event là phần anh Trường chia sẻ về một dự án chatbot.

Trong dự án có hai nhóm làm việc ở hai nơi khác nhau:

- BA làm việc ở nước ngoài
- Engineer làm việc tại Việt Nam

Do hai nhóm không làm việc cùng một nơi nên việc trao đổi thông tin, yêu cầu và xử lý các vấn đề có thể gặp khó khăn.

Từ vấn đề đó, team đã xây dựng một Triage Bot để hỗ trợ quá trình trao đổi và xử lý thông tin giữa các bên.

Qua phần chia sẻ này, tôi thấy rõ hơn cách một vấn đề thực tế trong quá trình làm việc có thể dẫn đến việc xây dựng một AI application để hỗ trợ team.

---

## 5. Triage Bot

Triage Bot được xây dựng để hỗ trợ việc xử lý và phân loại thông tin trong quá trình trao đổi giữa các team.

Trong phần demo, tôi được xem cách team định nghĩa bot thông qua file `SOUL.md`.

Một số phần tôi thấy trong `SOUL.md` gồm:

- Identity
- Expertise
- Tone & Style
- Skills used
- Domain-specific protocols
- Anti-patterns
- Out of scope

Điểm tôi thấy khá thú vị là bot không được thiết kế để trả lời tất cả mọi thứ.

Team xác định rõ:

- Bot là ai
- Bot có thể xử lý những nội dung gì
- Bot không được xử lý những nội dung gì
- Cách bot trả lời
- Phạm vi hoạt động của bot

Qua phần này, tôi hiểu thêm rằng khi xây dựng chatbot thì không chỉ cần AI model mà còn phải xác định rõ role, scope và cách bot hoạt động.

---

## 6. Kiến trúc Market Slack Bot

Trong phần trình bày, tôi được xem kiến trúc của Market Slack Bot.

Luồng chính trên slide gồm:

```text
Slack
  ↓
Socket Mode
  ↓
Response Gate
  ↓
Claude Code
```

Ngoài luồng chính, hệ thống còn có các thành phần:

- SOUL.md
- Memory
- bot-schedule
- Internal API
- Cron + database

### Socket Mode

Socket Mode sử dụng WebSocket để kết nối với Slack.

### Response Gate

Response Gate nằm trước phần xử lý của bot.

Theo cách tôi hiểu từ phần trình bày, thành phần này giúp kiểm soát khi nào bot nên phản hồi thay vì message nào cũng trả lời.

### SOUL.md

`SOUL.md` được dùng để định nghĩa vai trò, phạm vi và cách bot hoạt động.

### Memory

Memory được dùng để giữ context của các thread.

Nhờ vậy bot có thể dựa vào nội dung trao đổi trước đó thay vì chỉ xử lý từng message riêng lẻ.

### Bot Schedule

`bot-schedule` được dùng cho các hoạt động đã được lên lịch.

### Internal API

Internal API được dùng để xử lý các job bên trong application.

### Cron + Database

Cron + Database hỗ trợ phần memory và các cron jobs.

---

## 7. Điều tôi thấy đáng chú ý

Trong slide có câu:

> "Each piece answered a question I actually faced."

Điều tôi hiểu từ phần này là mỗi thành phần trong hệ thống được tạo ra để giải quyết một vấn đề cụ thể mà team đã gặp trong quá trình làm project.

Ví dụ:

- Slack là nơi nhận request
- Socket Mode dùng để kết nối
- Response Gate kiểm soát việc phản hồi
- SOUL.md xác định vai trò và phạm vi của bot
- Memory giữ context
- Internal API xử lý các job
- Cron + Database hỗ trợ các công việc chạy theo lịch

Qua đó, tôi hiểu thêm rằng khi thiết kế một hệ thống thì cần biết từng thành phần được thêm vào để giải quyết vấn đề gì.

---

## 8. Trải nghiệm kỹ thuật thực tế

Phần Triage Bot là phần giúp tôi có thêm góc nhìn thực tế về một AI application.

Trước đây khi nghĩ tới chatbot, tôi chủ yếu nghĩ tới AI model hoặc API.

Qua phần chia sẻ này, tôi thấy phía sau một chatbot còn có nhiều thành phần khác như:

- Scope
- Memory
- Context
- API
- Database
- Schedule
- Cách kiểm soát response

Tôi cũng hiểu thêm rằng một hệ thống AI thực tế cần được xây dựng để phù hợp với workflow của người sử dụng.

---

## 9. Kết nối và trao đổi

Buổi event giúp tôi có cơ hội gặp và giao lưu với các thành viên khác trong First Cloud AI Journey.

Ngoài ra, tôi còn được nghe phần giới thiệu từ CMC Global và phần chia sẻ thực tế về dự án chatbot.

Qua đó, tôi có thêm góc nhìn về cách các team phối hợp với nhau trong quá trình làm project.

---

## 10. Những gì tôi học được

Sau buổi event, tôi ghi lại được một số điều:

- Hiểu rõ hơn về FCAJ và Buildrathon
- Biết thêm về CMC Global
- Có thêm trải nghiệm giao lưu với các thành viên trong chương trình
- Biết thêm cách một project thực tế có thể được triển khai giữa nhiều team
- Thấy được vấn đề khi BA và Engineer làm việc ở hai nơi khác nhau
- Biết thêm cách chatbot có thể hỗ trợ quá trình trao đổi giữa các team
- Hiểu thêm về role và scope của một bot
- Biết thêm cách dùng `SOUL.md` để định nghĩa cách bot hoạt động
- Hiểu thêm vai trò của Memory và context
- Biết thêm kiến trúc cơ bản của một Slack Bot
- Hiểu rằng một AI application không chỉ có model mà còn có nhiều thành phần khác xung quanh

---

## 11. Bài học rút ra

Điều tôi nhớ nhất sau buổi event là phần chia sẻ về Triage Bot.

Từ một vấn đề trong quá trình trao đổi giữa BA và Engineer, team đã xây dựng một bot để hỗ trợ công việc.

Qua đó, tôi thấy rằng khi làm một project AI thì trước tiên cần xác định vấn đề cần giải quyết, sau đó mới lựa chọn cách xây dựng hệ thống phù hợp.

Tôi cũng hiểu thêm rằng một AI application thực tế không chỉ có model mà còn cần các thành phần hỗ trợ như memory, API, database, context và các cơ chế kiểm soát cách hệ thống phản hồi.

---

## 12. Một số hình ảnh khi tham gia sự kiện

### Không gian tại buổi kickoff

![Không gian tại sự kiện](images/background.jpg)

### Phần demo dự án Triage Bot

![Demo dự án Triage Bot](images/demo%20project.jpg)

### FCAJ Buildrathon Kickoff

![FCAJ Buildrathon Kickoff](images/buildhackathon.jpg)

### Phần demo cấu trúc SOUL.md

![Demo SOUL.md](images/soul.jpg)

### Kết thúc buổi event

![Kết thúc sự kiện](images/end.jpg)

---

## Tổng kết

Buổi kickoff giúp tôi hiểu rõ hơn về FCAJ, Buildrathon và có cơ hội giao lưu với các thành viên trong chương trình.

Phần tôi quan tâm nhất là phần chia sẻ về Triage Bot và kiến trúc Market Slack Bot.

Qua phần này, tôi hiểu thêm rằng một AI application được xây dựng từ một vấn đề thực tế và có nhiều thành phần phối hợp với nhau chứ không chỉ có AI model.