# 01 — Individual Problem Scan

**Học viên:** Ngô Việt Anh  
**Mã học viên:** 2A202601579  
**Vai trò / bối cảnh:** AI Researcher, tập trung vào Large Language Models (LLM)

> Ghi chú về bằng chứng: các mốc thời gian và tần suất dưới đây là baseline
> ước lượng từ workflow cá nhân. Trước khi dùng để quyết định triển khai, tôi
> cần ghi time log trong 2 tuần và đối chiếu với ít nhất 1–2 đồng nghiệp.

## 1. Scan rộng

Tôi scan 9 vấn đề trước khi chọn giải pháp. Các vấn đề trải trên bốn lăng kính:
lặp lại, tốn thời gian, AI có thể hỗ trợ tốt hơn và pain từ người khác.

| # | Lăng kính | Problem quan sát được | Ai chịu ảnh hưởng? | Dấu hiệu thật / cách kiểm chứng |
|---:|---|---|---|---|
| 1 | Lặp lại, tốn thời gian | Sau mỗi vòng benchmark, việc đọc output và gán taxonomy lỗi cho các model vẫn làm thủ công | AI Researcher, Research Lead | Ước lượng 3–4 giờ/vòng, khoảng 2 vòng/tuần; có thể đo từ timestamp của experiment và research note |
| 2 | Tốn thời gian, AI có thể hỗ trợ | Tìm, sàng lọc và ghi chú paper LLM mới từ nhiều nguồn làm chậm quá trình cập nhật hướng nghiên cứu | AI Researcher | Khoảng 4 giờ/tuần; nhiều paper chỉ bị loại sau khi đã đọc abstract, method và experiment |
| 3 | Tốn thời gian | Tái lập một paper từ bài báo, repository và file config thường mắc ở các giả định không được ghi rõ | AI Researcher, Research Engineer | Ước lượng 5–8 giờ trước khi có first valid run; thường phải sửa environment/config nhiều lần |
| 4 | Lặp lại | Kết quả thí nghiệm nằm rải rác trong terminal log, tracker, JSONL/CSV và notebook nên phải ghép thủ công khi viết báo cáo | AI Researcher, Research Lead | Lặp lại sau mỗi batch experiment; dễ lệch run ID, seed hoặc checkpoint |
| 5 | Tốn thời gian | Kiểm tra khả năng benchmark contamination giữa pretraining data, instruction data và evaluation set thiếu một quy trình truy vết nhất quán | AI Researcher, Evaluation Engineer | Cần search nhiều biến thể câu, so khớp gần đúng và review thủ công; kết luận thường còn bất định |
| 6 | Pain từ người khác | Research Lead khó biết một cải thiện metric đến từ prompt, data, seed, checkpoint hay code change nào | Research Lead, AI Researcher | Câu hỏi truy vết lặp lại trong review; metadata giữa các run chưa đồng nhất |
| 7 | Lặp lại | Sau khi đổi prompt, model hoặc serving stack, bộ regression test cho hành vi LLM phải được chạy và đọc lại | AI Researcher, ML Engineer | Lặp lại mỗi lần release/ablation; pass rate tổng có thể che lỗi nghiêm trọng ở một nhóm nhỏ |
| 8 | Pain từ người khác | GPU job thất bại nhưng log dài và thông báo cuối không chỉ ra nguyên nhân gốc | AI Researcher, MLOps/ML Engineer | Phải đọc scheduler log, stderr và metric trước lỗi; cùng loại lỗi có thể được xử lý lại nhiều lần |
| 9 | Pain từ người khác, lặp lại | Thành viên mới khó tìm lại lý do chọn dataset, metric, prompt hoặc loại một hướng thử nghiệm | Research Intern, thành viên mới, Research Lead | Quyết định nằm rải rác trong chat, issue và notebook; câu hỏi onboarding bị lặp lại |

## 2. Chọn Top 3

| Rank | Problem | Vì sao chọn | Điều còn chưa chắc |
|---:|---|---|---|
| 1 | Phân tích lỗi đầu ra LLM sau benchmark | Xảy ra thường xuyên, bottleneck rõ, có dữ liệu đầu vào/đầu ra và đo được thời gian lẫn chất lượng nhãn | Baseline thời gian thực tế; taxonomy lỗi có ổn định giữa các task không |
| 2 | Sàng lọc và tổng hợp paper LLM | Tốn thời gian hằng tuần; LLM phù hợp với đọc, so sánh và trích xuất nếu có ràng buộc nguồn | Recall của bước triage; quyền truy cập full text; cách đo “bỏ sót paper quan trọng” |
| 3 | Tạo runbook để tái lập paper/repository | Impact lớn, workflow có thể vẽ và giúp cả researcher mới lẫn người review | Chất lượng README/config giữa repository khác nhau; lỗi phần cứng khó chuẩn hóa |

