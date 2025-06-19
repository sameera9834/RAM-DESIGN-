# RAM-DESIGN-module sync_ram #(
    parameter DATA_WIDTH = 8,  // Width of each memory word (bits)
    parameter ADDR_WIDTH = 4,  // Width of address bus (bits)
    parameter DEPTH      = 16  // Number of memory locations (2^ADDR_WIDTH)
)(
    input clk,                  // Clock signal
    input we,                   // Write enable (active high)
    input [ADDR_WIDTH-1:0] addr,// Read/Write address
    input [DATA_WIDTH-1:0] din, // Data input for writes
    output reg [DATA_WIDTH-1:0] dout // Data output for reads
);

// Memory array declaration
reg [DATA_WIDTH-1:0] mem [0:DEPTH-1];

// Synchronous write and read operations
always @(posedge clk) begin
    if (we) begin
        mem[addr] <= din;      // Write operation
    end
    dout <= mem[addr];         // Read operation (captures data at current addr)
end

endmodule
