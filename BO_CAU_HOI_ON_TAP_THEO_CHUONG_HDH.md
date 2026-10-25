# BỘ CÂU HỎI ÔN TẬP TOÀN DIỆN MÔN HỆ ĐIỀU HÀNH THEO TỪNG CHƯƠNG
*(Kèm Đáp Án & Hướng Dẫn Giải Chi Tiết Chuẩn Ma Trận Đề Thi UIT)*

> **Cấu trúc bộ câu hỏi:**
> - **Chương 1:** Tổng quan Hệ điều hành & Kiến trúc máy tính
> - **Chương 2:** Cấu trúc & Dịch vụ của Hệ điều hành
> - **Chương 3:** Quản lý Tiến trình & Tiểu trình (Processes & Threads)
> - **Chương 4:** Định thời CPU (CPU Scheduling)
> 
> Mỗi chương được chia làm 3 phần:
> - **Phần A: Trắc nghiệm khách quan** (Có 4 phương án, chỉ ra bẫy đề thi và giải thích cặn kẽ).
> - **Phần B: Câu hỏi ngắn / Điền khuyết thuật ngữ** (Dạng câu hỏi 1.5đ trong đề thi chính thức).
> - **Phần C: Bài tập tình huống / Tính toán / Lần vết code** (Có bài giải từng bước chi tiết).

---

# CHƯƠNG 1: TỔNG QUAN HỆ ĐIỀU HÀNH & KIẾN TRÚC MÁY TÍNH

## PHẦN A: CÂU HỎI TRẮC NGHIỆM

#### Câu 1.1: Phát biểu nào sau đây về Hệ điều hành là KHÔNG CHÍNH XÁC?
A. Hệ điều hành là chương trình trung gian giữa phần cứng máy tính và người sử dụng.  
B. Hệ điều hành đóng vai trò là bộ phân phối tài nguyên (Resource Allocator).  
C. Hệ điều hành là chương trình trực tiếp giải quyết các bài toán tính toán cụ thể của người dùng.  
D. Hệ điều hành đóng vai trò là chương trình điều khiển (Control Program) ngăn ngừa lỗi và việc sử dụng máy tính không hợp lệ.  
- **Đáp án:** **C**  
- **Giải thích & Bẫy:** Chương trình trực tiếp giải quyết bài toán của người dùng là **Chương trình ứng dụng (Application Programs)** như Word, Trình duyệt, Game, Database. HĐH chỉ đóng vai trò môi trường và điều phối tài nguyên cho các ứng dụng đó chạy.

#### Câu 1.2: Chương trình nạp khởi động hệ thống (Bootstrap Program) thường được lưu trữ ở đâu và có nhiệm vụ gì?
A. Lưu trong RAM, nạp các chương trình ứng dụng của người dùng vào bộ nhớ.  
B. Lưu trong ROM hoặc EEPROM (phần sụn - firmware), khởi tạo phần cứng và nạp nhân (kernel) của HĐH vào RAM.  
C. Lưu trên ổ đĩa cứng, quản lý việc đăng nhập của người dùng.  
D. Lưu trong bộ nhớ đệm Cache L1, thiết lập bảng phân trang bộ nhớ.  
- **Đáp án:** **B**  
- **Giải thích:** Bootstrap program nằm trong ROM/EEPROM (bộ nhớ chỉ đọc, không mất dữ liệu khi tắt nguồn). Khi bật máy, CPU trỏ đến địa chỉ này để kiểm tra phần cứng (POST) và tìm nạp nhân HĐH vào bộ nhớ chính.

#### Câu 1.3: Ba tiêu chí cốt lõi được sử dụng để phân cấp hệ thống lưu trữ (Storage-Device Hierarchy) là gì?
A. Tốc độ truy xuất, Chi phí trên bit, Khả năng thực thi tập lệnh đa dụng.  
B. Tốc độ truy xuất, Chi phí trên bit, Tính bay hơi / khả năng duy trì dữ liệu khi mất điện (Volatility).  
C. Dung lượng lưu trữ, Chuẩn giao tiếp bus, Tần số xung nhịp.  
D. Tính bay hơi, Công nghệ bán dẫn, Số cổng kết nối I/O.  
- **Đáp án:** **B**  
- **Giải thích:** Giáo trình chuẩn Silberschatz nêu rõ 3 tiêu chí phân cấp: **Speed (Tốc độ)**, **Cost (Chi phí)**, và **Volatility (Tính bay hơi)**. Đi từ trên xuống (Registers $\to$ Cache $\to$ RAM $\to$ SSD $\to$ HDD $\to$ Băng từ): Tốc độ giảm dần, dung lượng tăng dần, giá thành trên mỗi GB giảm dần.

#### Câu 1.4: Sự khác biệt cơ bản giữa Ngắt phần cứng (Hardware Interrupt) và Ngắt phần mềm (Software Interrupt / Trap) là gì?
A. Ngắt phần cứng do bộ định thời CPU tạo ra, ngắt phần mềm do thiết bị bàn phím tạo ra.  
B. Ngắt phần cứng được gửi qua bus hệ thống từ thiết bị ngoại vi; Ngắt phần mềm phát sinh do lỗi thực thi lệnh hoặc lời gọi hệ thống (System Call).  
C. Ngắt phần cứng không cần Interrupt Vector, ngắt phần mềm bắt buộc phải dùng Interrupt Vector.  
D. Ngắt phần cứng chạy ở User mode, ngắt phần mềm chạy ở Kernel mode.  
- **Đáp án:** **B**  
- **Giải thích:** Ngắt cứng (Hardware interrupt) do bộ điều khiển thiết bị (Device Controller) kích hoạt qua bus tín hiệu. Ngắt mềm (Trap/Exception) phát sinh từ chính bên trong CPU do câu lệnh chương trình: chia cho 0, truy xuất bộ nhớ vi phạm, hoặc lệnh gọi `system call`. Cả hai đều tra cứu bảng Interrupt Vector để tìm hàm xử lý (ISR).

#### Câu 1.5: Hệ thống đa xử lý đối xứng (Symmetric Multiprocessing - SMP) có đặc điểm nào sau đây?
A. Một bộ xử lý đóng vai trò Master điều khiển toàn bộ hệ thống, các bộ xử lý khác là Slave.  
B. Các bộ xử lý chỉ giao tiếp với nhau thông qua mạng cục bộ LAN.  
C. Mỗi bộ xử lý chạy một bản sao giống nhau của hệ điều hành, cùng bình đẳng chia sẻ bộ nhớ chung và bus hệ thống.  
D. Mỗi bộ xử lý sở hữu một không gian bộ nhớ vật lý hoàn toàn tách biệt, không thể đọc dữ liệu của nhau.  
- **Đáp án:** **C**  
- **Giải thích & Bẫy:** Phương án A là Đa xử lý bất đối xứng (AMP). Phương án B & D là Hệ thống phân tán (Distributed System). Trong SMP, các CPU ngang hàng, cùng chia sẻ RAM chung (Tightly-coupled).

#### Câu 1.6: Ba ưu điểm lớn nhất của Hệ thống đa bộ xử lý (Multiprocessor Systems) so với hệ thống đơn bộ xử lý là:
A. Tăng thông lượng (Throughput), Tính kinh tế theo quy mô (Economy of Scale), Tăng độ tin cậy (Graceful degradation / Fault tolerance).  
B. Giảm giá thành phần cứng xuống 0, Tăng dung lượng đĩa cứng, Tự động sửa lỗi phần mềm.  
C. Không bao giờ xảy ra tình trạng thắt cổ chai, Tốc độ xung nhịp CPU tăng gấp đôi, Bộ nhớ không bị giới hạn.  
D. Đơn giản hóa cấu trúc HĐH, Không cần cơ chế ngắt, Loại bỏ hoàn toàn chuyển ngữ cảnh.  
- **Đáp án:** **A**  
- **Giải thích:** Giáo trình chuẩn liệt kê 3 ưu điểm: Increased Throughput, Economy of Scale (dùng chung nguồn, vỏ, thiết bị), Increased Reliability (hỏng 1 CPU các CPU khác vẫn hoạt động, hệ thống suy giảm hiệu năng chậm rãi chứ không sập hoàn toàn).