Tiêu chí ưu tiên của tôi là: pain lặp lại, có artifact thật để kiểm tra, có
human boundary rõ và có thể pilot nhỏ mà không cấp quyền tự chủ rộng cho AI.

---

## 3. Problem Card #1 — Phân tích lỗi đầu ra LLM

**Problem 1 câu:**  
Sau mỗi vòng benchmark, AI Researcher mất khoảng 3–4 giờ để ghép kết quả, đọc
các mẫu model trả lời sai và gán taxonomy lỗi thủ công, khiến vòng lặp
experiment → insight → thí nghiệm tiếp theo bị chậm.

**Actor:**  
AI Researcher chịu trách nhiệm đánh giá và so sánh các biến thể LLM.

**Thời điểm / bối cảnh:**  
Sau khi hoàn thành một vòng benchmark hoặc ablation, trước buổi research review
và trước khi quyết định thí nghiệm tiếp theo.

**Current workflow (7 bước):**

1. Xuất prediction, reference, score và metadata từ từng run.
2. Ghép dữ liệu theo sample ID, model, checkpoint, prompt và seed.
3. Lọc các mẫu điểm thấp, model bất đồng hoặc có lỗi nghiêm trọng.
4. Đọc lần lượt prompt, reference, response và judge feedback.
5. Gán loại lỗi, mức độ nghiêm trọng và ghi evidence.
6. Tổng hợp tỷ lệ lỗi, tìm pattern theo model/task/slice.
7. Viết error-analysis memo và đề xuất experiment tiếp theo.

**Bottleneck:**  
Bước 4–5: đọc và gán nhãn thủ công cho nhiều output, ước lượng khoảng 120 phút
trong tổng 210 phút cho một vòng; nhãn dễ thiếu nhất quán khi mệt hoặc khi
taxonomy chưa rõ.

**Impact:**  
Nếu có hai vòng đánh giá/tuần, riêng error analysis tốn khoảng 6–8 giờ. Insight
đến muộn làm chậm ablation tiếp theo; nhãn không nhất quán có thể dẫn đến chọn
sai hướng cải thiện model.

**Success metric:**

- Giảm median lead time từ khi benchmark kết thúc đến khi có memo từ khoảng
  210 phút xuống dưới 90 phút.
- Trên mẫu kiểm tra do researcher gán độc lập, nhãn hỗ trợ đạt Cohen's kappa
  tối thiểu 0,80; không chỉ đo accuracy tổng vì taxonomy có thể lệch lớp.
- 100% nhãn và nhận định trong memo truy ngược được tới `sample_id` và evidence.
- 100% lỗi mức nghiêm trọng cao được người thật review trước khi dùng để ra
  quyết định.

**Non-AI alternative:**  
Chuẩn hóa schema JSONL, tự động join run bằng script, dùng rule để chọn sample,
taxonomy cố định và giao diện gán nhãn. Phương án này nên làm trước vì giải
quyết lỗi dữ liệu và truy vết mà không cần LLM; tuy nhiên vẫn chưa giảm nhiều
effort đọc/ngữ nghĩa.

**AI hypothesis:**  
Sau bước rule-based sampling, LLM chỉ đề xuất `error_type`, `severity`,
`evidence_span` và `confidence` theo schema đóng. Researcher review nhãn quan
trọng, nhãn confidence thấp và một mẫu phân tầng; AI không tự quyết định model
nào tốt hơn hoặc experiment nào phải chạy.

**Quick gut:**

- [ ] No AI / process fix
- [ ] Rule
- [x] Workflow
- [ ] Agent
- [ ] Chưa biết

### Draft current workflow

```text
CURRENT STATE — baseline ước lượng 210 phút/vòng

[1 Export kết quả: 15']
→ [2 Join + kiểm schema: 25']
→ [3 Chọn mẫu cần xem: 20']
→ [4 Đọc output: 70']                 <-- bottleneck
→ [5 Gán taxonomy + evidence: 50']    <-- bottleneck
→ [6 Tổng hợp pattern: 20']
→ [7 Viết memo: 10']
```

### Draft future workflow

