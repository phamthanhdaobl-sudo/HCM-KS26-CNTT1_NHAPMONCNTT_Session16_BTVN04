# HCM-KS26-CNTT1_NHAPMONCNTT_Session16_BTVN04
**Họ và tên:** Phạm Thành Đạo  
**Lớp:** HCM-KS26-CNTT1  
**Môn học:** Nhập môn Công nghệ thông tin  
**Bài:** Bài 4 – Tối ưu hóa Lưu trữ Dữ liệu Doanh nghiệp

---

# PHẦN 1 – PHÂN TÍCH VẤN ĐỀ

## 1.1. Hiện trạng hệ thống

Nhóm đang quản lý khoảng 500GB dữ liệu video giám sát tại khuôn viên trường học (Campus), trong khi dung lượng SSD trên laptop của mỗi thành viên chỉ có 256GB.

Điều này gây ra một số vấn đề:

- **Thiếu dung lượng lưu trữ:** 500GB dữ liệu lớn gần gấp đôi dung lượng SSD 256GB.
- **Hiệu suất máy tính giảm:** Nếu tải toàn bộ video về máy, ổ cứng có thể bị đầy, khiến hệ điều hành và phần mềm hoạt động chậm.
- **Đồng bộ quá tải:** Việc tải đồng thời nhiều video dung lượng lớn gây tiêu tốn băng thông Internet và tài nguyên hệ thống.
- **Khó quản lý dữ liệu:** Các thành viên không cần sử dụng toàn bộ video nhưng vẫn phải lưu trữ nếu đồng bộ theo cách truyền thống.

## 1.2. Giải pháp đề xuất

Sử dụng mô hình **Cloud Storage kết hợp Files On-Demand** để tối ưu dung lượng lưu trữ.

Trong mô hình này:

- Dữ liệu video được lưu trữ tập trung trên Cloud.
- Laptop chỉ hiển thị danh sách file và thư mục thông qua các tệp đại diện (Placeholder).
- Khi thành viên cần xem một video cụ thể, hệ thống mới tải nội dung video đó xuống thiết bị.
- Những file đã tải nhưng không còn sử dụng có thể chuyển về trạng thái Online-only để giải phóng dung lượng SSD.

**Mục tiêu:** Giúp nhóm truy cập được 500GB dữ liệu trên Cloud mà không cần sở hữu ổ cứng 500GB trên từng laptop.

---

# PHẦN 2 – GIẢI PHÁP KỸ THUẬT: FILES ON-DEMAND

## 2.1. Khái niệm Files On-Demand

**Files On-Demand (Tệp theo yêu cầu)** là tính năng cho phép người dùng xem và quản lý các tệp lưu trữ trên Cloud ngay trong trình quản lý file của máy tính mà không cần tải toàn bộ nội dung về thiết bị.

Tính năng này giúp tiết kiệm dung lượng ổ cứng Local SSD bằng cách chỉ tải xuống những dữ liệu thực sự cần sử dụng.

## 2.2. Ba trạng thái lưu trữ của Files On-Demand

Files On-Demand thường có ba trạng thái chính:

### Trạng thái 1: Online-only (Chỉ trực tuyến)

- File được lưu trên Cloud.
- Trên laptop chỉ hiển thị biểu tượng hoặc tệp đại diện.
- Hầu như không chiếm dung lượng nội dung trên SSD.
- Khi mở file, hệ thống cần kết nối Internet để tải dữ liệu về.

**Ví dụ:** Video giám sát ngày 01/10 được lưu trên Cloud nhưng thành viên chưa cần xem nên không tải xuống laptop.

### Trạng thái 2: Locally available (Có sẵn trên thiết bị)

- File đã được tải xuống và có bản lưu trên laptop.
- Người dùng có thể mở file khi không có Internet.
- File vẫn được quản lý và đồng bộ với Cloud.
- Chiếm dung lượng SSD theo kích thước thực tế của dữ liệu.

**Ví dụ:** Thành viên tải video giám sát ngày 02/10 về để kiểm tra một sự cố tại bãi đỗ xe.

### Trạng thái 3: Always keep on this device (Luôn giữ trên thiết bị này)

- File được tải xuống và ưu tiên giữ lại trên laptop.
- Người dùng có thể truy cập file ngay cả khi mất kết nối Internet.
- File không tự động bị giải phóng dung lượng theo cơ chế Files On-Demand thông thường.

**Ví dụ:** Nhóm chọn giữ một số video quan trọng phục vụ báo cáo và thuyết trình cuối kỳ.

## 2.3. Quy trình thiết lập Files On-Demand

Nhóm có thể triển khai trên Microsoft OneDrive hoặc Google Drive bằng chế độ lưu trữ trực tuyến tương ứng.

### A. Thiết lập trên Microsoft OneDrive (Windows)

