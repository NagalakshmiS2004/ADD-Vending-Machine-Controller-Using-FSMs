# ADD-Vending-Machine-Controller-Using-FSMs
The vending machine is a ubiquitous tool that provides quick and easy access to a variety of products,  simplifying everyday transactions. Its seamless operation relies on a well-designed control system that governs  its functionality.



Verilog code

timescale 1ns / 1ps

module VendingMachine_tb;

 // Inputs to the VendingMachine module

 reg [3:0] item;

 reg five_in, ten_in, reset, clock;

 // Outputs from the VendingMachine module

 wire dispense, five_out;

 // Instantiate the VendingMachine module

 VendingMachine DUT (

 .item(item),

 .five_in(five_in),

 .ten_in(ten_in),

 .clock(clock),

 .reset(reset),

 .dispense(dispense),

 .five_out(five_out)

 );

 // Clock generation: 50MHz clock (20ns period)

 initial begin

 clock = 0;

 forever #10 clock = ~clock; // Toggle clock every 10ns

 end

 // Test sequence

 initial begin

 // Initialize inputs
 item = 4'b0000;

 five_in = 0;

 ten_in = 0;

 reset = 0;

 // Apply reset

 $display("Applying reset...");

 reset = 1;

 #20; // Wait for a few clock cycles

 reset = 0;

 // Test Item 1 (Price: 15)

 $display("Testing Item 1 (Price: 15)");

 item = 4'b0001;

 five_in = 1; #20; five_in = 0; // Insert 5

 ten_in = 1; #20; ten_in = 0; // Insert 10

 #20; // Wait for dispense

 $display("Dispense: %b, Five_out: %b", dispense, five_out);

 // Test Item 2 (Price: 25)

 $display("Testing Item 2 (Price: 25)");

 item = 4'b0010;

 five_in = 1; #20; five_in = 0; // Insert 5

 five_in = 1; #20; five_in = 0; // Insert 5

 ten_in = 1; #20; ten_in = 0; // Insert 10

 #20; // Wait for dispense

 $display("Dispense: %b, Five_out: %b", dispense, five_out);

 // Test Item 3 (Price: 35)

 $display("Testing Item 3 (Price: 35)");

 item = 4'b0100;

 five_in = 1; #20; five_in = 0; // Insert 5five_in = 1; #20; five_in = 0; // Insert 5

 ten_in = 1; #20; ten_in = 0; // Insert 10

 ten_in = 1; #20; ten_in = 0; // Insert 10

 #20; // Wait for dispense

 $display("Dispense: %b, Five_out: %b", dispense, five_out);

 // Test Item 4 (Price: 45)

 $display("Testing Item 4 (Price: 45)");

 item = 4'b1000;

 ten_in = 1; #20; ten_in = 0; // Insert 10

 ten_in = 1; #20; ten_in = 0; // Insert 10

 ten_in = 1; #20; ten_in = 0; // Insert 10

 five_in = 1; #20; five_in = 0; // Insert 5

 #20; // Wait for dispense

 $display("Dispense: %b, Five_out: %b", dispense, five_out);

 // Test Reset Functionality

 $display("Testing Reset Functionality");

 reset = 1; #20; reset = 0;

 $display("Reset Complete: Dispense: %b, Five_out: %b", dispense, five_out);

 // End simulation

 $stop;

 end

endmodule







Testbench

`timescale 1ns / 1ps

module VendingMachine_tb;

 // Inputs to the VendingMachine module

 reg [3:0] item;

 reg five_in, ten_in, reset, clock;

 // Outputs from the VendingMachine module
 wire dispense, five_out;

 // Instantiate the VendingMachine module

 VendingMachine DUT (

 .item(item),

 .five_in(five_in),

 .ten_in(ten_in),

 .clock(clock),

 .reset(reset),

 .dispense(dispense),

 .five_out(five_out)

 );

 // Clock generation: 50MHz clock (20ns period)

 initial begin

 clock = 0;

 forever #10 clock = ~clock; // Toggle clock every 10ns

 end

 // Test sequence

 initial begin

 // Initialize inputs

 item = 4'b0000;

 five_in = 0;

 ten_in = 0;

 reset = 0;

 // Apply reset

 $display("Applying reset...");

 reset = 1;

 #20; // Wait for a few clock cycles

 reset = 0;// Test Item 1 (Price: 15)

 $display("Testing Item 1 (Price: 15)");

 item = 4'b0001;

 five_in = 1; #20; five_in = 0; // Insert 5

 ten_in = 1; #20; ten_in = 0; // Insert 10

 #20; // Wait for dispense

 $display("Dispense: %b, Five_out: %b", dispense, five_out);

 // Test Item 2 (Price: 25)

 $display("Testing Item 2 (Price: 25)");

 item = 4'b0010;

 five_in = 1; #20; five_in = 0; // Insert 5

 five_in = 1; #20; five_in = 0; // Insert 5

 ten_in = 1; #20; ten_in = 0; // Insert 10

 #20; // Wait for dispense

 $display("Dispense: %b, Five_out: %b", dispense, five_out);

 // Test Item 3 (Price: 35)

 $display("Testing Item 3 (Price: 35)");

 item = 4'b0100;

 five_in = 1; #20; five_in = 0; // Insert 5

 five_in = 1; #20; five_in = 0; // Insert 5

 ten_in = 1; #20; ten_in = 0; // Insert 10

 ten_in = 1; #20; ten_in = 0; // Insert 10

 #20; // Wait for dispense

 $display("Dispense: %b, Five_out: %b", dispense, five_out);

 // Test Item 4 (Price: 45)

 $display("Testing Item 4 (Price: 45)");

 item = 4'b1000;

 ten_in = 1; #20; ten_in = 0; // Insert 10ten_in = 1; #20; ten_in = 0; // Insert 10

 ten_in = 1; #20; ten_in = 0; // Insert 10

 five_in = 1; #20; five_in = 0; // Insert 5

 #20; // Wait for dispense

 $display("Dispense: %b, Five_out: %b", dispense, five_out);

 // Test Reset Functionality

 $display("Testing Reset Functionality");

 reset = 1; #20; reset = 0;

 $display("Reset Complete: Dispense: %b, Five_out: %b", dispense, five_out);

 // End simulation

 $stop;

 end

endmodule
