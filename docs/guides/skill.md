# Quy trình agent hoàn thành Assignment M1 — TMC

> Dùng khi được giao phân tích, thiết kế, viết hoặc rà soát báo cáo M1 về hệ thống chấm công và kiểm soát ra/vào bằng QR của TMC. Đây là workflow nội dung; entrypoint để Codex phát hiện tự động nằm trong [.agents/skills/tmc-m1/SKILL.md](../../.agents/skills/tmc-m1/SKILL.md).

## 1. Bắt đầu và xác định đầu ra

1. Đọc [summary.md](../overview/summary.md) để lấy yêu cầu, ranh giới và các câu hỏi chưa rõ; đọc [rules.md](rules.md) để giữ mức chắc chắn và phạm vi đúng.
2. Đọc phần liên quan trong [knowledge.md](../reference/knowledge.md), dùng chỉ mục nguồn để mở PDF khi một quyết định phụ thuộc chi tiết cụ thể. Đừng dùng trí nhớ để thay yêu cầu có sẵn trong đề.
3. Xác định người dùng đang yêu cầu tạo mới báo cáo, sửa một phần, rà soát hay chỉ giải thích. Tạo đúng sản phẩm đó; không mặc định mọi lời gọi skill đều yêu cầu viết lại toàn bộ.
4. Khi được yêu cầu viết báo cáo hoàn chỉnh và chưa có tên đích, dùng `docs/deliverables/report-m1.md`. Nếu có báo cáo sẵn, kiểm tra cấu trúc rồi chỉnh có mục tiêu; không ghi đè bài làm khác mà chưa xem.

Mặc định dùng tiếng Việt kèm thuật ngữ tiếng Anh; nếu người dùng/lớp yêu cầu ngôn ngữ khác thì áp dụng yêu cầu đó. Không bịa thông tin nhóm. Không khẳng định các giả định thiết kế đã được khách hàng xác nhận.

## 2. Bước 1 — Chốt problem, scope và yêu cầu

**Đầu vào:** đề M1 PDF tr.1–3, summary và thông tin bổ sung thật sự được cung cấp.

**Thực hiện:**

- Nêu hai nhà máy, mục tiêu kiểm soát ra/vào và báo cáo chấm công; nhận diện sáu actor, các hệ thống hiện hữu, thiết bị và kênh hiển thị QR.
- Vẽ system context; tách hệ thống mình xây khỏi HR/Payroll và controller đã có.
- Giữ danh mục FR-01…05, INT-01…03, NFR-01…04, OUT-01/02 và DEL-01…09.
- Phân rã năm nhóm FR thành use case có actor, trigger, precondition, main flow, alternate/error flow, postcondition và requirement nguồn. Chi tiết tự đề xuất phải có nhãn.
- Lập glossary và mô hình dữ liệu khái niệm đủ phân biệt credential, access attempt, authorization, gate result, attendance event và audit.
- Tạo danh sách open questions/assumptions; tiếp tục việc có thể làm độc lập. Với policy chưa rõ, phân tích các lựa chọn hoặc chọn assumption có ảnh hưởng được nêu rõ.

**Đầu ra:** context, scope, actor/use case catalog, requirements ledger, assumptions/open questions.

**Điểm kiểm:** không lẫn payroll/visitor vào phạm vi; workload và deadline đúng summary; không hiểu “2 giây” thành một thống kê yếu hơn.

## 3. Bước 2 — Chuyển yêu cầu thành architecture characteristics

**Đọc:** knowledge mục 5; S4 PDF tr.3–22; B ch.4–7.

