# Template — Evidence Pack

Nộp kèm thin SPEC cuối Day 05.

## 1. Nhóm và track

**Tên nhóm: HTDA**  
**Track: 3**  
**Product/app đã chọn: CHatbot tư vấn món**  
**Build slice đang nghĩ: AI tư vấn món ăn ở Hà Nội **  

## 2. Self-use evidence

Nhóm tự dùng app/workflow và ghi lại điểm gãy.

| Observation | Screenshot/link | Path liên quan | Điều học được |
|---|---|---|---|
|Câu trả lời không đáp ứng được vị trí người dùng mong muốn và chỉ gợi những món ăn theo yêu cầu về tâm trạng|anh_minh_chung/1.png | Failure : AI không chỉ cho điền thiêu form đã có định dạng sẵn | AI không nên chỉ dựa vào mood; cần hỏi thêm location và các ràng buộc quan trọng trước khi recommend. |
| User muốn tìm món ăn theo tâm trạng và vị trí, nhưng app chỉ cho xem danh sách/gợi ý thủ công, không hỏi đủ ngữ cảnh. | anh_minh_chung/1.png | Failure | Đây là cơ hội để AI hỏi thêm vị trí, ngân sách, khẩu vị rồi gợi ý phù hợp hơn. |

## 3. User / review / social evidence

Nguồn có thể là review App Store/Play, group, comment, phỏng vấn nhanh, hoặc nguồn public khác.

| Quote / review / observation | Nguồn | User là ai? | Pain/failure mode |
|---|---|---|---|
| Nhiều lúc không biết ăn gì dù mở app đồ ăn cả tiếng. | Phỏng vấn nhanh 5 sinh viên trong lớp |Sinh viên  |Mất quá nhiều thời gian để trả lời cho câu hỏi 'Hôm nay ăn gì?'  |
|Món ăn ở quán đó không ngon và có mùi lạ  | shopee food  | Người mua hàng | Bỏ tiền ra mua nhưng ăn phải món ăn không ngon |
|  |  |  |  |

Nếu chưa có nguồn ngoài nhóm, ghi rõ:

```text
Đây là giả định. Nhóm sẽ kiểm bằng [cách] trước checkpoint M1 Day 06.
```

## 4. Competitor / analog evidence

| App / mô hình tham khảo | Họ xử lý task này thế nào? | Pattern học được | Có áp dụng trong 1 ngày không? |
|---|---|---|---|
| Shopee Food | Cho phép tìm kiếm theo món ăn, danh mục và vị trí giao hàng |Luôn thu thập vị trí người dùng trước khi gợi ý quán  | có |

## 5. Evidence -> Insight

Evidence nổi bật nhất:

Trong quá trình self-use, nhóm nhận thấy AI tư vấn món ăn vẫn chưa được phổ biến, chỉ đưa ra những câu trả lời rất chung chung và chưa có minh chứng xác thực. Ngoài ra, qua quan sát người dùng, nhiều người thường không biết ăn gì và phải mất nhiều thời gian tìm kiếm, lọc quán trên các ứng dụng giao đồ ăn.

Insight:

User không chỉ gặp vấn đề "không biết ăn gì".

Thật ra họ cần một người hỗ trợ ra quyết định, giúp thu thập đủ ngữ cảnh (tâm trạng, vị trí, ngân sách, khẩu vị) và nhanh chóng đề xuất các lựa chọn phù hợp thay vì phải tự tìm kiếm trong hàng trăm quán ăn.

Opportunity:

AI có thể giúp bằng cách đặt một số câu hỏi ngắn để hiểu nhu cầu hiện tại của người dùng, sau đó tự động tổng hợp và đề xuất một danh sách món ăn hoặc quán ăn phù hợp với tâm trạng, vị trí và các ràng buộc cá nhân của họ.

## 6. Evidence đổi SPEC như thế nào?

- [ ] Đổi user chính.
- [x] Đổi pain statement.
- [x] Đổi build slice.
- [ ] Đổi Auto/Aug decision.
- [x] Đổi 4 paths.
- [x] Đổi failure mode.
- [ ] Đổi owner/test plan.

Ghi rõ 1-2 thay đổi quan trọng:

```text
Trước evidence, nhóm định xây AI ẩm thực .
Sau evidence, nhóm đổi thành AI hỗ trợ ra quyết định ăn uống dựa trên nhiều yếu tố gồm tâm trạng, vị trí, ngân sách và sở thích ăn uống.
Lý do:
Kết quả self-use cho thấy AI hỗ trợ vấn đề quá rộng không tập chung vào 1 pain point. Người dùng thực tế cần những đề xuất có thể áp dụng ngay tại vị trí hiện tại và phù hợp với các ràng buộc cá nhân. Vì vậy AI cần thu thập thêm ngữ cảnh trước khi recommend thay vì chỉ dựa vào cảm xúc của người dùng.
```
