# Design code
module up_counter ( input wire clk, // Clock input input wire rst, // Reset input output wire [3:0] count // 4-bit counter output );

reg [3:0] count_reg;  // 4-bit counter register

always @(posedge clk or posedge rst) begin
    if (rst) begin
        count_reg <= 4'b0000;  // Reset the counter
    end else begin
        count_reg <= count_reg + 1;  // Increment the counter
    end
end

assign count = count_reg;  // Output is the value in the register
endmodule


# testbench
module tb_up_counter;

reg clk;
reg rst;
wire [3:0] count;

// Instantiate the up_counter module
up_counter uut (
    .clk(clk),
    .rst(rst),
    .count(count)
);

// Clock generation
always begin
    #5 clk = ~clk;
end

// Initialize signals
initial begin
    clk = 0;
    rst = 0;

    // Reset the counter
    rst = 1;
    #10 rst = 0;

    // Monitor the count
    $monitor("Time=%0t count=%h", $time, count);
end

// Simulate for some time
initial begin
    #50 $finish;
end
endmodule
![20231120_202843_0009](https://github.com/SWASTHI12/Layered_testbench/assets/131871466/8e8c2a09-b9b4-4ef7-98ea-f60cccb48e8f)
![20231120_202843_0010](https://github.com/SWASTHI12/Layered_testbench/assets/131871466/a34cda90-5e79-41f6-b69a-f911b31a34d7)