**Bước 1: Cài đặt và đăng nhập OneDrive**

- Cài đặt ứng dụng Microsoft OneDrive.
- Đăng nhập tài khoản doanh nghiệp hoặc tài khoản được nhóm cấp quyền.
- Kiểm tra biểu tượng OneDrive trên thanh Taskbar.

**Bước 2: Bật Files On-Demand**

- Nhấn biểu tượng OneDrive trên Taskbar.
- Chọn Settings (Cài đặt).
- Truy cập mục Sync and backup hoặc Advanced settings tùy phiên bản.
- Bật tính năng Files On-Demand.

**Bước 3: Kiểm tra trạng thái lưu trữ**

- Mở File Explorer.
- Truy cập thư mục OneDrive.
- Kiểm tra biểu tượng trạng thái của các file.
- Đảm bảo các file không cần sử dụng đang ở trạng thái Online-only.

### B. Thiết lập trên Google Drive (macOS hoặc Windows)

- Cài đặt Google Drive for Desktop.
- Đăng nhập tài khoản nhóm.
- Mở Preferences (Tùy chọn).
- Chọn chế độ **Stream files** thay vì Mirror files.
- Truy cập thư mục Google Drive trong Finder hoặc File Explorer để xem dữ liệu.

**Lý do chọn Stream files:**

- Dữ liệu được lưu chủ yếu trên Cloud.
- Laptop không phải tải toàn bộ 500GB video.
- Người dùng có thể mở file khi cần và tải nội dung về thiết bị.
- Phù hợp với laptop có dung lượng SSD hạn chế.

*Lưu ý: Tên tùy chọn và giao diện có thể khác nhau theo hệ điều hành và phiên bản ứng dụng. Files On-Demand của OneDrive và Stream files của Google Drive là hai cách triển khai tương tự về mục tiêu, không phải cùng một tính năng.*

---

# PHẦN 3 – GIẢI QUYẾT BẪY DỮ LIỆU: ĐỒNG BỘ VIDEO DUNG LƯỢNG LỚN

## 3.1. Vấn đề nghẽn băng thông Internet

500GB video là một lượng dữ liệu rất lớn. Nếu nhóm tải lên Cloud với tốc độ tối đa trong thời gian dài, đường truyền Internet của nhà trọ có thể bị chiếm dụng, ảnh hưởng đến việc học tập và sinh hoạt của những người khác.

**Giải pháp: Giới hạn tốc độ Upload (Bandwidth Throttling).**

Các bước thực hiện:

1. Mở ứng dụng Cloud Drive đang sử dụng.
2. Truy cập Settings hoặc Preferences.
3. Tìm mục Network hoặc Bandwidth.
4. Chọn giới hạn tốc độ Upload thay vì sử dụng toàn bộ băng thông.
5. Thiết lập tốc độ tải lên phù hợp với đường truyền Internet.

**Ví dụ:**

Nếu đường truyền Upload đạt 20Mbps, nhóm có thể giới hạn tốc độ đồng bộ ở mức khoảng 12–15Mbps.

Điều này giúp:
- Dành lại một phần băng thông cho những người khác.
- Hạn chế tình trạng mạng bị chậm hoặc mất kết nối.
- Giúp quá trình tải dữ liệu ổn định hơn.

## 3.2. Đồng bộ theo từng đợt (Batch Upload)

Không nên tải toàn bộ 500GB video cùng một thời điểm.

Nhóm nên chia dữ liệu thành các đợt:

| Đợt | Dữ liệu đồng bộ | Thời gian đề xuất |
|---|---|---|
| Đợt 1 | Video giám sát quan trọng | Ngày 1 |
| Đợt 2 | Video giám sát tuần gần nhất | Ngày 2 |
| Đợt 3 | Video của các tuần trước | Ngày 3 |
| Đợt 4 | Dữ liệu còn lại và kiểm tra | Ngày 4 |

**Lợi ích:**

- Giảm tải cho đường truyền Internet.
- Dễ kiểm tra dữ liệu đã đồng bộ.
- Nếu gặp lỗi, chỉ cần xử lý phần dữ liệu của đợt đó.
- Tránh tạo quá nhiều tác vụ tải lên cùng lúc.

## 3.3. Giải quyết tình trạng gián đoạn khi gập laptop

Một sai lầm thường gặp là nghĩ rằng chỉ cần bật đồng bộ thì laptop sẽ tiếp tục tải dữ liệu ngay cả khi gập máy.

Trên thực tế, khi gập laptop, thiết bị thường chuyển sang chế độ Sleep hoặc Standby, khiến quá trình đồng bộ bị tạm dừng.

**Giải pháp:**

