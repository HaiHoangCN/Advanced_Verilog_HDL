# 2024-03-30-Course_Digital_IC: Week 5 - Đồng hồ thế kỉ

Các phép toán cộng trừ, AND, OR, NOT được dùng. Hạn chế tối đa bộ phép nhân

## 1.1 - SPEC
<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/352c81e5-583b-421e-b7a0-becc5cf09eda" height="250">

| TT  | Trường hợp  | Trạng thái  | Đầu ra  |
|---|---|---|---|
| 1  | rst_n = 0  | Tất cả các biến s, mi, h, d, mo, y = 0  | led_s = 00 (abcdefg = 0000001, abcdefg = 0000001),<br> led_mi = 00,<br> led_h = 00,<br> led_d = 00,<br> led_mo = 00,<br> led_y = 00|
| 2  | rst_n = 1,<br> rising_edge clk  | cnt = cnt + 1.<br> if (cnt == 5e7) s = s + 1.<br> if (s == 60) mi = mi + 1; s = 0.<br> if (mi == 60) h = h + 1; mi = 0.<br> if (h == 24) d = d + 1; h = 0...  |   |
|   |   |   |   |

## 1.2 - Kiến trúc
- Các khối chức năng
- SPEC của các khối
- Cách các khối kết nối và trao đổi thông tin

Các khối:
- Tạo xung 1s
- Đếm s, mi, h, d, mo, y
- Điều khiển LED

<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/6348a952-8a8b-4976-8e68-71338292a423" height="400">

Có 2 cách count:
- Cách 1: Count binary s 0 -> 60 cần 6 bits (tương tự với mi, h, d, mo, y)
- Cách 2: BCD

Lựa chọn thiết kế kiến trúc số 1: Các bộ đếm cnt_s, cnt_mi,... là đếm nhị phân -> led_s,... là bộ giải mã binary to led7seg<br>
Spec của led_s:
| TT  | Bin  | 7seg
|---|---|---|
| 0  | 000000  | 00  |
| 1  | 000001  | 01  |
| 2  | 000010  | 02  |
| ...  |   |   |
| 59  | 111011  | 59  |

Lựa chọn thiết kế kiến trúc số 2: Các bộ đếm cnt_s, cnt_mi,... là đếm BCD<br>
Spec của cnt_s là:
| TT  | rising_clk  | pulse_1s  | cnt_s  |
|---|---|---|---|
| 0  | NO  | x  | cnt_s = cnt_s  |
| 1  | YES  | 0  | cnt_s = cnt_s  |
| 2  | YES  | 1  | cnt_s[3:0] = cnt_s[3:0] + 1<br> if(cnt_s[3:0] == 10)<br> {<br> cnt_s[3:0] = 0;<br> cnt_s[7:4] = cnt_s[7:4] + 1;<br> }<br> if...  |

Dùng cách 1 hoặc 2. Thì phải viết code cả 2 để xem cái nào tốt nhất

**BTVN1: (Từ bây giờ cho đến chiều nay 3/30/2024)**
- Code bằng cả 2 cách
- Viết báo cáo

**Chú ý:**
- 1 driver duy nhất trong 1 khối always thôi.
- 1 khối module chỉ có duy nhất 1 always
- Đồng bộ hết, TRỪ rst_n là không bị ảnh hưởng bởi đồng hồ.

```verilog
module millenium_clock
(
input clk_50MHz,
input rst_n,
input set_s, set_mi, set_h, set_d, set_mo, set_y,
output [13:0] led_s,
output [13:0] led_mi,
...
);

endmodule

module gen_pulse_1s
(
input clk_50MHz,
input rst_n,
output pulse_1s
);

reg [25:0] cnt;
always @(posedge clk or negedge rst_n)
begin
  if (~rst_n)
  begin
    cnt <= 0;
    pulse_1s <= 0;
  end
  else if (cnt == 5000000)
  begin
    ...
  end
  ...
end

endmodule

module cnt_s
(
input clk_50MHz,
input rst_n,
input pulse_1s,
input set_s,
output reg [6:0] cnt_s,
output reg pulse_1mi
);

always @(posedge clk or negedge rst_n)
begin
  if (~rst_n) begin cnt <= 0; pulse_1mi <= 0; end
  else
    if (cnt_s == 60) begin cnt_s <= 0; pulse_1mi <= 1; end
    else if (set_s) begin cnt_s <= cnt_s + 1; pulse_1mi <= 0; end
    else if (pulse_1s) begin cnt_s <= cnt_s + 1; pulse_1mi <= 0; end
    else begin cnt_s <= cnt_s; pulse_1mi <= 0; end
end

endmodule
```

**Đề cũ - Bỏ**<br>
<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/1a968fa8-8a60-479e-bb0a-0543c12d169f" height="250">

**Chú ý Midterm:**
- 8 dải tần thì dùng 8 bộ lọc
- Được dùng bất cứ bộ lọc gì cx được
- Điều khiển bộ lọc ntn thì giống count. Khi bấm set thì gain tương ứng +1 (từ 0 - 99)
- Độ trễ nhỏ nhất
- Hiện tại ko cần FPGA, chỉ cần mô phỏng. Tín hiệu âm thanh gen. bằng MATLAB/Python (TH) và viết tb để đọc file âm thanh. Dùng Python convert âm thanh to text. Vẽ đồ thị phổ bảng Python
- Code Python làm equalizer và mn chỉ cần chứng minh code Verilog giống code Python này. 
- Tuần sau các nhóm sẽ phải trình bày thiết kế Equaliser có đúng 10p. Bắt đầu sớm. Trình bày kiến trúc, kết quả..., kết quả mô phỏng...
- Một số tài liệu: https://community.nxp.com/pwmxy87654/attachments/pwmxy87654/imx-processors%40tkb/5738/1/i.MX8X%20DSP%20SOF%20IIR_FIR%20EQ%20Basic%20Theory.pdf

**Anh Nam sẽ hướng dẫn mọi người login vào Cadence của LAB. Thầy Minh sẽ hướng dẫn sau.**
- Tailscale: Tạo ra một mảng ảo, sau khi có thì dùng SSH đăng nhập vào, BMC để -> vào được server đã cài sẵn server.
- 10 người cùng vào thì chia thành 10 users khác nhau.
- 18 nhóm thì user từ 1 đến 18. Nhưng ko đủ tài nguyên thì phải đặt lịch.
- Sang nữa kỳ sau thì phải học phần tổng hợp. Phải thực hành trên user.
- RTl ra Netlist > Floor Planning Placement and Routing > Verify Timing, Power (kiểm tra hợp lệ)
- Tài liệu link về bài Cadence đã gửi thầy. Sẽ có hướng dẫn chi tiết + có cả bài lab trước của anh.

**BTVN2: (Từ bây giờ đến 11h30 3/30/2024)**
Phải login vào server.
