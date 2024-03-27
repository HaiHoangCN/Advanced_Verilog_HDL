# Verilog Code

```verilog
module test_module (sum, c_out, a, b);
	input a,b;
	output c_out, sum;
	xor (sum,a,b);
	and (c_out,a,b);
endmodule
```