```text
FUTURE STATE — mục tiêu dưới 90 phút/vòng

[1 Pipeline export + validate schema: 10']        -- Rule/script
→ [2 Chọn mẫu theo score/disagreement/slice: 5']  -- Rule
→ [3 LLM đề xuất nhãn + evidence + confidence: 5']
→ [4 Researcher review high-risk/low-confidence
     + 30% mẫu phân tầng: 45']                    -- Human boundary
→ [5 Script tổng hợp theo model/task/slice: 5']
→ [6 Researcher diễn giải + viết memo: 15']       -- Human decision

Fallback:
- LLM trả sai schema → retry một lần bằng structured output; vẫn sai → chuyển
  sang giao diện gán nhãn thủ công.
- Kappa dưới 0,80 hoặc lỗi high-severity bị bỏ sót → tắt bước auto-label,
  giữ script join/sampling và quay lại human labeling.
```

**Rủi ro chính:** automation bias, taxonomy drift, judge/model bias, response
có prompt injection, và model tạo evidence không tồn tại. Biện pháp kiểm soát là
chỉ trích evidence nguyên văn từ input, không cho tool access, version hóa
taxonomy/prompt và kiểm tra định kỳ bằng gold set.

**Vì sao bài này có impact:**  
Đây là bước nằm trên critical path của vòng lặp nghiên cứu. Giảm thời gian cơ
học nhưng giữ quyết định khoa học ở researcher giúp tăng tốc iteration mà
không đánh đổi khả năng kiểm chứng.

---

## 4. Problem Card #2 — Sàng lọc và tổng hợp paper LLM

**Problem 1 câu:**  
Mỗi tuần AI Researcher mất khoảng 4 giờ tìm, loại và ghi chú paper mới từ nhiều
nguồn, nhưng vẫn có nguy cơ bỏ sót công trình liên quan hoặc ghi nhận claim
thiếu đúng ngữ cảnh.

**Actor:**  
AI Researcher theo dõi một câu hỏi nghiên cứu cụ thể, ví dụ LLM evaluation,
reasoning hoặc efficient fine-tuning.

**Thời điểm / bối cảnh:**  
Literature watch hằng tuần hoặc khi bắt đầu một nhánh nghiên cứu mới.

**Current workflow (7 bước):**

1. Tìm paper bằng keyword, citation graph, newsletter và danh sách hội nghị.
2. Khử trùng lặp theo title/DOI/arXiv ID.
3. Đọc title và abstract để triage.
4. Đọc method, experiment, limitation của các paper còn lại.
5. Ghi claim, dataset, metric, baseline và hạn chế vào research note.
6. So sánh các paper theo câu hỏi nghiên cứu.
7. Chọn danh sách must-read và cập nhật related-work map.

**Bottleneck:**  
Bước 3–5 mất khoảng 150 phút/tuần. Thông tin quan trọng nằm ở nhiều section,
bảng và phụ lục; abstract có thể làm claim mạnh hơn bằng chứng thực nghiệm.

**Impact:**  
Mất thời gian nghiên cứu lặp lại, related work chậm cập nhật và có rủi ro thiết
kế lại thí nghiệm đã tồn tại hoặc so sánh thiếu baseline quan trọng.

**Success metric:**

- Giảm thời gian literature watch từ khoảng 240 xuống dưới 120 phút/tuần.
- Recall tối thiểu 90% trên một “must-read set” do researcher tự lập cho 4 tuần
  pilot.
- 100% claim được giữ lại phải có paper ID và vị trí bằng chứng
  (section/page/table); không chấp nhận citation do model tự tạo.
- Researcher đánh giá tối thiểu 4/5 cho độ hữu ích của shortlist sau mỗi tuần.

**Non-AI alternative:**  
Saved search/RSS, bộ keyword chuẩn, Zotero tag, dedup theo DOI/arXiv ID và
template note cố định. Đây là baseline chi phí thấp và vẫn cần triển khai dù có
dùng AI.

**AI hypothesis:**  
LLM chỉ đọc metadata/PDF đã được hệ thống cung cấp, trích xuất theo schema và
đối chiếu paper với research question. Search và dedup dùng rule/API; researcher
quyết định relevance, đọc sâu và viết synthesis cuối.

**Quick gut:**

- [ ] No AI / process fix
- [ ] Rule
- [x] Workflow
- [ ] Agent
- [ ] Chưa biết

### Draft current workflow

```text
CURRENT STATE — baseline ước lượng 240 phút/tuần

[1 Search nhiều nguồn: 45']
→ [2 Dedup: 15']
→ [3 Đọc title/abstract: 60']           <-- bottleneck
→ [4 Đọc method/experiment: 70']        <-- bottleneck
→ [5 Ghi note có cấu trúc: 30']
→ [6 So sánh + shortlist: 20']
```

