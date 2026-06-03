# Workshop — Mổ App AI Thật

**Sản phẩm:** Vietnam Airlines — NEO  
**Học viên:** Đặng Sỹ Tiến (Mã: 2A202600937)  
**Mục tiêu:** Tìm chỗ product gãy trong workflow thật, rồi viết finding đó thành quyết định product.

---

## 1. Chọn một sản phẩm để dùng thử

*   **Sản phẩm:** Vietnam Airlines — NEO
*   **AI feature:** Trợ lý ảo tìm kiếm chuyến bay, tra cứu thông tin vé, hành lý, và hỗ trợ khách hàng tự động 24/7.
*   **Cách truy cập:** Webchat trên Website chính thức / Zalo OA của Vietnam Airlines.

---

## 2. Dùng thử: promise vs reality

### Lời hứa của Product (Promise):
*   **Hành trình & Tìm kiếm giá vé:** Hỗ trợ hành khách tìm kiếm giá vé tốt nhất cho hành trình sắp tới một cách thuận tiện, nhanh chóng.
*   **Hỗ trợ thông tin:** Giải đáp mọi thắc mắc về hành lý (bao gồm hành lý đặc biệt như thú cưng), thủ tục, chính sách hoàn/đổi vé.
*   **Chuyển hướng thông minh:** Chuyển hướng gặp tư vấn viên đối với những câu hỏi NEO chưa thể giải đáp.
*   **Mẹo sử dụng:** *"Hãy hỏi câu hỏi ngắn, rõ ràng để NEO có thể hiểu được tốt nhất nội dung cần hỗ trợ"*.

### Thực tế trải nghiệm (Reality) & Điểm gãy (Failure points):
*   **Mất ngữ cảnh (Context Memory Loss):** Khi đang thực hiện luồng đặt vé (đã nhận diện đi từ Hà Nội, 3 người lớn), user chỉ cần chêm vào 1-2 câu hỏi ngoài lề (hỏi về thời tiết Nepal, hỏi về tính năng của bot), bot lập tức reset hoàn toàn số lượng khách về mặc định là 1 người lớn và bắt chọn lại điểm khởi hành từ đầu.
*   **Khóa trạng thái (State Lockout) & Quên thông tin khi tải chậm:** Khi bot đang trong trạng thái xử lý/tìm kiếm giá vé chặng bay mới (2 người lớn, 1 trẻ em), hệ thống bị "đơ" và liên tục yêu cầu user chờ đợi. Nếu user cố gắng sửa thông tin hành khách trong lúc này, bot từ chối cập nhật. Khi tìm kiếm xong, bot đột ngột bị "mất trí nhớ", quên sạch điểm đi (HAN) và ngày đi (07/06) đã lưu trước đó và bắt nhập lại toàn bộ.
*   **Hiểu sai ý định đính chính (NLU Intent Failure):** Khi user đính chính số lượng khách không phải 3 người lớn (*"đâu, tôi nói 3 người lớn đâu"*), bot không hiểu ngữ cảnh đính chính thông tin mà lại dịch thành ý định **hủy tìm kiếm** và bắt user xác nhận hủy (*"Quý khách vui lòng xác nhận lại việc hủy tìm kiếm giá vé hiện tại không?"*).
*   **Xử lý file đính kèm kém:** Gửi một file ảnh bất kỳ có thể làm bot tự động hủy bỏ luồng tìm kiếm vé ngay lập tức (*"NEO đã hủy chức năng tìm kiếm giá vé"*).

---

## 3. Vẽ 4 paths

| Path | Câu hỏi cần trả lời | Thực tế thể hiện tại NEO |
|---|---|---|
| **Happy** | Khi AI đúng và tự tin, user thấy gì? | User nhập thông tin hành trình liền mạch không ngắt quãng (Điểm đi, điểm đến, ngày đi, số khách) $\rightarrow$ Bot tổng hợp thông tin chính xác và tiến hành tìm vé. |
| **Low-confidence** | Khi AI không chắc, hệ thống có hỏi lại, show options hoặc chuyển người không? | **Chưa có cơ chế này tốt.** Khi user đính chính thông tin hoặc nhập thông tin mập mờ (như thủ đô Nepal không nhớ tên), bot tự ý suy diễn (thành 3 người lớn hoặc yêu cầu hủy tiến trình) thay vì đưa ra các nút chọn để xác nhận lại. |
| **Failure** | Khi AI sai, user biết bằng cách nào và sửa thế nào? | Bot tự động reset số lượng hành khách về 1 người hoặc mất sạch điểm đi mà không thông báo. User phát hiện bằng cách đọc lại tóm tắt thông tin của bot và buộc phải nhập lại từ đầu. |
| **Correction** | Khi user sửa, correction có được lưu/log/học lại không hay biến mất? | **Không được lưu.** Khi user sửa lại số lượng khách lúc hệ thống đang tải, bot phớt lờ yêu cầu, tiếp tục bắt chờ, sau đó reset sạch thông tin cũ làm user phải nhập lại toàn bộ hành trình. |

---

## 4. Viết finding thành quyết định

