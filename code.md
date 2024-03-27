# Verilog Code

### Code 4-1
```verilog
module test_module (sum, c_out, a, b);
	input a,b;
	output c_out, sum;
	xor (sum,a,b);
	and (c_out,a,b);
endmodule
```

Result:

<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/dd889817-bc48-4ccf-b365-b8e2033ee09a" height="140">

### Code 4-2
```verilog
module test_module (y_out,x_in1,x_in2,x_in3,x_in4,x_in5);
	output y_out;
	input x_in1,x_in2,x_in3,x_in4,x_in5;
	wire y1,y2;
	nor (y_out,y1,y2);
	and (y1,x_in1,x_in2);
	and (y2,x_in3,x_in4,x_in5);
endmodule
```

Result:

<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/3616d0a3-bcef-400f-8993-f2515ed863e0" height="140">

### Code 4-3
```verilog
// add_full_0_delay
module test_module (sum,c_out,a,b,c_in);
	input a,b,c_in;
	output sum,c_out;
	wire w1,w2,w3;
	add_half_0_delay M1(w1,w2,a,b);
	add_half_0_delay M2(sum,w3,c_in,w1);
	or(c_out,w2,w3);
endmodule

module add_half_0_delay (sum, c_out, a, b);
	input a,b;
	output c_out, sum;
	xor (sum,a,b);
	and (c_out,a,b);
endmodule
```

Result:

<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/9b00b6d1-6acd-485c-8456-a0ba57a398f3" height="140">

### Code 4-4
```verilog
// add_rca_16_0_delay
module test_module (sum,c_out,a,b,c_in);
	output [15:0] sum;
	output c_out;
	input [15:0] a,b;
	input c_in;
	wire c_in4, c_in8, c_in12, c_out;
	add_rca_4 M1(sum[3:0],c_in4,a[3:0],b[3:0],c_in);
	add_rca_4 M2(sum[7:4],c_in8,a[7:4],b[7:4],c_in4);
	add_rca_4 M3(sum[11:8],c_in12,a[11:8],b[11:8],c_in8);
	add_rca_4 M4(sum[15:12],c_out,a[15:12],b[15:12],c_in12);
endmodule

module add_rca_4(sum,c_out,a,b,c_in);
	output [3:0] sum;
	output c_out;
	input [3:0] a,b;
	input c_in;
	wire c_in2,c_in3,c_in4;
	add_full_0_delay M1(sum[0],c_in2,a[0],b[0],c_in);
	add_full_0_delay M2(sum[1],c_in3,a[1],b[1],c_in2);
	add_full_0_delay M3(sum[2],c_in4,a[2],b[2],c_in3);
	add_full_0_delay M4(sum[3],c_out,a[3],b[3],c_in4);
endmodule

module add_full_0_delay (sum,c_out,a,b,c_in);
	input a,b,c_in;
	output sum,c_out;
	wire w1,w2,w3;
	add_half_0_delay M1(w1,w2,a,b);
	add_half_0_delay M2(sum,w3,c_in,w1);
	or(c_out,w2,w3);
endmodule

module add_half_0_delay (sum, c_out, a, b);
	input a,b;
	output c_out, sum;
	xor (sum,a,b);
	and (c_out,a,b);
endmodule
```

Result:

<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/f1ba077a-be2d-4da0-a204-d6569219b200" height="200">

<img src="https://github.com/HaiHoangCN/Advanced_Verilog_HDL/assets/51068749/8c5b6a68-b018-45c0-9b08-39088698ca02" height="400">

### Code 4-5
```verilog

```

Result:

<img src="" height="140">
