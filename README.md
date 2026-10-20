# Assignment M1 — TMC: tài liệu học, phân tích và hướng dẫn agent

Bộ tài liệu giúp bạn hiểu Assignment M1 và giúp agent tạo một báo cáo thiết kế có đủ yêu cầu, lập luận và architectural views dựa trên nguồn môn học. Nội dung chính bằng tiếng Việt, giữ thuật ngữ tiếng Anh để đối chiếu slide/sách.

**Bắt đầu nhanh:** đọc [bản giải thích có sơ đồ](docs/guides/assignment-explained.md), sau đó dùng [summary.md](docs/overview/summary.md) làm checklist yêu cầu. Khi giao agent làm bài, dùng skill `tmc-m1`.

## 1. Bản đồ tài liệu

| Tài liệu | Trả lời câu hỏi |
|---|---|
| [summary.md](docs/overview/summary.md) | Đề yêu cầu gì, số liệu nào phải giữ đúng, M1 phải nộp những nội dung nào? |
| [knowledge.md](docs/reference/knowledge.md) | Kiến thức trong tám bộ slide và 27 chương giáo trình là gì, áp dụng cho TMC thế nào? |
| [skill.md](docs/guides/skill.md) | Agent đi từ đọc đề đến phân tích, chọn style, xây view, viết ADR và rà báo cáo ra sao? |
| [rules.md](docs/guides/rules.md) | Làm sao không bịa requirement, nhầm phạm vi, mất traceability hoặc dùng lý thuyết máy móc? |
| [assignment-explained.md](docs/guides/assignment-explained.md) | Hệ thống vận hành như thế nào và từng phần bài làm liên hệ với nhau ra sao? |
| [.agents/skills/tmc-m1/SKILL.md](.agents/skills/tmc-m1/SKILL.md) | Entrypoint để Codex phát hiện và kích hoạt quy trình M1 |

`skill.md` là hướng dẫn nội dung dùng được cho nhiều agent. `SKILL.md` trong `.agents/skills/tmc-m1` là manifest và bộ dẫn đường cho Codex, tham chiếu bộ tài liệu này để tránh hai bản hướng dẫn lệch nhau.

## 2. Thứ tự đọc

### Nếu bạn mới tiếp cận bài

1. Đọc assignment-explained để hiểu một lượt quét QR và một chu kỳ báo cáo tháng.
2. Đọc summary để nắm đầy đủ yêu cầu và các câu hỏi đề chưa nói rõ.
3. Đọc knowledge theo các mục 2 → 3 → 4 → 5 → 6 → 8 → 9. Mục 1 có chỉ mục sách/slide để tra nguồn.
4. Dùng skill để chia việc làm báo cáo; kiểm kết quả bằng rules và checklist summary.

### Nếu là agent đang làm M1

Đọc summary → rules → skill; sau đó nạp phần knowledge cần cho bước đang thực hiện và mở trang PDF khi cần kiểm chứng. Chỉ đọc assignment-explained như ví dụ để hiểu luồng; các kiến trúc minh họa trong đó chưa phải quyết định bắt buộc.

## 3. Kích hoạt skill trong Codex

Mở dự án/terminal làm việc tại chính thư mục:

```powershell
Set-Location 'C:/Users/stephen-work/Desktop/Project/software_architecture/assignment_ktpm'
codex
```

Trong Codex CLI/IDE, có thể tìm bằng `/skills` hoặc nhắc trực tiếp `$tmc-m1`. Khi yêu cầu khớp description, Codex có thể tự chọn skill. Nếu đang mở từ thư mục cha `Project`, hãy chuyển working folder sang `assignment_ktpm`; không mặc định Codex quét mọi thư mục con để tìm skill. Nếu skill chưa xuất hiện, kiểm tra thư mục làm việc, cấu hình bật skill và khởi động lại phiên khi cần.