#### Câu 1.7: Trong cơ chế hoạt động Hai chế độ (Dual-Mode Operation), bit chế độ (Mode bit) bằng 0 và 1 lần lượt đại diện cho:
A. Chế độ Người dùng (User mode) và Chế độ Hạt nhân (Kernel mode).  
B. Chế độ Hạt nhân (Kernel mode) và Chế độ Người dùng (User mode).  
C. Chế độ Khởi động (Boot mode) và Chế độ Tắt máy (Shutdown mode).  
D. Chế độ Đơn nhiệm (Single-task) và Chế độ Đa nhiệm (Multi-task).  
- **Đáp án:** **B**  
- **Giải thích:** Phần cứng máy tính quy ước: Mode bit = `0` là **Kernel mode** (Supervisor / Privileged / System mode); Mode bit = `1` là **User mode**. Khi xảy ra ngắt hoặc system call, phần cứng tự động đổi mode bit sang `0`. Khi trả về chương trình người dùng, mode bit được đặt lại thành `1`.

#### Câu 1.8: Lệnh nào sau đây là Lệnh đặc quyền (Privileged Instruction)?
A. Lệnh thực hiện phép cộng 2 thanh ghi (`ADD R1, R2`).  
B. Lệnh đọc dữ liệu từ một biến cục bộ trong ngăn xếp (Stack).  
C. Lệnh thay đổi giá trị của Bit chế độ (Mode bit) hoặc lệnh tắt ngắt toàn hệ thống (`CLI`).  
D. Lệnh nhảy không điều kiện (`JMP`).  
- **Đáp án:** **C**  
- **Giải thích:** Các lệnh can thiệp vào hoạt động cốt lõi của phần cứng (chuyển mode bit, quản lý bảng ngắt, giao tiếp thanh ghi điều khiển thiết bị I/O trực tiếp, quản lý bộ đếm thời gian Timer) là **lệnh đặc quyền**, chỉ được thực thi ở Kernel mode. Nếu User mode cố thực hiện, CPU sẽ chặn lại và phát sinh một Trap.

#### Câu 1.9: Khác biệt căn bản giữa Hệ thống Đa chương (Multiprogramming) và Hệ thống Đa nhiệm / Chia sẻ thời gian (Multitasking / Time-sharing) là:
A. Đa chương chỉ nạp 1 công việc vào RAM; Đa nhiệm nạp nhiều công việc vào RAM.  
B. Đa chương chuyển đổi CPU khi công việc hiện tại phải chờ đợi I/O; Đa nhiệm chuyển đổi CPU rất thường xuyên dựa trên lát cắt thời gian (Quantum) để người dùng tương tác trực tiếp với từng chương trình.  
C. Đa chương thi hành các công việc tuần tự; Đa nhiệm thi hành đồng thời.  
D. Đa chương dành cho hệ thống nhiều CPU; Đa nhiệm chỉ dùng cho hệ thống một CPU.  
- **Đáp án:** **B**  
- **Giải thích & Bẫy:** Cả Đa chương và Đa nhiệm đều nạp *nhiều công việc* vào bộ nhớ. Nhưng trong Đa chương cổ điển, CPU chỉ nhường quyền khi tiến trình tự nguyện chờ I/O. Còn Đa nhiệm (Time-sharing) là mở rộng của đa chương có thêm cơ chế chia sẻ thời gian (timer interrupt) để tạo cảm giác tương tác tức thời (interactive computing).

---

## PHẦN B: CÂU HỎI TRẢ LỜI NGẮN / ĐIỀN KHUYẾT THUẬT NGỮ

1. Thiết bị phần cứng duy nhất trong hệ thống lưu trữ dung lượng lớn mà CPU có thể truy xuất và thực thi chỉ lệnh trực tiếp là gì?  
   $\rightarrow$ **Trả lời:** `Main Memory` (hoặc `RAM` / `Bộ nhớ chính`).
2. Bảng chứa danh sách các địa chỉ trỏ tới các hàm phục vụ ngắt tương ứng trong hệ thống được gọi là gì?  
   $\rightarrow$ **Trả lời:** `Interrupt Vector` (hoặc `Véc-tơ ngắt`).
3. Phần cứng nào được tích hợp vào hệ thống để định kỳ phát sinh ngắt, nhằm ngăn chặn một chương trình người dùng độc chiếm CPU vô tận?  
   $\rightarrow$ **Trả lời:** `Timer` (hoặc `Bộ đếm thời gian`).
4. Khả năng hệ thống vẫn tiếp tục hoạt động (dù hiệu năng bị giảm sút) khi có một hoặc một vài thành phần phần cứng bị hỏng hóc được gọi là gì?  
   $\rightarrow$ **Trả lời:** `Graceful degradation` (hoặc `Fault tolerance` / `Khả năng chịu lỗi`).
5. Mô hình hệ thống phân tán được phân loại thành hai dạng kiến trúc cơ bản nào?  
   $\rightarrow$ **Trả lời:** `Client-Server` và `Peer-to-Peer` (P2P).

---

## PHẦN C: BÀI TẬP TÌNH HUỐNG

#### Tình huống 1: Quy trình xử lý khi chương trình người dùng đọc file từ đĩa
**Đề bài:** Một chương trình người dùng đang chạy ở User mode và thực hiện lệnh `read()` để đọc một khối dữ liệu từ tập tin trên ổ cứng. Hãy mô tả chi tiết 5 bước diễn ra ở mức phần cứng và HĐH (bao gồm sự thay đổi của Mode bit và tín hiệu ngắt).

**Lời giải chi tiết:**
1. **Bước 1:** Tiến trình gọi hàm thư viện `read()`. Hàm này thiết lập các tham số và phát sinh một lệnh ngắt mềm (Trap/System call instruction) để yêu cầu dịch vụ của HĐH.
2. **Bước 2:** Phần cứng CPU phát hiện Trap, lưu ngữ cảnh hiện tại (Program Counter, các thanh ghi) của tiến trình người dùng vào Stack của Kernel. Phần cứng **tự động chuyển Mode bit từ `1` (User mode) sang `0` (Kernel mode)**.
3. **Bước 3:** CPU tra cứu bảng Interrupt Vector, nhảy đến thực thi hàm phục vụ tương ứng trong HĐH. Nhân HĐH kiểm tra tính hợp lệ của tham số, điều khiển Bộ điều khiển thiết bị đĩa (Disk Controller) bắt đầu đọc dữ liệu vào bộ đệm, đồng thời chuyển trạng thái tiến trình người dùng từ `Running` sang `Waiting`. Trong khi đĩa đọc, CPU được cấp cho tiến trình khác chạy.
4. **Bước 4:** Khi thiết bị đĩa hoàn tất việc đọc dữ liệu vào bộ nhớ đệm, Disk Controller gửi một **tín hiệu ngắt phần cứng (Hardware Interrupt)** lên CPU qua bus hệ thống. CPU tiếp nhận ngắt, chuyển dữ liệu từ bộ đệm vào không gian nhớ của tiến trình người dùng, và chuyển trạng thái tiến trình này từ `Waiting` sang `Ready`.
5. **Bước 5:** HĐH khôi phục ngữ cảnh của tiến trình, **đặt lại Mode bit từ `0` sang `1`**, và chuyển quyền điều khiển trả lại cho tiến trình người dùng tiếp tục thực thi chỉ lệnh ngay sau lệnh `read()`.

---

# CHƯƠNG 2: CẤU TRÚC & DỊCH VỤ CỦA HỆ ĐIỀU HÀNH

## PHẦN A: CÂU HỎI TRẮC NGHIỆM

#### Câu 2.1: Chức năng "Ánh xạ tập tin/thư mục vào thiết bị lưu trữ thứ cấp tương ứng" thuộc về thành phần nào của Hệ điều hành?
A. Quản lý lưu trữ thứ cấp (Secondary Storage Management).  
B. Quản lý tập tin (File Management).  
C. Quản lý bộ nhớ chính (Main Memory Management).  
D. Quản lý hệ thống I/O (I/O System Management).  
- **Đáp án:** **B**  
- **Giải thích & Bẫy:** Đây là câu hỏi bẫy kinh điển trong Đề thi GK1 2024–2025. **File Management** chịu trách nhiệm tạo/xóa, thao tác và ánh xạ tập tin logic vào khối lưu trữ trên đĩa. Còn **Secondary Storage Management** chịu trách nhiệm cấp phát không gian đĩa vật lý (storage allocation), quản lý khối trống (free-space), và định thời đầu đọc đĩa (disk scheduling).