### Draft future workflow

```text
FUTURE STATE — mục tiêu dưới 120 phút/tuần

[1 Saved search/RSS lấy metadata: 10']            -- Rule/API
→ [2 Dedup DOI/arXiv/title: 5']                   -- Rule
→ [3 LLM triage trên abstract theo rubric: 10']
→ [4 LLM draft evidence table từ PDF được cấp: 15']
→ [5 Researcher kiểm citation, đọc sâu shortlist: 60']  -- Human boundary
→ [6 Researcher viết synthesis + quyết định: 15']

Fallback:
Không lấy được full text hoặc citation không khớp → bỏ phần AI extraction,
đưa paper vào hàng đợi đọc thủ công; không suy đoán nội dung thiếu.
```

**Rủi ro chính:** bỏ sót paper do keyword/ranking, hallucinated citation, đọc
sai bảng, và preference bias làm hẹp hướng nghiên cứu. Pilot phải có must-read
set, kiểm citation 100% và giữ một nhánh khám phá ngoài keyword hiện tại.

**Vì sao bài này có impact:**  
Workflow xuất hiện hằng tuần và có artifact kiểm chứng được. Giá trị của AI nằm
ở triage/trích xuất, không nằm ở việc thay researcher đánh giá novelty hoặc độ
tin cậy của bằng chứng.

---

## 5. Problem Card #3 — Runbook tái lập paper/repository

**Problem 1 câu:**  
Khi tái lập một paper LLM, AI Researcher thường mất 5–8 giờ để nối thông tin từ
paper, README, source code và config thành một run hợp lệ vì nhiều giả định về
environment, data và hyperparameter không được trình bày ở cùng một nơi.

**Actor:**  
AI Researcher hoặc Research Engineer cần reproduce một baseline trước khi làm
ablation.

**Thời điểm / bối cảnh:**  
Khi bắt đầu dùng một paper/repository mới hoặc bàn giao thí nghiệm cho thành
viên khác.

**Current workflow (7 bước):**

1. Đọc paper để xác định task, dataset, metric và configuration cần tái lập.
2. Đọc README, issues, script và file config trong repository.
3. Tạo environment, cài dependency và tải artifact.
4. Ánh xạ paper setting sang command/config thực tế.
5. Chạy smoke test, đọc log và sửa lỗi.
6. Chạy baseline đầy đủ, so kết quả với paper.
7. Ghi lại command, version, seed, hardware và deviation.

**Bottleneck:**  
Bước 2–5, đặc biệt là ánh xạ tên setting trong paper sang config/code và chẩn
đoán mismatch dependency. Ước lượng khoảng 180–300 phút trước first valid run.

**Impact:**  
Chậm khởi động nhánh nghiên cứu, tiêu tốn GPU cho run sai và làm kết quả khó
handoff hoặc audit. Nếu provenance không đủ, một kết quả “khác paper” không cho
biết do code, data, seed hay environment.

**Success metric:**

- Giảm median time-to-first-valid-run từ 5–8 giờ xuống dưới 3 giờ cho các repo
  nằm trong scope pilot.
- Có smoke test chạy thành công trong tối đa 2 lần rebuild environment.
- 100% runbook ghi commit hash, dependency lock, dataset/version, config, seed,
  hardware và command.
- Không thực thi tự động command chưa được researcher review.

**Non-AI alternative:**  
Container/template environment, checklist reproducibility, Makefile, config
schema, smoke-test dataset và runbook chuẩn. Phương án này xử lý phần lớn lỗi
lặp lại và là nền tảng bắt buộc.

**AI hypothesis:**  
LLM đọc paper và các file repository được chọn để draft một bảng
`claim → config/file/command → evidence → uncertainty`, sau đó tạo checklist
runbook. Researcher kiểm từng command, quyền truy cập và deviation trước khi
chạy trong môi trường sandbox.

**Quick gut:**

- [ ] No AI / process fix
- [ ] Rule
- [x] Workflow
- [ ] Agent
- [ ] Chưa biết

### Draft current workflow

```text
CURRENT STATE — baseline ước lượng 5–8 giờ/repository

[1 Đọc paper: 60']
→ [2 Đọc README/code/config/issues: 120']       <-- bottleneck
→ [3 Dựng environment + data: 90']
→ [4 Ánh xạ setting sang command: 60']         <-- bottleneck
→ [5 Smoke test + debug: 60–150']
→ [6 Full baseline + đối chiếu]
→ [7 Ghi runbook: 30']
```

