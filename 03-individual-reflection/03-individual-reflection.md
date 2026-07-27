# 03 — Individual Reflection

**Học viên:** Ngô Việt Anh  
**Mã học viên:** 2A202601579  
**Vai trò / bối cảnh:** AI Researcher, tập trung vào LLM  
**Bài toán nhóm chọn:** Ưu tiên và điều phối task bị kẹt trước thời hạn

> Reflection này được đối chiếu với bản `02-group-problem-statement`. Tôi dùng AI
> để rà cấu trúc, phản biện metric và diễn đạt lại ghi chú; nội dung pitch,
> challenge, quyết định và bài học cần phản ánh đúng điều tôi hiểu và chịu trách
> nhiệm, không coi câu trả lời của AI là trải nghiệm thay cho mình.

## 1. Tôi đã tham gia vào phần nào?

| Hoạt động | Tôi đã làm gì? | Kết quả / ảnh hưởng |
|---|---|---|
| Scan cá nhân | Scan 10 vấn đề từ công việc AI Researcher, sau đó chọn ba bài về LLM error analysis, literature review và reproducibility | Có ba Problem Cards với actor, workflow, bottleneck, metric và boundary rõ để đem vào thảo luận |
| Pitch Problem Card | Pitch bài phân tích lỗi output LLM sau benchmark: researcher phải đọc output dài, gán taxonomy thủ công và dễ bỏ sót lỗi | Nhóm có thêm candidate thuộc nhóm evaluation/review; bài không được chọn cuối nhưng giúp mở rộng góc nhìn về human review |
| Challenge bài của bạn khác | Challenge bài “ưu tiên task trước thời hạn” ở hai điểm: Jira rule có đủ không, và AI có được tự đổi assignee không | Nhóm tách rõ Rule dùng để lọc task `<24h`, AI chỉ tóm tắt comment, PM giữ quyền phân công |
| Gom trùng / cluster | Cùng nhóm phân biệt ba cluster: Task & Deadline, Báo cáo/tổng hợp thông tin, Giáo dục/trợ lý học thuật | Tránh gộp mọi pain thành một “AI assistant” quá rộng |
| Chọn candidate problem | Đồng thuận chọn “Ưu tiên công việc trước thời hạn” sau khi so với bài gom deadline cá nhân | Candidate được chọn có actor, workflow, baseline và khả năng pilot rõ hơn |
| Validation / research | Xem lại tín hiệu từ ba PM/Team Lead và đối chiếu Jira Automation với Jira Intelligence | Nhóm thu hẹp pain từ “không thấy task trễ” sang “PM tốn thời gian đọc comment để hiểu nguyên nhân bị kẹt” |
| Workflow nhóm | Góp góc nhìn tách workflow thành Rule → LLM → human review, đồng thời yêu cầu fallback về đọc comment gốc | Future workflow không trao quyền điều phối nhân sự cho AI; PM vẫn kiểm tra và assign |
| Problem Statement | Làm rõ AI intervention point và boundary: AI chen giữa bước phát hiện task kẹt và bước PM ra quyết định | Problem Statement v1 nói rõ AI chỉ tóm tắt, không đổi trạng thái hoặc assignee |
| Rule / Workflow / Agent | Lập luận chọn Workflow thay vì Agent; Rule đủ cho lọc deadline nhưng không đủ để hiểu comment kỹ thuật | Nhóm chọn đúng mức tự chủ, giảm permission và rủi ro giao sai người |
| Decision | Đồng thuận `Go với scope nhỏ`, thử trên 10 task trễ cũ trước khi tích hợp Jira/Trello | Có pilot, human review và đường rollback nếu tóm tắt không đáng tin cậy |

## 2. Bảng dùng AI

