---
title: "Amazon Transcribe Medical – chuyển lời nói y tế thành văn bản"
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Amazon Transcribe Medical: Chuyển lời nói y tế thành văn bản như thế nào?

Trong buổi khám, bác sĩ vừa trò chuyện với bệnh nhân vừa cần ghi lại triệu chứng, tiền sử bệnh và thuốc đang sử dụng. Ghi chép thủ công có thể khiến bác sĩ phải chia sự chú ý giữa cuộc trao đổi và hồ sơ bệnh án.

Amazon Transcribe Medical là dịch vụ nhận dạng giọng nói y tế của AWS. Dịch vụ chuyển lời đọc chính tả hoặc hội thoại y tế thành bản chép lời để nhân viên y tế rà soát và chỉnh sửa.

## Amazon Transcribe Medical có gì đáng chú ý?

- **Medical Dictation:** Chuyển lời đọc chính tả của nhân viên y tế thành văn bản.
- **Medical Conversation:** Phiên âm hội thoại giữa nhân viên y tế và bệnh nhân.
- **Speaker Diarization:** Gắn nhãn lượt nói của từng người trong hội thoại, chẳng hạn `spk_0` và `spk_1`. Dịch vụ không tự xác định ai là bác sĩ hay bệnh nhân.
- **Medical Custom Vocabulary:** Bổ sung từ vựng chuyên ngành để hỗ trợ nhận dạng thuật ngữ y tế. Không đưa thông tin bí mật, thông tin cá nhân hoặc PHI vào danh sách từ vựng.
- **Alternative Transcriptions:** Trả thêm phương án nhận dạng để nhân viên y tế cân nhắc khi âm thanh chưa rõ.
- **PHI Identification:** Đánh dấu thông tin sức khỏe cá nhân trong bản chép lời. Việc che hoặc xóa thông tin cần được xử lý riêng.

## Quy trình hoạt động

1. **Thu âm:** Ứng dụng nhận giọng nói qua microphone hoặc từ tệp ghi âm.
2. **Gửi âm thanh:** Âm thanh được truyền trực tiếp để xử lý hoặc gửi dưới dạng tệp ghi âm.
3. **Nhận bản chép lời:** Amazon Transcribe Medical trả về nội dung đã nhận dạng, có thể kèm nhãn người nói hoặc thông tin bổ sung tùy cấu hình.
4. **Rà soát:** Nhân viên y tế kiểm tra và chỉnh sửa bản chép lời trước khi lưu hoặc sử dụng.

## Có thể kết hợp với các dịch vụ AWS nào?

Amazon Transcribe Medical đảm nhiệm việc nhận dạng giọng nói. Ứng dụng có thể kết hợp Amazon S3 để lưu tệp âm thanh và bản chép lời; AWS Lambda để điều phối xử lý; Amazon Comprehend Medical để trích xuất thông tin y tế có cấu trúc; và Amazon Bedrock cho bước tóm tắt hoặc hỏi đáp theo thiết kế riêng.

Các dịch vụ này cần được tích hợp riêng. Chúng không phải chức năng tự động có sẵn bên trong Transcribe Medical.

## Những điểm cần lưu ý

- **Ngôn ngữ:** Dịch vụ hỗ trợ tiếng Anh Mỹ (`en-US`), chưa nhận dạng trực tiếp tiếng Việt.
- **Chuyên khoa:** Khi gửi yêu cầu phiên âm, cần chọn chuyên khoa phù hợp. Xử lý tệp ghi âm hỗ trợ nhóm Chăm sóc ban đầu, gồm y học gia đình, nội khoa, sản phụ khoa và nhi khoa. Một số chuyên khoa khác chỉ hỗ trợ âm thanh trực tiếp.
- **Độ chính xác:** Tiếng ồn, cách phát âm và thuật ngữ chuyên môn có thể ảnh hưởng đến kết quả.
- **Bảo vệ dữ liệu:** Âm thanh và bản chép lời có thể chứa thông tin sức khỏe nhạy cảm. Cần kiểm soát quyền truy cập và cách lưu trữ.
- **Rà soát chuyên môn:** Nhân viên y tế cần kiểm tra bản chép lời trước khi sử dụng trong quy trình chăm sóc bệnh nhân.

## Chi phí và trường hợp sử dụng

Amazon Transcribe Medical tính phí theo thời lượng âm thanh được phiên âm; mức phí phụ thuộc vào cách sử dụng và bảng giá tại thời điểm triển khai. Dịch vụ phù hợp khi cần tạo bản nháp từ lời đọc chính tả hoặc hội thoại y tế bằng tiếng Anh Mỹ. Bản chép lời là đầu vào để con người rà soát, không phải hồ sơ đã được xác nhận tự động.

## Nguồn tham khảo

- [AWS – Amazon Transcribe Medical](https://docs.aws.amazon.com/transcribe/latest/dg/transcribe-medical.html)
- [AWS – Transcribing a medical conversation](https://docs.aws.amazon.com/transcribe/latest/dg/transcribe-medical-conversation.html)
- [AWS – Transcribing a medical dictation](https://docs.aws.amazon.com/transcribe/latest/dg/transcribe-medical-dictation.html)
- [AWS – Medical custom vocabularies](https://docs.aws.amazon.com/transcribe/latest/dg/vocabulary-med.html)
- [AWS – Amazon Transcribe pricing](https://aws.amazon.com/transcribe/pricing/)