- Xác định driver từ yêu cầu gốc và business concerns; phân biệt explicit với inferred.
- Ưu tiên performance, reliability/data integrity, security/privacy/audit và các driver tích hợp/đúng hạn theo bối cảnh. Có thể chọn danh sách driver ngắn, nhưng không bỏ NFR bắt buộc.
- Viết measurable scenarios theo source, stimulus, environment, artifact, response và response measure.
- Với NFR-01, nêu ranh giới đo và cửa sổ tải; dữ kiện còn thiếu được đánh dấu. Với NFR-02, nêu điều kiện normal operation và invariant lưu bản ghi.
- Với INT-02, định nghĩa dữ liệu phải sẵn sàng đối soát, kỳ và acknowledgment cần thỏa thuận; thời gian dự phòng là đề xuất.
- Nêu xung đột: xác thực/bảo vệ QR với thời gian phản hồi; độ bền ghi với latency; tách deploy với chi phí network/ops; báo cáo tháng với đường quét.

**Đầu ra:** characteristic worksheet, quality scenarios, ưu tiên/rationale và kế hoạch đo.

**Điểm kiểm:** đặc tính nào cũng phải chỉ ra ảnh hưởng cấu trúc hoặc lý do không phải driver; không tuyên bố số liệu đo khi chỉ mới thiết kế.

## 4. Bước 3 — Xây logical architecture theo vòng lặp

**Đọc:** knowledge mục 3–5; S4 tr.30–55; B ch.8.

1. Chọn Actor/Action hoặc Workflow để tạo tập trách nhiệm ban đầu; tránh một Manager cho mỗi entity.
2. Gán requirement/use case cho component logic, ghi owner và interface khái niệm.
3. Xem cohesion, các lý do thay đổi và nhu cầu phối hợp; tách/gộp khi trách nhiệm quá rộng hoặc giao tiếp quá dày.
4. Áp characteristics để xem phần nào cần tốc độ/độ bền/quyền truy cập/phạm vi deployment khác.
5. Lặp và ghi một hoặc vài thay đổi quan trọng từ phiên bản ban đầu đến thiết kế được chọn.

Các trách nhiệm ứng viên để bắt đầu gồm quản lý credential/QR, quyết định truy cập, ghi attendance, quản lý trạm, báo cáo/audit, quản trị và HR integration. Đây là gợi ý khám phá; không coi là số component cố định hoặc mặc định mỗi phần là một service.

**Bảng catalog gợi ý:** `ID | trách nhiệm | requirements | dữ liệu sở hữu | interfaces cung cấp/cần dùng | phụ thuộc | lý do ranh giới`.

**Đầu ra:** logical decomposition, dependency rules, catalog và diễn giải các vòng tinh chỉnh.

**Điểm kiểm:** mỗi FR có owner; không còn God Component không lý giải; phân biệt dependency code với lời gọi runtime.

## 5. Bước 4 — So sánh và chọn style

**Đọc:** knowledge mục 6–7; S5.1/5.2/5.3; B ch.9–20.

- Lập shortlist có lý do. Với TMC, cân nhắc layered hoặc modular monolith, service-based, microservices; EDA có thể là style/phần xử lý bổ trợ. Các style khác chỉ đưa vào khi có lý do phù hợp hoặc cần giải thích loại.
- So sánh trên cùng bộ tiêu chí rút từ characteristic worksheet, kèm độ phức tạp, chi phí phát triển/vận hành và năng lực đội.
- Nếu dùng điểm số, ghi thang/trọng số và lý do. Một ứng viên vi phạm yêu cầu bắt buộc cần mitigation khả thi, không được thắng chỉ do tổng điểm.
- Chọn thiết kế cụ thể, chỉ rõ phạm vi các pattern kết hợp; giải thích lựa chọn bị loại, rủi ro chấp nhận và điều kiện xem xét lại.
- Giữ stack/product là lựa chọn kỹ thuật có cơ sở, không giả làm yêu cầu đề. Có thể giữ trung lập về product khi chưa có thông tin cần chốt.

**Đầu ra:** bảng alternatives, quyết định style và rationale.

**Điểm kiểm:** có cả ưu/nhược; lựa chọn dựa trên TMC thay vì xu hướng; không gắn mọi style đã học vào một hệ thống.