Vị trí `.agents/skills` và cơ chế gọi ngầm/đích danh theo [tài liệu OpenAI về skills](https://learn.chatgpt.com/docs/build-skills). Bộ này đặt skill trong dự án; không sửa cấu hình hay cài skill vào thư mục người dùng toàn máy.

### Prompt tạo báo cáo M1

```text
Dùng $tmc-m1 để hoàn thành báo cáo Assignment M1 của TMC trong docs/deliverables/report-m1.md.
Đọc docs/overview/summary.md, docs/guides/rules.md và docs/guides/skill.md; tra
docs/reference/knowledge.md và các trang PDF liên quan.
Bao phủ toàn bộ requirement gốc, trình bày từng bước xây kiến trúc logic/vật lý,
so sánh style, tạo Module/C&C/Allocation views, ADR và ví dụ SOLID.
Ghi rõ giả định, đề xuất bổ sung, rủi ro, điểm cần xác nhận và traceability.
Chỉ thực hiện phân tích và thiết kế của M1; không bịa kết quả kiểm thử.
```

### Prompt rà soát một bản báo cáo đã có

```text
Dùng $tmc-m1 review docs/deliverables/report-m1.md theo đề M1 và checklist trong
docs/overview/summary.md.
Chỉ ra requirement còn thiếu hoặc diễn giải sai, mâu thuẫn giữa các view,
quyết định chưa có trade-off, chỗ chưa chứng minh SOLID và giả định chưa công khai.
Gắn mỗi nhận xét với requirement ID, vị trí báo cáo và nguồn liên quan.
```

### Prompt học từng phần

```text
Dùng $tmc-m1 giải thích cách chuyển NFR-01 và NFR-02 thành architecture
characteristics, measurable scenarios và các lựa chọn thiết kế cho TMC.
Dùng ví dụ tiếng Việt và chỉ rõ đâu là đề cho, đâu là giả định/đề xuất.
```

Với agent không hỗ trợ Codex skills, dùng cùng prompt nhưng yêu cầu đọc các file bằng đường dẫn trực tiếp; nội dung workflow vẫn sử dụng được.

## 4. Nguồn, phiên bản và cách trích dẫn

- Đề chính thức: [SA_CC_hk261_Assignment_M1.pdf](SA_CC_hk261_Assignment_M1.pdf), 3 trang PDF.
- Tám file slide Chapter 1–6: tổng 412 trang PDF; Chapter 5 gồm ba phần. Chỉ mục file nằm trong knowledge mục 1.
- Sách cung cấp: 1.083 trang PDF, **Second Edition, A Modern Engineering Approach, copyright 2025**, xác định tại B tr.5–6. Slide có tham chiếu bản 2020; bộ tài liệu chỉ rõ phần khác nhau.
- `S4 PDF tr.31` nghĩa là trang thứ 31 của file Chapter 4, không phải số slide nội bộ. `B ch.21 PDF tr.770` nghĩa là đúng vị trí trong PDF đã cung cấp, không phải trang sách in.

Mỗi chương sách có hàng trong bản đồ knowledge. Phần tổng hợp được nhóm theo chủ đề để tránh lặp lại giữa slide và sách; phần bài tập/appendix được dùng để ôn phương pháp, không được nhập thành requirement M1. Văn bản được diễn giải, các sơ đồ mới là minh họa cho TMC.

## 5. Quy ước thông tin quan trọng

| Nhãn | Đọc như thế nào? |
|---|---|
| GỐC | Đề đã nêu, cần đáp ứng và có trang nguồn |
| SUY RA | Kết luận phân tích có lý do từ dữ kiện gốc |
| ĐỀ XUẤT | Bổ sung để thiết kế đủ rõ; chưa là yêu cầu chính thức |
| CẦN XÁC NHẬN | Thông tin còn thiếu, phải ghi câu hỏi/giả định và tác động |

Các mã FR/NFR/INT/DEL… là mã truy vết của bộ tài liệu. Khung báo cáo, tên module, tên interface, số sơ đồ và các tactics được gợi ý không phải rubric giảng viên bổ sung.

Đặc biệt giữ đúng: 800 **giao dịch/30 phút/nhà máy**, kiosk **≤ 2 giây**, không mất bản ghi **trong vận hành bình thường**, dữ liệu HR **sẵn sàng đối soát trước trưa ngày 1**. Hạn gửi dữ liệu nghiệp vụ khác với hạn nộp bài; đề hiện có chưa cung cấp hạn nộp.

## 6. Xem visualization

Mở [assignment-explained.md](docs/guides/assignment-explained.md) bằng trình xem Markdown có hỗ trợ Mermaid. Các khối `mermaid` có thể được render thành sơ đồ trong môi trường hỗ trợ; nếu trình xem chỉ hiện code, cần bật tính năng Mermaid hoặc dùng một trình xem tương thích. Không cần tạo website để đọc bộ tài liệu.

Mỗi sơ đồ có đoạn giải thích và mức chắc chắn ngay cạnh hình. Mermaid ở đây minh họa context/module/runtime/deployment; flowchart không được tuyên bố là UML chuẩn. Không đưa nội dung cá nhân hoặc tài liệu chưa công khai lên dịch vụ render bên ngoài chỉ để xem sơ đồ.

## 7. Bước tiếp theo và cách duy trì

Bộ hiện tại là tài liệu chuẩn bị và hướng dẫn, **chưa phải report-m1.md đã hoàn thành hoặc ứng dụng chạy được**. Để làm bài, dùng prompt tạo báo cáo rồi kiểm theo DEL-01…09. Người dùng kiểm tra quy định lớp/LMS và thực hiện nộp bài.

Khi có trả lời cho open questions hoặc giảng viên cập nhật đề, cập nhật summary trước, sau đó điều chỉnh rule/workflow và các minh họa bị ảnh hưởng. Khi có đặc tả M2, giữ ranh giới yêu cầu theo mốc; không thay ngầm phạm vi M1 bằng suy đoán về M2.

Trước khi bàn giao một lần chỉnh sửa, kiểm tra link nội bộ, source/page references, mọi khối Mermaid, manifest skill và consistency giữa các view. Kết quả kiểm tra cấu trúc tài liệu không thay cho đánh giá kiến trúc hoặc kiểm thử ứng dụng.