1. Kết nối laptop với nguồn điện trong suốt quá trình tải dữ liệu lớn.
2. Thiết lập chế độ không tự động Sleep khi đang cắm sạc và thực hiện đồng bộ.
3. Giữ ứng dụng Cloud Drive hoạt động.
4. Đặt laptop ở vị trí thoáng mát, tránh quá nhiệt.
5. Không gập máy nếu thiết bị được thiết lập để chuyển sang Sleep khi đóng nắp.
6. Nếu quá trình đồng bộ bị ngắt, mở lại laptop và ứng dụng để tiếp tục tải lên.

**Lưu ý:** Không nên tắt hoặc ngắt kết nối ứng dụng đồng bộ giữa chừng nếu không cần thiết. Nên sử dụng ứng dụng Cloud có hỗ trợ tiếp tục tải lên (Resume/Resumable Upload) để tránh phải tải lại toàn bộ dữ liệu khi mất mạng.

## 3.4. Giải pháp tổng thể

Nhóm áp dụng quy trình sau:

```text
DỮ LIỆU VIDEO 500GB
        |
        v
PHÂN LOẠI DỮ LIỆU
        |
        v
CHIA THÀNH CÁC ĐỢT UPLOAD
        |
        v
GIỚI HẠN BĂNG THÔNG UPLOAD
        |
        v
ĐỒNG BỘ LÊN CLOUD
        |
        v
KIỂM TRA DỮ LIỆU ĐÃ TẢI LÊN
        |
        v
FILES ON-DEMAND / STREAM FILES
        |
        v
LAPTOP CHỈ TẢI FILE KHI CẦN
        |
        v
TIẾT KIỆM DUNG LƯỢNG SSD
```

**Kết luận:** Kết hợp Upload theo từng đợt, giới hạn băng thông và cơ chế tiếp tục tải lên giúp quá trình đồng bộ 500GB dữ liệu ổn định hơn, hạn chế ảnh hưởng đến Internet và tránh mất tiến trình khi bị gián đoạn.

---

# PHẦN 4 – BÁO CÁO DUNG LƯỢNG VÀ CHỨNG MINH HIỆU QUẢ

## 4.1. Dữ liệu đầu vào

Giả sử nhóm có các thông số:

| Thông số | Dung lượng |
|---|---:|
| Tổng dữ liệu video trên Cloud | 500GB |
| Dung lượng SSD laptop | 256GB |
| Dung lượng hệ điều hành và ứng dụng | 100GB |
| Dung lượng còn trống ban đầu | 156GB |

## 4.2. Trường hợp 1: Đồng bộ toàn bộ dữ liệu về laptop

Nếu nhóm sử dụng chế độ tải toàn bộ dữ liệu về máy:

- Dữ liệu video: 500GB.
- SSD laptop: 256GB.

Ta có:

500GB > 256GB

Như vậy, chỉ riêng dữ liệu video đã vượt quá dung lượng SSD của laptop.

Nếu tính thêm 100GB dành cho hệ điều hành và ứng dụng:

500GB + 100GB = 600GB

Trong khi laptop chỉ có 256GB SSD.

**Kết luận:** Không thể lưu trữ toàn bộ dữ liệu video trên laptop này.

## 4.3. Trường hợp 2: Sử dụng Files On-Demand

Giả sử nhóm áp dụng Files On-Demand với phương án:

- Tổng dữ liệu trên Cloud: 500GB.
- Dữ liệu tải thực tế về laptop: 20GB.
- Dung lượng hệ điều hành và ứng dụng: 100GB.

Tổng dung lượng sử dụng:

100GB + 20GB = 120GB

Dung lượng còn trống:

256GB - 120GB = 136GB

Như vậy, laptop vẫn còn 136GB dung lượng trống để sử dụng cho những công việc khác.

## 4.4. Bảng so sánh hiệu quả

| Tiêu chí | Đồng bộ toàn bộ | Files On-Demand |
|---|---:|---:|
| Dữ liệu trên Cloud | 500GB | 500GB |
| Dữ liệu video lưu trên SSD | 500GB | 20GB |
| Hệ điều hành và ứng dụng | 100GB | 100GB |
| Tổng dung lượng cần thiết | 600GB | 120GB |
| Dung lượng SSD | 256GB | 256GB |
| Kết quả | Không đủ dung lượng | Đủ dung lượng |

## 4.5. Tính toán phần trăm tiết kiệm

Dung lượng tiết kiệm được:

500GB - 20GB = 480GB

Tỷ lệ tiết kiệm:

(480 / 500) × 100% = 96%

**Kết quả:** Files On-Demand giúp giảm khoảng 96% dung lượng lưu trữ video trên laptop trong ví dụ này.

Ngoài ra:

- Tổng dữ liệu Cloud lớn gấp khoảng 1,95 lần dung lượng SSD.
- Tổng dữ liệu Cloud lớn gấp 3,2 lần dung lượng SSD còn trống ban đầu.