#### Câu 2.2: Thành phần Quản lý hệ thống I/O (I/O System Management) của HĐH có nhiệm vụ chính nào?
A. Phân bổ không gian bộ nhớ RAM cho các biến toàn cục.  
B. Cung cấp giao diện chung thống nhất đến các trình điều khiển thiết bị (Device Drivers) và che giấu sự khác biệt phần cứng.  
C. Ánh xạ các khối dữ liệu vật lý vào thư mục logic.  
D. Quyết định tiến trình nào được nạp vào bộ nhớ khi có không gian trống.  
- **Đáp án:** **B**  
- **Giải thích:** Quản lý I/O cung cấp hệ thống bộ đệm (buffering, caching, spooling) và cung cấp giao diện chuẩn (general device-driver interface) để các lập trình viên không phải viết mã riêng biệt cho từng loại bàn phím hay chuột của các hãng khác nhau.

#### Câu 2.3: Mục đích của Hệ thống Bảo vệ và An ninh (Protection and Security) KHÔNG BAO GỒM mục đích nào sau đây?
A. Đảm bảo các tiến trình không can thiệp, xâm phạm vùng nhớ của nhau.  
B. Kiểm soát quyền truy cập của người dùng đối với các tài nguyên hệ thống (file, CPU, bộ nhớ).  
C. Thu thập số liệu, lưu vết sử dụng tài nguyên của người dùng để tính phí (Accounting).  
D. Xác thực danh tính của người sử dụng khi đăng nhập vào hệ thống.  
- **Đáp án:** **C**  
- **Giải thích & Bẫy:** Theo chuẩn giáo trình, việc lưu vết sử dụng tài nguyên để tính cước phí, thống kê thuộc về dịch vụ **Kế toán hệ thống (Accounting)**, không phải mục đích của dịch vụ Bảo vệ và An ninh (Protection & Security).

#### Câu 2.4: Ba phương pháp cơ bản nhất được sử dụng để truyền tham số từ tiến trình vào Lời gọi hệ thống (System Calls) là:
A. Sử dụng Thanh ghi (Registers), Khối bộ nhớ / Bảng trong RAM (Block/Table in memory), Ngăn xếp (Stack).  
B. Sử dụng Thanh ghi, Vùng nhớ Heap, Ngăn xếp.  
C. Sử dụng Vùng nhớ chia sẻ (Shared memory), Đường ống (Pipe), Hàng đợi thông điệp.  
D. Sử dụng Tập tin trên đĩa, Vùng nhớ Heap, Bảng véc-tơ ngắt.  
- **Đáp án:** **A**  
- **Giải thích & Bẫy:** 3 cách chuẩn: (1) Truyền trực tiếp qua Registers; (2) Lưu tham số vào một Block trong RAM rồi truyền con trỏ khối nhớ đó qua một thanh ghi (phổ biến trong Linux/Solaris); (3) Đẩy tham số vào Stack. Vùng nhớ Heap tuyệt đối không dùng để truyền tham số system call.

#### Câu 2.5: Đặc điểm nổi bật nhất của Kiến trúc Vi nhân (Microkernel) là gì?
A. Toàn bộ các dịch vụ HĐH được biên dịch thành một tập tin nhị phân duy nhất chạy trong không gian nhân.  
B. Chuyển phần lớn các dịch vụ không thiết yếu của HĐH ra khỏi không gian nhân (Kernel space) sang không gian người dùng (User space).  
C. Không hỗ trợ lời gọi hệ thống, chỉ hỗ trợ gọi hàm trực tiếp.  
D. Các module giao tiếp trực tiếp với nhau thông qua thanh ghi CPU mà không cần nhân trung gian.  
- **Đáp án:** **B**  
- **Giải thích:** Microkernel chỉ giữ lại các chức năng tối thiểu trong kernel: quản lý tiến trình cốt lõi, quản lý bộ nhớ tối thiểu, và giao tiếp liên tiến trình (IPC). Các dịch vụ khác như Quản lý File, Trình điều khiển thiết bị (Drivers) được đẩy ra chạy như các tiến trình người dùng bình thường (User space) và giao tiếp qua cơ chế Truyền thông điệp (Message Passing).

#### Câu 2.6: Nhược điểm lớn nhất của Kiến trúc Vi nhân (Microkernel) so với Kiến trúc Đơn khối (Monolithic) là gì?
A. Khi một dịch vụ người dùng bị sập, toàn bộ hệ điều hành sẽ bị treo cứng.  
B. Rất khó mở rộng hoặc thêm tính năng mới cho hệ điều hành.  
C. Hiệu năng hệ thống bị suy giảm do chi phí chuyển ngữ cảnh (Context switch overhead) và chi phí truyền thông điệp liên tục giữa user space và kernel space.  
D. Không thể áp dụng trên các hệ thống kiến trúc x86.  
- **Đáp án:** **C**  
- **Giải thích:** Trong Microkernel, để User Program đọc được 1 khối file: User Program phải gửi message tới Kernel $\to$ Kernel chuyển ngữ cảnh gửi tới File Service $\to$ File Service gửi tới Disk Driver $\to$ phản hồi ngược lại. Việc chuyển đổi qua lại giữa User mode và Kernel mode liên tục làm giảm hiệu năng đáng kể so với Monolithic (Monolithic gọi hàm trực tiếp trong cùng một không gian nhớ).

#### Câu 2.7: Kiến trúc Hệ thống Lai (Hybrid Systems) là kiến trúc:
A. Chỉ chạy được trên các máy tính sử dụng hai nguồn điện độc lập.  
B. Kết hợp nhiều cách tiếp cận cấu trúc khác nhau (như Monolithic, Phân lớp, Vi nhân) để đáp ứng tối ưu các yêu cầu về hiệu suất, bảo mật và tính tiện dụng.  
C. Chỉ sử dụng ngôn ngữ Assembly kết hợp với mã máy để viết nhân HĐH.  
D. Cho phép chạy hai hệ điều hành khác nhau trên cùng một lõi CPU tại cùng một chu kỳ xung nhịp.  
- **Đáp án:** **B**  
- **Giải thích:** Các HĐH hiện đại như Windows, macOS (Darwin), Android đều là Hybrid Systems. Ví dụ Darwin kết hợp Microkernel Mach (quản lý bộ nhớ, IPC) với Monolithic BSD (networking, file system, POSIX).

---

## PHẦN B: CÂU HỎI TRẢ LỜI NGẮN / ĐIỀN KHUYẾT THUẬT NGỮ

1. Giao diện lập trình chuẩn (API) cho các lời gọi hệ thống trên các hệ điều hành họ UNIX, Linux và macOS có tên là gì?  
   $\rightarrow$ **Trả lời:** `POSIX API` (hoặc `POSIX`).
2. Chương trình đóng vai trò là giao diện dòng lệnh giữa người dùng và HĐH, có nhiệm vụ đọc lệnh, thông dịch và gọi system call tương ứng được gọi là gì?  
   $\rightarrow$ **Trả lời:** `Command Interpreter` (hoặc `Shell` / `CLI`).
3. Kiến trúc nhân HĐH cho phép nạp thêm các module tính năng (như driver, định dạng file mới) vào nhân khi cần thiết lúc hệ thống đang chạy mà không phải biên dịch lại kernel được gọi là gì?  
   $\rightarrow$ **Trả lời:** `Loadable Kernel Modules` (hoặc `LKM` / `Module`).
4. Trong kiến trúc phân lớp (Layered Approach), Lớp 0 và Lớp N trên cùng đại diện cho thành phần nào?  
   $\rightarrow$ **Trả lời:** Lớp 0 là `Hardware` (Phần cứng), Lớp N là `User Interface` (Giao diện người dùng).

---

## PHẦN C: BÀI TẬP TÌNH HUỐNG

