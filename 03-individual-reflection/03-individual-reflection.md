# 03 — Individual Reflection

**Học viên:** Ngô Việt Anh  
**Mã học viên:** 2A202601579  
**Vai trò / bối cảnh:** AI Researcher, tập trung vào LLM  
**Trạng thái:** Bản nháp trước hoạt động nhóm — cần cập nhật bằng trải nghiệm thật

> Reflection là phần phải phản ánh đúng điều tôi đã làm trong nhóm. Vì hiện chưa
> có group artifact hoặc nhật ký thảo luận, tôi chỉ điền những hoạt động đã thực
> sự hoàn thành và để rõ phần cần cập nhật sau buổi nhóm. Tôi không dùng nội dung
> giả định để nhận là đóng góp đã xảy ra.

## 1. Tôi đã tham gia vào phần nào?

| Hoạt động | Tôi đã làm gì? | Kết quả / ảnh hưởng |
|---|---|---|
| Scan cá nhân | Scan 10 problems từ workflow của AI Researcher về evaluation, literature review, reproducibility, dataset, experiment tracking và GPU job | Có 3 candidate đủ actor, bottleneck, metric và boundary để pitch |
| Pitch Problem Card | Đã chuẩn bị pitch 60–90 giây cho bài phân tích lỗi đầu ra LLM | Sẵn sàng trình bày; kết quả shortlist cần cập nhật sau buổi nhóm |
| Challenge bài của bạn khác | Đã chuẩn bị tiêu chí hỏi về baseline, actor, process fix, failure cost và human boundary | Cần ghi lại câu hỏi thật đã đặt và bài nào thay đổi sau challenge |
| Gom trùng / cluster | Chưa diễn ra / chưa có dữ liệu nhóm | Cần cập nhật cluster và đóng góp cụ thể của tôi |
| Chọn candidate problem | Ưu tiên cá nhân là error analysis sau benchmark | Quyết định của nhóm chưa có; không được ghi thay bằng lựa chọn cá nhân |
| Validation / research | Đã đề xuất kế hoạch đo time log 2 tuần, phỏng vấn 1–2 đồng nghiệp và pilot 100–200 mẫu | Chưa có kết quả kiểm chứng; cần cập nhật evidence thật |
| Workflow nhóm | Đã có current/future workflow cá nhân cho 3 cards | Chưa biết workflow nào được nhóm dùng hoặc sửa |
| Problem Statement | Đã làm rõ actor, workflow, bottleneck, metric, boundary cho Card #1 | Problem Statement v0/v1 của nhóm chưa có |
| Rule / Workflow / Agent | Lập luận cá nhân chọn Workflow, dùng rule/script cho schema và sampling; không chọn Agent | Cần cập nhật lập luận và quyết định thật của nhóm |
| Decision | Đề xuất cá nhân: **Not Yet** cho triển khai rộng, **Go** cho pilot offline có human review | Final decision của nhóm chưa có |

## 2. Bảng dùng AI

| Phase | Tôi dùng AI để làm gì? | AI hữu ích ở đâu? | AI sai/hời hợt ở đâu? | Tôi sửa gì bằng nhận định của mình? |
|---|---|---|---|---|
| Scan | Mở rộng candidate theo bối cảnh AI Researcher về LLM | Gợi lại các pain quanh evaluation, paper triage và reproducibility | Một số gợi ý dễ thành “trợ lý nghiên cứu toàn năng”, không có actor/metric | Loại ý quá rộng, chỉ giữ workflow tôi có thể mô tả và kiểm chứng |
| Problem Card | Phản biện actor, bottleneck, metric, boundary và format lại nội dung | Giúp phát hiện metric chỉ đo tốc độ mà thiếu chất lượng | Có xu hướng xem số ước lượng như baseline đã được xác nhận | Ghi rõ số liệu là giả định; bổ sung kappa, traceability và review lỗi nghiêm trọng |
| Workflow | Chuyển mô tả thành current/future flow và chỉ ra intervention point | Làm rõ phần nào dùng rule, phần nào dùng LLM, phần nào người thật quyết định | Ban đầu có thể tự động hóa quá nhiều bước và làm mờ human boundary | Không cho AI tự ra quyết định khoa học, chạy command hay tiêu GPU |
| Research | Chưa dùng để tìm nguồn bên ngoài trong phase cá nhân này | Chưa đánh giá | Chưa đánh giá | Khi research, tôi sẽ chỉ giữ nguồn đã mở và kiểm tra trực tiếp |
| Problem Statement | Dùng để kiểm tra còn thiếu field nào | Giúp bổ sung failure condition và rollback | Không thể xác nhận pain hoặc baseline thay người trong workflow | Giữ kế hoạch interview/time log và không gọi giả định là evidence |
| Rule / Workflow / Agent | So sánh độ tự chủ và rủi ro của ba mức | Làm rõ Workflow đủ cho flow tuyến tính, Agent không cần thiết | Có thể đề xuất Agent vì nghe mạnh hơn dù chưa có nhu cầu lập kế hoạch động | Chọn rule cho join/sampling, LLM suggestion cho ngữ nghĩa, human review cho quyết định |
| Decision | Dùng AI làm checklist phản biện trước khi chốt | Nhắc kiểm tra exit criteria và fallback | AI không có quyền chốt Go/No-Go thay nhóm | Chỉ đề xuất pilot; quyết định cuối phải dựa vào evidence và đồng thuận nhóm |