### Draft future workflow

```text
FUTURE STATE — mục tiêu dưới 3 giờ tới first valid run

[1 Template clone + inventory file/config: 5']       -- Rule/script
→ [2 LLM draft claim-config-evidence map: 15']
→ [3 Researcher đối chiếu paper/code/issues: 45']    -- Human boundary
→ [4 Tạo environment từ lock/container: 30']         -- Rule
→ [5 Researcher review command + quyền + data: 15']  -- Security boundary
→ [6 Chạy smoke test sandbox + đọc log: 30–60']
→ [7 Researcher chốt deviation + runbook: 20']

Fallback:
Mapping không có evidence hoặc command có hành vi không rõ → không chạy;
researcher quay về README/source code và tạo runbook thủ công.
```

**Rủi ro chính:** AI tạo command nguy hiểm, nhầm version, bỏ qua license/data
access, hoặc “hợp lý hóa” khác biệt giữa paper và code. Vì vậy không chọn Agent:
AI không được tự cài, tải artifact, chạy shell hay tiêu GPU.

**Vì sao bài này có impact:**  
Runbook vừa giảm thời gian cá nhân vừa tạo provenance cho cả nhóm. Tuy nhiên
phần lớn giá trị nền tảng đến từ process fix và automation xác định; LLM chỉ hỗ
trợ đọc/ánh xạ các nguồn không đồng nhất.

---

## 6. Card muốn pitch nhất

**Card tôi muốn pitch nhất:**  
Problem Card #1 — Phân tích lỗi đầu ra LLM sau benchmark.

**Pitch ngắn:**  
“Sau mỗi vòng benchmark, AI Researcher đang mất khoảng 3–4 giờ để ghép kết
quả, đọc output lỗi và gán taxonomy thủ công. Bottleneck khoảng 120 phút nằm ở
đọc và gán nhãn, làm chậm experiment tiếp theo. Tôi đề xuất pilot một workflow:
rule/script lo schema và sampling, LLM chỉ đề xuất nhãn kèm evidence, researcher
review các trường hợp rủi ro và ra quyết định. Thành công là lead time dưới
90 phút, kappa tối thiểu 0,80 và mọi insight truy được về sample ID.”

**Vì sao chọn pitch:**  
Problem này gần công việc cốt lõi của tôi, xảy ra lặp lại, có dữ liệu thật để
pilot, đo được cả tốc độ lẫn chất lượng và có đường rollback rõ. Nó cũng cho
phép so sánh công bằng process fix, rule và AI workflow.

**Câu hỏi tôi muốn nhóm challenge:**

1. Baseline 3–4 giờ có đúng khi đo bằng log trong hai tuần hay đang bị nhớ lệch?
2. Kappa 0,80 có đủ cho taxonomy và mức độ nghiêm trọng của task cụ thể không?
3. Nếu rule-based sampling cộng giao diện gán nhãn đã đạt mục tiêu, LLM còn tạo
   thêm giá trị đủ lớn để bù chi phí và rủi ro không?
4. Cách lấy mẫu review nào phát hiện được lỗi hiếm nhưng nghiêm trọng thay vì
   chỉ tối ưu agreement trung bình?

## 7. Tôi đã dùng AI ở phase cá nhân như thế nào?

Tôi dùng AI để mở rộng danh sách candidate, phản biện độ cụ thể của actor,
workflow, metric và trình bày lại workflow ở dạng dễ kiểm tra. Tôi không coi
các con số AI gợi ý là bằng chứng. Tôi loại các ý quá rộng như “trợ lý nghiên
cứu tự động toàn bộ”, tách phần rule/script ra khỏi phần cần hiểu ngôn ngữ, giữ
human review ở quyết định khoa học và đánh dấu các baseline cần đo lại.

## 8. Tự kiểm phần cá nhân

- [] Có 9 problems cụ thể, nhiều hơn mức tối thiểu 5.
- [] Có actor và dấu hiệu/cách kiểm chứng cho từng problem.
- [] Có Top 3 Problem Cards đầy đủ.
- [] Mỗi card có current/future workflow, bottleneck, metric và fallback.
- [] Có so sánh non-AI alternative trước khi chọn AI.
- [] Không chọn Agent khi workflow tuyến tính và cần human review.
- [] Đã ghi rõ số liệu nào mới là ước lượng cần kiểm chứng.
- [] Có card muốn pitch và câu hỏi muốn nhóm challenge.