#### Tình huống 2: So sánh Monolithic Kernel và Microkernel
**Đề bài:** Giả sử một trình điều khiển card mạng (Network Driver) bị lỗi rò rỉ bộ nhớ hoặc truy xuất con trỏ `NULL`. Hãy phân tích điều gì sẽ xảy ra đối với toàn bộ hệ thống trong hai trường hợp: (a) Hệ điều hành dùng kiến trúc Monolithic; (b) Hệ điều hành dùng kiến trúc Microkernel.

**Lời giải chi tiết:**
- **Trường hợp (a) Kiến trúc Monolithic:**
  - Vì Driver chạy chung không gian địa chỉ hạt nhân (Kernel space) cùng với toàn bộ các thành phần cốt lõi của HĐH.
  - Khi Driver thực hiện truy xuất vùng nhớ bất hợp pháp hoặc crash, nó sẽ gây ra lỗi `Kernel Panic` (trên Linux) hoặc màn hình xanh chết chóc `Blue Screen of Death - BSOD` (trên Windows). **Toàn bộ hệ thống bị sập ngay lập tức**, máy tính buộc phải khởi động lại.
- **Trường hợp (b) Kiến trúc Microkernel:**
  - Driver card mạng chạy như một tiểu trình/tiến trình phục vụ trong không gian người dùng (**User space**).
  - Khi Driver bị crash, lỗi chỉ xảy ra cục bộ bên trong không gian địa chỉ của tiến trình mạng đó. Nhân vi mô (Microkernel) và các dịch vụ khác (Quản lý File, Tiến trình) hoàn toàn không bị ảnh hưởng.
  - HĐH có thể dễ dàng khởi động lại (restart) tiến trình Network Driver đó mà người dùng hầu như không nhận thấy sự gián đoạn, **hệ thống vẫn duy trì hoạt động an toàn**.

---

# CHƯƠNG 3: QUẢN LÝ TIẾN TRÌNH & TIỂU TRÌNH (PROCESSES & THREADS)

## PHẦN A: CÂU HỎI TRẮC NGHIỆM

#### Câu 3.1: Khi một chương trình C được nạp vào bộ nhớ để thực thi, các biến toàn cục (Global Variables) và biến tĩnh (Static Variables) được lưu trữ tại phân vùng nào?
A. Text Section.  
B. Stack Section.  
C. Data Section.  
D. Heap Section.  
- **Đáp án:** **C**  
- **Giải thích:** Phân vùng chuẩn:
  - **Text:** Mã máy của chương trình.
  - **Data:** Biến toàn cục (global) và biến tĩnh (static).
  - **Heap:** Bộ nhớ cấp phát động (`malloc`, `calloc`, `new`).
  - **Stack:** Biến cục bộ (local), tham số hàm, địa chỉ trả về của hàm.

#### Câu 3.2: Một tiến trình đang ở trạng thái `Running` KHÔNG THỂ chuyển trực tiếp sang trạng thái nào sau đây?
A. Ready.  
B. Waiting.  
C. Terminated.  
D. New.  
- **Đáp án:** **D**  
- **Giải thích & Bẫy:** `New` là trạng thái ban đầu khi tiến trình vừa được khởi tạo trên đĩa và nạp vào hệ thống. Một tiến trình đang `Running` chỉ có thể chuyển sang: `Ready` (khi bị ngắt/hết thời gian quantum), `Waiting` (khi chờ thao tác I/O hoặc sự kiện), hoặc `Terminated` (khi kết thúc). Không bao giờ có mũi tên từ `Running` quay ngược về `New`.

#### Câu 3.3: Trạng thái `Ready` của tiến trình được định nghĩa chính xác là gì?
A. Tiến trình vừa được tạo ra và đang nằm trên đĩa cứng chờ nạp vào RAM.  
B. Tiến trình đang được CPU thực thi các câu lệnh.  
C. Tiến trình đã có đầy đủ tài nguyên cần thiết trong RAM, chỉ còn chờ được cấp phát CPU để chạy.  
D. Tiến trình đang tạm dừng để chờ đợi một sự kiện nhập xuất (I/O) hoàn thành.  
- **Đáp án:** **C**  
- **Giải thích:** Phân biệt rõ: Nếu thiếu I/O hoặc tài nguyên khác $\to$ `Waiting`. Nếu đã có đủ mọi thứ và chỉ chờ đến lượt CPU $\to$ `Ready`.

#### Câu 3.4: Bộ định thời dài (Long-term Scheduler / Job Scheduler) có nhiệm vụ chính là gì?
A. Lựa chọn một tiến trình trong Ready Queue để trao quyền điều khiển CPU cho nó.  
B. Xác định chương trình nào được chấp nhận nạp từ đĩa vào bộ nhớ chính (Ready Queue) để thực thi, qua đó kiểm soát Mức độ đa chương (Degree of Multiprogramming).  
C. Hoán đổi (swap) các tiến trình từ RAM ra phân vùng Swap trên đĩa cứng khi bộ nhớ đầy.  
D. Quản lý việc chuyển ngữ cảnh giữa các luồng trong cùng một tiến trình.  
- **Đáp án:** **B**  
- **Giải thích & Bẫy:** Bộ định thời ngắn (Short-term / CPU scheduler) chọn tiến trình từ Ready queue cấp CPU (tần suất vài ms). Bộ định thời trung gian (Medium-term scheduler) làm nhiệm vụ Swapping. Bộ định thời dài (Long-term) nạp job từ đĩa vào RAM và kiểm soát số lượng tiến trình trong RAM (Degree of Multiprogramming).

#### Câu 3.5: Phát biểu nào sau đây về lời gọi hệ thống `fork()` trong môi trường UNIX/Linux là ĐÚNG?
A. `fork()` trả về giá trị âm cho tiến trình cha và số 0 cho tiến trình con.  
B. `fork()` trả về giá trị 0 cho tiến trình con, và trả về PID của tiến trình con cho tiến trình cha.  
C. Tiến trình con sau khi được tạo ra sẽ dùng chung không gian biến cục bộ và biến toàn cục với tiến trình cha.  
D. Tiến trình con luôn thực thi từ dòng đầu tiên của hàm `main()`.  
- **Đáp án:** **B**  
- **Giải thích:** `fork()` nhân bản tiến trình. Tại điểm phân nhánh: trả về `0` cho con, trả về `PID con` ($> 0$) cho cha, và `-1` nếu lỗi. Tiến trình con nhận một bản sao không gian nhớ độc lập và tiếp tục thực thi chỉ lệnh ngay sau lệnh `fork()`, chứ không chạy lại từ đầu `main()`.

#### Câu 3.6: Khái niệm "Tiến trình Zombie" (Zombie Process) ám chỉ điều gì?
A. Tiến trình cha đã kết thúc trước khi tiến trình con kết thúc.  
B. Tiến trình đang bị treo trong một vòng lặp vô tận không thể giải phóng CPU.  
C. Tiến trình con đã kết thúc việc thực thi (gọi `exit()`), nhưng tiến trình cha chưa gọi hàm `wait()` để đọc trạng thái kết thúc của nó.  
D. Tiến trình bị hệ thống buộc dừng do cố tình truy xuất vùng nhớ bất hợp pháp.  
- **Đáp án:** **C**  
- **Giải thích:** Khi con gọi `exit()`, tài nguyên của nó được giải phóng nhưng entry của nó trong bảng tiến trình (Process Table) vẫn được giữ lại để lưu exit status. Chừng nào cha chưa gọi `wait()`, tiến trình con đó được gọi là Zombie. Ngược lại, nếu cha chết trước con thì con gọi là Orphan (tiến trình mồ côi).

#### Câu 3.7: Ba điều kiện bắt buộc mà mọi giải pháp cho bài toán Vùng tranh chấp (Critical Section Problem) phải thỏa mãn là:
A. Mutual Exclusion (Loại trừ tương hỗ), Progress (Tiến triển), Bounded Waiting (Chờ đợi có giới hạn).  
B. Mutual Exclusion, Synchronization, Deadlock Prevention.  
C. Progress, First-Come First-Served, Fairness.  
D. Atomicity, Consistency, Isolation.  
- **Đáp án:** **A**  
- **Giải thích & Bẫy:** 3 điều kiện kinh điển:
  1. **Mutual Exclusion:** Chỉ 1 tiến trình được ở trong Critical Section tại một thời điểm.
  2. **Progress:** Nếu CS trống, chỉ những tiến trình muốn vào mới được cạnh tranh, không bị hoãn vô hạn.
  3. **Bounded Waiting:** Số lần các tiến trình khác được vượt mặt để vào CS phải có giới hạn (tránh Starvation).

