# Template — Thin SPEC Cuối Day 05

Thin SPEC không phải PRD đầy đủ. Đây là bản cam kết đủ rõ để sáng Day 06 nhóm build ngay.

## 1. Track, product/app và user

**Track: C - Food & Delivery**  
**Product/app thật: Chat bot hỗ trợ đề xuất món ăn**  
**User cụ thể: Sinh viên, dân văn phòng, khách du lịch**  
**Nhóm có phải user thật không? Nếu không, khác ở đâu?:Có. Các thành viên trong nhóm thường xuyên gặp tình trạng không biết ăn gì và phải mất nhiều thời gian tìm kiếm trên các ứng dụng giao đồ ăn.**  

## 2. Evidence summary

| Evidence | Nguồn | User/pain nói lên điều gì? | SPEC phải đổi gì? |
|---|---|---|---|
| AI/app chỉ gợi ý món ăn theo tâm trạng, chưa xét đến vị trí người dùng mong muốn. | anh_minh_chung/1.png | User không chỉ cần tên món, họ cần gợi ý có thể hành động được trong khu vực của mình. | SPEC phải thêm input bắt buộc về vị trí/khu vực trước khi AI recommend. |
| User muốn tìm món ăn theo tâm trạng và vị trí nhưng app chỉ hiển thị danh sách quán | Quan sát | User cần được hỗ trợ chốt quyết định, không phải nhận một danh sách chung chung. | SPEC phải có low-confidence path: AI hỏi lại 2-3 câu khi thiếu thông tin quan trọng. |
| Nếu gợi ý không phù hợp, user không có cách sửa tiêu chí ngay trong flow. |anh_minh_chung/1.png | User cần recovery path để chỉnh lại location, budget hoặc preference mà không phải bắt đầu lại. | SPEC phải thêm correction flow: user có thể sửa tiêu chí và AI tạo lại gợi ý. |

## 3. Pain statement

```text
Sinh viên, khách du lịch, dân văn phòng đang gặp khó ở việc tìm quán ăn họp lí,
vì có quá nhiều món ăn tại Hà Nội và họ không biết nên ăn ở hàng nào,
dẫn tới mất rất nhiều thời gian cho việc ăn uống, kèm theo đó là việc ăn bừa dẫn đến món ăn không ngon.
Bằng chứng chính là các bình luận review trên tiktok.
```

## 4. Build slice

```text
Cho [user] đang [task/workflow],
prototype sẽ dùng AI để automate hành động hẹp,
đưa ra vị trí địa điểm ăn uống mình mong muốn,
và xử lý trường hợp đề xuất không chính xác bằng cơ chế hỏi lại và cho phép người dùng điều chỉnh yêu cầu.
```

## 5. Auto/Aug decision

Chọn một:

- [x] **Augmentation:** AI gợi ý/draft/phân loại, user quyết cuối.
- [ ] **Conditional automation:** AI tự làm trong case hẹp; case mơ hồ/rủi ro chuyển người.
- [ ] **Automation:** AI tự quyết và tự hành động.

**Lý do chọn:**  
**Human role:** reviewer / decider / trainer / rescuer / none  

## 6. Four paths

| Path | Prototype phải thể hiện gì? |
|---|---|
| Happy | User cung cấp đầy đủ vị trí, ngân sách và sở thích ăn uống từ đó AI đề xuất 3–5 quán ăn phù hợp kèm lý do và thông tin địa điểm. |
| Low-confidence |User chỉ nhập yêu cầu mơ hồ như "Tôi không biết ăn gì" hoặc "Hôm nay buồn quá" dẫn đến AI nhận biết thiếu ngữ cảnh và hỏi thêm vị trí, ngân sách hoặc loại món ăn yêu thích. |
| Failure | AI không tìm được quán phù hợp hoặc dữ liệu không đủ cho khu vực người dùng yêu cầu dẫn đến AI thông báo rõ lý do và đề xuất mở rộng phạm vi tìm kiếm hoặc thay đổi tiêu chí. |
| Correction | User không hài lòng với kết quả ("quán này xa quá", "đắt quá", "tôi không thích đồ cay"). AI tiếp nhận phản hồi và đưa ra danh sách đề xuất mới phù hợp hơn. |

## 7. Failure mode nguy hiểm nhất

```text
Nếu user chỉ cung cấp yêu cầu mơ hồ như "Tôi muốn ăn gì đó ngon" hoặc "Hôm nay tôi buồn",
AI có thể đưa ra các quán ăn không phù hợp với vị trí, ngân sách hoặc khẩu vị thực tế của người dùng,
hậu quả là người dùng mất thời gian di chuyển, trải nghiệm không tốt và mất niềm tin vào hệ thống.
Prototype sẽ xử lý bằng cách hỏi lại các thông tin còn thiếu như vị trí, ngân sách và sở thích ăn uống trước khi đưa ra đề xuất.
Owner kiểm thử path này là Trần Nhất Huy.

```

## 8. Owner plan cho sáng Day 06

| Thành viên | Việc phụ trách | Bằng chứng cần có trong repo |
|---|---|---|
|Đặng Sỹ Tiến,Nguyễn Minh Anh,Nguyễn Trung Dân ,Trần Nhất Huy | Research / evidence |  |
|Trần Nhất Huy,Nguyễn Minh Anh | SPEC |  |
|Đặng Sỹ Tiến  | Prototype |  |
|Nguyễn Minh Anh, Trần Nhất Huy| Test / failure path |  |
|Nguyễn Trung Dân,Đặng Sỹ Tiến | Demo script / repo |  |
