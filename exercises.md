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
> *Khi temperature thấp như 0.0, mô hình trả lời ổn định, logic và ít sáng tạo hơn. Khi tăng temperature lên 0.5, 1.0 và 1.5, phản hồi trở nên đa dạng, tự nhiên và sáng tạo hơn, tuy nhiên ở mức cao thì câu trả lời có xu hướng dài hơn và đôi lúc ít ổn định hơn*

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> *Tôi sẽ đặt temperature khoảng 0.2–0.5 cho chatbot hỗ trợ khách hàng vì chatbot cần phản hồi ổn định, chính xác, nhất quán và hạn chế trả lời quá sáng tạo hoặc sai lệch thông tin*

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> *Tổng số request mỗi ngày là 10.000 × 3 = 30.000 request/ngày, tổng token mỗi ngày được tính theo công thức: Total Tokens = Users × Requests/User × Tokens/Request = 10.000 × 3 × 350 = 10.500.000 token/ngày. Theo pricing thực tế em có tìm thêm về pricing của input token 2 model này nên em thêm vào: GPT-4o input là $2.50 / 1M tokens và output là $10.00 / 1M tokens, trong khi GPT-4o-mini input là $0.15 / 1M tokens và output là $0.60 / 1M tokens. Ví dụ với input token: chi phí GPT-4o = (10.500.000 / 1.000.000) × 2.50 = 26.25 USD, còn GPT-4o-mini = (10.500.000 / 1.000.000) × 0.15 = 1.575 USD. Tỷ lệ chi phí là 26.25 / 1.575 = 16.7 lần, nên GPT-4o đắt hơn GPT-4o-mini khoảng 16–17 lần cho workload này.*

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> *GPT-4o phù hợp cho các tác vụ cần reasoning mạnh, độ chính xác cao và xử lý ngữ cảnh phức tạp như AI agent nhiều bước, hỗ trợ coding, phân tích tài liệu hoặc xử lý multimodal (text + image + audio), vì trong các trường hợp này chất lượng phản hồi quan trọng hơn chi phí. Ngược lại, GPT-4o-mini phù hợp hơn cho chatbot FAQ, hỗ trợ khách hàng cơ bản, auto-reply hoặc các workload lớn cần tối ưu chi phí và tốc độ, vì model rẻ hơn rất nhiều nhưng vẫn đáp ứng tốt các tác vụ đơn giản*

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> *Streaming quan trọng nhất trong các ứng dụng realtime như chatbot, trợ lý AI hoặc hệ thống trả lời dài vì người dùng có thể thấy phản hồi xuất hiện từng phần ngay lập tức thay vì phải chờ toàn bộ kết quả hoàn thành, từ đó giúp trải nghiệm mượt hơn và giảm cảm giác delay. Ngược lại, non-streaming phù hợp hơn trong các hệ thống backend, xử lý batch, sinh JSON hoặc workflow tự động khi chương trình cần nhận đầy đủ dữ liệu trước khi xử lý tiếp hoặc lưu vào hệ thống.*


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