#### Câu 3.8: Giữa các Tiểu trình (Threads) trong cùng một Tiến trình, thành phần nào sau đây là RIÊNG BIỆT cho từng tiểu trình (không chia sẻ)?
A. Phân vùng mã lệnh (Code/Text section).  
B. Phân vùng dữ liệu chứa các biến toàn cục (Data section).  
C. Danh sách các tập tin đang mở và tài nguyên HĐH.  
D. Ngăn xếp riêng (Stack), Bộ đếm chương trình (Program Counter) và Tập thanh ghi (Registers).  
- **Đáp án:** **D**  
- **Giải thích:** Các luồng trong cùng 1 process chia sẻ chung: Code, Data (biến toàn cục, static), Heap, OS resources (files, sockets). Mỗi luồng bắt buộc phải sở hữu riêng: Thread ID, PC (để biết đang chạy đến dòng lệnh nào), Registers, và Stack (để lưu biến cục bộ và các hàm gọi lồng nhau).

#### Câu 3.9: Nhược điểm lớn nhất của Mô hình Đa tiểu trình Nhiều - Một (Many-to-One Model) là gì?
A. Tốn quá nhiều chi phí của nhân HĐH để tạo và quản lý thread.  
B. Nếu một tiểu trình thực hiện một lời gọi hệ thống gây khóa (Blocking System Call), toàn bộ tiến trình sẽ bị chặn lại.  
C. Không thể cài đặt trên hệ điều hành Linux.  
D. Các tiểu trình không thể truy xuất vào biến toàn cục chung.  
- **Đáp án:** **B**  
- **Giải thích:** Trong Many-to-One, toàn bộ User Threads được quản lý ở User space bởi một Thread Library và ánh xạ vào duy nhất 1 Kernel Thread. Vì nhân HĐH chỉ nhìn thấy 1 luồng duy nhất, nếu bất kỳ user thread nào gọi I/O chặn, nhân sẽ khóa cả kernel thread đó $\to$ toàn bộ các user thread khác cũng bị dừng theo, và không thể tận dụng kiến trúc CPU đa lõi.

---

## PHẦN B: CÂU HỎI TRẢ LỜI NGẮN / ĐIỀN KHUYẾT THUẬT NGỮ

1. Cấu trúc dữ liệu dạng bản ghi được HĐH sử dụng để duy trì toàn bộ thông tin quản lý của một tiến trình được viết tắt là gì?  
   $\rightarrow$ **Trả lời:** `PCB` (hoặc `Process Control Block`).
2. Thời gian tiêu tốn để HĐH lưu lại trạng thái của tiến trình cũ và nạp trạng thái của tiến trình mới khi đổi CPU được gọi là gì?  
   $\rightarrow$ **Trả lời:** `Context switch latency` (hoặc `Context switch overhead`).
3. Lời gọi hệ thống thường được tiến trình con gọi ngay sau `fork()` để nạp đè một tập tin thực thi nhị phân mới vào không gian nhớ của nó là gì?  
   $\rightarrow$ **Trả lời:** `exec()` (hoặc `execvp`, `execl`).
4. Khi tiến trình cha kết thúc trước khi tiến trình con kết thúc, tiến trình con sẽ trở thành tiến trình gì và được nhận nuôi bởi tiến trình nào?  
   $\rightarrow$ **Trả lời:** Tiến trình mồ côi (`Orphan process`), được nhận nuôi bởi `systemd` (hoặc `init` / PID = 1).
5. Cơ chế giao tiếp liên tiến trình (IPC) nào cho phép các tiến trình trao đổi dữ liệu với tốc độ cao nhất ngang bằng tốc độ truy xuất RAM thông thường?  
   $\rightarrow$ **Trả lời:** `Shared Memory` (hoặc `Bộ nhớ chia sẻ`).

---

## PHẦN C: BÀI TẬP LẦN VẾT CODE `fork()` (CHẮC CHẮN CÓ TRONG ĐỀ THI)

### Bài tập 3.1: Đếm số tiến trình, số chuỗi in ra và số lần vào hàng đợi Waiting
**Đề bài:** Cho đoạn mã nguồn C sau:
```c
#include <stdio.h>
#include <unistd.h>

int main() {
    int i;
    printf("Start\n");
    fork();
    for (i = 0; i < 2; i++) {
        int pid = fork();
        if (pid == 0) {
            printf("Child\n");
        } else {
            printf("Parent\n");
        }
    }
    return 0;
}
```
**Yêu cầu:**
1. Có tổng cộng bao nhiêu tiến trình được tạo ra trong suốt vòng đời của chương trình (kể cả tiến trình ban đầu)?
2. Từ `Start`, `Child`, `Parent` lần lượt được in ra màn hình bao nhiêu lần?
3. Các tiến trình rơi vào hàng đợi `Waiting` tổng cộng bao nhiêu lần do các lệnh `printf`?

**Lời giải chi tiết từng bước:**
1. **Bước 1 (Lệnh `printf("Start\n")`):**
   - Chỉ có $1$ tiến trình ban đầu ($P_0$).
   - In ra **$1$ lần từ `Start`**.
   - Số lần vào Waiting: **1 lần**.
2. **Bước 2 (Lệnh `fork()` ngoài vòng lặp):**
   - $P_0$ gọi `fork()` sinh ra $P_1$. Lúc này hệ thống có **$2$ tiến trình** ($P_0, P_1$).
3. **Bước 3 (Vòng lặp `for (i = 0; i < 2; i++)`):**
   - **Tại $i = 0$:**
     - Cả 2 tiến trình ($P_0, P_1$) đều gọi `fork()` $\rightarrow$ Mỗi tiến trình tạo thêm 1 con mới ($P_0 \to P_2$, $P_1 \to P_3$).
     - Lúc này có $2 \times 2 = 4$ tiến trình.
     - Trong đó có 2 tiến trình cha gốc ($pid > 0$) và 2 tiến trình con mới sinh ($pid == 0$).
     - Điều kiện `if (pid == 0)`: 2 tiến trình con in `Child` $\rightarrow$ **$2$ lần `Child`**.
     - Nhánh `else`: 2 tiến trình cha in `Parent` $\rightarrow$ **$2$ lần `Parent`**.
     - Cả 4 tiến trình đều gọi `printf` $\rightarrow$ Vào Waiting thêm **4 lần**.
   - **Tại $i = 1$:**
     - Cả 4 tiến trình hiện tại ($P_0, P_1, P_2, P_3$) đều tiếp tục chạy đến lệnh `fork()` $\rightarrow$ Mỗi tiến trình sinh thêm 1 con mới.
     - Tổng số tiến trình tăng lên thành: $4 \times 2 = 8$ tiến trình.
     - Trong 4 cặp cha - con mới tạo này: có đúng 4 tiến trình cha ($pid > 0$) và 4 tiến trình con ($pid == 0$).
     - Điều kiện `if (pid == 0)`: 4 tiến trình con in `Child` $\rightarrow$ **$4$ lần `Child`**.
     - Nhánh `else`: 4 tiến trình cha in `Parent` $\rightarrow$ **$4$ lần `Parent`**.
     - Cả 8 tiến trình đều gọi `printf` $\rightarrow$ Vào Waiting thêm **8 lần**.
4. **Tổng kết câu trả lời:**
   - **Tổng số tiến trình tạo thành:** **$8$ tiến trình**.
   - **Số lần in từ `Start`:** **$1$ lần**.
   - **Số lần in từ `Child`:** $2 + 4 =$ **$6$ lần**.
   - **Số lần in từ `Parent`:** $2 + 4 =$ **$6$ lần**.
   - **Tổng số lần các tiến trình rơi vào hàng đợi `Waiting`:** $1 + 4 + 8 =$ **$13$ lần**.

---