| Phase | Tôi dùng AI để làm gì? | AI hữu ích ở đâu? | AI sai/hời hợt ở đâu? | Tôi sửa gì bằng nhận định của mình? |
|---|---|---|---|---|
| Scan | Gợi ý thêm problem theo bối cảnh AI Researcher | Mở rộng pain quanh evaluation, paper review và reproducibility | Một số ý quá rộng kiểu trợ lý nghiên cứu toàn năng | Chỉ giữ problem có actor, workflow thật và cách đo |
| Problem Card | Phản biện actor, bottleneck, metric và boundary | Giúp phát hiện metric chỉ đo tốc độ nhưng thiếu chất lượng | Có xu hướng xem thời gian ước lượng như baseline đã xác nhận | Ghi rõ giả định và yêu cầu đo lại bằng log/pilot |
| Workflow | Chuyển ghi chú before/after thành cấu trúc và Mermaid | Làm rõ bước Rule, bước AI và human boundary | Dễ nhảy từ “tóm tắt” sang “tự tìm người và assign” | Bỏ quyền tự hành động; PM luôn xem tóm tắt và tự phân công |
| Research | Gợi ý hướng tìm công cụ đang có | Giúp nhóm nhận ra Jira Automation và Jira Intelligence giải các phần khác nhau | Mô tả tính năng có thể lỗi thời hoặc nói quá nếu không mở nguồn | Chỉ dùng link chính thức và tự kiểm claim trước khi giữ |
| Problem Statement | Kiểm tra sáu field và chỉ ra chỗ mơ hồ | Giúp tách “phát hiện task trễ” khỏi “đọc hiểu nguyên nhân kẹt” | Có thể viết solution vào field Problem quá sớm | Viết lại bottleneck theo workflow hiện tại, đưa AI xuống intervention point |
| Rule / Workflow / Agent | So sánh mức tự chủ và failure cost | Làm rõ Agent không cần thiết khi flow cố định | AI thường đề xuất Agent vì nghe toàn diện hơn | Chọn Workflow; Rule lọc task, LLM tóm tắt, PM quyết định |
| Decision | Dùng checklist để rà pilot, boundary và rollback | Giúp tránh quyết định Go chung chung | AI không có bằng chứng thực tế và không được chốt thay nhóm | Nhóm tự chọn `Go với scope nhỏ`, giới hạn pilot ở 10 task lịch sử |

## 3. Reflection câu hỏi mở

### Tôi học được gì khi nghe problems của các bạn khác?

Tôi học được rằng problem có impact tốt không nhất thiết phải nằm đúng chuyên
môn LLM của mình. Candidate error analysis của tôi gần công việc cá nhân, nhưng
bài ưu tiên task sát deadline có actor phổ biến hơn, workflow dễ quan sát và
được hai trong ba PM/Team Lead xác nhận pain. Việc nghe các bài về deadline,
báo cáo và giáo dục cũng giúp tôi thấy nhiều problem có cùng pattern “đọc nhiều
ngữ cảnh rồi ra quyết định”, nhưng failure cost và human boundary rất khác nhau.

### Nhóm có lúc nào bị solution-first không?

Có. Cách gọi ban đầu “AI ưu tiên công việc” dễ dẫn tới ý tưởng Agent tự quét
task, kiểm tra lịch và đổi assignee. Sau khi vẽ workflow và xem phản hồi rằng
chỉ cần nhãn `Blocked` có thể giải một phần pain, nhóm nhận ra Rule đã đủ để
phát hiện task sát hạn. Phần đáng dùng LLM chỉ là đọc và tóm tắt comment dài;
quyết định phân người phải trả lại PM.

### Tôi có thay đổi ý kiến sau khi bị challenge không?

Ban đầu tôi ưu tiên bài phân tích lỗi output LLM vì có dữ liệu và metric phù hợp
với chuyên môn. Sau khi so score và xem validation của nhóm, tôi đồng ý chọn bài
ưu tiên task sát deadline vì scope pilot rõ hơn và có tín hiệu từ người dùng
ngoài người đề xuất. Tôi cũng thay đổi cách nhìn từ “AI giúp ưu tiên task” sang
“Rule phát hiện task cần chú ý, AI tóm tắt nguyên nhân, PM tự ưu tiên và assign”.

### Tôi đóng góp gì thật sự vào artifact cuối?

Đóng góp rõ nhất của tôi là góc nhìn đánh giá LLM: không xem một bản tóm tắt
trôi chảy là mặc nhiên đúng, luôn cần input gốc, human review và fallback. Góc
nhìn đó được phản ánh trong future workflow, boundary không cho AI đổi assignee
và cơ chế PM mở comment gốc khi tóm tắt vô lý. Tôi cũng giúp lập luận vì sao
Workflow phù hợp hơn Agent.

### Điều khó nhất khi viết Problem Statement là gì?

Khó nhất là xác định đúng bottleneck. Nếu viết “PM không biết task nào trễ”, một
filter deadline hoặc nhãn `Blocked` đã giải được phần lớn và AI không cần thiết.
Sau validation, nhóm sửa bottleneck thành “PM mất thời gian đọc nhiều comment
kỹ thuật để hiểu vì sao task bị kẹt”. Cách viết mới chỉ ra đúng intervention
point của LLM và giữ quyết định nhân sự ngoài phạm vi AI.

