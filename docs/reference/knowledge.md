# Kiến thức Software Architecture — slide Chapter 1–6 và giáo trình

> Tài liệu đúc kết khái niệm, phương pháp và trade-off theo toàn bộ các chương nguồn; ưu tiên cách dùng trong M1. Đây là tài liệu học tập và tra cứu, không phải bản chép sách, đáp án mọi bài tập nhỏ hoặc báo cáo M1 đã hoàn thành. Ví dụ TMC đều là phân tích/đề xuất của bộ tài liệu, trừ khi dẫn trực tiếp mã yêu cầu trong [summary.md](../overview/summary.md).

## Mục lục

1. [Nguồn và bản đồ kiến thức](#1-nguồn-và-bản-đồ-kiến-thức)
2. [Kiến trúc, tư duy kiến trúc và vai trò architect](#2-kiến-trúc-tư-duy-kiến-trúc-và-vai-trò-architect)
3. [SOLID và các design pattern hỗ trợ](#3-solid-và-các-design-pattern-hỗ-trợ)
4. [Modularity, cohesion, coupling và connascence](#4-modularity-cohesion-coupling-và-connascence)
5. [Characteristics, đo lường, quantum và component](#5-characteristics-đo-lường-quantum-và-component)
6. [Architecture styles và cách lựa chọn](#6-architecture-styles-và-cách-lựa-chọn)
7. [Các architectural pattern bổ sung](#7-các-architectural-pattern-bổ-sung)
8. [Documenting Software Architecture](#8-documenting-software-architecture)
9. [ADR, rủi ro, đội nhóm và các giao điểm](#9-adr-rủi-ro-đội-nhóm-và-các-giao-điểm)
10. [Áp dụng vào TMC và tự kiểm tra](#10-áp-dụng-vào-tmc-và-tự-kiểm-tra)
11. [Thuật ngữ và lưu ý khi đọc nguồn](#11-thuật-ngữ-và-lưu-ý-khi-đọc-nguồn)

## 1. Nguồn và bản đồ kiến thức

### 1.1. Quy ước trích dẫn

**PDF tr.** luôn tính từ trang đầu file, bắt đầu bằng 1. Một số slide có số nội bộ khác số trang PDF; sách là bản PDF dàn lại nên số trang không khớp sách in. Mã S1…S6, B và M1 chỉ là quy ước tra cứu trong bộ này.

| Mã | Nguồn cục bộ | Trang PDF | Nội dung chính |
|---|---|---:|---|
| S1 | [Chapter 1](../../Slides/Chapter1_SA_CC_hk251.pdf) | 1–28 | Môn học; định nghĩa kiến trúc; architect; separation of concerns; DevOps/process/data |
| S2 | [Chapter 2](../../Slides/Chapter2_SA_2025.pdf) | 1–69 | SOLID; Facade, Strategy, Adapter, Factory |
| S3 | [Chapter 3](../../Slides/Chapter3_SA_CC_hk251-v6.pdf) | 1–31 | Architectural thinking, trade-off, business drivers, modularity và metrics |
| S4 | [Chapter 4](../../Slides/Chapter4_SA_2025-v2.pdf) | 1–65 | Characteristics, tìm component, logical/physical architecture |
| S5.1 | [Chapter 5, phần 1](../../Slides/Chapter5-1_CC_2025.pdf) | 1–51 | Nền tảng, distributed fallacies, layered, pipeline, microkernel |
| S5.2 | [Chapter 5, phần 2](../../Slides/Chapter5-2_CC_2025.pdf) | 1–47 | Service-based, microservices, sidecar, mesh, saga |
| S5.3 | [Chapter 5, phần 3](../../Slides/Chapter5-3_CC_2025.pdf) | 1–45 | EDA, mediator/broker, data loss, space-based |
| S6 | [Chapter 6](../../Slides/Chapter6_SA_CC_2025.pdf) | 1–76 | Views and Beyond; Module, C&C, Allocation views |
| B | [Fundamentals of Software Architecture](../../books/Fundamentals%20of%20Software%20Architecture%20An%20Engineering%20Approach%20%28Mark%20Richards%2C%20Neal%20Ford%29%20%28Z-Library%29.pdf) | 1–1083 | Second Edition, A Modern Engineering Approach; Mark Richards, Neal Ford; copyright 2025 |
| M1 | [Assignment M1](../../SA_CC_hk261_Assignment_M1.pdf) | 1–3 | Đề bài TMC, yêu cầu và hướng dẫn nộp |

Tổng cộng 412 trang slide. B tr.5–6 xác định phiên bản sách; tên file không nói rõ Second Edition. S1 tr.5,8 tham chiếu bản 2020. Vì vậy không dùng số chương bản cũ để dẫn sang PDF sách này.

### 1.2. Chỉ mục đủ 27 chương sách

“M1 trực tiếp” nghĩa là giúp tạo deliverable thiết kế; “bổ trợ” nghĩa là kiến thức cần hiểu để đánh giá lựa chọn hoặc làm việc nhóm, không phải yêu cầu phải áp dụng toàn bộ vào TMC.

| Chương B | Trang PDF | Chủ đề, đóng góp cần nhớ | Mức liên quan và nơi tổng hợp |
|---|---|---|---|
| 1 | 20–42 | Định nghĩa đa chiều; ba luật; kỳ vọng với architect | Trực tiếp — mục 2 |
| 2 | 44–81 | Architecture/design; breadth; radar; phân tích trade-off; giữ hands-on | Trực tiếp/bổ trợ — mục 2 |
| 3 | 82–117 | Modularity; cohesion/coupling; abstractness/instability; connascence | Trực tiếp — mục 4 |
| 4 | 118–145 | Characteristics; operational/structural/cloud/cross-cutting; chất lượng là trade-off | Trực tiếp — mục 5 |
| 5 | 146–175 | Rút driver từ nghiệp vụ/yêu cầu; composite characteristics; kata và ưu tiên | Trực tiếp — mục 5 |
| 6 | 176–202 | Định nghĩa phép đo, complexity, governance, fitness functions | Trực tiếp — mục 5 |
| 7 | 203–224 | Phạm vi characteristics, coupling và architectural quantum | Trực tiếp — mục 5 |
| 8 | 225–266 | Component logic; Actor/Action, Workflow, Entity Trap; vòng lặp thiết kế; Demeter | Trực tiếp — mục 5 |
| 9 | 268–310 | Style/pattern; partitioning; distributed fallacies; team topologies | Trực tiếp — mục 6,9 |
| 10 | 311–334 | Layered: isolation, open/closed layer, sinkhole, rủi ro và dùng khi nào | Trực tiếp — mục 6 |
| 11 | 335–364 | Modular monolith: domain module, cấu trúc build, giao tiếp và governance | Trực tiếp — mục 6 |
| 12 | 365–390 | Pipeline: pipes/filters, governance, team fit và use cases | Tham khảo lựa chọn — mục 6 |
| 13 | 391–421 | Microkernel: core/plug-in, registry/contracts, mức độ microkernel và rủi ro | Tham khảo lựa chọn — mục 6 |
| 14 | 422–456 | Service-based: dịch vụ miền, UI/API/data variants, trade-off | Trực tiếp — mục 6 |
| 15 | 457–566 | EDA: event/message, payload, error/data loss, mediated EDA, data topology | Trực tiếp — mục 6,7 |
| 16 | 567–627 | Space-based: grid/cache, data pump, collision, elasticity | Bổ trợ — mục 6 |
| 17 | 628–655 | Orchestration-driven SOA: các loại service, ESB, reuse/coupling | Bổ trợ — mục 6 |
| 18 | 656–707 | Microservices: bounded context, data isolation, communication, sagas | Trực tiếp để so sánh — mục 6,7 |
| 19 | 708–733 | Chọn style theo domain, characteristics, data và tổ chức | Trực tiếp — mục 6 |
| 20 | 734–758 | Hexagonal, mesh, orchestration/choreography, CQRS, broker/domain | Trực tiếp/tham khảo — mục 7 |
| 21 | 760–796 | ADR; decision antipatterns; governance; AI hỗ trợ quyết định | Trực tiếp — mục 9 |
| 22 | 797–829 | Risk matrix, risk assessment, risk storming | Trực tiếp — mục 9 |
| 23 | 830–845 | Diagramming; UML/C4/ArchiMate; cách vẽ rõ và thay đổi được | Trực tiếp — mục 8 |
| 24 | 846–887 | Hiệu quả đội nhóm, constraints, architect personalities, checklists | Bổ trợ — mục 9 |
| 25 | 888–922 | Đàm phán, leadership, 4 Cs, pragmatism và collaboration | Bổ trợ — mục 9 |
| 26 | 923–959 | Giao điểm với implementation, infrastructure, data, team, business, AI | Trực tiếp/bổ trợ — mục 9 |
| 27 | 960–981 | Ôn ba luật, reuse/coupling, context và đánh giá trade-off lặp lại | Trực tiếp — mục 2,9 |

B tr.1–19 là phần đầu/preface; tr.43,267,759 mở các phần lớn; tr.982–1010 là câu hỏi thảo luận; tr.1011–1080 là index; tr.1081–1083 là tác giả/colophon. Các phần này hỗ trợ định vị và ôn tập, không tạo thêm requirement cho M1.

## 2. Kiến trúc, tư duy kiến trúc và vai trò architect

**Nguồn:** S1 tr.9–26; S3 tr.4–17; B ch.1–2,27, PDF tr.20–81,960–981.

### 2.1. Kiến trúc gồm những gì?

Kiến trúc mô tả các cấu trúc quan trọng của hệ thống, thành phần và quan hệ của chúng với nhau và với môi trường, cùng những quyết định giúp hệ thống đạt mục tiêu nghiệp vụ và chất lượng. Một sơ đồ máy chủ hoặc một danh sách framework chưa đủ để gọi là hồ sơ kiến trúc.

| Góc nhìn được dạy trong S1 tr.13–18 | Câu hỏi phải trả lời cho TMC |
|---|---|
| Structure | Phân chia hệ thống thế nào, các phần cộng tác và triển khai ra sao? |
| Architecture characteristics | Điều gì làm hệ thống thành công: tốc độ kiosk, không mất dữ liệu, bảo mật, tích hợp? |
| Architecture decisions | Những quy tắc thiết kế nào được chọn và có tính ràng buộc? |
| Design principles | Những hướng dẫn nào giúp xử lý các quyết định chi tiết nhất quán? |

**Khác biệt phiên bản:** B2e tr.22–27 trình bày characteristics, logical components, architecture styles và decisions như bốn chiều. S1 và đề M1 tách structure, characteristics, decisions, principles. Trong bài M1 dùng cấu trúc đề yêu cầu; dùng logical components và styles của sách để làm rõ phần Structure. Không xóa mục Design Principles chỉ vì mô hình định nghĩa trong sách mới đã đổi.

Architecture decision là quy tắc đã chốt trong bối cảnh cụ thể; design principle là định hướng có thể cân nhắc theo hoàn cảnh. Ví dụ **minh họa**, chưa được chấp nhận: quyết định “đường xử lý quét không gọi HR/Payroll đồng bộ”; nguyên tắc “giữ critical path của kiosk ngắn”. ADR phải giải thích vì sao, các lựa chọn bị loại và hệ quả.

### 2.2. Architecture và design nằm trên một phổ

Không chia đơn giản “architect vẽ, developer code”. Xem một quyết định theo ba tiêu chí của B ch.2: tính chiến lược, chi phí thay đổi và mức đáng kể của trade-off. Quyết định ranh giới lưu dữ liệu hoặc tổ chức deploy thường có tính kiến trúc; màu nút thường là thiết kế giao diện. Một framework có thể trở thành quyết định kiến trúc nếu nó quyết định khả năng thực hiện NFR.

Logical architecture trả lời **hệ thống có những trách nhiệm nào**. Physical architecture trả lời **trách nhiệm được hiện thực trong ứng dụng/process/service/UI/datastore nào**. Deployment/allocation trả lời **những phần thực thi được đặt ở môi trường/hardware nào**. Ba câu hỏi liên hệ nhưng không thay thế nhau.

### 2.3. Ba luật và cách dùng

| Luật/ý chính | Cách dùng khi làm bài |
|---|---|
| Mọi lựa chọn kiến trúc đều có đánh đổi | Không viết một style “tốt nhất mọi mặt”; giải thích phần phải trả giá |
| Lý do quan trọng hơn cách làm | Sơ đồ và tên công nghệ phải kèm rationale có bối cảnh |
| Phần lớn quyết định nằm trên một phổ giữa hai cực | Có thể kết hợp kiến trúc và pattern theo luồng; tránh lựa chọn nhị phân máy móc |

S1 tr.20 nêu hai luật đầu; luật thứ ba và hệ quả phải phân tích lại trade-off khi bối cảnh đổi nằm trong B2e tr.28–30,973–979. Nếu chưa thấy nhược điểm, cần tìm tiếp; không xem bảng so sánh chung là quyết định áp dụng vĩnh viễn.

**Ví dụ TMC:** xử lý đồng bộ giúp kiosk biết ngay kết quả nhưng phải chịu latency và lỗi của phụ thuộc; xử lý bất đồng bộ tách công việc dài nhưng đòi trạng thái, giám sát và xử lý giao lặp. Không thể kết luận “mọi thứ dùng async” chỉ từ NFR 2 giây.

### 2.4. Architect làm việc thế nào?

Tám kỳ vọng trong S1 tr.19 và B ch.1: đưa ra quyết định; liên tục đánh giá kiến trúc; cập nhật xu hướng; bảo đảm tuân thủ quyết định; có tiếp xúc công nghệ đa dạng; hiểu nghiệp vụ; có kỹ năng con người; hiểu và xử lý bối cảnh tổ chức.

Architect cần **technical breadth** để biết các lựa chọn và đánh đổi; developer thường cần **technical depth** để hiện thực tốt. Tam giác kiến thức gồm điều đã biết, điều biết rằng mình chưa biết, và điều chưa biết là tồn tại. Mở rộng breadth không có nghĩa quyết định mà không hiểu kỹ thuật.

B ch.2 bổ sung cách duy trì breadth: thời gian học đều đặn, technology radar cá nhân với Hold/Assess/Trial/Adopt, đánh giá công nghệ theo giai đoạn. Tránh Frozen Caveman: dùng mãi một trải nghiệm cũ để bác bỏ công nghệ dù bối cảnh đã đổi.

Giữ hands-on qua PoC, review, technical debt, bug fixing hoặc công cụ tự động hóa. Tránh bottleneck trap khi architect ôm phần code trên critical path nhưng không đủ thời gian. PoC chỉ kiểm chứng giả thuyết đã thử, không phải bằng chứng hệ thống hoàn chỉnh đáp ứng mọi NFR.

### 2.5. Separation of concerns

Tách business rules khỏi UI, framework, database và hệ thống ngoài để hạn chế lan truyền thay đổi và tăng testability. “Independent” là ranh giới dependency có chủ đích, không phải hệ thống chạy mà không cần hạ tầng. Với TMC, thay SDK cổng không nên bắt đổi quy tắc chấm công; thay định dạng báo cáo không nên làm thay luồng xác thực QR.

## 3. SOLID và các design pattern hỗ trợ

**Nguồn:** S2 tr.3–65; S1 tr.21–22. Sách Richards/Ford cung cấp ngữ cảnh modularity và architecture, nhưng năm nguyên tắc SOLID trong bộ nguồn được giảng trực tiếp ở S2.

| Nguyên tắc | Nội dung cốt lõi | Ứng dụng TMC đề xuất | Dấu hiệu sai |
|---|---|---|---|
| SRP — Single Responsibility | Một module phục vụ một nhóm lý do thay đổi/actor có liên quan | Tách quy tắc cấp QR, quyết định truy cập, lưu chấm công và trình bày báo cáo | Một lớp vừa gọi gate SDK, kiểm quyền, tính dữ liệu tháng và xuất báo cáo |
| OCP — Open/Closed | Mở rộng hành vi ở điểm biến đổi có chủ đích, hạn chế sửa phần ổn định | Thêm adapter nhà cung cấp cổng hoặc cách biểu diễn báo cáo qua abstraction ổn định | Mỗi nhà máy mới phải sửa một chuỗi điều kiện lớn trong core |
| LSP — Liskov Substitution | Implementation thay thế phải giữ contract và hành vi mà client trông đợi | Hai GateController adapter thống nhất ý nghĩa accepted/rejected/timeout | Adapter trả “success” khi chỉ gửi gói tin nhưng contract đòi controller xác nhận |
| ISP — Interface Segregation | Client không phải phụ thuộc các chức năng mình không dùng | Tách quyền đọc báo cáo, ghi sự kiện, điều khiển cổng và quản lý role | Scanner phụ thuộc một interface khổng lồ có cả quản lý HR và xuất lương |
| DIP — Dependency Inversion | Policy cấp cao và chi tiết phụ thuộc abstraction; chi tiết hiện thực abstraction | Core phụ thuộc GateController, AttendanceRepository, HRPayrollGateway; adapter phụ thuộc contract của core | Core import trực tiếp SDK controller/ORM và bị buộc theo data shape bên ngoài |

### 3.1. Các phân biệt dễ nhầm

- SRP không có nghĩa “một lớp chỉ có một method”. Cần xem ai yêu cầu thay đổi và thay đổi thường đi cùng nhau hay độc lập. S2 dùng ví dụ Employee có trách nhiệm phục vụ CFO/COO/CTO để chỉ ra các trục thay đổi.
- OCP không cấm sửa code. Chỉ nên tạo extension point khi có lý do thay đổi thực tế; không cần interface cho mọi lớp.
- LSP là behavioral contract, rộng hơn quan hệ kế thừa cú pháp. Preconditions, postconditions, invariants và ý nghĩa lỗi phải tương thích. Ví dụ Rectangle/Square trong S2 tr.37–38 cho thấy mô hình “is-a” ngoài đời không tự bảo đảm thay thế trong code mutable.
- ISP phân tách theo client/role; không chỉ chia interface thành các mẩu ngẫu nhiên. Ngôn ngữ dynamic vẫn có dependency về hành vi và runtime.
- DIP khác dependency injection. Injection chỉ là cách cấp implementation; nếu abstraction vẫn phụ thuộc schema/SDK biến động, thiết kế chưa đạt mục tiêu DIP.
- Mũi tên **source dependency** có thể ngược chiều **runtime control flow**. Trong ví dụ S2 tr.51–55, core gọi implementation qua interface nhưng implementation phụ thuộc abstraction của policy.

### 3.2. Pattern được nhắc trong S2

| Pattern | Dùng khi nào | Trade-off và ví dụ TMC |
|---|---|---|
| Facade | Cần một điểm truy cập đơn giản cho nhiều phần trách nhiệm tách biệt | Làm client đơn giản; tránh để facade ôm toàn bộ logic. Ví dụ cổng truy cập một application use case |
| Strategy | Có họ thuật toán/hành vi thay thế qua cùng contract | Tách biến thể; cần quản lý số lớp. Chỉ dùng chiến lược kiểm QR khi thực sự có nhiều chính sách |
| Adapter | Cần chuyển interface/format hiện hữu sang contract hệ thống | Cô lập nhà cung cấp; phải mapping lỗi chính xác. Hợp lý cho HR API và controller |
| Factory Method | Subclass quyết định loại product được tạo qua factory method | Giảm phụ thuộc vào concrete tại client; có thể làm hierarchy phức tạp |
| Abstract Factory | Tạo các nhóm product tương thích mà client không cần biết concrete | Phù hợp khi có cả họ adapter thay đổi cùng nhau; dư thừa nếu chỉ có một implementation |
| Builder | Lắp cấu trúc phức tạp theo nhiều bước | Được S2 tr.67 đưa ra để so sánh; không đồng nghĩa Factory và không bắt buộc dùng cho M1 |

**Bằng chứng SOLID trong M1:** mô tả trách nhiệm trước/sau khi tách, vẽ hướng dependency, đặt contract đủ rõ và giải thích một tình huống thay đổi. Chỉ viết năm định nghĩa hoặc gắn nhãn “SOLID” lên sơ đồ chưa chứng minh thiết kế đạt các nguyên tắc.

## 4. Modularity, cohesion, coupling và connascence

**Nguồn:** S3 tr.18–30; B ch.3, PDF tr.82–117; B ch.8 tr.253–259.

### 4.1. Module, granularity và cohesion

Module là nhóm code có trách nhiệm liên quan; granularity là kích thước/độ mịn của cách chia. Nhiều module không tự đồng nghĩa modularity tốt. Chia quá nhỏ làm tăng giao tiếp; chia quá lớn làm khó thay đổi, kiểm thử và phân trách nhiệm.

Cohesion biểu thị mức các phần trong cùng một module nên ở cùng nhau. Danh sách từ mức gắn kết mạnh đến yếu trong S3/B gồm:

| Loại | Cách hiểu | Ví dụ học tập |
|---|---|---|
| Functional | Các phần cùng phục vụ một mục tiêu chức năng | Xác thực một QR credential |
| Sequential | Đầu ra bước trước là đầu vào bước sau | Đọc → kiểm tra → chuẩn hóa dữ liệu |
| Communicational | Cùng dữ liệu hoặc đóng góp vào kết quả liên quan | Các phép xử lý một tập sự kiện |
| Procedural | Gom vì phải thực hiện theo thứ tự | Một chuỗi thao tác được quy trình áp đặt |
| Temporal | Gom vì thực hiện cùng thời điểm | Các tác vụ khởi động |
| Logical | Cùng phân loại tổng quát nhưng chức năng khác | Một thư viện utility rộng |
| Coincidental | Gần như không liên quan, chỉ ở chung file | Mọi hàm tiện ích bị đổ vào một chỗ |

Không máy móc coi mọi pipeline hay utility là thiết kế sai; mục tiêu là tìm ranh giới có lý do và hạn chế coupling vượt ranh giới.

### 4.2. Các chỉ số và giới hạn

| Chỉ số | Công thức/cách hiểu | Dùng để làm gì? |
|---|---|---|
| Afferent coupling, Ca | Số phụ thuộc đi vào module | Đánh giá mức module được các phần khác sử dụng và phạm vi ảnh hưởng khi đổi |
| Efferent coupling, Ce | Số phụ thuộc đi ra | Đánh giá module chịu tác động từ bao nhiêu phần khác |
| Instability, I | Ce / (Ca + Ce) | Gần 1: nhiều phụ thuộc đi ra; gần 0: nhiều phụ thuộc đi vào |
| Abstractness, A | Na / (Na + Nc), với Na là abstract types và Nc là concrete types theo cách đếm đã chọn | Đánh giá mức abstraction của đơn vị code |
| Distance from Main Sequence, D | abs(A + I − 1) | Phát hiện mất cân bằng giữa abstraction và stability |
| LCOM | Họ chỉ số Lack of Cohesion in Methods, có nhiều biến thể | Gợi ý lớp có nhiều nhóm method không chia sẻ dữ liệu/trách nhiệm |

Nếu Ca + Ce = 0, không tự chia 0; ghi module không có liên kết trong phạm vi đo hoặc quy ước của công cụ. S3 tr.24 trình bày LCOM1 theo số cặp method không chung thuộc tính; LCOM2 = max(P − Q, 0). Không trộn số đo giữa các biến thể hoặc công cụ.

“Zone of pain” là ít abstraction nhưng quá nhiều bên phụ thuộc; “zone of uselessness” là abstraction cao nhưng ít giá trị sử dụng. Đây là tín hiệu phân tích, không là kết luận tự động về thiết kế.

S3 tr.28,30 có các khoảng Ce/Ca/I khuyến nghị. Khi áp dụng, ghi đó là hướng dẫn trong slide và chọn phạm vi đo cụ thể; không biến thành luật phổ quát hoặc NFR mới của TMC. B tr.106 nhấn mạnh giới hạn của metrics: chúng không đánh giá trọn vẹn chất lượng kiến trúc.

### 4.3. Connascence — cùng chịu thay đổi

Hai phần có connascence khi đổi một phần buộc đổi phần kia để hệ thống tiếp tục đúng. Khái niệm này làm rõ **bản chất** coupling thay vì chỉ đếm đường nối.

| Nhóm | Dạng | Ví dụ áp dụng để suy nghĩ về TMC |
|---|---|---|
| Static | Name | Hai bên phải thống nhất tên trường employeeId |
| Static | Type | Bên gửi/nhận phải thống nhất kiểu timestamp |
| Static | Meaning | Cùng hiểu mã IN/OUT, không dùng magic number không giải thích |
| Static | Position | Cùng hiểu thứ tự phần tử trong một tuple/API positional |
| Static | Algorithm | Cùng tuân thủ cách tạo/kiểm chữ ký QR |
| Dynamic | Execution | Phải kiểm quyền trước khi điều khiển cổng theo quy ước đã chọn |
| Dynamic | Timing | Token hết hạn, timeout hoặc race giữa hai lần quét |
| Dynamic | Values | Các giá trị chỉ đúng khi thay đổi nhất quán với nhau |
| Dynamic | Identity | Hai bên phải thao tác đúng cùng một thực thể/sự kiện |

Đánh giá theo **strength** (mức khó thay đổi/phát hiện), **locality** (các phần gần hay xa nhau), **degree** (bao nhiêu phần bị ràng buộc). Hạn chế connascence mạnh qua biên module/dịch vụ; đưa các phần buộc thay đổi cùng nhau vào ranh giới phù hợp. Ưu tiên contract rõ mà static analysis có thể kiểm tra, nhưng không thể loại bỏ toàn bộ coupling của nghiệp vụ.

**Law of Demeter — B ch.8:** giảm kiến thức một component phải biết về nội bộ của component khác. Ví dụ thành phần quyết định truy cập gọi contract của gate adapter, không lần lượt điều khiển các bước nội bộ riêng của từng hãng cổng.

## 5. Characteristics, đo lường, quantum và component

**Nguồn:** S4 tr.3–64; B ch.4–8, PDF tr.118–266.

### 5.1. Từ business driver đến architecture characteristic

Functional requirement mô tả hệ thống phải làm gì; characteristic mô tả các khả năng/đặc tính chất lượng cần đạt. Theo S4 tr.4 và B ch.4, một characteristic có ý nghĩa kiến trúc khi nó phản ánh quan tâm ngoài chức năng miền, ảnh hưởng cấu trúc và quan trọng cho thành công.

Tìm characteristics qua ba nguồn: yêu cầu được nói rõ, mối quan tâm nghiệp vụ và kiến thức miền ngầm định. Mỗi suy luận phải có lý do. “Không làm chậm nhân viên đổi ca” chuyển thành yêu cầu hiệu năng có môi trường/tải và phản hồi đo được; “dữ liệu dùng cho đối soát” chuyển thành độ tin cậy, khả năng truy vết và tính đúng hạn.

| Nhóm | Khái niệm chính cần phân biệt |
|---|---|
| Operational | Availability, performance, scalability, elasticity, reliability, recoverability, robustness, continuity |
| Structural | Modularity, maintainability, testability, deployability, extensibility, configurability, portability, installability, upgradeability, reuse |
| Cross-cutting | Security, authentication, authorization, privacy, auditability, legal constraints, accessibility, archivability |
| Cloud — B2e bổ sung | Vị trí vùng dữ liệu, quản lý hạ tầng/provider, elasticity, chi phí và giới hạn tài nguyên |

Availability là khả dụng tại thời điểm cần; reliability là thực hiện đúng trong điều kiện/khoảng thời gian; fault tolerance là tiếp tục vận hành khi có lỗi; recoverability là phục hồi; scalability là đáp ứng khi quy mô tăng; elasticity là thích ứng với tải biến đổi. Không dùng chúng thay cho nhau.

### 5.2. Hệ thuật ngữ chất lượng trong slide

S4 tr.8–15 tổng hợp các nhóm thuật ngữ từ mô hình chất lượng được dùng trong tài liệu môn học:

- Performance efficiency: time behavior, resource utilization, capacity.
- Compatibility: coexistence, interoperability.
- Usability: nhận biết tính phù hợp, dễ học, bảo vệ người dùng khỏi lỗi, accessibility.
- Security: confidentiality, integrity, nonrepudiation, accountability, authenticity.
- Reliability: maturity, availability, fault tolerance, recoverability.
- Maintainability: modularity, reusability, analyzability, modifiability, testability.
- Portability: adaptability, installability, replaceability.

Đây là cách phân loại của nguồn học, không phải tuyên bố bộ tài liệu đã kiểm định một phiên bản tiêu chuẩn hiện hành. Nếu báo cáo viện dẫn tiêu chuẩn cụ thể, cần ghi đúng phiên bản đã kiểm chứng. B tr.140–142 thảo luận vì sao functional suitability khác nhóm quality attributes ngoài nghiệp vụ.

### 5.3. Ưu tiên và composite characteristics

Không cố tối ưu mọi “-ility” cùng lúc. Xem tầm quan trọng với nghiệp vụ và độ khó/rủi ro đạt được (S4 tr.16). Phân biệt driver làm đổi cấu trúc với các chuẩn chất lượng nền vẫn phải giữ. B ch.5 dùng bảng worksheet và bài kata để giới hạn danh sách driver, tránh quá nhiều mục tiêu cạnh tranh.

Các characteristic tổng hợp phải được phân rã: agility phụ thuộc maintainability/testability/deployability; security cần authn/authz, confidentiality/integrity/audit chứ không phải chỉ có trang login. TMC không được bỏ privacy hay API deadline vì đã chọn performance là driver ưu tiên.

Kata là bài luyện thiết kế từ bối cảnh, actors, requirements và additional context, dùng để thực hành suy luận và trình bày trade-off. Các ví dụ Silicon Sandwiches, Going Green, Going Going Gone trong sách là tình huống học phương pháp; không nhập yêu cầu thanh toán/đấu giá của chúng vào M1.

### 5.4. Đo lường và architectural governance

**B ch.6:** thống nhất định nghĩa trước khi đo. Cần phép đo operational, structural và process phù hợp mục tiêu. Average latency có thể che khuất đuôi phân bố; xem phân vị/max và điều kiện thử, nhưng không thay ngưỡng đề bằng một phân vị tự chọn.

Cyclomatic complexity cho một đồ thị điều khiển đơn liên thông thường là CC = E − N + 2; dạng tổng quát CC = E − N + 2P. Giá trị lớn gợi ý nhiều nhánh kiểm thử và khả năng khó bảo trì. Phải phân biệt complexity thiết yếu do nghiệp vụ với complexity do cách triển khai. Không suy từ ít nhánh code rằng kiến trúc đã tốt.

Fitness function là cơ chế đánh giá khách quan một đặc tính kiến trúc theo thời gian. Có thể dùng automated tests/static analysis, đo runtime hoặc review có tiêu chí; không đồng nghĩa unit test nghiệp vụ.

| Fitness function ứng viên cho TMC | Đánh giá gì? | Mức M1 |
|---|---|---|
| Kiểm dependency core không import SDK gate/HR | DIP và ranh giới module | Mô tả quy tắc và cách kiểm; M2 mới cần chạy trên code |
| Đo phản hồi kiosk theo tải đề, kèm phân bố latency | NFR-01 | Thiết kế phép thử và measurement boundary |
| Đối chiếu IDs các sự kiện chấp nhận với bản ghi lưu bền | NFR-02 | Mô tả invariant và tập dữ liệu kiểm chứng |
| Kiểm access denied đối với role/phạm vi sai | NFR-03 | Permission cases và vị trí enforcement |
| Theo dõi phần dữ liệu xuất chưa được xác nhận trước deadline | INT-02 | Mô hình trạng thái và điểm cảnh báo đề xuất |

Tools như ArchUnit, NetArchTest hay dependency analyzers trong B ch.6 là ví dụ phương tiện, không là stack được đề yêu cầu. Governance nhằm duy trì quyết định thiết kế qua thay đổi, không phải thêm thủ tục vô nghĩa.

### 5.5. Architectural quantum và phạm vi chất lượng

Một quantum là ranh giới giúp xác định phạm vi characteristics, gắn với khả năng triển khai độc lập, functional cohesion và các coupling cần xét. B ch.7 làm rõ static implementation coupling và synchronous dynamic coupling; chỉ đếm process/service không đủ xác định số quantum.

Nếu nhiều dịch vụ phải đồng thời hoạt động để xử lý một yêu cầu đồng bộ, availability/performance của luồng vẫn bị ràng buộc. Chia nhiều service nhưng dùng chung schema, phát hành cùng nhau và gọi nhau dày đặc có thể không tạo độc lập như mong đợi.

**TMC:** luồng quyết định tại cổng và luồng xuất báo cáo có thể có đặc tính vận hành khác nhau. Đây là lý do để đánh giá cách tách trách nhiệm và critical path; chưa phải bằng chứng bắt buộc tách thành microservices. Một module của monolith vẫn có thể có worker/background job riêng trong thiết kế phù hợp.

### 5.6. Component-based thinking và quy trình từ logic sang vật lý

S4 tr.30 phân biệt module triển khai code và component runtime; B ch.8 dùng **logical component** cho khối chức năng phản ánh cách tổ chức code. S6 dùng component trong C&C cho runtime elements. Khi viết bài, luôn ghi rõ đang nói logical component hay runtime component; không ép mỗi logical component thành một service deploy riêng.

Vòng lặp thiết kế trong S4 tr.31–34 và B tr.233–252:

1. Chọn phân chia ban đầu theo actor/actions hoặc workflow.
2. Gắn requirement/use case vào các component ứng viên.
3. Phân tích vai trò, trách nhiệm và mức granularity.
4. Đánh giá characteristics tác động đến ranh giới.
5. Tách/gộp/chuyển trách nhiệm, kiểm tra dependency và lặp lại.

**Actor/Action:** từ HR → đối soát/xuất dữ liệu; bảo vệ → giám sát cổng; nhân viên → hiển thị QR/ra-vào để suy ra trách nhiệm. Một action không nhất thiết là một component.

**Workflow:** quét → kiểm tra credential/quyền → xử lý truy cập/ghi nhận → tổng hợp → xuất; xác định mỗi bước có owner và interface nào. Không dùng thứ tự minh họa này để che mất câu hỏi về xác nhận người đã qua cổng.

**Entity Trap:** biến mọi danh từ Employee/Gate/Report thành một Manager rồi gọi đó là kiến trúc. Entity cần trong data model nhưng component phải có trách nhiệm hành vi rõ; không chỉ là lớp CRUD quanh bảng.

Sau khi có logical components và driver, so sánh style để map logic vào các runtime artifact. Tiếp đó phân bổ artifact lên thiết bị/máy chủ/nhà máy. S4 tr.56–64 minh họa vì sao sơ đồ cloud không cho biết đầy đủ chức năng nằm ở đâu; cần bảng mapping từ logic sang vật lý và source organization ở mức thích hợp.

## 6. Architecture styles và cách lựa chọn

**Nguồn:** S5.1 tr.3–50; S5.2 tr.3–46; S5.3 tr.3–44; B ch.9–19, PDF tr.268–733.

### 6.1. Các phân biệt nền tảng

Architecture **style** mô tả cấu trúc tổng thể/topology, cách deploy, communication và data topology. Architecture **pattern** giải quyết một bài toán cấu trúc/tương tác có thể xuất hiện trong nhiều style. Strategy/Facade là design patterns ở mức nhỏ hơn; sidecar, CQRS hay orchestration là architectural patterns. Không xếp PostgreSQL, REST hoặc Docker như những style ngang hàng microservices/layered.

**Technical partitioning** chia theo loại công việc kỹ thuật (presentation/business/persistence). **Domain partitioning** chia theo năng lực/nghiệp vụ. Mỗi module miền có thể lại phân lớp nội bộ. Không nhầm layer logic với tier triển khai trên mạng: nhiều layer có thể nằm trong một process.

Một monolith chủ yếu là một đơn vị deploy cho logic ứng dụng, không nhất thiết một máy vật lý hoặc một source file. Distributed architecture có nhiều đơn vị triển khai liên kết qua remote protocols; độc lập triển khai phải được thiết kế chứ không tự sinh khi tách process.

Big Ball of Mud là cấu trúc tăng trưởng hỗn loạn, thiếu ranh giới và governance, không phải đích thiết kế. Unitary, desktop + database, browser + web server và three-tier cho thấy lịch sử tách trách nhiệm. Chúng không xác định sẵn giải pháp cho TMC.

### 6.2. Distributed computing: lợi ích và chi phí

S5.1 tr.9–17 và B ch.9 nhắc tám giả định sai kinh điển:

| Giả định sai | Câu hỏi phải đặt cho TMC |
|---|---|
| Mạng luôn tin cậy | Nếu kết nối nhà máy–backend ngắt thì sự kiện và quyết định ở đâu? |
| Latency bằng 0 | Có bao nhiêu remote call nối tiếp trong ngân sách 2 giây? |
| Bandwidth vô hạn | Payload QR/attendance có mang dữ liệu nhân sự không cần thiết? |
| Mạng luôn an toàn | Ai được gọi API trạm/cổng; xác thực thiết bị và mã hóa ra sao? |
| Topology không đổi | Thay địa chỉ/instance/controller thì client tìm dịch vụ thế nào? |
| Chỉ có một administrator | Ai sở hữu backend, mạng nhà máy, HR API và thiết bị cổng? |
| Transport không tốn chi phí | Chi phí hạ tầng, vận hành, kết nối liên nhà máy là gì? |
| Mạng đồng nhất | Thiết bị/nhà cung cấp/protocol khác nhau được cô lập thế nào? |

B2e ch.9 tr.305–307 bổ sung ba fallacy: **versioning dễ**, **compensating updates luôn thành công**, **observability là tùy chọn**. Đây là phần mở rộng so với tám mục trong slide. Distributed logging, tracing, timeout, retries, contract/versioning và transactional boundaries là công việc thực tế phải trả giá.

Stamp coupling xảy ra khi truyền object/data structure lớn trong khi bên nhận chỉ cần ít trường: tăng bandwidth, lộ dữ liệu và contract coupling. Chỉ truyền dữ liệu cần thiết, đồng thời cân nhắc snapshot so với tra cứu thêm dữ liệu.

### 6.3. Bảng nhận diện các style

| Style | Cấu trúc/data điển hình | Điểm mạnh có điều kiện | Chi phí/rủi ro chính |
|---|---|---|---|
| Layered | Các layer kỹ thuật; thường một deploy ứng dụng và database chung | Dễ hiểu, chi phí ban đầu thấp, phù hợp quy trình đơn giản | Thay đổi nghiệp vụ đi qua nhiều layer; coupling, sinkhole; scale/fault isolation không chi tiết |
| Modular monolith | Module theo miền, một deployment; có thể dùng schema/module ownership | Local calls, transaction đơn giản hơn, ranh giới nghiệp vụ rõ | Không scale/deploy độc lập từng module; dễ xói mòn ranh giới |
| Pipeline | Producer → filters → consumer qua pipes | Tái sử dụng bước xử lý, test riêng từng phép biến đổi | Trạng thái/nhánh phức tạp, xử lý lỗi và luồng tương tác không tự nhiên |
| Microkernel | Core ổn định + plug-ins qua contracts/registry | Extensibility và cô lập biến thể | Core phình, plug-in phụ thuộc nhau, tương thích/versioning |
| Service-based | Một số domain services thô, remote calls, database thường chia sẻ | Cân bằng độ độc lập với chi phí phân tán | Schema coupling, transaction xuyên service, shared DB contention |
| Event-driven | Producers/processors, event channels/brokers; xử lý chủ yếu async | Phản ứng, fan-out, mở rộng và cách ly consumer | Ordering, duplicates, delivery, workflow visibility, eventual consistency |
| Space-based | Processing units + memory grid; data pumps ra storage | Elasticity và tải tăng vọt, tránh DB trong đường nóng | Cache collision/consistency, memory/data volume, đồng bộ và vận hành phức tạp |
| Orchestration-driven SOA | Business/enterprise/application/infrastructure services qua orchestration/ESB | Tích hợp/tái sử dụng trong doanh nghiệp có nền tảng phù hợp | Coupling qua shared services và orchestrator; phối hợp thay đổi khó |
| Microservices | Bounded contexts, services deploy riêng, data ownership riêng | Independent change/scale khi ranh giới và vận hành tốt | Network overhead, distributed workflow/data, versioning và observability |

Đây là khuynh hướng cấu trúc, không phải số đo hiệu năng. Bảng sao trong slide/sách dùng để học khả năng hỗ trợ tương đối của style, không phải benchmark hoặc chứng nhận một thiết kế TMC cụ thể.

### 6.4. Layered architecture

**Nguồn:** S5.1 tr.20–31; B ch.10 tr.311–334.

Presentation xử lý giao diện, business xử lý quy tắc nghiệp vụ, persistence quản lý truy cập dữ liệu; database là nơi lưu. Số layer và cách đóng gói thay đổi theo hệ thống. Các layer có thể ở cùng deploy hoặc nhiều tier.

**Closed layer** yêu cầu luồng từ trên đi qua layer ngay dưới; **open layer** cho phép bỏ qua theo quy tắc đã định. Layers of isolation hạn chế tác động thay đổi, nhưng một chuỗi layer chỉ chuyển tiếp không thêm giá trị gây **architecture sinkhole**. Không chữa sinkhole bằng cách tùy ý cho UI truy cập DB trực tiếp mà bỏ lý do cô lập.

Phù hợp khi tính đơn giản và khả năng xây dựng quan trọng, phạm vi chưa đòi scale/deploy từng miền. Rủi ro: code dồn vào business layer, toàn hệ thống phải release cùng nhau, một lỗi có thể ảnh hưởng toàn process. Governance: kiểm permitted dependencies, không có cycle/skip layer trái quyết định. Team tổ chức theo kỹ thuật dễ tiếp cận, nhưng thay đổi miền có thể cần nhiều team phối hợp.

**TMC:** là một ứng viên cần so sánh. Nếu chọn, phải chỉ ra nơi nghiệp vụ cổng/chấm công/báo cáo nằm trong các layer và nơi tích hợp controller/HR được cô lập.

### 6.5. Modular monolith

**Nguồn:** S5.1 tr.24–25 có đối chiếu; B ch.11 tr.335–364 trình bày riêng.

Chia top-level theo miền/trách nhiệm và deploy chung. B nêu hai dạng tổ chức: module trong cùng cấu trúc project hoặc module build thành artifact riêng rồi ghép thành một deployment. **Artifact build riêng không tự có nghĩa service deploy độc lập.**

Module có thể giao tiếp peer-to-peer qua contract hoặc qua mediator. Peer-to-peer đơn giản nhưng làm tăng phụ thuộc nếu gọi chéo rộng; mediator tập trung giao tiếp nhưng có thể trở thành điểm coupling. Data có thể dùng chung database, song cần ownership và quyền truy cập rõ để module không dựa vào chi tiết bảng của nhau.

Rủi ro: module quá to, liên lạc chéo dày, ranh giới bị phá bởi import hoặc shared entity library. Governance: kiểm namespace/module đã định, allowed dependencies, cycle, số liên kết ở phạm vi phù hợp; không lấy ngưỡng tùy ý làm tiêu chuẩn chung. Team theo domain thường phù hợp.

**TMC:** có thể đặt các module Credential, Access/Attendance, Reporting, HR Integration trong một backend; đây là ví dụ, chưa là lựa chọn đã chốt. Muốn worker HR chạy độc lập phải nói rõ cách đóng gói và giao tiếp, không gọi toàn hệ thống “monolith thuần” một cách thiếu chính xác.

### 6.6. Pipeline — pipes and filters

**Nguồn:** S5.1 tr.32–36; B ch.12 tr.365–390.

Pipe thường một chiều, point-to-point; filter nhận/biến đổi/kiểm hoặc tiêu thụ dữ liệu. Bốn vai trò là producer, transformer, tester và consumer. Tổ chức pipeline giúp chia bài toán thành bước có I/O rõ, dễ thay thế và kiểm thử riêng.

Độ phù hợp giảm khi cần nhiều trạng thái tương tác hoặc transaction trải rộng các bước. Cần quy ước dữ liệu sai, retry ở bước nào, khả năng tiếp tục từ checkpoint, backlog và backpressure nếu dùng xử lý streaming. Governance kiểm loại filter, hướng giao tiếp và contract; đội xử lý kỹ thuật hoặc subsystem chuyên biệt thường phù hợp hơn áp dụng cho mọi tác vụ.

**TMC:** là pattern/style ứng viên cho luồng trích xuất → chuẩn hóa → kiểm tra → tổng hợp → gửi dữ liệu HR. Không vì có một pipeline xuất dữ liệu mà kết luận mọi phần kiểm soát cổng phải theo pipeline.

### 6.7. Microkernel — plug-in architecture

**Nguồn:** S5.1 tr.37–50; B ch.13 tr.391–421.

Core giữ chức năng tối thiểu, ổn định; plug-ins hiện thực tính năng/biến thể qua contract. Registry giúp core tìm plug-in bằng tên, thông tin contract và cơ chế gọi. Plug-in có thể gắn lúc build hoặc nạp runtime; runtime linh hoạt hơn nhưng tăng quản lý tương thích và vòng đời.

Không phải hệ thống có extension point nào cũng là microkernel; B2e ch.13 đặt vấn đề mức độ chức năng ở core và plug-ins. Tránh core chứa toàn bộ business logic rồi gọi vài adapter là “microkernel” mà không chứng minh cấu trúc. Plug-in không nên tùy tiện phụ thuộc nhau; phiên bản core/contract/data phải được quản lý.

Ưu điểm là thay biến thể và cô lập phần dễ đổi. Rủi ro: volatile core, shared dependency conflict, registry phức tạp, plug-in kéo sập core nếu cùng process. Governance kiểm hướng core/plugin dependencies, contract và tương thích. Có thể có team core và các team feature/plug-in.

**TMC:** nếu thực tế có nhiều hãng cổng và nghiệp vụ extension rõ, có thể đánh giá plug-in. Với một controller hiện hữu, adapter interface đơn giản có thể đủ; sự tồn tại của adapter không buộc chọn microkernel.

### 6.8. Service-based architecture

**Nguồn:** S5.2 tr.3–18; B ch.14 tr.422–456.

Các dịch vụ miền tương đối thô và UI triển khai riêng; database thường dùng chung. Có các biến thể UI theo nhóm người dùng/domain, API gateway tùy chọn và database chung hoặc partition theo miền. Con số số service điển hình trong nguồn là mô tả, không phải yêu cầu phải tạo đúng số service.

Một domain service có thể dùng ACID transaction trên dữ liệu thuộc trách nhiệm của nó. Khi workflow đi qua nhiều dịch vụ/database, vẫn phải phân tích tính nguyên tử và cách xử lý kết quả một phần; không mặc định shared DB giải quyết mọi consistency.

Rủi ro chính là dịch vụ đọc/ghi chéo schema và shared entity library khiến đổi một phần buộc redeploy nhiều phần. Phân quyền dữ liệu, ownership, tách schema phù hợp và contract rõ giúp giảm coupling. Team theo miền thuận lợi; platform team hỗ trợ phần vận hành chung.

**TMC:** là ứng viên khi muốn tách Access/Attendance khỏi Reporting/Integration với mức phân tán vừa phải. Báo cáo phải cân chi phí mạng/vận hành với lợi ích; không viết “phân tán nên chắc chắn nhanh hơn monolith”.

### 6.9. Event-driven architecture — EDA

**Nguồn:** S5.3 tr.3–26; B ch.15 tr.457–566.

**Event** diễn tả sự việc đã xảy ra, như AttendanceRecorded; **command/query message** yêu cầu làm việc, như OpenGate hoặc GetExportStatus. B2e tr.467–469 nhấn mạnh khác biệt ngữ nghĩa này. Tên queue/topic không tự quyết định một payload là fact hay command.

| Topology | Lợi ích | Đánh đổi |
|---|---|---|
| Broker/choreographed | Processor phản ứng và phát sinh sự kiện; giảm điều phối trung tâm, dễ thêm consumer | Workflow và trạng thái phân tán; khó theo dõi hoàn tất, recovery và lỗi |
| Mediator/mediated | Có thành phần điều phối bước xử lý, trạng thái và lỗi | Tăng coupling với coordinator, chi phí phối hợp và nguy cơ bottleneck |

Async cải thiện thời gian phản hồi cho producer khi không phải đợi công việc dài, nhưng chưa nói công việc đã hoàn tất. Request-reply qua messaging vẫn có sự phụ thuộc vào phản hồi; cần correlation ID, reply destination, timeout và cleanup. Nó không tạo latency bằng 0.

**Payload:** data-based events mang snapshot dữ liệu giúp consumer ít gọi ngược nhưng tăng payload, privacy và contract coupling; key-based events nhẹ và schema đơn giản hơn nhưng consumer phải truy vấn nguồn, dễ tăng latency/phụ thuộc runtime. Tránh anemic events thiếu thông tin cần thiết và Swarm of Gnats khi một thay đổi sinh quá nhiều event quá nhỏ. Chọn theo tính độc lập và dữ liệu thực sự cần.

**Không mất dữ liệu — S5.3 tr.19–20, B tr.509–513:** xem ba chặng producer→channel, channel→consumer, consumer→database. Cần persistence/durable channel phù hợp, xác nhận sau bước cần bảo đảm, xử lý consumer crash và lỗi lưu. Durable transport không tự loại được tác dụng phụ trùng do redelivery.

Trong thiết kế TMC, có thể đề xuất transactional outbox, retry có giới hạn, idempotency, dead-letter handling và reconciliation để xử lý khoảng hở DB–message. Đây là **tactics bổ sung của bộ hướng dẫn**, không phải tên kỹ thuật được đề M1 bắt buộc hoặc bảo đảm “exactly once” trên toàn DB–controller–HR. Nếu chỉ chọn worker đọc trạng thái DB để xuất cũng cần giải thích độ bền và trạng thái công việc.

Data topology của EDA có thể chung, theo miền hoặc riêng processor; chọn topology ảnh hưởng coherence, transaction và mức độc lập. Governance phải kiểm event schema/ownership, duplicate/order handling, độ trễ xử lý, lag, routing và error handling. Event-driven dễ tăng responsiveness nhưng kiểm thử end-to-end và quan sát hệ thống khó hơn.

**TMC:** rất hữu ích để đánh giá phần báo cáo/xuất HR sau khi sự kiện đã được lưu bền. Đường phản hồi kiosk vẫn phải có kết quả xác thực và quyết định rõ; không gửi event rồi hiện “chấm công thành công” khi mới ghi vào RAM.

### 6.10. Space-based architecture

**Nguồn:** S5.3 tr.27–44; B ch.16 tr.567–627.

Ứng dụng được đặt trong **processing units**, dữ liệu giao dịch nóng nằm trong memory grid để giảm bottleneck từ truy cập database trực tiếp. Điều này không có nghĩa toàn hệ thống không có database; dữ liệu có thể được đẩy bền xuống storage qua data pump/data writer và đọc lại khi cần.

| Thành phần | Trách nhiệm |
|---|---|
| Messaging grid | Phân phối request/session đến processing unit |
| Data grid | Đồng bộ/replicate dữ liệu giữa các unit |
| Processing grid | Phối hợp xử lý cần nhiều processing unit |
| Deployment manager | Tăng/giảm instance theo điều kiện tải |
| Data pump | Gửi thay đổi bất đồng bộ ra đường ghi storage |
| Data writer | Hiện thực việc ghi xuống database |
| Data reader | Khôi phục/nạp dữ liệu khi khởi động, phục hồi hoặc truy vấn dữ liệu ngoài cache |

Replicated cache cho mỗi unit giữ dữ liệu liên quan, giúp đọc nhanh và có bản sao nhưng gặp replication latency/collision. Distributed cache chia dữ liệu giữa các nơi, giảm nhân bản nhưng thêm remote access và phải xem availability của nơi giữ dữ liệu. Near-cache lại đưa vấn đề invalidation/freshness vào thiết kế.

Source nêu collision phụ thuộc số instance N, update rate UR, cache size S và replication latency RL; dạng ước lượng là CollisionRate ≈ N × UR² / S × RL (S5.3 tr.39–41; B tr.607–613). Phải chuẩn hóa đơn vị và kiểm chứng mô hình trước khi tính; không dùng chuỗi công thức trích xuất mất định dạng để cam kết xác suất mất dữ liệu. Nhiều instance không tự làm dữ liệu đúng hơn.

Rủi ro: frequent database reads phá mục tiêu, dữ liệu lớn vượt bộ nhớ, update/collision, eventual consistency giữa grid và durable DB. Cần năng lực vận hành middleware, memory capacity, recovery và thử tải. Thích hợp để nghiên cứu bài toán tải cực lớn/tăng đột biến; không có căn cứ từ 800 giao dịch/30 phút để khẳng định TMC bắt buộc dùng style này. S5.3 tr.33 lặp mô tả messaging grid ở mục processing grid; dùng B tr.590–592 để phân biệt hai vai trò.

### 6.11. Orchestration-driven SOA

**Nguồn:** B ch.17, PDF tr.628–655. Đây là chương mở rộng của sách, không là mục riêng trong slide Chapter 5 đã cung cấp.

SOA theo hướng orchestration tổ chức business services, enterprise services dùng chung, application services và infrastructure services; orchestration engine/message bus phối hợp workflow. Mục tiêu lịch sử là tích hợp/tái sử dụng năng lực cấp doanh nghiệp, thường với giao tiếp và biến đổi dữ liệu trung gian.

Tái sử dụng tạo coupling: thay shared service có thể ảnh hưởng nhiều ứng dụng; centralized orchestration giúp quản workflow nhưng tăng phụ thuộc và phối hợp tổ chức. Không nhầm SOA với service-based hoặc microservices chỉ vì cả ba dùng từ service. Phù hợp khi bối cảnh doanh nghiệp đã có nhu cầu và nền tảng tương ứng; không mặc định dựng ESB mới chỉ để nối một HR API.

### 6.12. Microservices

**Nguồn:** S5.2 tr.19–46; B ch.18, PDF tr.656–707.

Các dịch vụ tổ chức theo **bounded context**, có functional cohesion, data ownership và khả năng thay đổi/deploy tương đối độc lập. Bounded context nói về phạm vi ý nghĩa của mô hình miền; không đồng nghĩa một entity hoặc một endpoint. Kích thước service được quyết định theo purpose, transaction boundaries và nhu cầu cộng tác; “micro” không có một số dòng code chuẩn.

- **Data isolation:** không dùng shared database schema làm điểm tích hợp không kiểm soát. Hai service có thể chạy DB trên cùng hạ tầng nhưng ownership và coupling mới là điều phải phân tích.
- **API layer:** gateway/reverse proxy hữu ích cho routing/auth/rate limits, nhưng không phải bản thân style hoặc thành phần luôn bắt buộc.
- **Operational reuse:** sidecar và service mesh đưa logging, monitoring, policy, routing… vào đường vận hành chung, tăng nhất quán nhưng thêm tài nguyên và độ khó debug.
- **Frontend:** UI có thể tập trung hoặc chia microfrontend; chia frontend không tự làm backend độc lập.
- **Communication:** REST/RPC đồng bộ hay messaging/EDA bất đồng bộ đều cần contract; nhiều cuộc gọi nhỏ nối tiếp tạo latency và temporal coupling.
- **Heterogeneity:** cho phép nhiều stack không có nghĩa cố tình mỗi service một ngôn ngữ. Enforced heterogeneity có thể tăng chi phí vô ích.
- **Transactions:** local ACID vẫn tồn tại trong service. Workflow qua nhiều service cần xử lý consistency và partial failure; không viết “microservices không có transaction”.

Saga phối hợp các local transactions và compensating actions khi bước sau thất bại; compensation là hành động nghiệp vụ mới, không phải DB rollback toàn cục hoặc bảo đảm không thể thất bại. Nếu phần lớn workflow cần transaction chặt xuyên service, xem lại granularity. Với gate vật lý, không thể “undo việc nhân viên đã qua cổng” bằng một lệnh rollback.

Phù hợp khi nhu cầu independent change/scale/domain ownership đủ lớn và đội có năng lực automation/observability. Rủi ro: distributed monolith, contract drift, shared library coupling, chatty calls và chi phí vận hành. Governance gồm contract compatibility, data ownership, dependency graph, delivery pipeline và runtime health.

**TMC:** nên xuất hiện trong so sánh khi thích hợp; quy mô 1.400 nhân viên không tự chứng minh phải chọn hoặc phải loại microservices. Cần cân deadline, workload thật, năng lực đội và các lựa chọn đơn giản hơn.

### 6.13. Chọn style theo bối cảnh

**B ch.19:** chọn theo domain, structural characteristics, data architecture và tổ chức; chú ý thay đổi hệ sinh thái, công nghệ và business. Đừng chọn chỉ vì đã quen, vì mẫu công ty nổi tiếng hoặc vì nhiều dấu cộng trong bảng chung.

Quy trình áp dụng cho M1:

1. Xác nhận các driver và các ràng buộc không thể bỏ qua.
2. Có logical components đủ rõ trước khi đóng gói deploy.
3. Lập shortlist có lý do; có thể so sánh layered/modular monolith, service-based, microservices, và dùng EDA cho phần việc phù hợp.
4. Dùng cùng tiêu chí cho mọi ứng viên: kiosk latency, durability, integration, security/audit, simplicity, deploy/ops cost, khả năng thay đổi.
5. Nếu chấm điểm, công bố trọng số là lựa chọn của nhóm; ghi căn cứ từng điểm. Không bù một vi phạm NFR bắt buộc bằng nhiều điểm ở tiêu chí khác.
6. Chọn giải pháp và nêu trade-off/mitigation; điều kiện nào sẽ khiến nhóm xem xét lại.

Kết hợp style/pattern được phép nếu mô tả rõ phạm vi. Ví dụ minh họa: backend modular monolith, adapter theo ports/interfaces, xuất HR qua worker bền. Đây là một ứng viên để phân tích, chưa phải kiến trúc được bộ tài liệu quyết định thay nhóm.

## 7. Các architectural pattern bổ sung

**Nguồn:** B ch.20 PDF tr.734–758; S5.2 tr.27–45; S5.3 tr.15–24.

| Pattern | Bài toán và cơ chế | Đánh đổi cần nêu cho M1 |
|---|---|---|
| Hexagonal / Ports and Adapters | Core nghiệp vụ giao tiếp qua port; adapter cho UI, DB, controller, HR | Dễ thay/test phụ thuộc nhưng thêm abstraction/mapping; không phải một loại triển khai vật lý |
| Sidecar / Service Mesh | Tách coupling vận hành khỏi coupling nghiệp vụ, điều phối telemetry/policy chung | Tốn thêm process/proxy/ops; không thay business authorization trong core |
| Orchestration | Có coordinator nắm bước/trạng thái workflow | Dễ theo dõi/recover hơn; coordinator thêm coupling và có thể bottleneck |
| Choreography | Thành phần phản ứng sự kiện, không có coordinator nghiệp vụ tập trung | Giảm phối hợp trung tâm; khó quan sát hoàn tất, lỗi và state xuyên nhiều phần |
| CQRS | Tách trách nhiệm/đường đọc và ghi, có thể dùng read model riêng | Tối ưu mục tiêu khác nhau; nếu tách store phải xử lý đồng bộ/freshness; không bắt buộc event sourcing |
| Broker–Domain và Domain–Broker | Tập trung broker cho các domain hoặc phân broker theo domain | Cân discovery/ít hạ tầng với isolation, scaling, fault tolerance và chi phí |

Hexagon là ký hiệu để nhấn mạnh nhiều interface, không yêu cầu đúng sáu port. Mesh và hexagonal minh họa tách coupling theo mối quan tâm, có thể cùng xuất hiện. Orchestration/choreography nằm trên một phổ: một workflow có thể có coordinator cục bộ mà không biến toàn hệ thống thành SOA.

**Tactics triển khai được đề xuất thêm cho TMC:** timeouts giới hạn chờ; retry có giới hạn và backoff; idempotency cho gửi lặp; circuit breaker khi dependency liên tục lỗi; durable job/outbox để không mất việc cần xuất; log/correlation ID cho truy vết. Chỉ đưa vào thiết kế khi giải thích lỗi nào được xử lý, state ở đâu, chi phí gì. Không cần vẽ toàn bộ thành service/process riêng.

## 8. Documenting Software Architecture

**Nguồn:** S6 tr.3–75; B ch.23 tr.830–845; S4 tr.56–64.

### 8.1. Views and Beyond

Tài liệu kiến trúc phục vụ giáo dục, giao tiếp và phân tích/xây dựng. Nó vừa **prescriptive** (ràng buộc việc phải làm), vừa **descriptive** (mô tả điều đã thiết kế). Người mới cần nhìn tổng quan; developer cần trách nhiệm/interface; tester cần hành vi/tải/lỗi; operator cần deployment/phụ thuộc; HR và quản lý cần biết nhu cầu của họ được đáp ứng ở đâu.

Views and Beyond không chọn một sơ đồ duy nhất cho mọi stakeholder. Phải xác định nhu cầu người đọc, chọn view trả lời câu hỏi đó, ghi quyết định và thông tin chung giữa các view, rồi kiểm tra tài liệu dùng được. Đề M1 yêu cầu nhiều view; bộ hướng dẫn chọn ba nhóm S6 làm cách đáp ứng có căn cứ môn học.

### 8.2. Ba nhóm view

| Nhóm | Elements/relations | Dùng phân tích gì? | Sản phẩm đề xuất cho TMC |
|---|---|---|---|
| Module | Đơn vị triển khai code; is-part-of, depends-on, is-a | Modifiability, reuse, impact, allowed dependency | Phân rã module/trách nhiệm, dependency; mô hình dữ liệu mức cần thiết |
| C&C | Runtime components và connectors: request/response, messaging, DB access | Behavior, latency, concurrency, reliability, availability | Runtime topology và sequence quét QR, xuất HR |
| Allocation | Mapping software elements sang phần ngoài software | Phù hợp tài nguyên, deployment, operational risk | Thiết bị ở hai nhà máy, backend/storage và kết nối HR/controller |

Một logical component có thể hiện thực bằng nhiều module và nhiều instance runtime; nhiều logical component cũng có thể ở chung một process. Cần bảng mapping, không giả định quan hệ 1:1.

### 8.3. Module views chi tiết

**S6 tr.18–37:** mô tả đơn vị implementation và trách nhiệm, quan hệ phụ thuộc, interface visibility, ràng buộc và mapping code nếu đã có. Có thể thể hiện decomposition, uses/layering, generalization, data model hoặc Dependency Structure Matrix (DSM).

- **Is-part-of:** phần thuộc tổng thể, không tự suy ra gọi runtime.
- **Depends-on:** cần nói là import/uses/allowed-to-use/data relation nào; mũi tên chung chung không đủ.
- **Is-a:** generalization/specialization, bao gồm inheritance/interface realization khi phù hợp.
- **DSM:** hàng/cột là module, ô cho biết dependency theo quy ước đã giải thích; hỗ trợ nhận diện cycle và cụm coupling.

Module view không chứng minh latency/reliability runtime chỉ từ số hộp. TMC cần kết hợp với C&C và Allocation để lập luận NFR.

### 8.4. Component-and-Connector views chi tiết

**S6 tr.38–53:** component là đơn vị runtime, như client/server/process/object/datastore; connector là cơ chế tương tác có semantics, ports/roles và protocol. Các dạng trong nguồn gồm client–server, transactional authenticated database access và publish–subscribe.

Nêu rõ sync/async, message/data, hướng mũi tên, timeout và response ở mức liên quan. Một đường publish-subscribe có thể được biểu diễn bằng connector event bus hoặc bằng event dispatcher component cộng connector thích hợp; không đổi cách vẽ mà bỏ mất ý nghĩa.

UML components/ports có thể hỗ trợ view này, nhưng connector phức tạp cần chú giải hoặc mô tả bổ sung. Sequence diagram giải thích hành vi một scenario; nó bổ sung, không tự thay mọi runtime topology. Với TMC phải biết ở đâu quyết định quyền, ở đâu lưu bền, ở đâu có tác dụng phụ mở cổng và ở đâu xuất dữ liệu HR.

### 8.5. Allocation views chi tiết

**S6 tr.54–75** giới thiệu ba style:

| Allocation style | Mapping | Câu hỏi cụ thể |
|---|---|---|
| Deployment | Runtime elements → hardware/execution environment | Backend, DB, scanner/client ở node nào; network/failure boundary nào? |
| Install | Components/artifacts → file/configuration organization | Package, executable, config, log và thư mục triển khai được tổ chức thế nào? |
| Work assignment | Modules → người/team/đơn vị tổ chức | Ai xây và tích hợp phần nào, có kỹ năng/tài nguyên gì? |

Deployment cần xét CPU, memory, disk, bandwidth, fault tolerance và resource requirements. Không bịa số server/vCPU như thông số được khách hàng cung cấp. Có thể dùng giả định sizing có cơ sở và cách đo lại.

M1 nên có deployment view hai nhà máy và tích hợp ngoài. Install/work assignment được trình bày khi giúp hiểu thiết kế/phân công; đề không buộc mọi sơ đồ mẫu của Chapter 6 đều xuất hiện trong báo cáo. Không bịa tên thành viên khi chưa có thông tin nhóm.

### 8.6. Mỗi view cần đi cùng gì?

Theo S6 tr.15–16, tối thiểu cần:

1. Primary presentation: sơ đồ hoặc bảng chính có tên/phạm vi/legend.
2. Element catalog: mỗi thành phần là gì, trách nhiệm, thuộc tính quan trọng.
3. Interface và behavior: dữ liệu, giao tiếp, hành vi cần biết.
4. Variability guide: điểm cấu hình/thay thế; có thể ghi chưa có cơ chế biến thể được chọn.
5. Rationale/design information: vì sao cấu trúc này đáp ứng mục tiêu.

Thông tin beyond-view gồm reader guide, quan hệ giữa view, constraints/rationale chung và thông tin duy trì tài liệu. Đừng chỉ dán ảnh rồi gọi là tài liệu kiến trúc.

### 8.7. UML, C4, ArchiMate và Mermaid

B ch.23 mô tả UML, C4 và ArchiMate là các cách mô hình hóa/giao tiếp khác nhau. C4 đi từ Context → Container → Component → Code; “container” của C4 không mặc định là Docker container. C4 không tự thay toàn bộ ba nhóm view của S6, đặc biệt allocation và thông tin interface/rationale.

Mermaid được bộ này chọn làm cú pháp sơ đồ trong Markdown. Một flowchart Mermaid không tự thành UML component/deployment diagram chuẩn. Nếu dùng để minh họa, ghi loại view, ý nghĩa mũi tên và semantics; nếu giảng viên yêu cầu UML chuẩn thì chuyển sang công cụ/cú pháp UML phù hợp.

Sơ đồ tốt có title/scope, tên nhất quán, label và legend, không trộn abstraction quá xa trong cùng hình. Màu sắc chỉ hỗ trợ; không dùng màu làm cách phân biệt duy nhất. **Irrational Artifact Attachment** là bám một sơ đồ cũ chỉ vì đã tốn công vẽ, dù nó không còn phục vụ người đọc. Chấp nhận sửa/bỏ sơ đồ khi thiết kế đổi.

## 9. ADR, rủi ro, đội nhóm và các giao điểm

### 9.1. Architectural Decision Records

**Nguồn:** B ch.21 PDF tr.760–796; S1 tr.16–18.

ADR ghi một quyết định đáng kể cùng bối cảnh và hệ quả, giữ lịch sử để người sau hiểu **vì sao**. Một ADR ngắn có thể hiệu quả hơn nhiều trang mô tả không thể hiện lựa chọn. Cấu trúc cốt lõi: title, status, context, decision, consequences. B bổ sung compliance và notes khi cần.

Status có thể proposed, accepted, rejected, deprecated hoặc superseded; giữ liên kết quyết định mới thay quyết định cũ, không xóa lý do lịch sử. Đây là trạng thái nội bộ hồ sơ thiết kế, không phải bằng chứng giảng viên/khách hàng đã duyệt. Với bài cá nhân/nhóm, ghi ai chọn và trạng thái đang là đề xuất hay thiết kế đã chọn của nhóm.

| Antipattern | Hậu quả | Cách tránh |
|---|---|---|
| Covering Your Assets | Trì hoãn quyết định để tránh trách nhiệm | Chọn theo thông tin có, ghi assumption/risk và điều kiện xem xét lại |
| Groundhog Day | Bàn lại cùng lựa chọn vì mất lý do cũ | Lưu alternatives và rationale có thể tra cứu |
| Email-Driven Architecture | Quyết định chỉ nằm trong trao đổi khó tìm | Đưa quyết định về nơi tài liệu chung, có mã/liên kết |
| Out of Context | Đếm ưu/nhược mà không xét trọng số bối cảnh | Gắn trade-off với NFR và điều kiện của TMC |

AI có thể gợi ý alternatives, rà consistency và đặt câu hỏi, nhưng không cung cấp chứng cứ thực nghiệm hoặc biết thay nhóm về ngân sách, năng lực vận hành, quyết định kinh doanh chưa được cung cấp.

### 9.2. Architecture risk và risk storming

**Nguồn:** B ch.22 tr.797–829.

Risk là khả năng một kết quả không mong muốn tác động mục tiêu. Đánh giá theo **likelihood** và **impact**, ghi căn cứ và rủi ro còn lại sau mitigation. Có thể dùng thang thấp/vừa/cao và tích điểm, nhưng bảng điểm là quy ước đánh giá, không phải xác suất đã đo. Một điểm phụ thuộc nhỏ nhưng gây mất toàn bộ attendance data có thể quan trọng hơn nhiều lỗi giao diện.

Risk storming gồm **nhận diện độc lập → thống nhất đánh giá → giảm thiểu rủi ro**, dựa trên sơ đồ có phạm vi rõ. Nhiều vai trò cùng nhìn giúp phát hiện điều architect bỏ sót; không tự tuyên bố đã tổ chức phiên họp khi chưa diễn ra. Theo dõi risk theo thời gian, thay vì coi hoàn tất một bảng là hết việc.

| Rủi ro ứng viên TMC | Driver chịu tác động | Hướng giảm thiểu để đánh giá |
|---|---|---|
| QR hợp lệ bị chia sẻ | Identity/security | Xác minh yêu cầu chống chia sẻ, đánh giá QR động và kiểm tra bổ sung |
| Controller trả timeout sau khi đã mở | Data integrity, safety/operations | Phân biệt trạng thái chưa biết, request identity, đối soát; không retry mù |
| Export HR chưa hoàn tất sát deadline | Timeliness | Xuất sớm, trạng thái ack, retry và cảnh báo theo điều kiện thỏa thuận |
| Ghi attendance rồi lỗi gửi message, hoặc ngược lại | Reliability | Xác định transaction boundary và cơ chế lưu công việc bền |
| Quản trị viên xuất vượt phạm vi dữ liệu | Privacy/audit | Authorization ở backend, scope và audit phù hợp |

Các scenario mất điện/mất mạng thuộc robustness mở rộng cần đánh giá; phải giữ sự khác biệt với NFR-02 gốc chỉ nói vận hành bình thường. Availability/SLA/SLO không phải cùng khái niệm: SLA thường là cam kết hợp đồng, SLO là mục tiêu vận hành; không bịa “five nines” cho bài này.

### 9.3. Team topologies và hiệu quả làm việc

**Nguồn:** B ch.9 tr.308–310 và phần team considerations ở các style; B ch.24 tr.846–887.

| Topology | Vai trò | Liên hệ kiến trúc |
|---|---|---|
| Stream-aligned | Theo một dòng giá trị/miền nghiệp vụ | Thuận với domain partitioning và ownership trọn luồng |
| Enabling | Giúp team vượt khoảng trống năng lực | Hỗ trợ học kỹ thuật/triển khai, không sở hữu vĩnh viễn mọi việc |
| Complicated-subsystem | Chuyên môn sâu cho subsystem phức tạp | Hữu ích với thuật toán, integration/device đặc thù |
| Platform | Cung cấp nền tảng dùng chung | Giảm ma sát CI/CD, telemetry, runtime, nhưng cần interface rõ |

Conway's law nhắc cấu trúc hệ thống chịu ảnh hưởng cách tổ chức giao tiếp của đội. Không chọn microservices để có độc lập trong khi mọi thay đổi vẫn phải chờ một team trung tâm làm tất cả.

B ch.24 phân biệt architect kiểu control freak đặt quá nhiều ràng buộc, armchair tách khỏi team và effective architect cung cấp ranh giới vừa đủ. Mức tham gia phụ thuộc độ quen nhau, quy mô/kinh nghiệm team, độ phức tạp và thời gian dự án. Không lấy các bảng điểm minh họa trong sách như quy tắc nhân sự bắt buộc.

Các dấu hiệu cần để ý: **process loss** do chi phí phối hợp, **pluralistic ignorance** khi ai cũng ngại nói ý kiến khác, **diffusion of responsibility** khi không ai thật sự nhận trách nhiệm. Checklist code completion, tests, release giúp tránh bỏ sót; automation phù hợp thay cho kiểm tay lặp lại. Với M1, checklist tập trung requirements, views, ADR và consistency.

### 9.4. Negotiation và leadership

**Nguồn:** B ch.25 tr.888–922.

Đổi yêu cầu mơ hồ thành đại lượng có bối cảnh: “luôn sẵn sàng” cần thời gian dịch vụ và downtime chấp nhận; “cực nhanh” cần response boundary/tải. Đàm phán bằng tác động kinh doanh và bằng chứng, không thắng bằng cấp bậc hoặc thuật ngữ.

4 Cs trong B tr.903 là **communication, collaboration, clear, concise**, khác bốn mức của C4 diagramming. Cùng phân tích alternatives, giải thích vì sao, dẫn dắt bằng ví dụ, tôn trọng developer flow và duy trì liên hệ với team. Cân bằng pragmatic và visionary: xử lý bottleneck thực tế, giữ khả năng tiến hóa, tránh thiết kế xa nhu cầu chỉ vì dự đoán tương lai.

**TMC:** nếu ai đó đòi mọi API và thao tác vật lý hoàn tất trong 2 giây, cần làm rõ hợp đồng và phân bổ thời gian với bên controller; không lặng lẽ đổi ngưỡng hoặc bảo đảm điều ngoài quyền kiểm soát.

### 9.5. Architectural intersections

**Nguồn:** S1 tr.23–26; B ch.26 tr.923–959.

| Giao điểm | Điều cần bảo đảm nhất quán |
|---|---|
| Implementation | Code giữ boundaries, operational concerns và constraints mà thiết kế đã chọn |
| Infrastructure | Tài nguyên, network, deployment và failure domains đủ cho mục tiêu vận hành |
| Data | Data topology/schema/ownership/read-write profile phù hợp style và transaction |
| Engineering practices | CI/CD, kiểm thử và fitness functions hỗ trợ chứ không phá tính độc lập |
| Team topology | Ownership/giao tiếp của team phù hợp ranh giới công việc |
| Systems integration | Contract và trách nhiệm với hệ thống ngoài được xem xét sớm |
| Enterprise/business | Chính sách, chi phí, lịch thay đổi và bối cảnh kinh doanh ảnh hưởng lựa chọn |
| Generative AI | Dùng abstraction cho phần dễ biến động; kiểm chứng đầu ra và giữ người chịu trách nhiệm |

Kiến trúc không “độc lập hoàn toàn” với quy trình hoặc tổ chức. Process và structure là khái niệm khác nhau, nhưng engineering practices và team arrangements có thể tạo ma sát hoặc giúp kiến trúc đạt mục tiêu. Ví dụ thiết kế có deploy độc lập nhưng pipeline buộc release tất cả cùng lúc thì độc lập thực tế bị suy giảm.

### 9.6. Tái xét ba luật trong B ch.27

Shared library giảm remote calls và cho từng bên chọn phiên bản, nhưng có thể làm release/version và code coupling lan rộng. Shared service hỗ trợ nhiều nền tảng và đổi behavior tập trung, nhưng tạo runtime dependency, latency và failure coupling. Đếm số ưu điểm không quyết định được kết quả: trọng số theo bối cảnh mới quan trọng.

Queue và topic cũng vậy: point-to-point có routing/contract theo consumer và khả năng quản lý riêng, nhưng producer biết nhiều đích hơn; publish-subscribe thêm consumer dễ hơn nhưng cần cân data exposure, contract và observability của sản phẩm được chọn. Không lặp lại phát biểu tổng quát “topic không thể giám sát” như luật mọi broker — khả năng thực tế tùy công nghệ.

Khi workload, team, integration hoặc policy đổi, xem lại quyết định. Không tái sử dụng một ADR ở bối cảnh khác mà bỏ điều kiện và weighting của nó.

## 10. Áp dụng vào TMC và tự kiểm tra

### 10.1. Chuỗi lập luận cần có trong báo cáo

| Từ | Sang | Chứng cứ cần viết |
|---|---|---|
| Đề và business context | Requirements | Mã gốc, diễn giải, assumption/open question |
| Requirements | Characteristics | Driver ảnh hưởng cấu trúc, ưu tiên và scenario đo |
| Actors/workflows | Logical components | Trách nhiệm và requirement allocation; tránh Entity Trap |
| Components + characteristics | Style choice | Alternatives, trade-offs và quyết định theo cùng tiêu chí |
| Logical architecture | Physical/runtime/allocation | Mapping có giải thích, không nhảy thẳng sang cloud icons |
| Quyết định | ADR + principles | Vì sao chọn, ràng buộc, hệ quả, hướng dẫn và cách kiểm |
| Thiết kế | Đánh giá | Walkthrough, risk, traceability, dự kiến tests/fitness functions |

S1/S4 giúp xác định nội dung; S2/S3 giúp giữ ranh giới; S5 và B ch.9–20 giúp so sánh cấu trúc; S6 và B ch.21–23 giúp truyền đạt/kiểm chứng; B ch.24–27 giúp phối hợp và tránh quyết định thiếu bối cảnh.

### 10.2. Ví dụ trade-off cần tự trả lời

- Nếu gọi HR API trực tiếp trong lượt quét, hệ thống còn đáp ứng NFR-01 khi HR chậm không? Dữ liệu nào thực sự cần từ HR trong critical path?
- Nếu kiosk báo thành công trước khi dữ liệu được ghi bền, chứng minh NFR-02 bằng cách nào?
- Nếu DB commit rồi controller timeout, có thể kết luận nhân viên đã qua cổng không? Hệ thống cần hiển thị trạng thái gì?
- Nếu retry xuất HR, phía HR nhận một hay hai lần và dữ liệu được đối soát theo định danh nào?
- Nếu reports đọc trên cùng DB với kiosk, tải cuối tháng ảnh hưởng đường quét thế nào? Có cần tách read model hay chỉ index/query/scheduling phù hợp?
- Nếu chọn một service cho mỗi entity, transaction/quy trình thực tế cần bao nhiêu remote calls? Ranh giới ấy giúp hay cản việc đổi nghiệp vụ?
- Mỗi actor nhìn thấy dữ liệu nào; quyền được áp ở UI, backend hay cả hai; ai có thể đọc audit?
- Điều kiện nào sẽ khiến lựa chọn monolith/service-based/microservices cần được xem xét lại?

### 10.3. Phần nào cần cho M1, phần nào để sau?

M1 cần **đặc tả/thiết kế đủ đánh giá**: context, use cases, NFR scenarios, components, alternatives, views, ADR/principles, risks và cách kiểm. Các tactics như durable storage/idempotency phải có logic giải thích nếu dùng. M1 chưa có code để đo, do đó chỉ viết mục tiêu và kế hoạch kiểm chứng, không tạo kết quả giả.

M2 sẽ bổ sung đặc tả và đòi implementation/testing; chỉ dùng nội dung M2 khi tài liệu của mốc đó được cung cấp. Các chủ đề space-based, mesh, SOA, gen AI hay quy trình release giúp hiểu phạm vi lựa chọn, không trở thành checklist “phải dùng” cho hệ thống nhỏ.

## 11. Thuật ngữ và lưu ý khi đọc nguồn

| Thuật ngữ | Cách hiểu ngắn |
|---|---|
| Architecture characteristic / quality attribute | Đặc tính chất lượng ảnh hưởng cấu trúc và thành công |
| Constraint | Điều kiện giới hạn giải pháp; có thể do đề, môi trường hoặc quyết định thiết kế |
| Design principle | Hướng dẫn cân nhắc; không đồng nhất với quyết định cứng |
| Logical component | Khối trách nhiệm/chức năng trong mô hình logic |
| Runtime component | Phần có sự hiện diện/hành vi lúc chạy trong C&C view |
| Module | Đơn vị tổ chức/hiện thực code có trách nhiệm gắn kết |
| Connector | Cơ chế tương tác có semantics, protocol/roles |
| Deployment unit | Artifact/ứng dụng được phát hành theo một đơn vị |
| Architectural quantum | Phạm vi cấu trúc/coupling dùng để xét các đặc tính kiến trúc |
| Bounded context | Ranh giới ý nghĩa/mô hình của một miền nghiệp vụ |
| Durability | Khả năng dữ liệu đã xác nhận được lưu bền trong mô hình lỗi đã định |
| Idempotency | Lặp cùng một yêu cầu logic không tạo thêm hiệu ứng nghiệp vụ ngoài dự kiến |
| Audit log | Bằng chứng ai làm gì/lúc nào/trên gì/kết quả gì theo chính sách |
| Observability | Khả năng hiểu trạng thái/hành vi qua telemetry như logs, metrics, traces |
| Reconciliation | Đối chiếu dữ liệu hai phía để phát hiện/giải quyết chênh lệch |

### Lưu ý về độ bao phủ và cách dùng

- Chỉ mục mục 1 bao phủ toàn bộ tám bộ slide và 27 chương B; nội dung được nhóm theo khái niệm để tránh lặp, không chép lại từng trang hay giải toàn bộ bài tập nhỏ.
- Các sơ đồ/bảng trong slide đã được đối chiếu trực quan ở những phần trọng yếu, gồm SOLID, component iteration, logical/physical mapping, style scorecards và ba nhóm view. Những con số đánh giá trong nguồn được giữ như hướng dẫn học tập, không biến thành measurement của TMC.
- Khi một quyết định phụ thuộc công thức, sơ đồ hoặc cách dùng thuật ngữ cụ thể, mở đúng trang gốc. Đặc biệt lưu ý LCOM có nhiều biến thể, formula PDF có thể mất định dạng, và coupling có thể nói về code, dữ liệu hoặc runtime.
- Nếu đề, slide và sách khác phạm vi/thuật ngữ, dùng đề để quyết định nghĩa vụ; trình bày theo slide cho bài môn học; ghi sách như diễn giải/mở rộng có phiên bản. Không dùng sách để tự bổ sung requirement cho khách hàng.
- Mọi ví dụ TMC trong tài liệu này hỗ trợ agent thiết kế và lý giải. Để tạo bài làm, tiếp tục theo [skill.md](../guides/skill.md) và kiểm bằng [rules.md](../guides/rules.md).