### Bài tập 3.2: Lần vết giá trị biến toàn cục qua nhiều nhánh `fork()`
**Đề bài:** Cho đoạn mã sau:
```c
#include <stdio.h>
#include <unistd.h>

int val = 10;

int main() {
    int pid = fork();
    if (pid == 0) {
        val += 5;
        fork();
        val += 10;
    } else {
        val += 2;
        fork();
        val += 3;
    }
    printf("%d\n", val);
    return 0;
}
```
**Hỏi:**
1. Có bao nhiêu tiến trình được tạo ra khi kết thúc chương trình?
2. Những giá trị nào của biến `val` sẽ được in ra màn hình và mỗi giá trị xuất hiện bao nhiêu lần?

**Lời giải chi tiết:**
1. **Xét cây tiến trình:**
   - Bắt đầu có $P_{init}$ với $val = 10$.
   - Lệnh `pid = fork()` đầu tiên chia nhánh:
     - **Nhánh CON (`pid == 0`):**
       - Có 1 tiến trình con $C_1$.
       - Thực hiện: $val = 10 + 5 = 15$.
       - Gọi `fork()` thứ hai: $C_1$ sinh ra thêm $C_2$. Cả 2 tiến trình đều giữ bản sao riêng với $val = 15$.
       - Cả 2 tiến trình thực hiện: $val = 15 + 10 = 25$.
       - Cả 2 tiến trình in giá trị của nó $\rightarrow$ **In số 25 (2 lần)**.
     - **Nhánh CHA (`pid > 0`):**
       - Có 1 tiến trình cha gốc $P_{init}$.
       - Thực hiện: $val = 10 + 2 = 12$.
       - Gọi `fork()` thứ ba: $P_{init}$ sinh ra thêm con $P_{new}$. Cả 2 tiến trình đều giữ bản sao riêng với $val = 12$.
       - Cả 2 tiến trình thực hiện: $val = 12 + 3 = 15$.
       - Cả 2 tiến trình in giá trị của nó $\rightarrow$ **In số 15 (2 lần)**.
2. **Kết luận:**
   - **Tổng số tiến trình:** $2 + 2 =$ **$4$ tiến trình**.
   - **Các giá trị được in ra màn hình:**
     - Giá trị **`25`** được in ra **2 lần**.
     - Giá trị **`15`** được in ra **2 lần**.
   *(Lưu ý: Thứ tự in giữa 25 và 15 phụ thuộc vào bộ định thời CPU, nhưng các giá trị và số lần in là bất biến!)*.

---

# CHƯƠNG 4: ĐỊNH THỜI CPU (CPU SCHEDULING)

## PHẦN A: CÂU HỎI TRẮC NGHIỆM

#### Câu 4.1: Tiêu chuẩn định thời nào sau đây cần được TỐI THIỂU HÓA (Minimizing)?
A. Hiệu suất sử dụng CPU (CPU Utilization).  
B. Thông lượng hệ thống (Throughput).  
C. Thời gian hoàn thành (Turnaround Time) và Thời gian chờ (Waiting Time).  
D. Số lượng chuyển ngữ cảnh trong một đơn vị thời gian.  
- **Đáp án:** **C**  
- **Giải thích:** Mục tiêu định thời CPU:
  - Cần **Tối đa hóa (Maximize):** CPU Utilization, Throughput.
  - Cần **Tối thiểu hóa (Minimize):** Turnaround Time (TAT), Waiting Time (WT), Response Time (RT).

#### Câu 4.2: Nhược điểm "Hiệu ứng đoàn tàu" (Convoy Effect) là đặc trưng của giải thuật định thời nào?
A. Round Robin.  
B. Shortest Job First (SJF).  
C. First-Come, First-Served (FCFS).  
D. Multilevel Feedback Queue.  
- **Đáp án:** **C**  
- **Giải thích:** Convoy effect xảy ra trong FCFS khi một tiến trình có CPU burst rất lớn được cấp phát CPU trước, khiến toàn bộ các tiến trình ngắn đến sau phải xếp hàng chờ đợi rất lâu, làm sụt giảm nghiêm trọng CPU và Device utilization.

#### Câu 4.3: Giải thuật định thời nào sau đây được chứng minh là TỐI ƯU NHẤT trong việc giảm thiểu Thời gian chờ trung bình (Average Waiting Time)?
A. FCFS.  
B. Shortest-Job-First (SJF).  
C. Round Robin với $q = 10$ ms.  
D. Priority Scheduling.  
- **Đáp án:** **B**  
- **Giải thích:** Định lý toán học đã chứng minh SJF (cả phiên bản preemptive SRTF và non-preemptive SJF) luôn cho Average Waiting Time nhỏ nhất so với bất kỳ giải thuật nào khác với cùng tập tiến trình.

#### Câu 4.4: Khi kích thước lát cắt thời gian (Time Quantum - $q$) trong giải thuật Round Robin tiến tới vô cùng ($q \to \infty$), giải thuật Round Robin sẽ hoạt động tương đương với giải thuật nào?
A. SJF.  
B. SRTF.  
C. Priority Scheduling.  
D. FCFS.  
- **Đáp án:** **D**  
- **Giải thích & Bẫy:** Nếu $q$ lớn hơn mọi burst time của các tiến trình, không có tiến trình nào bị ngắt timer giữa chừng. Do đó, tiến trình nào đến trước trong FIFO queue sẽ chạy cho đến khi kết thúc $\to$ biến thành **FCFS**. Ngược lại, nếu $q$ quá bé $\to$ Processor sharing (chuyển ngữ cảnh liên tục, overhead khổng lồ).

#### Câu 4.5: Trong hệ thống sử dụng Round Robin với $n$ tiến trình nằm trong Ready Queue và lát cắt thời gian là $q$, một tiến trình bất kỳ sẽ không phải chờ đợi quá bao lâu để nhận được phản hồi CPU đầu tiên?
A. $n \times q$  
B. $(n - 1) \times q$  
C. $(n + 1) \times q$  
D. $q / n$  
- **Đáp án:** **B**  
- **Giải thích:** Nếu một tiến trình vừa vào cuối Ready Queue gồm $n$ tiến trình, nó phải đợi tối đa $n - 1$ tiến trình xếp trước nó chạy hết mỗi tiến trình tối đa 1 lát cắt $q$. Do đó, thời gian chờ tối đa là: $\mathbf{(n - 1) \times q}$.

#### Câu 4.6: Điểm khác biệt CĂN BẢN NHẤT giữa Hàng đợi nhiều mức (Multilevel Queue - MQ) và Hàng đợi phản hồi nhiều mức (Multilevel Feedback Queue - MFQ) là:
A. MQ chỉ dùng cho CPU đơn lõi; MFQ dùng cho CPU đa lõi.  
B. MQ gán tiến trình cố định vào một hàng đợi duy nhất; MFQ cho phép tiến trình di chuyển linh hoạt giữa các hàng đợi khác nhau (hỗ trợ Aging).  
C. MQ hỗ trợ chế độ Preemptive; MFQ chỉ hỗ trợ Non-preemptive.  
D. MQ có thời gian đáp ứng nhanh hơn MFQ.  
- **Đáp án:** **B**  
- **Giải thích:** Trong Multilevel Queue thông thường, một tiến trình khi vào hệ thống sẽ được xếp vĩnh viễn vào một hàng đợi (VD: Foreground hoặc Background) và không thể đổi hàng đợi. Trong Multilevel Feedback Queue, tiến trình tiêu tốn quá nhiều CPU sẽ bị đẩy xuống hàng đợi thấp hơn; tiến trình chờ quá lâu ở hàng đợi thấp sẽ được nâng lên hàng đợi cao hơn (**cơ chế Aging** chống Starvation).

#### Câu 4.7: Trong giải thuật định thời Highest Response Ratio Next (HRRN), tỷ số phản hồi được tính bằng công thức $R = \frac{w + s}{s}$. Ưu điểm lớn nhất của giải thuật này là gì?
A. Là giải thuật trưng dụng (preemptive) nhanh nhất.  
B. Vừa ưu tiên các tiến trình ngắn (burst nhỏ), vừa giải quyết triệt để tình trạng đói tài nguyên (Starvation) cho các tiến trình dài khi thời gian chờ $w$ tăng lên.  
C. Không cần biết trước thời gian burst $s$.  
D. Có thời gian chuyển ngữ cảnh bằng 0.  
- **Đáp án:** **B**  
- **Giải thích:** Khi tiến trình mới vào, $w = 0 \to R = 1$, tiến trình ngắn ($s$ nhỏ) có $R$ lớn hơn sẽ được ưu tiên. Khi một tiến trình dài ($s$ lớn) phải chờ trong hàng đợi rất lâu, $w$ tăng dần làm cho $R$ tăng lên. Đến một thời điểm nào đó, $R$ của nó sẽ vượt qua các tiến trình mới đến và nó sẽ được chạy $\to$ Hoàn toàn loại bỏ Starvation!