Một khó khăn khác là metric hiện chủ yếu đo thời gian `60 → 15 phút`. Metric này
chưa đủ bảo vệ chất lượng: tóm tắt nhanh nhưng bỏ mất blocker hoặc bịa nguyên
nhân vẫn có thể làm PM assign sai. Nếu phát triển tiếp, tôi sẽ thêm guardrail:
không bịa blocker/owner và giữ đủ các chi tiết quan trọng do PM đánh dấu trên
bộ 10 task pilot.

### Nếu làm lại, tôi sẽ challenge nhóm mạnh hơn ở điểm nào?

Tôi sẽ challenge mạnh hơn về quality metric và exit criterion. Điều kiện
rollback “AI sai ở 70% task” quá lỏng đối với một workflow ảnh hưởng tới phân
công nhân sự; ngay cả tỷ lệ sai thấp hơn cũng có thể gây hại nếu lỗi rơi đúng
task critical. Tôi sẽ yêu cầu nhóm định nghĩa “tóm tắt đúng và đủ”, gán nhãn
gold cho 10 task lịch sử, đo tỷ lệ bỏ sót blocker, tỷ lệ bịa chi tiết và thời
gian PM phải đọc lại comment trước khi quyết định mở rộng.

## 4. Bài học chính

- Bắt đầu từ actor và bottleneck giúp tách phần Rule đủ dùng khỏi phần thực sự
  cần hiểu ngôn ngữ.
- Validation có thể làm đổi problem: pain không nằm ở việc thấy task trễ mà ở
  việc hiểu nhanh nguyên nhân kẹt.
- Một Workflow tốt không nhất thiết giảm số bước; nó giảm effort ở đúng bước
  nghẽn và giữ điểm kiểm soát của con người.
- Human-in-the-loop không chỉ là “có người xem”. Người review phải có dữ liệu
  gốc, quyền override và trách nhiệm với quyết định cuối.
- Agent không phải mức trưởng thành mặc định. Khi đường đi cố định và hành động
  có failure cost cao, Workflow hẹp dễ audit phù hợp hơn.

Nếu làm lại:

> Tôi sẽ yêu cầu baseline chất lượng song song với baseline thời gian ngay từ
> đầu, đồng thời thử Rule-only trước. Chỉ khi Rule lọc task vẫn để lại bottleneck
> đọc comment đáng kể và LLM đạt yêu cầu fidelity trên dữ liệu lịch sử, tôi mới
> đề xuất tích hợp workflow vào công cụ quản lý dự án.

## 5. Kiểm tra hiểu bài cá nhân

**Problem → Workflow:**  
PM/Team Lead gần deadline phải rà Kanban, mở từng task, đọc nhiều comment, hỏi
người rảnh rồi assign hỗ trợ. Bước đọc comment khoảng 40/60 phút là bottleneck.

**Workflow → Metric:**  
Target chính là giảm thời gian rà soát và điều phối từ 60 xuống 15 phút. Cần bổ
sung metric chất lượng về blocker bị bỏ sót, chi tiết bị bịa và effort đọc lại.

**Metric → Boundary:**  
Vì một tóm tắt sai có thể dẫn đến giao sai người, AI chỉ tóm tắt. PM được xem
comment gốc và giữ toàn quyền đổi trạng thái/assignee.

**Boundary → độ phù hợp với AI:**  
Rule phù hợp với deadline có cấu trúc. LLM phù hợp với tóm tắt comment kỹ thuật.
Workflow đủ vì thứ tự bước cố định; Agent không cần thiết và có failure surface
lớn hơn.

**Decision:**  
`Go với scope nhỏ`: thử thủ công trên 10 task trễ lịch sử, đo thời gian và chất
lượng rồi mới cân nhắc tích hợp Jira/Trello. Nếu summary sai hoặc không tạo lợi
ích so với Rule + đọc tay, rollback về workflow cũ.

## 6. Tự kiểm cuối bài

- [x] [12đ cá nhân] Có 10 problems và Top 3 Problem Cards.
- [x] [12đ cá nhân] Đã pitch problem cá nhân và challenge bài nhóm về Rule,
  Agent và quyền đổi assignee.
- [x] Nhóm đã hội tụ từ các cluster về một candidate.
- [x] [15đ nhóm] Có workflow trước/sau, bottleneck và fallback.
- [x] [20đ nhóm] Có Problem Statement v0/v1 với metric và boundary.
- [x] [15đ nhóm] Có so sánh Rule / Workflow / Agent.
- [x] [10đ nhóm] Có quyết định `Go với scope nhỏ`, pilot và rollback.
- [x] [10đ cá nhân] Reflection nêu vai trò, cách dùng AI, bài học và điều sẽ đổi.
- [x] [6đ cá nhân] Tự giải thích được problem → workflow → metric → boundary →
  độ phù hợp với AI.