Điều này chứng minh rằng dung lượng Cloud có thể lớn hơn đáng kể so với dung lượng ổ cứng vật lý của từng thành viên.

*Lưu ý: Đây là số liệu giả định để minh họa hiệu quả. Dung lượng thực tế có thể thay đổi tùy số lượng video được mở, bộ nhớ đệm và các file được chọn giữ ngoại tuyến.*

---

# PHẦN 5 – QUẢN LÝ VÒNG ĐỜI DỮ LIỆU TRÊN CLOUD

Để quản lý 500GB video giám sát lâu dài, nhóm cần xây dựng quy trình quản lý vòng đời dữ liệu (Data Lifecycle Management).

## 5.1. Các giai đoạn quản lý dữ liệu

**Giai đoạn 1: Data Creation – Tạo dữ liệu**

- Camera ghi hình và tạo video giám sát.
- Video được phân loại theo ngày, tháng và khu vực.
- Đặt tên file thống nhất để thuận tiện tìm kiếm.

**Giai đoạn 2: Data Storage – Lưu trữ dữ liệu**

- Đồng bộ dữ liệu lên Cloud Workspace.
- Phân chia thư mục theo khu vực giám sát.
- Phân quyền truy cập theo nhiệm vụ của từng thành viên.

**Giai đoạn 3: Data Usage – Sử dụng dữ liệu**

- Thành viên truy cập video thông qua Files On-Demand.
- Chỉ tải xuống các video thực sự cần kiểm tra.
- Những video quan trọng có thể được giữ ngoại tuyến trong thời gian xử lý.

**Giai đoạn 4: Data Archiving – Lưu trữ lâu dài**

- Chuyển các video cũ, ít sử dụng sang khu vực lưu trữ phù hợp.
- Sử dụng các gói lưu trữ dài hạn hoặc Archive Storage nếu nhà cung cấp hỗ trợ.
- Hạn chế tải các dữ liệu lưu trữ lâu dài về laptop.

**Giai đoạn 5: Data Deletion – Xóa dữ liệu**

- Xác định các video đã hết thời hạn lưu trữ.
- Kiểm tra yêu cầu bảo quản dữ liệu trước khi xóa.
- Xóa dữ liệu không còn giá trị sử dụng theo chính sách của doanh nghiệp.
- Kiểm tra thùng rác và quy định xóa vĩnh viễn của nhà cung cấp Cloud.

## 5.2. Quy định quản lý dữ liệu

Nhóm thống nhất một số nguyên tắc:

1. Không lưu trữ video không cần thiết trên laptop cá nhân.
2. Không tự ý xóa video giám sát khi chưa có sự đồng ý của người phụ trách.
3. Phân quyền truy cập phù hợp với vai trò của từng thành viên.
4. Kiểm tra định kỳ tình trạng đồng bộ và dung lượng Cloud.
5. Thiết lập thời hạn lưu trữ dựa trên yêu cầu của dự án và quy định bảo vệ dữ liệu.
6. Dữ liệu quan trọng cần có phương án sao lưu độc lập, không phụ thuộc hoàn toàn vào một bản Cloud duy nhất.

---

# PHẦN 6 – KẾT LUẬN

Qua bài tập Tối ưu hóa Lưu trữ Dữ liệu Doanh nghiệp, em hiểu rằng việc quản lý dữ liệu trên Cloud không chỉ đơn giản là tải file lên Internet mà còn cần tối ưu cách sử dụng dung lượng và xây dựng quy trình lưu trữ lâu dài.

Các kiến thức quan trọng được vận dụng:

- **Files On-Demand:** Cho phép truy cập dữ liệu Cloud mà không cần tải toàn bộ về laptop.
- **Online-only:** Tiết kiệm dung lượng ổ cứng bằng cách chỉ lưu tệp đại diện trên thiết bị.
- **Locally available:** Lưu file trên thiết bị để sử dụng khi cần.
- **Bandwidth Throttling:** Giới hạn tốc độ Upload để tránh nghẽn mạng.
- **Batch Upload:** Chia dữ liệu thành nhiều đợt để đồng bộ ổn định.
- **Data Lifecycle Management:** Quản lý dữ liệu từ khi tạo ra đến khi lưu trữ hoặc xóa bỏ.

**Kết luận chung:** Việc kết hợp Cloud Storage và Files On-Demand giúp nhóm quản lý 500GB dữ liệu video trên những laptop chỉ có 256GB SSD mà không cần tải toàn bộ dữ liệu về máy. Giải pháp này vừa tiết kiệm dung lượng lưu trữ, vừa nâng cao hiệu quả làm việc và giúp doanh nghiệp quản lý dữ liệu bền vững hơn.