## 3. Reflection hiện tại

Điều tôi học rõ nhất ở phase cá nhân là một bài toán “đúng chất LLM” chưa chắc
cần một Agent. Trong Card #1, phần ghép dữ liệu, kiểm schema và lấy mẫu phù hợp
với rule/script; LLM chỉ có lợi ở bước cần đọc ngữ nghĩa và đề xuất taxonomy.
Quyết định khoa học vẫn phải do researcher thực hiện vì một nhãn nghe hợp lý
nhưng sai có thể dẫn cả vòng ablation sang hướng khác.

Tôi cũng nhận ra metric “giảm từ 3–4 giờ xuống dưới 90 phút” chưa đủ. Nếu chỉ
tối ưu tốc độ, workflow có thể tạo automation bias hoặc bỏ sót lỗi hiếm nhưng
nghiêm trọng. Vì vậy tôi bổ sung agreement trên gold subset, khả năng truy vết
về `sample_id`, review 100% high-severity case và điều kiện rollback khi chất
lượng nhãn dưới ngưỡng.

Thay đổi quan điểm quan trọng của tôi là không coi AI là giải pháp đầu tiên.
Một schema kết quả thống nhất, taxonomy versioned, rule-based sampling và UI
gán nhãn có thể tạo phần lớn giá trị với rủi ro thấp. Chỉ khi baseline này vẫn
không đạt lead-time mục tiêu thì mới có lý do kiểm thử LLM-assisted labeling.

Phần khó nhất khi viết Problem Statement là phân biệt dữ kiện tôi đã quan sát
với con số tôi chỉ đang nhớ hoặc ước lượng. Tôi đã giữ các con số để tạo
hypothesis đo được, nhưng đánh dấu rõ chúng cần time log và phỏng vấn ngắn trước
khi trở thành bằng chứng.

Nếu làm lại phase cá nhân, tôi sẽ lấy hai experiment log thật trước khi xếp
hạng Top 3. Tôi cũng sẽ tạo taxonomy v0 từ 20–30 mẫu thật trước khi đặt ngưỡng
kappa, vì độ khó và phân bố lớp quyết định ngưỡng agreement nào là thực tế.

## 4. Phần tôi phải tự cập nhật sau hoạt động nhóm

Để reflection trở thành bản nộp cuối và trung thực, tôi sẽ thay phần này bằng
câu trả lời cụ thể ngay sau buổi thảo luận:

1. **Từ top 3 của các bạn, tôi học được:** `[ghi problem và insight cụ thể]`
2. **Nhóm có bị solution-first không:** `[thời điểm, ai challenge, nhóm sửa gì]`
3. **Tôi đổi ý sau challenge nào:** `[ý cũ → bằng chứng/câu hỏi → ý mới]`
4. **Đóng góp của tôi vào artifact cuối:** `[workflow/metric/boundary/research]`
5. **Điểm khó nhất của Problem Statement nhóm:** `[mô tả cụ thể]`
6. **Nếu làm lại, tôi sẽ challenge mạnh hơn:** `[điểm và lý do]`

## 5. Kiểm tra hiểu bài cá nhân

**Problem → Workflow:**  
Không thể biết AI nên nằm ở đâu nếu chưa mô tả ai đang làm gì và bước nào
nghẽn. Với Card #1, pain không phải “chưa có AI agent” mà là 120 phút đọc và
gán taxonomy trong workflow error analysis.

**Workflow → Metric:**  
Metric phải đo bottleneck và guardrail. Lead time đo tốc độ; kappa, traceability
và recall lỗi nghiêm trọng đo chất lượng.

**Metric → Boundary:**  
Vì lỗi nhãn có thể làm sai quyết định nghiên cứu, LLM chỉ đề xuất nhãn/evidence.
Researcher review trường hợp rủi ro và quyết định insight/experiment tiếp theo.

**Boundary → độ phù hợp với AI:**  
Rule/script đủ cho dữ liệu có cấu trúc. LLM phù hợp với đọc ngữ nghĩa trong một
workflow xác định. Agent không phù hợp vì chưa cần tự lập kế hoạch, tự dùng tool
hay tự hành động.

**Decision:**  
Hiện tại chọn **Go cho pilot offline, Not Yet cho triển khai rộng**. Chỉ mở rộng
khi đo được giảm lead time, đạt chất lượng nhãn và không bỏ sót lỗi nghiêm trọng;
nếu không, rollback về schema + rule + human labeling.

## 6. Tự kiểm cuối bài

- [x] Có 10 problems và Top 3 Problem Cards trong phần scan cá nhân.
- [ ] Đã pitch thật và ghi kết quả/challenge của nhóm.
- [ ] Đã cập nhật nhật ký hội tụ và candidate problem nhóm.
- [ ] Đã ghi đóng góp thật của tôi vào workflow/Problem Statement nhóm.
- [x] Đã giải thích cách dùng AI, điểm yếu và phần tôi tự sửa.
- [x] Đã nêu điều học được ở phase cá nhân và nếu làm lại sẽ đổi gì.
- [x] Tự giải thích được problem → workflow → metric → boundary → AI fit.
- [ ] Đã thay toàn bộ placeholder ở Mục 4 bằng trải nghiệm thật sau buổi nhóm.
