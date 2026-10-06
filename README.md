# Track 1 — Day 20: Metrics Pack

## Thông tin học viên

- **Họ tên:** Đinh Thị Minh Tâm
- **MHV:** 2A202602433
- **Dự án chọn làm:** Triplan — AI Travel Planner hỗ trợ người dùng lên kế hoạch chuyến đi cá nhân

## Tệp Metrics Pack

- **Link:** [https://docs.google.com/document/d/1IL81yFdJVrZYdhdiNP4wtG9PtwuoDQrgHMUiZ29zapE/edit?hl=vi&tab=t.y1p5kpjxrbz8](https://docs.google.com/document/d/1IL81yFdJVrZYdhdiNP4wtG9PtwuoDQrgHMUiZ29zapE/edit?hl=vi&tab=t.y1p5kpjxrbz8)

## Điều tôi mang về áp dụng cho dự án thật

Qua bài lab, tôi nhận ra không nên bắt đầu xây metric từ những chỉ số quen thuộc như DAU, số lượt mở app hay số lần hỏi AI, mà cần bắt đầu từ hành vi chứng minh người dùng thực sự nhận được giá trị.

Với Triplan, điều quan trọng không phải AI tạo được bao nhiêu lịch trình mà là người dùng có thể chốt được một lịch trình đủ phù hợp để sử dụng cho chuyến đi. Vì hành vi này xảy ra theo từng chu kỳ lên kế hoạch du lịch chứ không phải hàng ngày, tôi sẽ ưu tiên đo theo trip planning cycle và next-trip retention thay vì ép các chỉ số D7 hoặc weekly retention.

Khi áp dụng vào dự án thật, tôi muốn dùng bộ metric này để kiểm tra liệu Triplan có thực sự giúp người dùng lên kế hoạch nhanh hơn, ít phải sửa lại hơn và có quay lại sử dụng cho chuyến đi tiếp theo hay không. Kết quả mong muốn là giảm effort trong quá trình lập kế hoạch nhưng vẫn đảm bảo itinerary đủ phù hợp và khả thi.

## AI Support Log

Xem [ai-support-log.md](ai-support-log.md).

## Khung nội dung tệp Metrics Pack

### 00 — Dự án, persona, core job

- **Dự án:** Triplan — AI Travel Planner hỗ trợ người dùng lên kế hoạch chuyến đi cá nhân.
- **Persona:** Người trẻ tự lên kế hoạch cho chuyến du lịch cá nhân hoặc nhóm nhỏ.
- **Core job:** Tôi mất nhiều thời gian tìm, so sánh và ghép thông tin từ nhiều nguồn nhưng vẫn khó chốt được một lịch trình phù hợp với thời gian, ngân sách và sở thích của mình.

### 01 — Core Action Card (+ kết quả tự kiểm 5 tiêu chí)

#### Core Action Card

| Thành phần | Nội dung |
| --- | --- |
| **Target user** | Người trẻ tự lên kế hoạch cho chuyến du lịch cá nhân hoặc nhóm nhỏ |
| **Core job** | Tìm và chốt được một lịch trình phù hợp với thời gian, ngân sách và sở thích mà không phải mất nhiều công sức tổng hợp thông tin |
| **Core action** | Chốt một lịch trình chuyến đi để sử dụng |
| **Object** | Itinerary của một chuyến đi cụ thể |
| **Preconditions** | Người dùng đã có ít nhất điểm đến, thời gian chuyến đi và một itinerary để xem xét |
| **Completion rule** | Người dùng chủ động xác nhận itinerary là kế hoạch họ dự định sử dụng |
| **Core value** | Có một kế hoạch chuyến đi đủ rõ ràng và khả thi để sử dụng |
| **Evidence of value** | Người dùng chủ động chốt itinerary thay vì chỉ xem output AI |
| **Candidate event** | `itinerary_committed` |

| Tiêu chí tự kiểm | Kết quả | Giải thích / bằng chứng |
| --- | --- | --- |
| 1. Gần core value | Đạt | Khi user chốt itinerary, họ đã tiến gần trực tiếp tới việc có một kế hoạch sử dụng được |
| 2. Có thể lặp lại | Đạt | Hành vi có thể xuất hiện ở mỗi chuyến đi mới |
| 3. Có thể quan sát | Đạt | Có thể xác định chính xác khi itinerary chuyển sang trạng thái committed |
| 4. Có ý nghĩa | Đạt | Itinerary được chốt có ý nghĩa hơn số lượng itinerary chỉ được AI generate |
| 5. Có thể tác động | Đạt | Team có thể cải thiện recommendation, routing, personalization và editing flow để tăng khả năng user chốt itinerary |

### 02 — Action Nature Card + kết luận cadence

#### Action Nature Card

| Thành phần | Nội dung |
| --- | --- |
| **Actor** | Người dùng đang tự lên kế hoạch cho một chuyến đi cụ thể |
| **Intent** | Muốn chốt được lịch trình phù hợp với thời gian, ngân sách và sở thích |
| **Trigger** | Chủ yếu do user chủ động khi có ý định đi du lịch; đôi khi do kỳ nghỉ, vé máy bay, lời rủ hoặc sự kiện sắp tới |
| **Effort** | Trung bình đến cao, vì user cần cung cấp thông tin và xem xét/chỉnh sửa itinerary |
| **Value timing** | Value xuất hiện khi itinerary đủ rõ ràng để dùng, và được xác nhận thêm khi chuyến đi thực sự diễn ra |
| **State** | Itinerary, preference, địa điểm, thời gian và các lựa chọn của user được lưu lại |
| **Dependency** | Phụ thuộc vào thời gian chuyến đi, địa điểm, giờ mở cửa, thời gian di chuyển, ngân sách và đôi khi người đi cùng |
| **Repeat condition** | Khi user có chuyến đi mới hoặc itinerary hiện tại thay đổi đáng kể |

- **Kết luận cadence:** Core action thuộc dạng **theo dự án**. Hành vi chốt itinerary thường xuất hiện một hoặc một vài lần trong mỗi trip planning cycle. Vì vậy nhịp đo phù hợp là theo **trip planning cycle ở cấp Trip × User**, không phải daily hoặc weekly.

### 03 — Metric System (activation / engagement / NSM / leading / counter)

| Nhóm metric | Metric | Định nghĩa / cách tính | Cửa sổ đo |
| --- | --- | --- | --- |
| **Activation** | Trip Activation Rate | Số trip có `itinerary_committed` / số `trip_created` đủ điều kiện | Trong 7 ngày từ `trip_created` hoặc trước ngày khởi hành, tùy mốc nào đến trước |
| **Engagement** | Committed Trip Rate | Số trip có `itinerary_committed` / số eligible trip planning cycles | Theo trip planning cycle |
| **Engagement** | Time to Commitment | Thời gian từ `trip_created` đến `itinerary_committed` | Theo từng trip planning cycle |
| **NSM** | Qualified Committed Trips / Eligible Planner / Planning Cycle | Số trip có itinerary được user chốt và vượt quality threshold trên mỗi planner có nhu cầu lập kế hoạch | Theo trip planning cycle |
| **Leading** | First Draft Acceptance Rate | Tỷ lệ itinerary được commit mà không cần major regeneration | Theo trip planning cycle |
| **Leading** | Recommendation-to-Plan Add Rate | Số recommendation được thêm vào itinerary / số recommendation được xem | Theo trip planning cycle |
| **Leading** | Major Revision Rate | Số trip cần major revision / số trip có itinerary generated | Theo trip planning cycle |
| **Counter** | Post-commit Major Correction Rate | Số committed trip phải sửa lớn sau khi commit / tổng committed trip | Theo trip planning cycle |
| **Counter** | Itinerary Feasibility Error Rate | Tỷ lệ itinerary có lỗi nghiêm trọng về thời gian, di chuyển hoặc constraint | Theo trip planning cycle |

### 04 — Retention Definition (6 thành phần)

| Thành phần | Định nghĩa |
| --- | --- |
| **1. Unit** | User / planner |
| **2. Cohort entry** | User lần đầu có một `qualified_itinerary_committed` |
| **3. Return event** | User có `qualified_itinerary_committed` trên một trip mới |
| **4. Window** | Next eligible travel-planning cycle, quan sát tối đa 12 tháng |
| **5. Threshold** | Có ít nhất 1 qualified committed itinerary cho trip mới |
| **6. Segment** | User thực sự phát sinh ít nhất một `trip_created` mới trong observation window |

**Retention metric:** Next-Trip Retention Rate

`Số user chốt itinerary ở chuyến tiếp theo / số user thực sự phát sinh chuyến đi tiếp theo`

### 05 — Product Loop (2 chu kỳ + metric hypothesis)

- **Chu kỳ 1:** Có ý định đi du lịch → tạo trip và cung cấp constraint → Triplan tạo itinerary → user review/chỉnh sửa → chốt itinerary → có kế hoạch rõ ràng → lưu preference và itinerary → kế hoạch thay đổi → quay lại điều chỉnh → chốt lại itinerary.

- **Chu kỳ 2:** Trip trước được hoàn thành → preference và lịch sử lựa chọn được giữ lại → user phát sinh chuyến đi mới → Triplan dùng dữ liệu trước đó để tạo đề xuất phù hợp hơn → user cần ít chỉnh sửa hơn → chốt itinerary cho chuyến mới → preference tiếp tục được cập nhật.

- **Metric hypothesis:** Nếu product loop hoạt động tốt, **Next-Trip Retention Rate sẽ tăng trong vòng 12 tháng**, vì preference và lịch sử lập kế hoạch được lưu từ chuyến trước giúp người dùng tạo và chốt itinerary cho chuyến tiếp theo với ít effort hơn.

### 06 — Tracking nhanh (4–8 events + 2 acceptance criteria)

| Event | Khi nào ghi nhận | Thuộc tính cần thu thập | Metric liên quan |
| --- | --- | --- | --- |
| `trip_created` | Khi trip mới được lưu thành công với ít nhất điểm đến và thời gian dự kiến | `user_id`, `trip_id`, `destination`, `start_date`, `end_date`, `timestamp` | Activation denominator, Time to Commitment, Next-Trip eligibility |
| `itinerary_generated` | Khi một itinerary hoàn chỉnh được tạo và lưu thành công | `user_id`, `trip_id`, `itinerary_id`, `version`, `timestamp` | First Draft Acceptance Rate, Major Revision Rate |
| `recommendation_viewed` | Khi recommendation thực sự được hiển thị cho user | `user_id`, `trip_id`, `recommendation_id`, `timestamp` | Recommendation-to-Plan Add Rate |
| `recommendation_added` | Khi recommendation được thêm thành công vào itinerary | `user_id`, `trip_id`, `recommendation_id`, `itinerary_id`, `timestamp` | Recommendation-to-Plan Add Rate |
| `itinerary_majorly_revised` | Khi một thay đổi lớn đối với cấu trúc itinerary được lưu thành công | `user_id`, `trip_id`, `itinerary_id`, `version`, `revision_type`, `timestamp` | Major Revision Rate |
| `itinerary_committed` | Khi user chủ động chuyển itinerary từ draft/review sang committed | `user_id`, `trip_id`, `itinerary_id`, `timestamp` | Activation, NSM, Committed Trip Rate, Retention |
| `itinerary_reopened` | Khi itinerary đã committed được chuyển lại sang editing và có major revision | `user_id`, `trip_id`, `itinerary_id`, `timestamp` | Post-commit Major Correction Rate |
| `itinerary_validation_failed` | Khi hệ thống kiểm tra và phát hiện ít nhất một lỗi feasibility nghiêm trọng | `user_id`, `trip_id`, `itinerary_id`, `error_type`, `timestamp` | Itinerary Feasibility Error Rate |

1. **Acceptance criterion 1:** Với mỗi cặp `user_id` và `trip_id`, hệ thống chỉ ghi `itinerary_committed` khi itinerary thực sự chuyển từ trạng thái chưa chốt sang committed do hành động của user. Reload, autosave, request thất bại hoặc backend retry không được tạo thêm event.

2. **Acceptance criterion 2:** `recommendation_added` chỉ được ghi khi recommendation thực sự được thêm thành công vào itinerary. Việc user chỉ xem chi tiết, click recommendation hoặc request thêm bị lỗi không được tính.