#### Câu 4.8: Trên hệ thống đa xử lý đối xứng (SMP), thao tác Cân bằng tải (Load Balancing) di chuyển tiến trình từ CPU quá tải sang CPU rảnh rỗi sẽ gây ảnh hưởng tiêu cực trực tiếp đến tính chất nào?
A. Chu kỳ xung nhịp CPU.  
B. Tính chất Ái lực bộ xử lý (Processor Affinity).  
C. Không gian địa chỉ ảo của tiến trình.  
D. Tốc độ quay của ổ cứng.  
- **Đáp án:** **B**  
- **Giải thích & Bẫy:** Khi một tiến trình đang chạy trên CPU 0, dữ liệu của nó được cache đầy trong bộ nhớ đệm (L1/L2 Cache) của CPU 0 (Processor Affinity). Nếu cơ chế Load Balancing đẩy tiến trình này sang CPU 1, toàn bộ cache trên CPU 0 trở nên vô dụng và CPU 1 phải nạp lại dữ liệu từ RAM $\to$ Chi phí suy hao hiệu năng rất lớn.

#### Câu 4.9: Bộ định thời CFS (Completely Fair Scheduler) của Linux dựa trên cấu trúc dữ liệu nào và sử dụng tiêu chí nào để chọn tiến trình kế tiếp?
A. Hàng đợi FIFO; chọn tiến trình có PID nhỏ nhất.  
B. Cây Đỏ - Đen (Red-Black Tree); chọn tiến trình có thời gian chạy ảo (`vruntime`) nhỏ nhất.  
C. Bảng băm (Hash Table); chọn tiến trình có số lượng tiểu trình nhiều nhất.  
D. Ngăn xếp (LIFO Stack); chọn tiến trình vừa mới nạp vào.  
- **Đáp án:** **B**  
- **Giải thích:** Linux CFS theo dõi thời gian thực thi ảo `vruntime` của từng tác vụ và lưu vào Red-Black Tree. Nút ngoài cùng bên trái (leftmost node) của cây luôn chứa tác vụ có `vruntime` nhỏ nhất $\to$ CPU được cấp cho tác vụ này để đảm bảo tính công bằng.

---

## PHẦN B: CÂU HỎI TRẢ LỜI NGẮN / ĐIỀN KHUYẾT THUẬT NGỮ

1. Module của hệ điều hành chịu trách nhiệm trực tiếp trao quyền điều khiển CPU cho tiến trình được chọn bởi Short-term Scheduler được gọi là gì?  
   $\rightarrow$ **Trả lời:** `Dispatcher` (hoặc `Bộ phân phối`).
2. Kỹ thuật tăng dần độ ưu tiên của các tiến trình phải chờ đợi quá lâu trong hệ thống nhằm giải quyết hiện tượng Starvation được gọi là gì?  
   $\rightarrow$ **Trả lời:** `Aging` (hoặc `Lão hóa`).
3. Trong hệ điều hành Linux, giá trị dùng để điều chỉnh độ ưu tiên của một tiến trình trong khoảng từ -20 đến +19 được gọi là giá trị gì?  
   $\rightarrow$ **Trả lời:** `nice value` (hoặc `nice`).
4. Giải thuật định thời thời gian thực định kỳ nào gán độ ưu tiên tĩnh tỷ lệ nghịch với chu kỳ của tác vụ (chu kỳ càng ngắn độ ưu tiên càng cao)?  
   $\rightarrow$ **Trả lời:** `Rate Monotonic` (hoặc `RM`).
5. Nếu trong giải thuật Round Robin với quantum $q = 10$ ms, một tiến trình phải chờ tối đa là $150$ ms để nhận được phản hồi đầu tiên, hỏi có bao nhiêu tiến trình đang ở trong hàng đợi Ready?  
   $\rightarrow$ **Trả lời:** $16$ tiến trình (Áp dụng công thức: $(n - 1) \times 10 = 150 \Rightarrow n - 1 = 15 \Rightarrow n = 16$).

---

## PHẦN C: BÀI TẬP TỰ LUẬN ĐỊNH THỜI CPU (2.5 ĐIỂM TRONG ĐỀ THI)

### Đề bài tự luận tổng hợp:
Cho 5 tiến trình trong bảng sau:

| Tiến trình | Thời điểm đến ($AT$) | Thời gian thực thi ($BT$) | Độ ưu tiên ($Priority$) *(Số nhỏ = Ưu tiên cao)* |
| :---: | :---: | :---: | :---: |
| **P1** | 0 | 9 | 3 |
| **P2** | 2 | 4 | 1 |
| **P3** | 4 | 7 | 4 |
| **P4** | 5 | 3 | 2 |
| **P5** | 8 | 2 | 5 |

**Yêu cầu:**
1. Vẽ giản đồ Gantt và tính Thời gian chờ trung bình ($AWT$), Thời gian hoàn thành trung bình ($ATAT$), Thời gian đáp ứng trung bình ($ART$) cho giải thuật **SRTF** (SJF trưng dụng).
2. Vẽ giản đồ Gantt và tính toán các thông số trên cho giải thuật **Round Robin với Time Quantum $q = 4$**.
3. Vẽ giản đồ Gantt cho giải thuật **Định thời theo Độ ưu tiên có trưng dụng (Preemptive Priority Scheduling)**.

---

### HƯỚNG DẪN GIẢI CHI TIẾT:

---

### 1. Giải thuật SRTF (Shortest Remaining Time First)
- **Diễn biến từng mốc thời gian:**
  - $t = 0$: Chỉ có $P_1$ đến ($BT = 9$). $P_1$ chạy.
  - $t = 2$: $P_2$ đến với $BT = 4$. Lúc này $P_1$ đã chạy 2 đơn vị $\to$ còn lại $9 - 2 = 7$. Vì $BT(P_2) = 4 < 7 \to$ **$P_2$ trưng dụng CPU!** ($P_1$ về Ready).
  - $t = 4$: $P_3$ đến ($BT = 7$). $P_2$ còn lại $4 - (4-2) = 2 < 7 \to P_2$ tiếp tục chạy.
  - $t = 5$: $P_4$ đến ($BT = 3$). $P_2$ còn lại $1 < 3 \to P_2$ tiếp tục chạy.
  - $t = 6$: $P_2$ hoàn thành ($Finish = 6$). Ready queue gồm: $P_4$ (còn 3), $P_1$ (còn 7), $P_3$ (còn 7). Nhỏ nhất là $P_4$ ($BT=3$) $\to$ **$P_4$ được cấp CPU**.
  - $t = 8$: $P_5$ đến ($BT = 2$). Lúc này $P_4$ đã chạy từ $6 \to 8$ (2 đơn vị) $\to$ còn lại $3 - 2 = 1$. Vì $Remaining(P_4) = 1 < BT(P_5) = 2 \to$ **$P_4$ tiếp tục chạy, không bị trưng dụng!**
  - $t = 9$: $P_4$ hoàn thành ($Finish = 9$). Ready queue gồm: $P_5$ (2), $P_1$ (7), $P_3$ (7). Nhỏ nhất là $P_5$ (2) $\to$ **$P_5$ chạy từ $9 \to 11$**.
  - $t = 11$: $P_5$ hoàn thành ($Finish = 11$). Ready queue gồm: $P_1$ (7) và $P_3$ (7). Vì burst bằng nhau, ưu tiên tiến trình đến trước là $P_1$ $\to$ **$P_1$ chạy từ $11 \to 18$**.
  - $t = 18$: $P_1$ hoàn thành ($Finish = 18$). Cấp CPU cho $P_3$ $\to$ **$P_3$ chạy từ $18 \to 25$**.
  - $t = 25$: $P_3$ hoàn tất.

