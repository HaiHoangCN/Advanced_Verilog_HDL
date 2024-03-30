# 2024-03-30-Course_Digital_IC
# Week 5 - Đồng hồ thế kỉ

Các phép toán cộng trừ, AND, OR, NOT được dùng. Hạn chế tối đa bộ phép nhân

## 1.1 - SPEC
![image](https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/352c81e5-583b-421e-b7a0-becc5cf09eda)

| TT  | Trường hợp  | Trạng thái  | Đầu ra  |
|---|---|---|---|
| 1  | rst_n = 0  | Tất cả các biến s, mi, h, d, mo, y = 0  | led_s = 00 (abcdefg = 0000001, abcdefg = 0000001),<br> led_mi = 00,<br> led_h = 00,<br> led_d = 00,<br> led_mo = 00,<br> led_y = 00|
| 2  | rst_n = 1,<br> rising_edge clk  | cnt = cnt + 1.<br> if (cnt == 5e7) s = s + 1.<br> if (s == 60) mi = mi + 1; s = 0.<br> if (mi == 60) h = h + 1; mi = 0.<br> if (h == 24) d = d + 1; h = 0...  |   |
|   |   |   |   |

## 1.2 - Kiến trúc
- Các khối chức năng
- SPEC của các khối
- Cách các khối kết nối và trao đổi thông tin
