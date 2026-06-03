# Toolkit — Từ Evidence Đến Build Slice

Dùng sau khi nhóm đã có evidence. Mục tiêu là chốt một build slice đủ nhỏ cho Day 06.

## 1. Gom evidence thành cụm

Gom theo **workflow/pain**, không gom theo tên feature.

Các cụm evidence của nhóm:

- "User không biết hôm nay ăn gì nhưng app chỉ gợi ý món chung chung theo tâm trạng."
- "Kết quả gợi ý chưa xét đến vị trí/khu vực user mong muốn nên khó hành động ngay."
- "User vẫn phải tự lọc lại theo khoảng cách, ngân sách, khẩu vị hoặc thời gian."
- "App chưa có flow hỏi lại khi thiếu thông tin quan trọng như location, budget, food preference."

Pain chính được chọn:

```text
User muốn được giúp chốt món/quán ăn phù hợp với hoàn cảnh hiện tại,nhưng app hiện tại chỉ gợi ý theo mood nên kết quả thiếu ngữ cảnh để ra quyết định.
```

## 2. Viết insight

Form:

```text
User [segment] không chỉ cần [surface need].
Họ thật ra cần [deeper need],
vì [evidence pattern].
```

Ví dụ:

```text
User đang phân vân không biết ăn gì không chỉ cần một danh sách món ăn.
Họ thật ra cần được hỗ trợ chốt lựa chọn phù hợp với ngữ cảnh cá nhân,
vì evidence cho thấy gợi ý chỉ theo tâm trạng là chưa đủ nếu thiếu vị trí,
ngân sách, khẩu vị và thời gian.
```

## 3. Viết opportunity

Form:

```text
Cơ hội là dùng AI để [augment/automate hành động hẹp],
giúp user [kết quả],
trong khi vẫn kiểm soát [failure/risk].
```

Opportunity của nhóm:

```text
Cơ hội là dùng AI để hỏi thêm 2-3 thông tin còn thiếu
như vị trí, ngân sách và khẩu vị,
giúp user nhận được 3 gợi ý món/quán có thể hành động ngay,
trong khi vẫn kiểm soát rủi ro gợi ý sai bằng cách hỏi lại khi thiếu location
hoặc khi confidence thấp.
```

## 4. Chọn build slice

Build slice tốt phải qua 5 câu hỏi:

| Câu hỏi | Đạt khi |
|---|---|
| User cụ thể chưa? | Sinh viên/người đi làm đang phân vân không biết ăn gì trong một khu vực cụ thể. |
| Task đủ hẹp chưa? | Demo trong 3-5 phút: nhập mood + location + budget, AI trả 3 gợi ý. |
| AI decision rõ chưa? | AI gợi ý món/quán phù hợp nhất dựa trên mood, vị trí và ràng buộc. |
| Failure path rõ chưa? | Nếu thiếu vị trí hoặc input mơ hồ, AI phải hỏi lại thay vì gợi ý ngay. |
| Có evidence không? | Có self-use evidence: app trả lời chưa đáp ứng vị trí user mong muốn và chỉ gợi món theo tâm trạng. Cần bổ sung review/phỏng vấn nhanh trước M1 Day 06. |

Build slice chốt:

```text
Cho user đang phân vân không biết ăn gì,
prototype dùng AI để hỏi mood, vị trí và ngân sách,
sau đó gợi ý 3 món/quán phù hợp kèm lý do ngắn.
Nếu thiếu vị trí hoặc thông tin quá mơ hồ, AI hỏi lại trước khi recommend.
```

## 5. Quyết định: giữ, giảm scope, hay đổi hướng?

| Tình huống | Quyết định |
|---|---|
| Evidence yếu, user mơ hồ | Bổ sung phỏng vấn nhanh 3 user trước checkpoint M1 Day 06. |
| Ý tưởng quá rộng | Giữ domain ăn uống, cắt xuống một flow: gợi ý món/quán cho một bữa ăn. |
| AI không cần thiết | AI vẫn hữu ích vì cần hiểu mood/input tự nhiên và chuyển thành tiêu chí gợi ý. |
| Rủi ro cao | Chọn augmentation: AI chỉ gợi ý, user quyết định cuối cùng. |
| Không demo được trong 1 ngày | Không build đặt món, map, thanh toán, review thật; chỉ build flow recommend + hỏi lại. |

Quyết định chốt:

```text
Giữ hướng AI food recommendation nhưng giảm scope.
Không build app ăn uống đầy đủ.
Chỉ build một assistant nhỏ giúp user chốt 3 gợi ý món/quán theo mood,
location và budget, có low-confidence path khi thiếu thông tin.
```

## 6. Câu chốt cuối

Điền câu này trước khi rời lớp:

```text
Dựa trên evidence rằng app hiện tại gợi ý món ăn chưa xét đến vị trí
và chỉ phản hồi theo tâm trạng,
nhóm sẽ build prototype AI gợi ý 3 món/quán phù hợp,
cho sinh viên/người đi làm đang phân vân không biết ăn gì,
để giải quyết pain phải tự lọc quá nhiều lựa chọn,
bằng cách AI hỏi thêm mood, location, budget rồi recommend có lý do,
và sẽ test failure path khi user không nhập vị trí hoặc nhập nhu cầu quá mơ hồ.
```

## 7. Backlog

Những thứ **không build trong Day 06**:

- Tích hợp bản đồ hoặc định vị GPS thật.
- Đặt món/thanh toán trong app.
- Crawl dữ liệu quán ăn real-time.
- Hệ thống review/rating đầy đủ.
- Cá nhân hóa dài hạn theo lịch sử ăn uống.
