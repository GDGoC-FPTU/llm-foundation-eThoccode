# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---

## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Khi temperature tăng từ 0.0 đến 1.5, câu trả lời dịch chuyển từ tính nhất quán, an toàn (luôn lặp lại một sự thật phổ biến như xuất khẩu cà phê/hồ tiêu) sang sự sáng tạo và đa dạng hơn. Tuy nhiên, ở mức 1.5, văn phong bắt đầu trở nên lộn xộn, mất cấu trúc và có thể xuất hiện hiện tượng "ảo tưởng" (hallucination) với các thông tin sai lệch.

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Nên đặt temperature từ 0.0 đến 0.2. Đối với chatbot hỗ trợ khách hàng, sự chính xác, đồng nhất và đáng tin cậy của thông tin là yếu tố quan trọng nhất. Cấu hình thấp giúp chatbot luôn đưa ra một câu trả lời chuẩn xác duy nhất cho cùng một câu hỏi, tránh việc tự ý "sáng tạo" ra các chính sách hoặc thông tin sai sự thật gây ảnh hưởng đến trải nghiệm người dùng.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> Xét theo bảng giá API tiêu chuẩn của OpenAI (với tỷ lệ token giả định tương đương giữa Input/Output):GPT-4o: $\$2.50$ / 1M input tokens và $\$10.00$ / 1M output tokens.GPT-4o-mini: $\$0.15$ / 1M input tokens và $\$0.60$ / 1M output tokens.Dù số lượng người dùng hay số token có tăng lên bao nhiêu, tỷ lệ giá giữa hai mô hình vẫn cố định. GPT-4o đắt hơn GPT-4o-mini chính xác ~16.67 lần (cho cả Input và Output). Do đó, tổng chi phí cho workload này của GPT-4o sẽ đắt hơn GPT-4o-mini khoảng 16.7 lần.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> GPT-4o xứng đáng khi: Cần xử lý các tác vụ phức tạp đòi hỏi tư duy logic cao, phân tích dữ liệu chuyên sâu, lập trình phần mềm phức tạp, hoặc khi cần độ chính xác tuyệt đối trong các quyết định tài chính/y tế. GPT-4o-mini tốt hơn khi: Thực hiện các tác vụ lặp đi lặp lại với khối lượng lớn nhưng cấu trúc đơn giản như: phân loại sắc thái bình luận (sentiment analysis), tóm tắt văn bản ngắn, trích xuất thông tin cơ bản, hoặc làm chatbot phản hồi nhanh với ngân sách tối ưu.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất trong các ứng dụng tương tác trực tiếp với con người (như Chatbot AI, trợ lý ảo), nơi "Thời gian phản hồi đầu tiên" (Time to First Token - TTFT) quyết định trải nghiệm người dùng; việc nhìn thấy chữ chạy ra liên tục giúp giảm cảm giác sốt ruột khi mô hình phải xử lý câu trả lời dài. Ngược lại, Non-streaming lại phù hợp hơn trong các tác vụ xử lý ngầm (background jobs) không cần người dùng đợi xem kết quả ngay lập tức, ví dụ như: chạy script phân tích dữ liệu hàng loạt, trích xuất thông tin từ hóa đơn, dịch thuật sách, hoặc khi hệ thống cần lấy toàn bộ file JSON kết quả để truyền tiếp vào một API/hệ thống khác.


## Danh Sách Kiểm Tra Nộp Bài
- [ ] Tất cả tests pass: `pytest tests/ -v`
- [ ] `call_openai` đã triển khai và kiểm thử
- [ ] `call_openai_mini` đã triển khai và kiểm thử
- [ ] `compare_models` đã triển khai và kiểm thử
- [ ] `streaming_chatbot` đã triển khai và kiểm thử
- [ ] `retry_with_backoff` đã triển khai và kiểm thử
- [ ] `batch_compare` đã triển khai và kiểm thử
- [ ] `format_comparison_table` đã triển khai và kiểm thử
- [ ] `exercises.md` đã điền đầy đủ
- [ ] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 