## 6. Bước 5 — Map sang physical architecture và hành vi

**Đọc:** S4 tr.56–64; S6; B ch.8,23,26.

- Map logical components sang ứng dụng/process/service/worker/UI/datastore được chọn. Với từng deployment unit, ghi trách nhiệm, dữ liệu và lý do gom/tách.
- Bổ sung C&C: connector sync/async, protocol ở mức cần thiết, request/result, transaction boundaries, điểm ghi bền và trust boundaries.
- Vẽ sequence cho lượt quét hợp lệ, lượt bị từ chối và trường hợp lỗi đáng kể; vẽ luồng tổng hợp/xuất HR và acknowledgment.
- Thiết kế allocation: kiosk/scanner/controller ở nhà máy, backend/storage và liên kết HR. Nếu đặt backend tập trung hoặc cục bộ, ghi đó là quyết định và giải thích tác động latency/network/ops.
- Chỉ định các contract cần thiết ở mức M1: ý nghĩa input/output, identity và kết quả/lỗi, owner, xác thực, tính lặp lại; không bịa endpoint/schema của nhà cung cấp như dữ kiện thật.
- Nếu dùng retry/queue/outbox/background job, làm rõ dữ liệu bền ở đâu, khi nào ack, cơ chế xử lý trùng và trạng thái chưa biết. Kiểm tra gap giữa DB và tác dụng phụ ngoài.

**Mapping bắt buộc trong workflow này:** `Logical component → runtime unit → datastore/interface → deployment node → requirements/ADR`.

**Đầu ra:** physical/runtime architecture, deployment/allocation, mapping table, scenario sequences và interface catalog đủ dùng.

**Điểm kiểm:** thiết kế hiện thực được logical architecture đã chọn; QR valid không bị đồng nhất với người đã thực sự qua cổng; HR API không bị kéo vào critical path nếu chưa có lý do.

## 7. Bước 6 — ADR, design principles và SOLID

**Đọc:** knowledge mục 3,9; S1 tr.16–18; B ch.21.

Tạo ADR cho các quyết định có trade-off đáng kể, ví dụ style/deployment, thời điểm ghi nhận và xác nhận sự kiện, luồng tích hợp HR, boundary dữ liệu và kiểm quyền. Không có số lượng ADR bắt buộc trong đề; mỗi vấn đề phải được giải quyết rõ dù gộp hay tách.

### Mẫu ADR

| Trường | Nội dung cần điền |
|---|---|
| ID và title | Mã duy nhất, mô tả quyết định |
| Status | Proposed/chosen by team/superseded…; không giả là được khách hàng duyệt |
| Context và drivers | Vấn đề, requirement IDs, constraints, assumption ảnh hưởng |
| Alternatives | Những lựa chọn thật sự đã so sánh |
| Decision | Quy tắc chọn, phạm vi áp dụng |
| Consequences | Lợi ích, chi phí, rủi ro và giới hạn |
| Compliance/validation | Cách review/test/fitness function kiểm quyết định |
| Revisit condition | Điều kiện bối cảnh thay đổi cần đánh giá lại |
| Sources | File/chương/trang PDF liên quan |

Viết design principles riêng theo dạng: `nguyên tắc → lý do → ví dụ TMC → cách kiểm → trường hợp cần cân nhắc`. Thể hiện đủ SRP/OCP/LSP/ISP/DIP qua phân chia trách nhiệm, adapter contracts và source dependency. Không bắt buộc tất cả pattern S2 xuất hiện trong bài.

**Đầu ra:** decision log, ADRs và principles có ví dụ áp dụng.

## 8. Bước 7 — Đóng gói báo cáo theo nhiều view

Khung báo cáo dưới đây là **đề xuất để bao phủ đề**, không phải template giảng viên đã ban hành:

1. Bối cảnh, mục tiêu, stakeholder và ranh giới.
2. Yêu cầu chức năng/phi chức năng, assumptions và glossary/data concepts.
3. Architecture characteristics và quality scenarios.
4. Logical architecture: phương pháp khám phá và các vòng tinh chỉnh.
5. So sánh style và quyết định chọn.
6. Physical/runtime architecture và allocation/deployment.
7. Interfaces và các luồng trọng yếu, bao gồm lỗi và tích hợp.
8. Architecture decisions và design principles/SOLID.
9. Đánh giá NFR, risk, traceability và giới hạn.
10. Kết luận thiết kế, phần cần xác nhận và tài liệu tham khảo.

Với Module/C&C/Allocation, thêm title/scope, diagram, element catalog, interface/behavior, variability nếu có và rationale. Dùng mục beyond-view để chỉ đường đọc và mapping, tránh mô tả ba hệ thống khác nhau trong ba hình.

Không cần dựng toàn bộ class diagram/DDL/OpenAPI chi tiết chỉ để làm báo cáo dài hơn. Chọn độ sâu đủ giải thích kiến trúc, business rules quan trọng và đáp ứng yêu cầu thiết kế của đề.

## 9. Bước 8 — Kiểm tra coverage và walkthrough

| Scenario | Kiểm tra tối thiểu | Liên quan |
|---|---|---|
| Quét hợp lệ vào/ra | Credential, quyền, hướng, ghi nhận, gate result, feedback | FR-01/03, INT-03 |
| Quét không hợp lệ/bị từ chối | Không mở theo policy; phản hồi và audit; không tự tính thành lượt công | NFR-03, FR-04 |
| Lần quét/gửi lặp | Phân biệt một request bị gửi lại với một lần qua cổng khác thật sự | NFR-02, FR-03 |
| Controller timeout | Trạng thái chưa biết, tránh retry tác dụng phụ mù, không khẳng định đã qua cổng | INT-03 |
| Ghi bền hoặc chuyển việc lỗi | Không báo thành công khi chưa đạt điều kiện được chọn; có recovery trong phạm vi giả định | NFR-02 |
| HR API tạm lỗi/gửi lặp | Retry có trạng thái, xác nhận, loại trùng và theo dõi deadline | INT-01/02 |
| Ranh giới tháng/ca qua đêm | Múi giờ/kỳ, bản ghi đến muộn và quy tắc chưa xác nhận | FR-04, INT-02 |
| Role hoặc data scope sai | Từ chối ở backend và audit phù hợp | NFR-03/04 |
| Đổi ca theo workload | Ngân sách đường quét và thiết kế phép thử ≤ 2 giây | NFR-01 |

Những scenario mở rộng được ghi rõ là đề xuất, không tự trở thành NFR gốc. Lập ma trận `requirement ID → section/view/ADR cụ thể → cách đánh giá → trạng thái/gap`. Với deliverable đã viết, thay tên chung bằng anchor hoặc ID thật.

Chỉ ghi “đã kiểm thử đạt” nếu có test và kết quả thực. Ở M1, dùng “thiết kế nhằm đáp ứng”, “walkthrough cho thấy” hoặc “cần đo ở bước implementation” đúng với chứng cứ.

## 10. Điều kiện bàn giao

- Bao phủ toàn bộ yêu cầu gốc và DEL-01…09, có cách chuẩn bị SUB-01 phù hợp yêu cầu người dùng.
- Cả logic, runtime và allocation nhất quán; đủ catalogue/interface/rationale, không chỉ có hình.
- Chosen architecture có alternatives/trade-off, ADR và SOLID cụ thể.
- Các câu hỏi chưa xác nhận, giả định ảnh hưởng, giới hạn bảo đảm và risk còn lại được công khai.
- Link/sơ đồ/citation kiểm tra được; ngôn ngữ và thuật ngữ nhất quán.
- Bàn giao đường dẫn báo cáo, mô tả phần hoàn tất và điểm còn cần xác nhận. Không tự tuyên bố đã nộp LMS hoặc đã triển khai hệ thống.