### Finding 1: Mất ngữ cảnh hội thoại khi có câu hỏi xen ngang (Context Memory Loss)
*   **Trigger:** Khi user đang ở giữa luồng đặt vé (đã lưu 3 khách người lớn, chặng bay Hà Nội), hỏi một câu ngoài phạm vi (Out-of-scope) như thời tiết hoặc tính năng của bot, rồi quay lại cung cấp tiếp thông tin ngày đi.
*   **Failure:** AI/product tự động xóa/reset các thông tin đã thu thập trước đó, quay về mặc định là 1 khách người lớn và bắt khai báo lại điểm đi.
*   **Impact (Hậu quả):** Trải nghiệm hội thoại bị đứt gãy nghiêm trọng, tốn thời gian khai báo lại, dễ gây nhầm lẫn dẫn đến đặt sai số lượng vé.
*   **Lỗi thuộc layer:** `Session State / Context Tracking`.
*   **Nên sửa bằng (Product Decision):** 
    *   *UX/Fallback:* Lưu trữ tạm thời các slot thông tin đã điền (Origin, Passengers, Destination) vào Cache Session. Khi user quay lại luồng đặt vé sau khi ngắt quãng, bot hiển thị thông báo: *"Bạn đang đặt vé cho 3 người lớn đi từ Hà Nội. Chúng ta tiếp tục nhé?"*.

### Finding 2: Khóa trạng thái tìm kiếm (Search Lockout) & Reset thông tin
*   **Trigger:** Khi hệ thống đang gọi API tìm kiếm giá vé và bị chậm, user gửi yêu cầu cập nhật lại số lượng khách.
*   **Failure:** Bot khóa tương tác (Loading state), liên tục bắt user chờ đợi và không cho phép cập nhật thông tin mới. Sau khi load xong, bot tự reset toàn bộ điểm đi và ngày đi.
*   **Impact (Hậu quả):** Người dùng bị kẹt, không thể chỉnh sửa thông tin sai và cuối cùng phải làm lại từ đầu do bot mất dữ liệu.
*   **Lỗi thuộc layer:** `UX Recovery / State Machine`.
*   **Nên sửa bằng (Product Decision):** 
    *   *Requirement/UX:* Hỗ trợ nút "Hủy tìm kiếm và sửa lại thông tin" ngay lập tức khi đang tải. Khi hoàn tất tải, giữ nguyên các thông tin cũ đã điền thành công, chỉ cập nhật lại trường thông tin được sửa đổi.

---

## 5. Sketch as-is / to-be

### Sơ đồ luồng hiện tại (As-is Flow)
```text
[Bắt đầu đặt vé] 
      │
      ▼
[User khai báo: Hà Nội, 3 người lớn] (NEO ghi nhận: HAN, 3 Adults)
      │
      ▼
[User hỏi xen ngang: Thời tiết Nepal] ──► [NEO báo: Ngoài phạm vi]
      │
      ▼
[User nhập ngày đi: 6/6]
      │
      ▼
[Điểm gãy: NEO quên thông tin cũ] ◄── LỖI: Reset về 1 Người lớn & bắt nhập lại điểm đi!
      │
      ▼
[User phải gõ lại từ đầu]
```

### Sơ đồ luồng đề xuất (To-be Flow)
```text
[Bắt đầu đặt vé] 
      │
      ▼
[User khai báo: Hà Nội, 3 người lớn] (Lưu vào Session Cache: Origin=HAN, Passengers=3)
      │
      ▼
[User hỏi xen ngang: Thời tiết Nepal] ──► [NEO báo: Ngoài phạm vi]
      │
      ▼
[User nhập ngày đi: 6/6]
      │
      ▼
[NEO đối chiếu Session Cache] ──► Nhận diện thông tin cũ vẫn còn hiệu lực
      │
      ▼
[NEO phản hồi thông minh] ──► "NEO tiếp tục tìm vé HAN đi Nepal ngày 6/6 cho 3 người lớn nhé?"
                                 [Đồng ý]    [Sửa thông tin]
```

---

## 6. Tự kiểm trước khi nộp

*   [x] Có ít nhất 1 screenshot hoặc observation cụ thể (Trích dẫn trực tiếp hội thoại thực tế của user).
*   [x] Có đủ 4 paths hoặc nói rõ path nào chưa có trong product (Đã chỉ ra Low-confidence path chưa có).
*   [x] Finding được viết thành product decision, không chỉ là nhận xét (Đã viết rõ layer lỗi và đề xuất kỹ thuật/UX).
*   [x] Sketch có as-is và to-be (Đã phác thảo dạng sơ đồ chữ rõ ràng).
*   [x] Có một câu nói rõ finding này sẽ đổi gì trong SPEC.
    *   *Câu chốt:* Finding này chứng minh việc **Quản lý trạng thái phiên làm việc (Session state)** và **Khôi phục lỗi (UX Recovery)** là tối quan trọng đối với Chatbot AI giao dịch. Trong bản SPEC của nhóm, chúng tôi sẽ bổ sung bắt buộc yêu cầu kỹ thuật về việc lưu trữ Session Cache cho các trường thông tin quan trọng và cơ chế hiển thị nút hủy/sửa nhanh khi hệ thống đang xử lý tác vụ dài (Loading state).
