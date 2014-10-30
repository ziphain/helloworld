module stimulus;

	parameter period = 10;
	parameter delay = 1;
	parameter fsdb = "elevator";

	reg clk, rst_n;
	reg u1, u2, d2, d3, f1, f2, f3;
	
	wire [1:0] direction;
	wire open;
	wire [1:0] floor;


	always #(period/2) clk = ~clk;


	ELEVATOR elevator(
		.CLK(clk),
		.RST_N(rst_n),
		.U1(u1),
		.U2(u2),
		.D2(d2),
		.D3(d3),
		.F1(f1),
		.F2(f2),
		.F3(f3),
		.Direction(direction),
		.Open(open),
		.Floor(floor)
	);
	
	initial begin
		$fsdbDumpfile("elevator.fsdb");
		$fsdbDumpvars;

		/*$monitor($time, " CLK=%b RST_N=%b,U1=%b U2=%b D2=%b D3=%b F1=%b F2=%b F3=%b | Direction=%b Open=%b Floor=%b",
		clk, rst_n, u1, u2, d2, d3, f1, f2, f3, direction, open, floor);*/
	end
	
	
	initial begin	
		clk = 0;
		rst_n = 1;
		#(delay) rst_n = 0;
		#(period) rst_n = 1;

		$display("");
		$display("Now@1F, Press 2F up button -> 2F, (up/hold)");
		pattern(7'b0100000);
		#(period*10);
		
		$display("");
		$display("Now@2F, Press 2F button to open the door -> 2F, (up/hold)");
		pattern(7'b0000010);
		#(period*10);
		
		$display("");
		$display("Now@2F, Press 3F button -> 3F, hold");
		pattern(7'b0000001);
		#(period*10);
		
		$display("");
		$display("Now@3F, Press 2F up and down buttons -> 2F, (up/down/hold), open two times");
		pattern(7'b0110000);
		#(period*10);
		
		$display("");
		$display("Now@2F, Press 1F up button -> 1F, hold");
		pattern(7'b1000000);
		#(period*10);
		
		$display("");
		$display("Now@1F, Press 3F button -> 3F, hold");
		pattern(7'b0000001);
		#(period*10);
		
		$display("");
		$display("Now@3F, Press 1F and 3F down buttons -> 1F, (up/hold), 3F, hold");
		pattern(7'b0000100);
		pattern(7'b0001000);
		#(period*10);
		
		
		$display("");
		$display("Now@3F, Press 1F up button -> 1F, hold");
		pattern(7'b1000000);
		#(period*10);
		
		$display("");
		$display("Now@1F, Press all buttons -> 1F, 2F, 3F, 2F");
		pattern(7'b1111000);
		pattern(7'b0000111);
		#(period*10);
		
		
	/*	
		pattern(7'b0000001);
		#(period*5);
		pattern(7'b1111010);
    */
	
		#(period*20) $finish;
		
	end
	
	always @ (posedge clk)
	begin
		if(open) $display("direction=%b floor=%b" ,direction,floor);
	end

	task pattern;
		input [6:0] Button;
		begin
			//#(delay);
			{u1,u2,d2,d3,f1,f2,f3} = Button[6:0];
			/*u1 = Button[6];
			u2 = Button[5];
			d2 = Button[4];
			d3 = Button[3];
			f1 = Button[2];
			f2 = Button[1];
			f3 = Button[0];*/
			#(period);
			{u1,u2,d2,d3,f1,f2,f3} = 6'b0;
			
		end
	endtask
	
	
	
endmodule	