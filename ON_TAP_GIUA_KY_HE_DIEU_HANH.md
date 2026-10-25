# TỔNG HỢP KIẾN THỨC ÔN TẬP GIỮA KỲ MÔN HỆ ĐIỀU HÀNH (OPERATING SYSTEMS)

> **Tài liệu tổng hợp dựa trên:**
> 1. Chuỗi bài giảng Lý thuyết: Chương 1 (Tổng quan), Chương 2 (Cấu trúc HĐH), Chương 3 (Tiến trình & Tiểu trình), Chương 4-1 & Chương 4-2 (Định thời CPU).
> 2. Các bộ đề thi Giữa kỳ chính thức: Đề GK1 2020–2021, Đề GK2 2020–2021, Đề GK1 2024–2025 (Khoa Kỹ thuật Máy tính - ĐH Công nghệ Thông tin ĐHQG-HCM).

---

## MỤC LỤC
1. [MA TRẬN & CẤU TRÚC ĐỀ THI GIỮA KỲ](#1-ma-trận--cấu-trúc-đề-thi-giữa-kỳ)
2. [CHƯƠNG 1: TỔNG QUAN VỀ HỆ ĐIỀU HÀNH & KIẾN TRÚC MÁY TÍNH](#2-chương-1-tổng-quan-về-hệ-điều-hành--kiến-trúc-máy-tính)
3. [CHƯƠNG 2: CẤU TRÚC & CÁC DỊCH VỤ CỦA HỆ ĐIỀU HÀNH](#3-chương-2-cấu-trúc--các-dịch-vụ-của-hệ-điều-hành)
4. [CHƯƠNG 3: TIẾN TRÌNH & TIỂU TRÌNH (PROCESSES & THREADS)](#4-chương-3-tiến-trình--tiểu-trình-processes--threads)
5. [CHƯƠNG 4: ĐỊNH THỜI CPU (CPU SCHEDULING)](#5-chương-4-định-thời-cpu-cpu-scheduling)
6. [HƯỚNG DẪN GIẢI CÁC DẠNG BÀI TẬP TỰ LUẬN CHẮC CHẮN CÓ TRONG ĐỀ](#6-hướng-dẫn-giải-các-dạng-bài-tập-tự-luận-chắc-chắn-có-trong-đề)
   - [Dạng 1: Phân tích mã nguồn `fork()`, biến và đếm số lần vào hàng đợi Waiting](#dạng-1-phân-tích-mã-nguồn-fork-biến-và-đếm-số-lần-vào-hàng-đợi-waiting)
   - [Dạng 2: Bài tập định thời CPU (Vẽ giản đồ Gantt & Tính các chỉ số)](#dạng-2-bài-tập-định-thời-cpu-vẽ-giản-đồ-gantt--tính-các-chỉ-số)
   - [Dạng 3: Câu hỏi tự luận điền khuyết / Trả lời ngắn thuật ngữ](#dạng-3-câu-hỏi-tự-luận-điền-khuyết--trả-lời-ngắn-thuật-ngữ)
7. [BẢNG TRA CỨU CÂU HỎI TRẮC NGHIỆM & CÁC BẪY LÝ THUYẾT KINH ĐIỂN](#7-bảng-tra-cứu-câu-hỏi-trắc-nghiệm--các-bẫy-lý-thuyết-kinh-điển)

---

# 1. MA TRẬN & CẤU TRÚC ĐỀ THI GIỮA KỲ

- **Thời gian làm bài:** 60 – 65 phút. Sinh viên không được sử dụng tài liệu. Làm bài trực tiếp trên đề thi.
- **Cấu trúc điểm số:**
  1. **Phần 1: Trắc nghiệm (6.0đ – 7.5đ)** gồm 12 – 15 câu (0.5đ/câu), phủ đều 4 chương.
  2. **Phần 2: Tự luận (2.5đ – 4.0đ)** gồm 2 dạng:
     - **Câu hỏi ngắn (1.5đ):** Điền thuật ngữ tiếng Anh chính xác hoặc con số cụ thể (VD: *Stack, Data section, 0, 6, Registers*), hoặc lần vết biến trong cây tiến trình `fork()`.
     - **Bài tập định thời CPU (2.5đ):** Cho bảng 5 tiến trình (Process, Arrival Time, Burst Time). Yêu cầu vẽ 2 giản đồ Gantt (thường là **Round Robin** và **SRTF**) và tính chi tiết: Thời gian hoàn thành ($TAT$), Thời gian chờ ($WT$), Thời gian đáp ứng ($RT$) trung bình.

---

# 2. CHƯƠNG 1: TỔNG QUAN VỀ HỆ ĐIỀU HÀNH & KIẾN TRÚC MÁY TÍNH

### 1.1. Khái niệm & Mục tiêu của Hệ điều hành
- **Định nghĩa:** Hệ điều hành (HĐH - Operating System) là một chương trình đóng vai trò **trung gian** giữa phần cứng máy tính và người sử dụng. HĐH có chức năng điều khiển, phối hợp việc sử dụng phần cứng và cung cấp các dịch vụ cơ bản cho các ứng dụng.
- **Hai mục tiêu chính:**
  1. Giúp người dùng **dễ dàng sử dụng** hệ thống (Convenience).
  2. Quản lý và cấp phát tài nguyên hệ thống một cách **hiệu quả** (Efficiency).
- **Phân biệt 4 thành phần trong hệ thống máy tính:**
  - *Phần cứng (Hardware):* CPU, bộ nhớ, thiết bị I/O (cung cấp tài nguyên tính toán cơ bản).
  - *Hệ điều hành (Operating System):* Điều khiển và phối hợp việc sử dụng tài nguyên phần cứng giữa các chương trình ứng dụng.
  - *Chương trình ứng dụng (Application Programs):* Sử dụng hệ thống tài nguyên để giải quyết một bài toán tính toán cụ thể của người dùng (compilers, database, web browsers, games). *(Bẫy trắc nghiệm: HĐH không trực tiếp giải quyết bài toán của người dùng, mà là chương trình ứng dụng!)*.
  - *Người dùng (Users):* Con người, máy móc, hoặc máy tính khác.

### 1.2. Hoạt động bên trong máy tính
- **Nhân (Kernel):** Là chương trình duy nhất **luôn luôn chạy** tại tất cả các thời điểm máy tính hoạt động. Đi kèm với nhân gồm: các *chương trình hệ thống* (system programs) và *chương trình ứng dụng* (application programs).
- **Chương trình khởi động (Bootstrap Program):** Được lưu trong ROM hoặc EEPROM (phần sụn - firmware), được nạp khi bật nguồn hoặc khởi động lại. Nhiệm vụ: Khởi tạo tất cả các khía cạnh phần cứng của hệ thống, định vị và nạp nhân HĐH vào RAM, sau đó bắt đầu thực thi nhân.
- **Tương tác CPU và Thiết bị I/O:**
  - Mỗi loại thiết bị có một **Bộ điều khiển thiết bị (Device Controller)** tương ứng. Mỗi controller có một bộ nhớ đệm cục bộ (local buffer).
  - CPU và các Device Controller có thể **thực thi đồng thời** (concurrently). CPU chuyển dữ liệu giữa bộ nhớ chính và các local buffers.
  - Sau khi hoàn thành thao tác, Device Controller thông báo cho CPU biết bằng cách gửi một **tín hiệu ngắt (Interrupt)**.

### 1.3. Cơ chế Ngắt (Interrupts)
- **Phân loại ngắt:**
  1. *Ngắt phần cứng (Hardware Interrupt):* Do thiết bị ngoại vi phát sinh qua đường truyền bus hệ thống đến CPU.
  2. *Ngắt phần mềm (Software Interrupt / Trap / Exception):* Do lỗi phần mềm phát sinh (chia cho 0, truy xuất bộ nhớ không hợp lệ) hoặc do tiến trình yêu cầu dịch vụ của HĐH thông qua **lời gọi hệ thống (System Call)**.
- **Quy trình xử lý ngắt:**
  1. CPU dừng lệnh hiện tại, lưu địa chỉ của lệnh kế tiếp (Program Counter - PC) và trạng thái các thanh ghi vào ngăn xếp (stack).
  2. CPU tra cứu địa chỉ của hàm phục vụ ngắt (**Interrupt Service Routine - ISR**) thông qua **Véc-tơ ngắt (Interrupt Vector)**.
  3. CPU nhảy đến thực thi ISR tương ứng.
  4. Sau khi xử lý xong, CPU khôi phục lại ngữ cảnh đã lưu và tiếp tục công việc bị gián đoạn.

### 1.4. Phân cấp hệ thống lưu trữ (Storage Hierarchy)
Hệ thống lưu trữ được tổ chức phân cấp dựa trên **3 đặc điểm cốt lõi** *(Câu hỏi trắc nghiệm GK1 2024–2025)*:
1. **Tốc độ truy xuất (Speed).**
2. **Chi phí trên đơn vị dung lượng (Cost).**
3. **Tính bay hơi / Khả năng lưu trữ khi mất điện (Volatility).**

```
Nhanh nhất, Đắt nhất, Dung lượng nhỏ, Bay hơi (Volatile)
  ▲  [ Registers (Thanh ghi trong CPU) ]
  │  [ Cache (L1, L2, L3) ]
  │  [ Main Memory (Bộ nhớ chính / RAM) ]
──┼──────────────────────────────────────────────────────── (Ranh giới Volatile / Non-Volatile)
  │  [ Electronic Disk / SSD (Ổ cứng thể rắn) ]
  │  [ Magnetic Disk / HDD (Đĩa từ) ]
  ▼  [ Optical Disk (Đĩa quang), Magnetic Tapes (Băng từ) ]
Chậm nhất, Rẻ nhất, Dung lượng lớn, Không bay hơi (Non-volatile)
```
- **Bộ nhớ chính (RAM):** Thiết bị lưu trữ dung lượng lớn duy nhất mà CPU có thể truy xuất trực tiếp. Truy xuất ngẫu nhiên (Random Access), mất dữ liệu khi mất điện (Volatile).
- **Bộ nhớ đệm (Caching):** Sao chép thông tin tạm thời từ bộ nhớ chậm sang bộ nhớ nhanh hơn để tăng tốc độ truy xuất.

### 1.5. Kiến trúc hệ thống máy tính
- **Hệ thống đơn bộ xử lý (Single-Processor Systems):** Chỉ có một CPU đa dụng (general-purpose CPU) với một lõi thực thi các lệnh của tiến trình.
- **Hệ thống đa bộ xử lý (Multiprocessor Systems / Parallel Systems / Tightly-coupled Systems):**
  - Đặc điểm: Hai hay nhiều bộ xử lý cùng chia sẻ bus hệ thống, đồng hồ, và **chia sẻ bộ nhớ chung** *(Đề GK2 2020–2021)*.
  - **3 ưu điểm lớn:**
    1. *Tăng thông lượng (Increased Throughput):* Hoàn thành nhiều công việc hơn trong thời gian ngắn hơn.
    2. *Tính kinh tế theo quy mô (Economy of Scale):* Tiết kiệm chi phí do dùng chung thiết bị ngoại vi, nguồn, vỏ máy.
    3. *Tăng độ tin cậy (Increased Reliability):* Hỏng một CPU không làm tê liệt toàn hệ thống (suy giảm hiệu năng mềm mại - Graceful degradation / Khả năng chịu lỗi - Fault tolerance).
  - **Phân loại đa xử lý:**
    - **Đa xử lý bất đối xứng (Asymmetric Multiprocessing - AMP):** Quan hệ Chủ - Tớ (Master - Slave). Master processor định thời và phân công việc cho các slave processors; chỉ Master truy xuất các cấu trúc dữ liệu của HĐH.
    - **Đa xử lý đối xứng (Symmetric Multiprocessing - SMP):** Mỗi bộ xử lý chạy một bản sao giống nhau của HĐH, bình đẳng ngang hàng, cùng chia sẻ bộ nhớ.
- **Hệ thống gom cụm (Clustered Systems):**
  - Gồm hai hay nhiều hệ thống độc lập (nodes) kết nối với nhau qua mạng nội bộ LAN hoặc mạng lưu trữ SAN (Storage-Area Network). Cung cấp tính sẵn sàng cao (High-availability).
- **Hệ thống phân tán (Distributed Systems):**
  - Các bộ xử lý nằm ở các trạm vật lý khác nhau, mỗi processor có bộ nhớ riêng, kết nối qua mạng viễn thông.
  - Phân loại theo mô hình: **Client-Server** và **Peer-to-Peer** *(Đề GK2 2020–2021)*.

### 1.6. Các chế độ hoạt động trong HĐH
- **Đơn chương (Uniprogramming):** Chỉ duy nhất một công việc/chương trình được nạp vào bộ nhớ tại một thời điểm. Thực thi tuần tự. Khi công việc đợi I/O, CPU hoàn toàn rảnh rỗi.
- **Đa chương (Multiprogramming):** Nhiều công việc được nạp đồng thời vào bộ nhớ chính. Khi tiến trình hiện tại phải chờ (chờ I/O, sự kiện), HĐH lập tức chuyển CPU sang thực thi tiến trình khác. Giúp tăng tối đa hiệu suất sử dụng CPU. *(Bẫy đề thi: Trong đa chương, các công việc KHÔNG thi hành tuần tự!)*.
- **Đa nhiệm / Chia sẻ thời gian (Multitasking / Time-sharing):** Mở rộng của đa chương, trong đó CPU chuyển đổi giữa các công việc rất thường xuyên (lát cắt thời gian ms) đến mức người dùng cảm thấy có thể tương tác trực tiếp với từng chương trình đang chạy.
- **Cơ chế Hai chế độ (Dual-Mode Operation):**
  - Bảo vệ HĐH và các tiến trình khỏi các tiến trình có lỗi hoặc độc hại.
  - Sử dụng **Mode bit** được hỗ trợ bởi phần cứng:
    - `0`: Chế độ hạt nhân (**Kernel mode** / Monitor mode / Supervisor mode / System mode).
    - `1`: Chế độ người dùng (**User mode**).
  - **Lệnh đặc quyền (Privileged Instructions):** Các lệnh nguy hiểm (truy xuất I/O trực tiếp, quản lý ngắt, đổi mode bit, quản lý bảng trang) **chỉ được phép thực thi ở Kernel mode**. Nếu cố tình gọi ở User mode, phần cứng sẽ tạo ra một Trap ngắt chương trình.
- **Đồng hồ đếm thời gian (Timer):** Ngăn chặn một tiến trình chạy vòng lặp vô tận độc chiếm CPU. Sau mỗi khoảng thời gian định trước, Timer phát sinh ngắt đưa quyền điều khiển về cho HĐH.

---

# 3. CHƯƠNG 2: CẤU TRÚC & CÁC DỊCH VỤ CỦA HỆ ĐIỀU HÀNH

### 3.1. Các thành phần chính của Hệ điều hành và Nhiệm vụ cụ thể
*(Trọng tâm câu hỏi lý thuyết ghép nối chức năng vào thành phần)*

| Thành phần HĐH | Chức năng & Nhiệm vụ cốt lõi | Các bẫy thường gặp |
| :--- | :--- | :--- |
| **Quản lý tiến trình** *(Process Management)* | - Tạo và xóa cả tiến trình người dùng và tiến trình hệ thống.<br>- Tạm dừng (suspend) và tiếp tục (resume) tiến trình.<br>- Cung cấp cơ chế đồng bộ hóa (synchronization) và giao tiếp liên tiến trình (IPC). | Không quản lý vùng nhớ đĩa. |
| **Quản lý bộ nhớ chính** *(Main Memory Management)* | - Theo dõi, quản lý các vùng nhớ nào đang trống, vùng nào đã cấp phát và do ai sử dụng.<br>- Quyết định nạp chương trình nào khi có không gian nhớ trống.<br>- Cấp phát và thu hồi các vùng nhớ khi cần thiết. | **KHÔNG** cung cấp giao diện cho thiết bị I/O! |
| **Quản lý file / tập tin** *(File Management)* | - Tạo và xóa file, thư mục.<br>- Cung cấp các thao tác xử lý file/thư mục (đọc, ghi, đổi tên, copy).<br>- **Ánh xạ file/thư mục vào thiết bị lưu trữ thứ cấp tương ứng** *(Câu hỏi Đề GK1 2024–2025)*.<br>- Sao lưu (backup) và phục hồi dữ liệu. | Dữ liệu logic do File Management quản lý. |
| **Quản lý hệ thống I/O** *(I/O System Management)* | - Che giấu sự khác biệt của các thiết bị phần cứng I/O trước người dùng.<br>- Cung cấp bộ nhớ đệm (Buffering), bộ nhớ lưu tạm (Caching), cơ chế Spooling.<br>- **Cung cấp giao diện chung đến các trình điều khiển thiết bị (Device Drivers)**. | Quản lý việc đọc ghi vật lý của Driver. |
| **Quản lý lưu trữ thứ cấp** *(Secondary Storage Management)* | - **Cấp phát không gian lưu trữ (Storage allocation)** *(Đề GK1 2020–2021)*.<br>- Quản lý không gian đĩa còn trống (Free-space management).<br>- Định thời truy xuất đĩa (Disk scheduling). | Quản lý khối vật lý trên HDD/SSD. |
| **Hệ thống bảo vệ** *(Protection & Security)* | - Kiểm soát việc truy cập của các tiến trình hoặc người dùng đối với các tài nguyên hệ thống.<br>- Đảm bảo các tiến trình độc lập không xâm phạm, ảnh hưởng lẫn nhau.<br>- Xác thực người dùng (Authentication). | **Lưu vết để tính phí/thống kê là thuộc Accounting, KHÔNG phải mục đích chính của Protection/Security!** *(Đề GK1 2024–2025)* |
| **Hệ thống thông dịch lệnh** *(Command Interpreter / Shell)* | - Là giao diện trực tiếp giữa người dùng và HĐH (CLI - Command Line Interface).<br>- Đọc lệnh từ người dùng, biên dịch và gọi System Call tương ứng để HĐH thực thi. | Shell chạy ở User space, không phải Kernel. |

### 3.2. Lời gọi hệ thống (System Calls)
- **Định nghĩa:** Lời gọi hệ thống là giao diện lập trình (programming interface) cung cấp phương tiện để **tiến trình giao tiếp với hệ điều hành**, yêu cầu các dịch vụ của nhân HĐH *(Đề GK1 2020–2021)*.
- **3 Giao diện lập trình ứng dụng (API) thông dụng:**
  1. **Win32 API** cho hệ điều hành Windows.
  2. **POSIX API** cho các hệ thống dựa trên POSIX (tất cả các phiên bản UNIX, Linux, macOS).
  3. **Java API** cho máy ảo Java (JVM).
- **3 Phương pháp truyền tham số cho Lời gọi hệ thống** *(Chắc chắn xuất hiện trong phần tự luận ngắn / trắc nghiệm)*:
  1. **Qua các thanh ghi (Registers):** Phương pháp đơn giản nhất, nhanh nhất. Hạn chế: số lượng thanh ghi của CPU có hạn.
  2. **Qua một khối nhớ / vùng nhớ (Block / Table in Memory):** Các tham số được ghi vào một khối nhớ trong bộ nhớ, sau đó **địa chỉ của khối nhớ** được chuyển đến HĐH thông qua một thanh ghi *(Linux, Solaris sử dụng cách này khi số tham số vượt quá số thanh ghi)*.
  3. **Qua Ngăn xếp (Stack):** Chương trình đẩy (push) các tham số vào stack của tiến trình, và HĐH sẽ lấy (pop) các tham số ra khỏi stack.
  *(Bẫy đề thi: "Heap" KHÔNG phải là phương pháp truyền tham số cho System Call!)*.

### 3.3. Các kiểu Cấu trúc Hệ điều hành (OS Structures)
- **Cấu trúc nguyên khối (Monolithic - UNIX cổ điển, MS-DOS):**
  - Toàn bộ chức năng HĐH (quản lý tiến trình, bộ nhớ, file, driver) được biên dịch chung thành một khối duy nhất chạy trong không gian nhân (Kernel space).
  - *Ưu điểm:* Hiệu năng cao, tốc độ nhanh vì gọi hàm trực tiếp.
  - *Nhược điểm:* Khó mở rộng, khó gỡ lỗi; lỗi ở một thành phần có thể làm sập toàn bộ HĐH.
- **Cấu trúc phân lớp (Layered Approach):**
  - HĐH chia thành nhiều lớp (từ Lớp $0$ đến Lớp $N$). Lớp dưới cùng (Lớp $0$) là phần cứng, lớp trên cùng (Lớp $N$) là giao diện người dùng.
  - Nguyên tắc: **Một lớp chỉ có thể gọi các dịch vụ của các lớp bên dưới nó** và cung cấp dịch vụ cho lớp ngay trên nó.
  - *Ưu điểm:* Tính module cao, dễ xây dựng và gỡ lỗi.
  - *Nhược điểm:* Khó phân định ranh giới giữa các lớp một cách hợp lý, giảm hiệu năng do phải truyền qua nhiều lớp trung gian.
- **Cấu trúc vi nhân (Microkernel - CMU Mach, QNX):**
  - **Chuyển phần lớn các chức năng của HĐH từ kernel space sang user space** *(Đề GK1 2020–2021)*.
  - Nhân chỉ giữ lại các cơ chế tối thiểu cần thiết: quản lý tiến trình cơ bản, quản lý bộ nhớ tối thiểu, và cơ chế giao tiếp liên tiến trình (IPC).
  - Các module dịch vụ người dùng giao tiếp với nhau bằng cơ chế **truyền thông điệp (Message Passing)** thông qua microkernel.
  - *Ưu điểm:* Dễ mở rộng, an toàn và tin cậy hơn (dịch vụ nào chết thì chỉ crash service đó ở user space, nhân không sập).
  - *Nhược điểm:* Hiệu năng giảm do tốn chi phí chuyển ngữ cảnh (context switch) và chi phí truyền thông điệp liên tục.
- **Cấu trúc Module (Loadable Kernel Modules - LKM):**
  - Lõi nhân gọn nhẹ, các thành phần tính năng bổ sung (như driver, file system) được viết thành các module và **nạp động vào nhân khi cần thiết** (dynamic linking) lúc khởi động hoặc lúc đang chạy mà không cần biên dịch lại kernel (Linux, Solaris).
- **Cấu trúc Lai (Hybrid Systems):**
  - **Kết hợp nhiều cách tiếp cận** cấu trúc khác nhau để giải quyết hài hòa các nhu cầu về hiệu suất, bảo mật, và tính tiện dụng *(Đề GK1 2024–2025)*.
  - Hầu hết các HĐH hiện đại đều là hệ thống lai:
    - *macOS và iOS (Darwin):* Lớp trên là cấu trúc phân lớp; phần nhân cốt lõi kết hợp giữa Microkernel Mach (quản lý bộ nhớ, IPC) và Monolithic BSD (file system, networking, POSIX API).
    - *Windows:* Nhân kết hợp giữa Monolithic và các hệ thống con phân tầng (subsystems).
    - *Android:* Dựa trên nhân Linux, kết hợp môi trường thực thi máy ảo ART (Android Runtime) và các thư viện C/C++.

---

# 4. CHƯƠNG 3: TIẾN TRÌNH & TIỂU TRÌNH (PROCESSES & THREADS)

### 4.1. Tiến trình (Process) & Bố cục bộ nhớ (Memory Layout)
- **Định nghĩa:** Tiến trình là **một chương trình đang thực thi**.
  - Chương trình là thực thể **bị động** (passive entity) – tập tin lưu trên đĩa.
  - Tiến trình là thực thể **chủ động** (active entity) – chương trình đã được nạp vào bộ nhớ và đang được CPU thực thi kèm theo bộ đếm chương trình (Program Counter) và tập thanh ghi.
- **Bố cục bộ nhớ của một chương trình C khi nạp vào RAM** *(Xuất hiện liên tục trong tự luận điền khuyết và trắc nghiệm)*:
  1. **Text Section:** Chứa mã máy thực thi của chương trình (program code instructions).
  2. **Data Section:** Chứa các **biến toàn cục (Global variables)** và biến tĩnh (Static variables) *(Đề GK1 2020, Đề GK1 2024)*.
  3. **Heap Section:** Vùng nhớ cấp phát động tại thời điểm chạy (`malloc()`, `calloc()`, `new`), phát triển từ dưới lên trên (về phía địa chỉ cao hơn).
  4. **Stack Section:** Vùng nhớ chứa dữ liệu tạm thời, phát triển từ trên xuống dưới (về phía địa chỉ thấp hơn):
     - **Biến cục bộ (Local variables)** *(Đề GK1 2020, Đề GK2 2020)*.
     - **Địa chỉ trả về của hàm (Return address)**.
     - **Tham số truyền cho hàm (Function parameters / arguments)**.

### 4.2. Vòng đời và Các trạng thái của Tiến trình (Process States)
Mô hình chuẩn gồm **5 trạng thái**:
1. **New:** Tiến trình vừa mới được tạo ra (đang chuẩn bị nạp vào bộ nhớ).
2. **Ready:** Tiến trình **đã có đầy đủ tài nguyên cần thiết, chỉ còn chờ được cấp CPU** để chạy *(Đề GK2 2020–2021)*.
3. **Running:** Các chỉ lệnh của tiến trình **đang được CPU thực thi**.
4. **Waiting (hay Blocked):** Tiến trình phải tạm dừng để **chờ một sự kiện xảy ra** (như chờ I/O hoàn tất, chờ nhận tín hiệu từ tiến trình khác) *(Đề GK1 2024–2025)*.
5. **Terminated:** Tiến trình đã hoàn thành việc thực thi và kết thúc.

```
       [New] ──(admit)──► [Ready] ◄──────(interrupt)────── [Running] ──(exit)──► [Terminated]
                             ▲                               │
                             │                               │ (I/O or event wait)
                             └─── (I/O completion) ─── [Waiting]
```
- **Các quy tắc chuyển trạng thái quan trọng (Bẫy đề thi):**
  - Từ `Running` **CHỈ CÓ THỂ** chuyển sang 3 trạng thái: `Ready` (hết thời gian quantum/bị ngắt), `Waiting` (gọi I/O/chờ sự kiện), hoặc `Terminated` (gọi exit/lỗi).
  - Từ `Running` **KHÔNG THỂ chuyển trực tiếp sang `New`** *(Đề GK1 2020–2021)*.
  - Từ `Waiting` **KHÔNG THỂ nhảy thẳng lên `Running`**, mà bắt buộc phải chuyển sang `Ready` để chờ bộ định thời CPU phân phối lại.

### 4.3. Khối điều khiển tiến trình (PCB - Process Control Block)
Mỗi tiến trình trong hệ thống được đại diện bởi một khối PCB (còn gọi là Task Control Block), bao gồm:
- **Process State:** Trạng thái hiện tại (new, ready, running, waiting, terminated).
- **Program Counter (PC):** Địa chỉ của lệnh tiếp theo sẽ thực thi.
- **CPU Registers:** Nội dung các thanh ghi tích lũy, con trỏ ngăn xếp, thanh ghi chỉ số,...
- **CPU-Scheduling Information:** Độ ưu tiên, con trỏ đến các hàng đợi định thời.
- **Memory-Management Information:** Bảng phân trang (page table), bảng phân đoạn, thanh ghi cơ sở và giới hạn.
- **Accounting Information:** Thời gian CPU đã sử dụng, giới hạn thời gian, số hiệu tài khoản.
- **I/O Status Information:** Danh sách các thiết bị I/O được cấp phát, danh sách file đang mở.

### 4.4. Định thời Tiến trình & Các Bộ định thời (Schedulers)
- **Các hàng đợi định thời:**
  - *Job Queue:* Chứa tất cả các tiến trình trong hệ thống.
  - *Ready Queue:* Chứa các tiến trình đang ở trong bộ nhớ chính, sẵn sàng và đang chờ được cấp CPU. **Bộ định thời CPU chọn tiến trình từ Ready queue** *(Đề GK1 2024–2025)*.
  - *Device Queues (I/O Queues):* Hàng đợi chứa các tiến trình đang chờ một thiết bị I/O cụ thể.
- **Phân loại 3 Bộ định thời:**
  1. **Bộ định thời dài (Long-term Scheduler / Job Scheduler):**
     - Chức năng: **Xác định chương trình nào được chấp nhận nạp vào hệ thống (vào bộ nhớ chính) để thực thi** *(Đề GK1 2020–2021)*.
     - Kiểm soát **mức độ đa chương (Degree of Multiprogramming)**. Tần suất thực thi thấp (vài giây đến vài phút).
     - Phải cân bằng hợp lý giữa tiến trình thiên về I/O (*I/O-bound process* - nhiều burst ngắn) và tiến trình thiên về CPU (*CPU-bound process* - ít burst nhưng burst rất dài).
  2. **Bộ định thời ngắn (Short-term Scheduler / CPU Scheduler):**
     - Chức năng: Lựa chọn một tiến trình trong số các tiến trình đang ở `Ready queue` để cấp phát CPU.
     - Tần suất thực thi cực cao (vài mili-giây). Bắt buộc phải chạy cực nhanh để không gây lãng phí CPU.
  3. **Bộ định thời trung gian (Medium-term Scheduler):**
     - Chức năng: Giảm mức độ đa chương khi bộ nhớ quá tải bằng cơ chế **Hoán đổi (Swapping)**: đưa tiến trình từ RAM ra đĩa (*Swap-out*) và nạp lại vào RAM khi có chỗ trống (*Swap-in*).

### 4.5. Chuyển ngữ cảnh (Context Switch)
- **Định nghĩa:** Chuyển ngữ cảnh là **quá trình CPU chuyển từ thực thi tiến trình này sang thực thi tiến trình khác** *(Đề GK1 2024–2025)*.
- **Quy trình:**
  1. HĐH lưu lại trạng thái (ngữ cảnh) của tiến trình cũ vào khối PCB của nó.
  2. Nạp trạng thái đã lưu của tiến trình mới từ khối PCB của tiến trình mới đó.
- **Đặc tính:** Thời gian chuyển ngữ cảnh là **chi phí thuần túy (pure overhead)** vì hệ thống không thực hiện được công việc tính toán hữu ích nào trong suốt thời gian này. Tốc độ phụ thuộc rất nhiều vào sự hỗ trợ của phần cứng.

### 4.6. Tạo và Kết thúc tiến trình (Process Creation & Termination)
- **Cơ chế tạo tiến trình:**
  - Tiến trình tạo gọi là **tiến trình cha (Parent)**, tiến trình được tạo gọi là **tiến trình con (Child)**, tạo nên một cây phân cấp tiến trình (định danh bằng `PID`).
  - *Tài nguyên:* Tiến trình con có thể nhận tài nguyên trực tiếp từ HĐH, hoặc **chia sẻ một phần / toàn bộ tài nguyên từ tiến trình cha** *(Đề GK1 2020, Đề GK2 2020)*.
  - *Trình tự thực thi:* Tiến trình cha và tiến trình con có thể **thực thi đồng thời (concurrently)**, hoặc tiến trình cha **chờ (wait)** cho đến khi tiến trình con kết thúc. *(Phát biểu: "Cha và con luôn thực thi đồng thời" là SAI!)*.
  - *Trong UNIX/Linux:*
    - Lời gọi hàm `fork()`: Tạo một tiến trình con mới là một **bản sao giống hệt (clone)** của cha. Giá trị trả về của `fork()`:
      - Trả về **`0`** cho tiến trình con.
      - Trả về **`PID của con` ($> 0$)** cho tiến trình cha.
      - Trả về **`-1`** nếu tạo tiến trình thất bại.
    - Lời gọi hàm `exec()`: Dùng sau `fork()` để **nạp đè một tập tin thực thi mới** vào không gian địa chỉ của tiến trình.
    - Lời gọi hàm `wait()`: Cho phép tiến trình cha tạm dừng đợi một tiến trình con kết thúc.
- **Kết thúc tiến trình:**
  - Tiến trình gọi hàm `exit()` để tự kết thúc và trả về mã trạng thái.
  - Tiến trình cha có thể hủy tiến trình con bằng cách gọi lệnh `abort(pid)`.
  - **Zombie process:** Tiến trình đã kết thúc (gọi exit) nhưng tiến trình cha chưa gọi `wait()` để thu hồi mã trạng thái. Bảng tiến trình vẫn phải giữ lại entry của nó.
  - **Orphan process:** Tiến trình cha đã kết thúc trước khi gọi `wait()`, bỏ rơi tiến trình con. Trong Linux, tiến trình mồ côi sẽ được nhận nuôi bởi tiến trình gốc `systemd` (hoặc `init`, PID = 1).

### 4.7. Giao tiếp liên tiến trình (IPC - Inter-Process Communication)
Các tiến trình cộng tác cần IPC để chia sẻ dữ liệu và đồng bộ hoạt động qua 2 mô hình cơ bản *(Đề GK2 2020–2021)*:
1. **Bộ nhớ chia sẻ (Shared Memory):**
   - HĐH thiết lập một vùng nhớ chung có thể được truy xuất bởi nhiều tiến trình.
   - **Tốc độ rất nhanh** (tương đương tốc độ truy xuất RAM), sau khi thiết lập vùng nhớ thì HĐH không còn can thiệp vào quá trình trao đổi.
   - Trách nhiệm đồng bộ hóa, chống tranh chấp (race condition) hoàn toàn thuộc về lập trình viên ứng dụng.
2. **Truyền thông điệp (Message Passing):**
   - Các tiến trình trao đổi thông tin bằng cách gửi thông điệp thông qua nhân HĐH (`send(message)`, `receive(message)`).
   - Rất thích hợp cho các hệ thống phân tán qua mạng.
   - Tốc độ chậm hơn vì phải chuyển quyền vào kernel (system call overhead).

### 4.8. Bài toán Vùng tranh chấp (Critical Section Problem)
- Vùng tranh chấp là đoạn mã trong tiến trình có thao tác truy xuất và thay đổi dữ liệu dùng chung.
- **3 Yêu cầu bắt buộc cho lời giải của bài toán Critical Section** *(Đề GK2 2020–2021)*:
  1. **Loại trừ lẫn nhau (Mutual Exclusion):** Nếu một tiến trình $P$ đang thực thi trong vùng tranh chấp của nó thì không có tiến trình $Q$ nào khác được phép thực thi trong vùng tranh chấp của $Q$.
  2. **Tiến triển (Progress):** Nếu không có tiến trình nào đang trong vùng tranh chấp và có một số tiến trình muốn vào, thì chỉ những tiến trình không bị chặn bên ngoài vùng tranh chấp mới được tham gia quyết định ai sẽ vào tiếp theo, và quyết định này không được hoãn vô hạn.
  3. **Chờ đợi có giới hạn (Bounded Waiting):** Phải tồn tại một giới hạn về số lần các tiến trình khác được vào vùng tranh chấp sau khi một tiến trình đã đưa ra yêu cầu vào, để tránh tình trạng **đói tài nguyên (starvation)**.
  *(Bẫy đề thi: "Tất cả tiến trình phải được đối xử như nhau" KHÔNG phải là yêu cầu của vùng tranh chấp!)*.

### 4.9. Tiểu trình (Threads)
- **Khái niệm:** Tiểu trình là đơn vị cơ bản sử dụng CPU, đại diện cho một luồng điều khiển bên trong một tiến trình.
- **Thành phần của một Thread:**
  - *Thành phần riêng của mỗi Thread:* **Thread ID, Bộ đếm chương trình (PC), Tập thanh ghi (Registers), Vùng ngăn xếp riêng (Stack)**.
  - *Thành phần dùng chung giữa các Thread trong cùng một Process:* **Mã nguồn (Code/Text), Vùng dữ liệu (Data section: biến toàn cục), Tài nguyên HĐH (files đang mở, signals)**.
- **Ưu điểm của đa tiểu trình:** Đáp ứng nhanh (Responsiveness), Chia sẻ tài nguyên dễ dàng, Tiết kiệm chi phí tạo và chuyển ngữ cảnh (so với Process), Tận dụng tốt kiến trúc đa xử lý/đa lõi (Scalability).
- **3 Mô hình đa tiểu trình (Multithreading Models):**
  1. **Mô hình Nhiều – Một (Many-to-One):**
     - Nhiều tiểu trình người dùng (user threads) được ánh xạ đến **một tiểu trình hạt nhân** (kernel thread) *(Đề GK1 2024–2025)*.
     - *Nhược điểm:* Nếu một thread thực hiện lời gọi hệ thống gây khóa (blocking system call), toàn bộ tiến trình sẽ bị khóa. Không thể chạy song song trên kiến trúc đa lõi.
  2. **Mô hình Một – Một (One-to-One):**
     - Mỗi tiểu trình người dùng ánh xạ tới **một tiểu trình hạt nhân**.
     - Cung cấp tính đồng thời cao, thread này block không làm thread khác bị dừng.
     - *Nhược điểm:* Việc tạo thread người dùng đòi hỏi phải tạo kèm kernel thread, tốn chi phí tài nguyên (Linux, Windows sử dụng mô hình này với số lượng bị giới hạn).
  3. **Mô hình Nhiều – Nhiều (Many-to-Many):**
     - Cho phép nhiều user thread được ánh xạ vào một số lượng tương đương hoặc ít hơn các kernel thread.
     - Khắc phục nhược điểm của 2 mô hình trên, linh hoạt nhưng thuật toán cài đặt phức tạp nhất.

---

# 5. CHƯƠNG 4: ĐỊNH THỜI CPU (CPU SCHEDULING)

### 5.1. Các Khái niệm Cơ bản & Hai Yếu tố của Giải thuật Định thời
- **Chu kỳ thực thi CPU-I/O Burst:** Quá trình thực thi của một tiến trình luôn bao gồm một chuỗi luân phiên giữa chu kỳ bận xử lý CPU (*CPU burst*) và chu kỳ chờ đợi nhập xuất (*I/O burst*).
- **Trình điều phối (Dispatcher):** Là module trao quyền điều khiển CPU cho tiến trình được chọn bởi bộ định thời ngắn. Công việc: chuyển ngữ cảnh, chuyển sang User mode, nhảy đến địa chỉ thích hợp để tiếp tục chạy chương trình.
  - *Dispatch Latency:* Thời gian cần thiết để Dispatcher dừng một tiến trình và khởi động tiến trình tiếp theo.
- **Hai yếu tố của một giải thuật định thời** *(Đề GK2 2020–2021)*:
  1. **Chế độ quyết định (Decision Mode):**
     - **Không trưng dụng (Non-preemptive):** Một khi CPU đã được cấp phát cho một tiến trình, tiến trình đó sẽ **giữ CPU cho đến khi kết thúc hoặc tự nguyện chuyển sang trạng thái Waiting** (chờ I/O). HĐH không tự ý giật lại CPU.
     - **Trưng dụng / Chiếm quyền (Preemptive):** Tiến trình đang chạy bình thường **có thể bị ngắt nửa chừng và bị chuyển về trạng thái Ready** khi có tiến trình ưu tiên cao hơn xuất hiện hoặc khi hết lát cắt thời gian (Quantum).
  2. **Hàm lựa chọn (Selection Function):** Tiêu chí để HĐH chọn tiến trình kế tiếp trong Ready queue dựa trên:
     - $w$: Thời gian đã chờ đợi trong Ready queue (waiting time).
     - $e$: Thời gian đã thực thi trên CPU (execution time so far).
     - $s$: Tổng thời gian yêu cầu CPU cần thiết (total service / burst time).

### 5.2. Các Tiêu chuẩn Định thời CPU (Scheduling Criteria) & Công thức
*(Bắt buộc nắm vững để giải bài tập tự luận và trắc nghiệm)*

1. **Hiệu năng sử dụng CPU (CPU Utilization):** Tỷ lệ phần trăm thời gian CPU bận làm việc (mong muốn từ $40\%$ đến $90\%$).
2. **Thông lượng (Throughput):** Số lượng tiến trình hoàn thành trên một đơn vị thời gian (càng cao càng tốt).
3. **Thời gian hoàn thành / lưu lại (Turnaround Time - $TAT$):** Khoảng thời gian từ lúc tiến trình xuất hiện trong hệ thống ($Arrival\ Time$) đến khi nó kết thúc hoàn toàn ($Finish\ Time$):
   $$\mathbf{TAT = Finish\ Time - Arrival\ Time}$$
4. **Thời gian chờ (Waiting Time - $WT$):** Tổng thời gian mà tiến trình phải nằm chờ trong `Ready queue`. Nếu tiến trình không có thao tác I/O trong quá trình chạy:
   $$\mathbf{WT = TAT - Burst\ Time}$$
   *(Hoặc tính bằng tổng các khoảng thời gian tiến trình nằm trong hàng đợi sẵn sàng trên trục Gantt)*.
5. **Thời gian đáp ứng (Response Time - $RT$):** Khoảng thời gian từ lúc tiến trình vào Ready queue ($Arrival\ Time$) cho đến khi nó **được cấp phát CPU lần đầu tiên** ($First\ CPU\ Time$):
   $$\mathbf{RT = First\ CPU\ Time - Arrival\ Time}$$

### 5.3. Chi tiết các Giải thuật Định thời Đơn Bộ xử lý

#### 1. First-Come, First-Served (FCFS)
- **Hàm lựa chọn:** $\min[Arrival\ Time]$ (Tiến trình yêu cầu trước được cấp trước).
- **Chế độ quyết định:** Không trưng dụng (Non-preemptive). Cài đặt bằng hàng đợi FIFO.
- **Nhược điểm lớn nhất:** Hiệu ứng đoàn tàu (**Convoy Effect**) – các tiến trình ngắn phải đứng sau một tiến trình có CPU burst rất dài, làm cho thời gian chờ trung bình tăng vọt.

#### 2. Shortest-Job-First (SJF - Không trưng dụng)
- **Hàm lựa chọn:** $\min[s]$ (Chọn tiến trình có thời gian CPU burst ngắn nhất trong số các tiến trình đang ở Ready queue).
- **Chế độ quyết định:** Không trưng dụng (Non-preemptive).
- **Đặc tính:** **SJF là giải thuật tối ưu nhất trong việc giảm thiểu thời gian chờ trung bình (Average Waiting Time)**.
- **Hạn chế:** Không thể biết trước chính xác thời gian CPU burst tiếp theo (phải dự đoán bằng công thức trung bình mũ: $\tau_{n+1} = \alpha t_n + (1 - \alpha)\tau_n$).
- **Nguy cơ:** Gây ra hiện tượng **đói tài nguyên (Starvation)** đối với các tiến trình dài nếu các tiến trình ngắn liên tục xuất hiện.

#### 3. Shortest-Remaining-Time-First (SRTF - SJF Trưng dụng)
- **Hàm lựa chọn:** $\min[s_{còn\ lại}]$ (Chọn tiến trình có thời gian thực thi còn lại ngắn nhất).
- **Chế độ quyết định:** Trưng dụng (Preemptive).
- **Thời điểm kích hoạt:** Khi có một tiến trình mới xuất hiện tại thời điểm $t$, nếu $Burst_{mới} < Remaining\ Time_{đang\ chạy}$, HĐH lập tức **thu hồi CPU** của tiến trình đang chạy và cấp cho tiến trình mới!
- **Đặc tính:** Cho thời gian chờ và thời gian hoàn thành trung bình tốt hơn SJF không trưng dụng, nhưng tốn chi phí chuyển ngữ cảnh (Context switch). Vẫn có nguy cơ Starvation đối với tiến trình dài.

#### 4. Định thời theo Độ ưu tiên (Priority Scheduling)
- Mỗi tiến trình được gán một mức độ ưu tiên (thường biểu diễn bằng một con số nguyên).
- CPU được cấp cho tiến trình có độ ưu tiên cao nhất. *(Lưu ý: SJF thực chất là một dạng đặc biệt của Priority scheduling với độ ưu tiên là $1 / \text{CPU burst predicted}$)*.
- Có thể hoạt động ở cả 2 chế độ: Trưng dụng hoặc Không trưng dụng.
- **Vấn đề:** Hiện tượng **đói tài nguyên / trì hoãn vô hạn định (Starvation / Indefinite Blocking)** đối với tiến trình độ ưu tiên thấp.
- **Giải pháp:** Cơ chế **Lão hóa (Aging)** – tăng dần độ ưu tiên của các tiến trình khi chúng phải chờ đợi quá lâu trong hệ thống.

#### 5. Round Robin (RR - Luân phiên)
- Được thiết kế chuyên biệt cho các hệ thống chia sẻ thời gian (Time-sharing).
- **Hàng đợi Ready:** Được tổ chức theo dạng danh sách vòng FIFO.
- **Lát cắt thời gian (Time Quantum / Time Slice - $q$):** Mỗi tiến trình được cấp một lượng thời gian CPU nhất định (thường từ $10 - 100$ ms).
  - Nếu tiến trình chạy hết $q$ mà chưa xong: Bị ngắt (timer interrupt), HĐH đưa nó về **cuối hàng đợi Ready** để nhường CPU cho tiến trình tiếp theo.
- **Đặc tính quan trọng:**
  - Nếu $q$ **rất lớn**: Round Robin trở thành **FCFS** *(Đề GK2 2020–2021)*.
  - Nếu $q$ **rất nhỏ**: Gây ra quá nhiều lần chuyển ngữ cảnh, làm tăng chi phí quản lý (OS overhead), làm giảm hiệu năng hệ thống.
  - *Quy tắc ngón tay cái:* Khoảng $80\%$ CPU-burst của các tiến trình nên ngắn hơn quantum $q$.
- **Công thức thời gian chờ tối đa cho phản hồi đầu tiên** *(Đề GK1 2020–2021)*:
  Nếu có $n$ tiến trình trong Ready queue và time quantum là $q$, thì không có tiến trình nào phải chờ đợi quá:
  $$\mathbf{T_{wait\_max} = (n - 1) \times q}$$

#### 6. Highest Response Ratio Next (HRRN)
- **Chế độ quyết định:** Không trưng dụng (Non-preemptive).
- **Hàm lựa chọn:** Chọn tiến trình có tỷ số phản hồi (**Response Ratio - $R$**) lớn nhất:
  $$\mathbf{R = \frac{w + s}{s} = 1 + \frac{w}{s}}$$
  - Trong đó: $w$ là thời gian đã chờ (waiting time), $s$ là thời gian yêu cầu CPU (service time / burst time).
- **Ưu điểm vượt trội:**
  - Khi mới vào ($w=0$), các tiến trình ngắn ($s$ nhỏ) có $R$ lớn nên được ưu tiên chạy trước (giống SJF).
  - Đối với tiến trình dài ($s$ lớn), khi phải chờ lâu trong hàng đợi thì $w$ tăng dần, kéo theo $R$ tăng lên. Đến một lúc nào đó nó sẽ có $R$ lớn nhất và được chạy $\rightarrow$ **Giải quyết triệt để tình trạng Starvation!**

#### 7. Hàng đợi nhiều mức (Multilevel Queue - MQ)
- Chia `Ready queue` thành nhiều hàng đợi riêng biệt dựa trên loại tiến trình (ví dụ: Hàng đợi ưu tiên cao cho tiến trình hệ thống, hàng đợi tương tác Foreground dùng RR, hàng đợi chạy ngầm Background dùng FCFS).
- **Tiến trình được gán CỐ ĐỊNH vào một hàng đợi duy nhất, KHÔNG THỂ di chuyển giữa các hàng đợi** *(Đề GK1 2020, Đề GK2 2020)*.
- Định thời giữa các hàng đợi: Thường dùng chế độ ưu tiên cố định (Fixed Priority) hoặc chia sẻ thời gian giữa các hàng đợi (Time Slice, VD: $80\%$ CPU cho Foreground, $20\%$ cho Background).

#### 8. Hàng đợi phản hồi nhiều mức (Multilevel Feedback Queue - MFQ)
- **Cho phép tiến trình DI CHUYỂN giữa các hàng đợi khác nhau** *(Đề GK1 2020, Đề GK1 2024)*.
- **Nguyên lý hoạt động:**
  - Phân loại tiến trình theo đặc tính CPU-burst.
  - Một tiến trình mới đến sẽ vào hàng đợi cao nhất ($Q_0$, có quantum $q$ nhỏ nhất).
  - Nếu tiến trình dùng hết cả lát cắt thời gian mà vẫn chưa xong (CPU-bound), nó sẽ bị hạ xuống hàng đợi thấp hơn ($Q_1$ với quantum lớn hơn).
  - Tiến trình hướng I/O hoặc tương tác giải phóng CPU trước khi hết quantum sẽ ở lại hàng đợi ưu tiên cao.
  - **Áp dụng cơ chế Aging:** Tiến trình chờ quá lâu ở hàng đợi thấp sẽ được chuyển lên hàng đợi cao hơn để tránh Starvation.

### 5.4. Định thời Đa Bộ xử lý (Multiprocessor Scheduling)
- **Đa xử lý bất đối xứng (AMP):** Một CPU làm Master xử lý lập lịch và I/O; các CPU còn lại chỉ chạy mã người dùng.
- **Đa xử lý đối xứng (SMP):** Mỗi CPU tự lập lịch cho chính mình.
  - Hai cách tổ chức hàng đợi:
    1. *Một hàng đợi chung (Common Ready Queue):* Dễ xảy ra tranh chấp vùng nhớ, cần khóa đồng bộ.
    2. *Mỗi CPU có hàng đợi riêng (Private Ready Queue):* Phổ biến nhất trên HĐH hiện đại.
- **Cân bằng tải (Load Balancing):** Đảm bảo chia đều công việc cho các bộ xử lý, gồm 2 cơ chế:
  - *Push migration:* Một tác vụ định kỳ kiểm tra tải của các CPU; nếu CPU nào quá tải thì đẩy bớt tiến trình sang CPU rảnh.
  - *Pull migration:* CPU rảnh rỗi tự động kéo tiến trình từ hàng đợi của CPU bận rộn về cho mình.
- **Ái lực bộ xử lý (Processor Affinity):**
  - Khi một tiến trình chạy trên một CPU, dữ liệu của nó được lưu trong bộ nhớ đệm (Cache) của CPU đó. Nếu di chuyển tiến trình sang CPU khác, toàn bộ cache cũ mất hiệu lực và phải nạp lại từ RAM (tốn chi phí lớn). Do đó, HĐH luôn có xu hướng giữ tiến trình chạy trên cùng một CPU.
  - Gồm *Soft Affinity* (HĐH cố gắng giữ nhưng không đảm bảo) và *Hard Affinity* (tiến trình ràng buộc danh sách CPU được phép chạy qua hàm `sched_setaffinity()`).
  - **Mâu thuẫn then chốt:** **Cơ chế Cân bằng tải (Load Balancing) sẽ làm triệt tiêu / ảnh hưởng tiêu cực đến tính chất Ái lực bộ xử lý (Processor Affinity)** *(Đề GK1 2024–2025)*!

### 5.5. Định thời Thời gian thực (Real-time Scheduling)
- **Soft Real-time:** Đảm bảo các tác vụ quan trọng được ưu tiên cao nhất, nhưng nếu trễ hạn (deadline) thì chỉ làm giảm chất lượng dịch vụ, không gây hỏng hệ thống.
- **Hard Real-time:** Bắt buộc các tác vụ phải hoàn thành chính xác trước hạn định nghiêm ngặt; nếu trễ hạn sẽ dẫn đến thảm họa.
- **Hai giải thuật định thời thời gian thực định kỳ (Periodic Tasks với chu kỳ $p$, thời gian xử lý $t$, deadline $d$):**
  1. **Rate Monotonic (RM):** Gán độ ưu tiên tĩnh. **Chu kỳ càng ngắn thì độ ưu tiên càng cao** (Ưu tiên $\propto 1/p$).
  2. **Earliest Deadline First (EDF):** Gán độ ưu tiên động. **Tác vụ nào có hạn chót (Deadline) gần nhất thì được ưu tiên cao nhất**.

### 5.6. Định thời trên Một số Hệ điều hành Thực tế
- **Linux:** Từ bản 2.6.23 sử dụng bộ định thời **CFS (Completely Fair Scheduler)**.
  - Hoạt động dựa trên khái niệm **thời gian chạy ảo (`virtual run time` - `vruntime`)**. Mỗi tác vụ được theo dõi `vruntime` trong cấu trúc Cây Đỏ - Đen (Red-Black Tree). Bộ định thời luôn chọn tác vụ có **`vruntime` nhỏ nhất** để chạy tiếp theo.
  - Độ ưu tiên được điều chỉnh qua giá trị **`nice`** từ **`-20` đến `+19`** (Số `nice` càng nhỏ thì độ ưu tiên càng cao, `vruntime` tích lũy chậm hơn nên được cấp nhiều CPU hơn).
  - **Target Latency:** Khoảng thời gian mục tiêu mà trong đó mọi tiến trình đang sẵn sàng đều phải được chạy ít nhất một lần.
- **Windows:** Định thời dựa trên độ ưu tiên với chế độ chiếm quyền (Preemptive, 32 mức độ ưu tiên từ $0$ đến $31$):
  - Mức $0$: Quản lý trang nhớ (Zero Page Thread).
  - Mức $1 - 15$: Các mức ưu tiên biến đổi thông thường (**Variable priorities**), có cơ chế tự động tăng độ ưu tiên tạm thời (**Priority Boosting**) khi vừa hoàn thành I/O hoặc đang là cửa sổ người dùng tương tác.
  - Mức $16 - 31$: Các mức ưu tiên thời gian thực (**Real-time priorities**).

---

# 6. HƯỚNG DẪN GIẢI CÁC DẠNG BÀI TẬP TỰ LUẬN CHẮC CHẮN CÓ TRONG ĐỀ

---

## DẠNG 1: PHÂN TÍCH MÃ NGUỒN `fork()`, BIẾN VÀ ĐẾM SỐ LẦN VÀO HÀNG ĐỢI WAITING

### Phương pháp phân tích chuẩn:
1. **Mỗi lệnh `fork()`:** Nhân đôi số tiến trình đang có tại thời điểm thực thi.
2. **Quy luật giá trị trả về:**
   - Trong tiến trình cha: biến nhận giá trị `k > 0` (chính là PID của con).
   - Trong tiến trình con: biến nhận giá trị `k == 0`.
3. **Tính độc lập của biến (Biến toàn cục & biến cục bộ):**
   - Sau `fork()`, tiến trình con sở hữu một **bản sao dữ liệu riêng biệt** (vùng nhớ độc lập). Mọi phép thay đổi giá trị biến ($x = x + i$,...) ở tiến trình này **hoàn toàn KHÔNG ảnh hưởng** đến giá trị của biến ở tiến trình khác!
4. **Quy tắc đếm số lần vào hàng đợi Waiting:**
   - Mỗi lệnh I/O (như `printf`, `scanf`, đọc ghi file) sẽ yêu cầu dịch vụ của HĐH và đưa tiến trình gọi nó vào hàng đợi `Waiting` $1$ lần cho đến khi thao tác I/O hoàn tất.

---

### Bài toán 1.1 (Trích Đề GK1 2020–2021 & GK2 2020–2021):
```c
#include <stdio.h>
#include <unistd.h>
int x = 15;
int main() {
    int i;
    fork();
    printf("hi\n");
    for (i = 0; i < 2; i++){
        int k = fork();
        if (k > 0)
            printf("hello\n");
    }
    return 0;
}
```
**Yêu cầu 1: Bao nhiêu từ `hello` được in ra?**
- **Bước 1:** Bắt đầu có $1$ tiến trình ($P_0$).
- **Bước 2:** Gọi `fork()` ngoài vòng lặp $\rightarrow$ Tạo ra $P_1$. Lúc này có **2 tiến trình** ($P_0, P_1$).
- **Bước 3:** Cả 2 tiến trình in chữ `hi` (In được 2 chữ `hi`).
- **Bước 4:** Vòng lặp `for (i = 0; i < 2; i++)`:
  - **Tại $i = 0$:**
    - Cả 2 tiến trình ($P_0, P_1$) đều gọi `fork()` $\rightarrow$ Mỗi tiến trình sinh ra 1 con mới ($P_0 \to P_2$, $P_1 \to P_3$).
    - Tổng số tiến trình lúc này là $4$.
    - Trong đó: 2 tiến trình cha có $k > 0$ ($P_0, P_1$); 2 tiến trình con mới có $k = 0$ ($P_2, P_3$).
    - Điều kiện `if (k > 0)`: Chỉ có 2 tiến trình cha in `hello` $\rightarrow$ **In 2 từ `hello`**.
  - **Tại $i = 1$:**
    - Cả 4 tiến trình ($P_0, P_1, P_2, P_3$) đều chạy tiếp và gọi `fork()` $\rightarrow$ Mỗi tiến trình sinh thêm 1 con mới.
    - Tổng số tiến trình sau bước này là $4 \times 2 = 8$ tiến trình.
    - Trong 4 cặp cha - con vừa sinh ra: có đúng 4 tiến trình cha có $k > 0$.
    - Điều kiện `if (k > 0)`: 4 tiến trình cha in `hello` $\rightarrow$ **In 4 từ `hello`**.
- **Tổng số từ `hello` in ra:** $2 + 4 =$ **$6$ từ `hello`**.

**Yêu cầu 2: Tất cả các tiến trình nằm trong hàng đợi `waiting` tổng cộng bao nhiêu lần?**
- Mỗi lần gọi `printf(...)`, tiến trình đó phải vào `waiting` để chờ I/O hoàn thành:
  - Khi gọi `printf("hi\n")`: Có 2 tiến trình gọi $\rightarrow$ **2 lần**.
  - Khi gọi `printf("hello\n")` tại $i = 0$: Có 2 tiến trình gọi $\rightarrow$ **2 lần**.
  - Khi gọi `printf("hello\n")` tại $i = 1$: Có 4 tiến trình gọi $\rightarrow$ **4 lần**.
- **Tổng số lần vào hàng đợi Waiting:** $2 + 2 + 4 =$ **$8$ lần**.

---

### Bài toán 1.2 (Trích Tự luận Câu 1c Đề GK1 2024–2025):
```c
#include <stdio.h>
#include <unistd.h>
int x = 24;
int main() {
    int i;
    printf("hello\n");
    int f = fork();
    for (i = 0; i <= 2; i++){
        int k = fork();
        printf("%d\n", f + i);
        x = x + i;
    }
    printf("hi\n");
    if (f == 0) {
        printf("%d\n", x);
        fork();
        x = x + 2;
    }
    return 0;
}
```
**Câu hỏi:** *Hỏi có bao nhiêu tiến trình mà giá trị cuối cùng của biến `x` (ở mỗi tiến trình) là 25?*

**Lời giải chi tiết từng bước:**
1. **Ban đầu:** 1 tiến trình ban đầu có biến toàn cục $x = 24$. In `hello`.
2. **Lệnh `int f = fork();`:**
   - Tạo ra 2 tiến trình:
     - Tiến trình Cha: có $f > 0$, giá trị $x = 24$.
     - Tiến trình Con: có $f = 0$, giá trị $x = 24$.
3. **Vòng lặp `for (i = 0; i <= 2; i++)`:** Gồm 3 lần lặp ($i = 0, 1, 2$):
   - **Lần lặp $i = 0$:**
     - 2 tiến trình gọi `fork()` $\rightarrow$ Thành 4 tiến trình (2 tiến trình có $f > 0$, 2 tiến trình có $f = 0$).
     - Cả 4 tiến trình đều thực hiện: $x = x + 0 \rightarrow x = 24$.
   - **Lần lặp $i = 1$:**
     - Cả 4 tiến trình gọi `fork()` $\rightarrow$ Thành 8 tiến trình (4 tiến trình có $f > 0$, 4 tiến trình có $f = 0$).
     - Cả 8 tiến trình đều thực hiện: $x = x + 1 \rightarrow x = 24 + 1 = 25$.
   - **Lần lặp $i = 2$:**
     - Cả 8 tiến trình gọi `fork()` $\rightarrow$ Thành 16 tiến trình (8 tiến trình có $f > 0$, 8 tiến trình có $f = 0$).
     - Cả 16 tiến trình đều thực hiện: $x = x + 2 \rightarrow x = 25 + 2 = 27$.
4. **Sau khi thoát khỏi vòng lặp `for`:**
   - Tất cả 16 tiến trình hiện có **đều đang giữ giá trị $x = 27$**!
5. **Xét khối lệnh rẽ nhánh `if (f == 0)`:**
   - 8 tiến trình có $f > 0$ (nhóm cha gốc): Điều kiện `f == 0` là SAI. Chúng bỏ qua khối lệnh `if`, đi thẳng tới `return 0;` $\rightarrow$ **Giá trị cuối cùng của $x$ ở 8 tiến trình này là $27$**.
   - 8 tiến trình có $f == 0$ (nhóm con gốc): Điều kiện `f == 0` là ĐÚNG. Chúng vào trong `if`:
     - Mỗi tiến trình gọi `fork()` $\rightarrow$ Nhân đôi thành $8 \times 2 = 16$ tiến trình.
     - Cả 16 tiến trình này đều thực hiện: $x = x + 2 \rightarrow x = 27 + 2 = 29$.
     - Kết thúc chương trình $\rightarrow$ **Giá trị cuối cùng của $x$ ở 16 tiến trình này là $29$**.
6. **Kết luận:**
   - Toàn bộ chương trình kết thúc tạo ra tổng cộng $24$ tiến trình, trong đó:
     - $8$ tiến trình có $x = 27$.
     - $16$ tiến trình có $x = 29$.
   - **Số lượng tiến trình có giá trị cuối cùng $x = 25$ là:** **$0$ tiến trình**.

---

## DẠNG 2: BÀI TẬP ĐỊNH THỜI CPU (VẼ GIẢN ĐỒ GANTT & TÍNH CÁC CHỈ SỐ)

### Quy tắc vẽ Giản đồ Gantt chuẩn và Thứ tự Hàng đợi Ready:
1. **Đối với SRTF (SJF trưng dụng):**
   - Chỉ xét trưng dụng khi có **tiến trình mới xuất hiện** tại thời điểm $t$.
   - So sánh thời gian thực thi còn lại ($Remaining\ Time$) của tiến trình đang chạy với $Burst\ Time$ của tiến trình mới đến. Nếu tiến trình mới có burst nhỏ hơn strictly $\rightarrow$ Trưng dụng CPU ngay. Nếu bằng nhau $\rightarrow$ Tiến trình đang chạy tiếp tục giữ CPU.
2. **Đối với Round Robin (RR):**
   - **Quy tắc xếp hàng đợi (Queue management):** Khi một tiến trình hết lát cắt thời gian $q$ tại thời điểm $t$, nếu tại đúng thời điểm $t$ đó có một hoặc nhiều tiến trình mới xuất hiện:
     $$\mathbf{Ưu\ tiên\ đưa\ các\ tiến\ trình\ MỚI\ ĐẾN\ vào\ hàng\ đợi\ TRƯỚC,\ sau\ đó\ mới\ đưa\ tiến\ trình\ vừa\ bị\ hết\ quantum\ vào\ CUỐI\ hàng\ đợi!}$$

---

### Bài toán 2.1: Giải chi tiết Bài Tự Luận Đề GK1 2024–2025
**Đề bài:** Cho 5 tiến trình với thông số như sau:

| Process | Arrival Time ($AT$) | Burst Time ($BT$) |
| :---: | :---: | :---: |
| **P1** | 8 | 5 |
| **P2** | 3 | 4 |
| **P3** | 0 | 10 |
| **P4** | 6 | 12 |
| **P5** | 11 | 11 |

Yêu cầu: Vẽ giản đồ Gantt, tính Thời gian hoàn thành ($TAT$), Thời gian đợi ($WT$), Thời gian đáp ứng ($RT$) trung bình cho:
a) **SRTF**
b) **Round Robin với $q = 7$**

---

#### a) Giải thuật SRTF:
- **Diễn biến thực thi theo trục thời gian:**
  - $t = 0$: Chỉ có $P_3$ đến với $BT = 10$. $P_3$ chạy.
  - $t = 3$: $P_2$ đến với $BT = 4$. Lúc này $P_3$ đã chạy được 3 đơn vị $\rightarrow$ $P_3$ còn lại $10 - 3 = 7$. Vì $BT(P_2) = 4 < 7$, $P_2$ **trưng dụng CPU**! $P_3$ về Ready queue.
  - $t = 6$: $P_4$ đến với $BT = 12$. $P_2$ còn lại $4 - (6-3) = 1$. So sánh $1 < 12$, $P_2$ tiếp tục chạy.
  - $t = 7$: $P_2$ chạy xong ($Finish = 7$). Ready queue gồm: $P_3$ (còn 7), $P_4$ (còn 12). Chọn $P_3$ có burst còn lại ngắn nhất (7). $P_3$ chạy từ $7$.
  - $t = 8$: $P_1$ đến với $BT = 5$. Lúc này $P_3$ vừa chạy được 1 đơn vị ($7 \to 8$) $\rightarrow$ $P_3$ còn lại $7 - 1 = 6$. Vì $BT(P_1) = 5 < 6$, $P_1$ **trưng dụng CPU**! $P_3$ về Ready queue.
  - $t = 11$: $P_5$ đến với $BT = 11$. $P_1$ đã chạy được 3 đơn vị ($8 \to 11$) $\rightarrow$ $P_1$ còn lại 2. $P_1$ tiếp tục chạy.
  - $t = 13$: $P_1$ hoàn thành ($Finish = 13$). Ready queue gồm: $P_3$ (còn 6), $P_5$ (còn 11), $P_4$ (còn 12). Chọn $P_3$ (ngắn nhất, 6). $P_3$ chạy từ $13 \to 19$.
  - $t = 19$: $P_3$ hoàn thành ($Finish = 19$). Ready queue gồm: $P_5$ (11), $P_4$ (12). Chọn $P_5$ (11). $P_5$ chạy từ $19 \to 30$.
  - $t = 30$: $P_5$ hoàn thành ($Finish = 30$). $P_4$ chạy từ $30 \to 42$.
  - $t = 42$: $P_4$ hoàn thành.

**Giản đồ Gantt (SRTF):**
```
|  P3  |  P2  | P3 |   P1   |   P3   |    P5    |     P4     |
0      3      7    8        13       19         30           42
```

**Bảng tính chi tiết các chỉ số SRTF:**

| Process | $AT$ | $BT$ | First CPU | Finish Time | $TAT = Finish - AT$ | $WT = TAT - BT$ | $RT = First - AT$ |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **P1** | 8 | 5 | 8 | 13 | $13 - 8 = \mathbf{5}$ | $5 - 5 = \mathbf{0}$ | $8 - 8 = \mathbf{0}$ |
| **P2** | 3 | 4 | 3 | 7 | $7 - 3 = \mathbf{4}$ | $4 - 4 = \mathbf{0}$ | $3 - 3 = \mathbf{0}$ |
| **P3** | 0 | 10 | 0 | 19 | $19 - 0 = \mathbf{19}$ | $19 - 10 = \mathbf{9}$ | $0 - 0 = \mathbf{0}$ |
| **P4** | 6 | 12 | 30 | 42 | $42 - 6 = \mathbf{36}$ | $36 - 12 = \mathbf{24}$ | $30 - 6 = \mathbf{24}$ |
| **P5** | 11 | 11 | 19 | 30 | $30 - 11 = \mathbf{19}$ | $19 - 11 = \mathbf{8}$ | $19 - 11 = \mathbf{8}$ |
| **Trung bình** | | | | | $\mathbf{16.60}$ | $\mathbf{8.20}$ | $\mathbf{6.40}$ |

- Thời gian hoàn thành trung bình ($ATAT$): $(5 + 4 + 19 + 36 + 19) / 5 = \mathbf{16.60}$
- Thời gian đợi trung bình ($AWT$): $(0 + 0 + 9 + 24 + 8) / 5 = \mathbf{8.20}$
- Thời gian đáp ứng trung bình ($ART$): $(0 + 0 + 0 + 24 + 8) / 5 = \mathbf{6.40}$

---

#### b) Giải thuật Round Robin ($q = 7$):
- **Diễn biến hàng đợi theo thời gian:**
  - $t = 0$: $P_3$ vào hàng đợi: `Queue: [P3(10)]`. $P_3$ chạy $7$ đơn vị.
    - Trong khi $P_3$ chạy: $P_2$ đến tại $t=3$, $P_4$ đến tại $t=6$.
  - $t = 7$: $P_3$ hết quantum $7$ (còn lại $10 - 7 = 3$). $P_2, P_4$ đã có sẵn trong queue. Đưa $P_3$ vào cuối `Queue: [P2(4), P4(12), P3(3)]`.
  - $t = 7$: Lấy $P_2$ chạy. Vì $BT(P_2) = 4 < 7$, $P_2$ chạy $4$ đơn vị từ $7 \to 11$.
    - Trong khoảng này: $P_1$ đến tại $t=8$, $P_5$ đến tại $t=11$.
  - $t = 11$: $P_2$ hoàn tất! Thêm $P_1, P_5$ vào cuối `Queue: [P4(12), P3(3), P1(5), P5(11)]`.
  - $t = 11$: Lấy $P_4$ chạy $7$ đơn vị từ $11 \to 18$ (còn $12 - 7 = 5$).
  - $t = 18$: Đưa $P_4$ về cuối `Queue: [P3(3), P1(5), P5(11), P4(5)]`.
  - $t = 18$: Lấy $P_3$ chạy $3$ đơn vị từ $18 \to 21$. $P_3$ hoàn tất! `Queue: [P1(5), P5(11), P4(5)]`.
  - $t = 21$: Lấy $P_1$ chạy $5$ đơn vị từ $21 \to 26$. $P_1$ hoàn tất! `Queue: [P5(11), P4(5)]`.
  - $t = 26$: Lấy $P_5$ chạy $7$ đơn vị từ $26 \to 33$ (còn $11 - 7 = 4$). Đưa $P_5$ về cuối `Queue: [P4(5), P5(4)]`.
  - $t = 33$: Lấy $P_4$ chạy $5$ đơn vị từ $33 \to 38$. $P_4$ hoàn tất! `Queue: [P5(4)]`.
  - $t = 38$: Lấy $P_5$ chạy $4$ đơn vị từ $38 \to 42$. $P_5$ hoàn tất! Kết thúc.

**Giản đồ Gantt (Round Robin $q = 7$):**
```
|   P3   |  P2  |   P4   |  P3  |  P1  |   P5   |  P4  |  P5  |
0        7      11       18     21     26       33     38     42
```

**Bảng tính chi tiết các chỉ số Round Robin ($q = 7$):**

| Process | $AT$ | $BT$ | First CPU | Finish Time | $TAT = Finish - AT$ | $WT = TAT - BT$ | $RT = First - AT$ |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **P1** | 8 | 5 | 21 | 26 | $26 - 8 = \mathbf{18}$ | $18 - 5 = \mathbf{13}$ | $21 - 8 = \mathbf{13}$ |
| **P2** | 3 | 4 | 7 | 11 | $11 - 3 = \mathbf{8}$ | $8 - 4 = \mathbf{4}$ | $7 - 3 = \mathbf{4}$ |
| **P3** | 0 | 10 | 0 | 21 | $21 - 0 = \mathbf{21}$ | $21 - 10 = \mathbf{11}$ | $0 - 0 = \mathbf{0}$ |
| **P4** | 6 | 12 | 11 | 38 | $38 - 6 = \mathbf{32}$ | $32 - 12 = \mathbf{20}$ | $11 - 6 = \mathbf{5}$ |
| **P5** | 11 | 11 | 26 | 42 | $42 - 11 = \mathbf{31}$ | $31 - 11 = \mathbf{20}$ | $26 - 11 = \mathbf{15}$ |
| **Trung bình** | | | | | $\mathbf{22.00}$ | $\mathbf{13.60}$ | $\mathbf{7.40}$ |

- Thời gian hoàn thành trung bình ($ATAT$): $(18 + 8 + 21 + 32 + 31) / 5 = \mathbf{22.00}$
- Thời gian đợi trung bình ($AWT$): $(13 + 4 + 11 + 20 + 20) / 5 = \mathbf{13.60}$
- Thời gian đáp ứng trung bình ($ART$): $(13 + 4 + 0 + 5 + 15) / 5 = \mathbf{7.40}$

---

### Bài toán 2.2: So sánh hiệu năng hai giải thuật (Dạng Đề GK1 2020–2021)
**Đề bài:** Cho 5 tiến trình P1(AT=0, BT=11), P2(AT=6, BT=4), P3(AT=2, BT=8), P4(AT=5, BT=16), P5(AT=11, BT=6). So sánh xem giải thuật nào cho thời gian đợi trung bình và thời gian đáp ứng trung bình tốt hơn giữa:
a) **Round Robin ($q = 7$)**
b) **SRTF**

**Kết quả tính toán chuẩn xác:**
- **Với SRTF:**
  - Gantt: `P1[0-2] -> P3[2-10] -> P2[10-14] -> P5[14-20] -> P1[20-29] -> P4[29-45]`
  - $AWT = (18 + 4 + 0 + 24 + 3) / 5 = \mathbf{9.80}$
  - $ART = (0 + 4 + 0 + 24 + 3) / 5 = \mathbf{6.20}$
  - $ATAT = (29 + 8 + 8 + 40 + 9) / 5 = \mathbf{18.80}$
- **Với Round Robin ($q = 7$):**
  - Gantt: `P1[0-7] -> P3[7-14] -> P4[14-21] -> P2[21-25] -> P1[25-29] -> P5[29-35] -> P3[35-36] -> P4[36-43] -> P4[43-45]`
  - $AWT = (18 + 15 + 26 + 24 + 18) / 5 = \mathbf{20.20}$
  - $ART = (0 + 15 + 5 + 9 + 18) / 5 = \mathbf{9.40}$
  - $ATAT = (29 + 19 + 34 + 40 + 24) / 5 = \mathbf{29.20}$
- **Kết luận:** **Giải thuật SRTF cho thời gian đợi trung bình tốt hơn (9.80 < 20.20) và thời gian đáp ứng trung bình tốt hơn (6.20 < 9.40) so với Round Robin.**

---

## DẠNG 3: CÂU HỎI TỰ LUẬN ĐIỀN KHUYẾT / TRẢ LỜI NGẮN THUẬT NGỮ

Dưới đây là bộ các câu hỏi tự luận ngắn bắt buộc phải trả lời bằng **1 từ tiếng Anh hoặc con số** (đã xuất hiện trong Đề thi GK1 2024–2025 và tương tự):

1. **Ba phương pháp truyền tham số khi sử dụng lời gọi hệ thống bao gồm: sử dụng thanh ghi (registers), khối vùng nhớ (block/table in memory) và phương pháp nào?**
   - **Trả lời:** `Stack` (hoặc `ngăn xếp`).
2. **Khi một chương trình được nạp vào bộ nhớ, các biến toàn cục (global variables) của nó được chứa ở phân vùng nào?**
   - **Trả lời:** `Data section` (hoặc `data`).
3. **Các biến cục bộ (local variables), địa chỉ trả về của hàm được chứa ở phân vùng nào?**
   - **Trả lời:** `Stack section` (hoặc `stack`).
4. **Bộ nhớ cấp phát động qua `malloc()` được chứa ở phân vùng nào?**
   - **Trả lời:** `Heap section` (hoặc `heap`).
5. **Khối cấu trúc dữ liệu quan trọng nhất được HĐH dùng để lưu trữ toàn bộ thông tin của một tiến trình là gì?**
   - **Trả lời:** `PCB` (hoặc `Process Control Block`).
6. **Mô hình IPC nào cho phép các tiến trình trao đổi dữ liệu ở tốc độ cao nhất mà không cần sự can thiệp của nhân sau khi khởi tạo?**
   - **Trả lời:** `Shared memory`.
7. **Cơ chế tăng dần độ ưu tiên của một tiến trình khi nó đã chờ đợi quá lâu trong hàng đợi để chống tình trạng starvation được gọi là gì?**
   - **Trả lời:** `Aging`.
8. **Đặc tính mà dữ liệu của một tiến trình vẫn còn lưu trong bộ nhớ đệm (cache) của CPU, khiến hệ thống muốn giữ tiến trình chạy trên CPU đó được gọi là gì?**
   - **Trả lời:** `Processor affinity`.
9. **Khoảng thời gian mà Dispatcher cần để dừng một tiến trình và nạp một tiến trình mới vào chạy được gọi là gì?**
   - **Trả lời:** `Dispatch latency`.

---

# 7. BẢNG TRA CỨU CÂU HỎI TRẮC NGHIỆM & CÁC BẪY LÝ THUYẾT KINH ĐIỂN

*(Tổng hợp từ 100% các câu hỏi trắc nghiệm trong 3 đề thi đã phân tích)*

| Nội dung câu hỏi | Đáp án đúng | Giải thích chi tiết & Bẫy cần tránh |
| :--- | :--- | :--- |
| **Đặc điểm của Cấu trúc vi nhân (Microkernel)?** | Một số chức năng HĐH được chuyển từ **kernel space sang user space**. | Bẫy: Các module giao tiếp qua Message Passing (thông điệp), KHÔNG phải qua thanh ghi trực tiếp. |
| **Phát biểu SAI về Hệ điều hành?** | "Hệ điều hành sử dụng tài nguyên để giải quyết một bài toán nào đó của người dùng." | **Sai** vì đó là chức năng của **Chương trình ứng dụng** (Application Program), HĐH chỉ quản lý tài nguyên và làm trung gian. |
| **Phân loại Hệ thống song song / Đa xử lý?** | **Đa xử lý đối xứng (SMP) và Đa xử lý bất đối xứng (AMP).** | Phân tán là Client-Server & P2P; Đơn/Đa chương là chế độ nạp job; Real-time là Hard & Soft. |
| **Phân loại Hệ thống phân tán?** | **Client-Server và Peer-to-Peer.** | Các nút độc lập kết nối qua mạng viễn thông. |
| **Mô hình IPC?** | **Shared memory và Message passing.** | PCB/TCB là cấu trúc điều khiển; Lời gọi hệ thống là interface. |
| **Đặc điểm của Hệ thống song song?** | **Hai hay nhiều bộ xử lý cùng chia sẻ một bộ nhớ chung.** | Các CPU cùng chia sẻ RAM, bus, clock (Tightly-coupled). |
| **Tiến trình ở trạng thái Waiting khi nào?** | **Tiến trình đợi I/O hoàn tất, hoặc đợi tín hiệu/sự kiện.** | Khi gọi `printf`, đọc đĩa, hoặc đợi tiến trình con. |
| **Tiến trình ở trạng thái Ready khi nào?** | **Tiến trình đã có đủ tài nguyên, chỉ còn cần CPU.** | Khác với New (chưa nạp đủ) và Waiting (thiếu I/O/tài nguyên khác). |
| **Tiến trình ở trạng thái Running KHÔNG THỂ chuyển sang?** | **Trạng thái `New`.** | Chỉ có thể chuyển sang `Ready` (hết quantum), `Waiting` (gọi I/O), hoặc `Terminated` (kết thúc). |
| **3 Tiêu chí phân cấp hệ thống lưu trữ?** | **(1) Tốc độ truy xuất, (2) Chi phí, (4) Tính bay hơi (khả năng lưu trữ khi mất điện).** | Khả năng thực thi tập lệnh đa dụng không phải tiêu chuẩn phân cấp lưu trữ. |
| **Ánh xạ file/thư mục vào thiết bị thứ cấp tương ứng là của?** | **Quản lý file (File Management).** | Quản lý việc ánh xạ cấu trúc logic file vào các khối vật lý. |
| **Cung cấp giao diện chung cho các trình điều khiển thiết bị là của?** | **Quản lý hệ thống I/O (I/O System Management).** | Thường bị nhầm sang Quản lý bộ nhớ chính hoặc Quản lý thiết bị thứ cấp. |
| **Cấp phát không gian lưu trữ (Storage allocation) là của?** | **Quản lý lưu trữ thứ cấp (Secondary Storage Management).** | Đi kèm với Free-space management và Disk scheduling. |
| **Mục đích của Protection & Security KHÔNG bao gồm?** | **Lưu vết người dùng để tính phí hoặc thống kê.** | Lưu vết tính phí/thống kê là chức năng **Kế toán (Accounting)**. |
| **Bộ định thời CPU chọn tiến trình từ hàng đợi nào?** | **Hàng đợi sẵn sàng (Ready Queue).** | Chọn từ Ready queue để đưa vào Running. |
| **Chuyển ngữ cảnh (Context Switch) là gì?** | **Quá trình CPU chuyển từ thực thi tiến trình này sang tiến trình khác.** | Lưu trạng thái PCB cũ và nạp trạng thái PCB mới. |
| **Phát biểu SAI về Hệ thống Đa chương?** | "Công việc/chương trình được thi hành tuần tự." | **Sai** vì đa chương thực thi xen kẽ (chuyển việc khi chờ I/O), đơn chương mới thi hành tuần tự. |
| **Đặc điểm của Multilevel Feedback Queue?** | **Cho phép tiến trình di chuyển giữa các hàng đợi (hỗ trợ Aging).** | Multilevel Queue thông thường thì tiến trình bị gắn cố định. |
| **Cân bằng tải trên SMP làm ảnh hưởng đến tính chất gì?** | **Ái lực bộ xử lý (Processor Affinity).** | Khi chuyển CPU thì bộ đệm cache bị vô hiệu hóa. |
| **Phát biểu SAI về FCFS?** | "Khi CPU trống, HĐH sẽ chọn tiến trình có CPU burst ngắn nhất." | **Sai** vì đó là SJF. FCFS luôn chọn tiến trình đến trước nhất ($\min[Arrival]$). |
| **Quan hệ cha - con khi tạo tiến trình?** | Tiến trình con có thể chia sẻ một phần tài nguyên của cha; Cha có thể đợi con hoặc chạy đồng thời. | Cha và con **không bắt buộc** phải luôn chạy đồng thời. |
| **Nếu Quantum time của Round Robin quá lớn?** | **Round Robin trở thành FCFS.** | Vì mọi tiến trình đều hoàn thành burst trước khi hết quantum. |
| **Giải thuật định thời "Xổ số" (Lottery Scheduling)?** | Tính tổng số vé tích lũy từ $P_1 \to P_n$. Nếu tại $P_k$, tổng tích lũy $> \text{số ngẫu nhiên}$ thì $P_k$ được chọn. | Ví dụ: vé $5, 6, 2, 7$, số tạo ra là $10$: $P_1(5) \le 10$, $P_1+P_2 = 11 > 10 \rightarrow$ Chọn $P_2$. |
| **Thời gian chờ tối đa trong Round Robin?** | **$(n - 1) \times q$.** | Nếu time quantum $q = 10$ ms, thời gian chờ lâu nhất là $120$ ms $\rightarrow (n-1) \times 10 = 120 \Rightarrow n = 13$ tiến trình! |
| **Chế độ quyết định Trưng dụng (Preemptive)?** | **Thời gian đáp ứng tốt hơn so với chế độ không trưng dụng.** | Tiến trình bị ngắt chuyển về `Ready` (không phải `Waiting`); chi phí cao hơn do context switch. |
| **Bộ định thời nào nạp chương trình vào RAM để thực thi?** | **Bộ định thời dài (Long-term Scheduler / Job Scheduler).** | Điều chỉnh mức độ đa chương của hệ thống. |
| **Cấu trúc HĐH kết hợp nhiều cách tiếp cận để tối ưu?** | **Cấu trúc Lai (Hybrid Structure).** | Ví dụ điển hình: macOS, iOS, Windows, Android. |
| **Mô hình Đa tiểu trình nhiều user thread map vào 1 kernel thread?** | **Mô hình Nhiều – Một (Many-to-One).** | 1 thread bị block sẽ block toàn bộ tiến trình. |

---

# TỔNG KẾT BÍ KÍP LÀM BÀI ĐẠT ĐIỂM TỐI ĐA (10/10)

1. **Phần Trắc nghiệm (6.0 - 7.5đ):**
   - Đọc kỹ từ khóa phủ định: **KHÔNG PHẢI**, **SAI**, **ĐÚNG**.
   - Nhớ chính xác vị trí phân vùng bộ nhớ: Biến toàn cục $\to$ **Data**, Biến cục bộ / tham số $\to$ **Stack**, Cấp phát động $\to$ **Heap**, Mã lệnh $\to$ **Text**.
   - Nắm chắc 3 phương pháp truyền tham số system call: **Thanh ghi, Khối nhớ, Ngăn xếp** *(không có Heap)*.
   - Nắm chắc công thức tính số tiến trình của Round Robin: $(n - 1) \times q = T_{wait\_max}$.
2. **Phần Câu hỏi ngắn (1.5đ):**
   - Viết chính xác thuật ngữ tiếng Anh chuẩn giáo trình: `Stack`, `Data section`, `Shared memory`, `Processor affinity`, `Aging`.
   - Lần vết `fork()` theo cây tiến trình, không đoán mò.
3. **Phần Bài tập Định thời (2.5đ):**
   - Vẽ trục Gantt phải liền mạch từ $0$ đến tổng Burst time (nếu không có thời gian CPU rỗi).
   - Đánh dấu rõ các mốc thời gian $0, 3, 7, 8, \dots$ dưới trục.
   - Kiểm tra kỹ các mốc đến của tiến trình để không bỏ sót sự kiện tranh chấp CPU trong SRTF hoặc Round Robin.
   - Luôn kẻ bảng đầy đủ 5 cột: `Process | AT | BT | Finish Time | Turnaround Time | Waiting Time | Response Time` và ghi rõ công thức tính giá trị trung bình ở cuối bảng.
