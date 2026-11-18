# [Bài thực hành 2] Xây dựng chuỗi Prompt viết bài PR sản phẩm công nghệ
## Promting Chaining
PROMPT 1:Nghiên cứu khách hàng và pain points
```Prompt 1: Nghiên cứu khách hàng và pain points
# VAI TRÒ
Bạn là chuyên gia nghiên cứu thị trường B2B về công nghệ.

# NGỮ CẢNH
Sản phẩm: [Tên], giải pháp AI Chatbot cho doanh nghiệp.
Tính năng chính: [liệt kê 3-5 tính năng].

# NHIỆM VỤ
Hãy suy nghĩ từng bước: (1) xác định 2-3 nhóm khách hàng mục tiêu,
(2) với mỗi nhóm, liệt kê 3-4 pain points cụ thể,
(3) ghép mỗi pain point với tính năng sản phẩm giải quyết nó.

# ĐỊNH DẠNG ĐẦU RA (JSON, không viết thêm gì ngoài JSON)
{
  "product": "...",
  "target_audiences": [
    {
      "name": "...",
      "profile": "...",
      "pain_points": [
        {"id": "P1", "pain": "...", "solution_feature": "..."}
      ]
    }
  ],
  "main_keywords": ["...", "..."]
}
```
Prompt 2: Lập dàn ý (dựa trên Output 1)
```Prompt 2
# VAI TRÒ
Bạn là biên tập viên nội dung PR và chuyên gia SEO.

# DỮ LIỆU ĐẦU VÀO BẮT BUỘC (Output của Prompt 1)
<output_1>
[dán JSON từ Prompt 1]
</output_1>

# NHIỆM VỤ
Chỉ dùng dữ liệu trong <output_1> để lập dàn ý bài PR 1000-1500 từ.
Mỗi pain point (P1, P2...) phải xuất hiện ít nhất một lần trong dàn ý.
Không thêm thông tin ngoài dữ liệu đã cho.

# ĐỊNH DẠNG ĐẦU RA (JSON)
{
  "headline": "...",
  "lead_summary": "...",
  "sections": [
    {
      "h2": "...",
      "h3": ["...", "..."],
      "pain_ids": ["P1"],
      "target_words": 250,
      "keywords": ["..."]
    }
  ],
  "cta": "..."
}
```
Prompt 3: Viết bài + tối ưu SEO (dựa trên Output 1 và 2)
```Prompt 3
# VAI TRÒ
Bạn là copywriter PR công nghệ kiêm chuyên gia SEO.

# DỮ LIỆU ĐẦU VÀO BẮT BUỘC
<output_1>[JSON pain points]</output_1>
<output_2>[JSON dàn ý]</output_2>

# NHIỆM VỤ
Viết bài PR hoàn chỉnh theo đúng dàn ý trong <output_2>.
Giữ nguyên thứ tự H2/H3, không bỏ, không thêm mục.

# YÊU CẦU
- Độ dài 1000-1500 từ, đúng target_words từng phần.
- Headline hấp dẫn, có từ khóa chính.
- Lead 80-120 từ, mở bằng pain point của khách hàng.
- Từ khóa chính xuất hiện tự nhiên (mật độ khoảng 1-2%), không nhồi nhét.
- Kết bằng CTA rõ ràng (hành động cụ thể: đăng ký dùng thử, liên hệ...).
- Giọng văn chuyên nghiệp, không lặp ý giữa các phần.

# ĐỊNH DẠNG
Markdown: # Headline, đoạn Lead, ## H2, ### H3, mục CTA ở cuối.
```
Prompt 4: Xử lý khi AI bị ngắt quãng
```prompt 4
Bài viết bị ngắt giữa chừng. Hãy tiếp tục viết ngay từ câu cuối cùng
đã dừng: "[dán 1-2 câu cuối AI vừa viết]".
Quy tắc:
- Không viết lại phần đã có, không tóm tắt lại.
- Giữ nguyên giọng văn, từ khóa và cấu trúc H2/H3 theo <output_2>.
- Tiếp tục đến hết phần còn lại, kết thúc bằng CTA.
```