**Giản đồ Gantt (SRTF):**
```
|  P1  |   P2   |   P4   |  P5  |     P1     |      P3      |
0      2        6        9      11          18             25
```

**Bảng tổng hợp chỉ số SRTF:**

| Process | $AT$ | $BT$ | First CPU | Finish | $TAT = Finish - AT$ | $WT = TAT - BT$ | $RT = First - AT$ |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **P1** | 0 | 9 | 0 | 18 | $18 - 0 = \mathbf{18}$ | $18 - 9 = \mathbf{9}$ | $0 - 0 = \mathbf{0}$ |
| **P2** | 2 | 4 | 2 | 6 | $6 - 2 = \mathbf{4}$ | $4 - 4 = \mathbf{0}$ | $2 - 2 = \mathbf{0}$ |
| **P3** | 4 | 7 | 18 | 25 | $25 - 4 = \mathbf{21}$ | $21 - 7 = \mathbf{14}$ | $18 - 4 = \mathbf{14}$ |
| **P4** | 5 | 3 | 6 | 9 | $9 - 5 = \mathbf{4}$ | $4 - 3 = \mathbf{1}$ | $6 - 5 = \mathbf{1}$ |
| **P5** | 8 | 2 | 9 | 11 | $11 - 8 = \mathbf{3}$ | $3 - 2 = \mathbf{1}$ | $9 - 8 = \mathbf{1}$ |
| **Trung bình** | | | | | $\mathbf{10.00}$ | $\mathbf{5.00}$ | $\mathbf{3.20}$ |

- $ATAT = (18 + 4 + 21 + 4 + 3) / 5 = \mathbf{10.00}$
- $AWT = (9 + 0 + 14 + 1 + 1) / 5 = \mathbf{5.00}$
- $ART = (0 + 0 + 14 + 1 + 1) / 5 = \mathbf{3.20}$

---

### 2. Giải thuật Round Robin ($q = 4$)
- **Diễn biến hàng đợi Ready:**
  - $t = 0$: $P_1$ vào `Queue: [P1(9)]`. $P_1$ chạy 4 đơn vị ($0 \to 4$).
    - Tại $t=2$: $P_2$ đến; Tại $t=4$: $P_3$ đến.
  - $t = 4$: $P_1$ hết quantum (còn $9 - 4 = 5$). Thêm $P_2, P_3$ vào trước rồi mới đưa $P_1$ vào cuối:
    `Queue: [P2(4), P3(7), P1(5)]`.
  - $t = 4$: Lấy $P_2$ chạy 4 đơn vị ($4 \to 8$).
    - Tại $t=5$: $P_4$ đến; Tại $t=8$: $P_5$ đến.
  - $t = 8$: $P_2$ xong hoàn toàn ($Finish = 8$). Thêm $P_4, P_5$ vào cuối:
    `Queue: [P3(7), P1(5), P4(3), P5(2)]`.
  - $t = 8$: Lấy $P_3$ chạy 4 đơn vị ($8 \to 12$, còn lại 3).
  - $t = 12$: Đưa $P_3$ về cuối `Queue: [P1(5), P4(3), P5(2), P3(3)]`.
  - $t = 12$: Lấy $P_1$ chạy 4 đơn vị ($12 \to 16$, còn lại 1).
  - $t = 16$: Đưa $P_1$ về cuối `Queue: [P4(3), P5(2), P3(3), P1(1)]`.
  - $t = 16$: Lấy $P_4$ chạy 3 đơn vị ($16 \to 19$). $P_4$ xong ($Finish = 19$).
    `Queue: [P5(2), P3(3), P1(1)]`.
  - $t = 19$: Lấy $P_5$ chạy 2 đơn vị ($19 \to 21$). $P_5$ xong ($Finish = 21$).
    `Queue: [P3(3), P1(1)]`.
  - $t = 21$: Lấy $P_3$ chạy 3 đơn vị ($21 \to 24$). $P_3$ xong ($Finish = 24$).
    `Queue: [P1(1)]`.
  - $t = 24$: Lấy $P_1$ chạy nốt 1 đơn vị ($24 \to 25$). $P_1$ xong ($Finish = 25$).

**Giản đồ Gantt (Round Robin $q = 4$):**
```
|   P1   |   P2   |   P3   |   P1   |  P4  |  P5  |  P3  | P1 |
0        4        8        12       16     19     21     24   25
```

**Bảng tổng hợp chỉ số Round Robin ($q = 4$):**

| Process | $AT$ | $BT$ | First CPU | Finish | $TAT = Finish - AT$ | $WT = TAT - BT$ | $RT = First - AT$ |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **P1** | 0 | 9 | 0 | 25 | $25 - 0 = \mathbf{25}$ | $25 - 9 = \mathbf{16}$ | $0 - 0 = \mathbf{0}$ |
| **P2** | 2 | 4 | 4 | 8 | $8 - 2 = \mathbf{6}$ | $6 - 4 = \mathbf{2}$ | $4 - 2 = \mathbf{2}$ |
| **P3** | 4 | 7 | 8 | 24 | $24 - 4 = \mathbf{20}$ | $20 - 7 = \mathbf{13}$ | $8 - 4 = \mathbf{4}$ |
| **P4** | 5 | 3 | 16 | 19 | $19 - 5 = \mathbf{14}$ | $14 - 3 = \mathbf{11}$ | $16 - 5 = \mathbf{11}$ |
| **P5** | 8 | 2 | 19 | 21 | $21 - 8 = \mathbf{13}$ | $13 - 2 = \mathbf{11}$ | $19 - 8 = \mathbf{11}$ |
| **Trung bình** | | | | | $\mathbf{15.60}$ | $\mathbf{10.60}$ | $\mathbf{5.60}$ |

- $ATAT = (25 + 6 + 20 + 14 + 13) / 5 = \mathbf{15.60}$
- $AWT = (16 + 2 + 13 + 11 + 11) / 5 = \mathbf{10.60}$
- $ART = (0 + 2 + 4 + 11 + 11) / 5 = \mathbf{5.60}$

---

### 3. Giải thuật Định thời theo Độ ưu tiên có trưng dụng (Preemptive Priority)
*(Quy ước: Giá trị Priority càng nhỏ thì độ ưu tiên càng cao)*
- **Diễn biến:**
  - $t = 0$: $P_1$ đến ($Priority = 3$). $P_1$ chạy.
  - $t = 2$: $P_2$ đến ($Priority = 1 < 3$). Vì có độ ưu tiên cao hơn, **$P_2$ trưng dụng CPU ngay lập tức!**
  - $t = 4$: $P_3$ đến ($Priority = 4 > 1$). $P_2$ tiếp tục chạy.
  - $t = 5$: $P_4$ đến ($Priority = 2 > 1$). $P_2$ tiếp tục chạy.
  - $t = 6$: $P_2$ xong ($Finish = 6$). Trong Ready queue có: $P_4 (Prio=2)$, $P_1 (Prio=3)$, $P_3 (Prio=4)$. Chọn $P_4$ có ưu tiên cao nhất (2) $\to$ **$P_4$ chạy**.
  - $t = 8$: $P_5$ đến ($Priority = 5 > 2$). $P_4$ tiếp tục chạy.
  - $t = 9$: $P_4$ xong ($Finish = 9$). Còn lại: $P_1 (Prio=3)$, $P_3 (Prio=4)$, $P_5 (Prio=5)$. Chọn $P_1$ chạy tiếp 7 đơn vị còn lại $\to$ **$P_1$ chạy từ $9 \to 16$**.
  - $t = 16$: $P_1$ xong ($Finish = 16$). Chọn $P_3$ ($Prio=4$) $\to$ **$P_3$ chạy từ $16 \to 23$**.
  - $t = 23$: $P_3$ xong ($Finish = 23$). Chọn $P_5$ ($Prio=5$) $\to$ **$P_5$ chạy từ $23 \to 25$**.
  - $t = 25$: $P_5$ xong.

**Giản đồ Gantt (Preemptive Priority):**
```
|  P1  |   P2   |   P4   |     P1     |      P3      |  P5  |
0      2        6        9          16             23     25
```
