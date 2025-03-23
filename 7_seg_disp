`timescale 1ns / 1ps
//////////////////////////////////////////////////////////////////////////////////
// Company: 
// Engineer: 
// 
// Create Date:    16:05:31 08/12/2024 
// Design Name: 
// Module Name:    display 
// Project Name: 
// Target Devices: 
// Tool versions: 
// Description: 
//
// Dependencies: 
//
// Revision: 
// Revision 0.01 - File Created
// Additional Comments: 
//
//////////////////////////////////////////////////////////////////////////////////



module display(
Clk,
Seven_seg_display,
Seven_seg_en1,
Seven_seg_en2,
Seven_seg_en3);

input wire Clk;
output reg [7:0] Seven_seg_display;
output reg Seven_seg_en1;
output reg Seven_seg_en2;
output reg Seven_seg_en3;


parameter WORD_LENGTH=4,
          R=8'b00010001,
          O=8'b00000011,
          L=8'b11100011,
          A=8'b00010001;


reg [24:0] licznik;
reg slow_clk = 1'b0;
reg [1:0] iterator=2'b0;
reg [8*WORD_LENGTH-1:0] phrase ={R,O,L,A};
reg [23:0] disp_output =24'b0;
reg [12:0] letter_iterator=0;
reg [3:0] word_iterator=0;
always @(posedge Clk)
  begin
    if(licznik ==5000)
      begin
        licznik <=25'b0;
		  slow_clk<=~slow_clk;
      end
    else
      begin
        licznik<=licznik+1;
 
	   end
    end

always @(posedge slow_clk)
  begin
  
 if(letter_iterator<1200)
 begin
  iterator <=iterator +1;
  letter_iterator <=letter_iterator+1;
  case (iterator)
    2'b00 : begin
		Seven_seg_display <= disp_output[23-:8];
      Seven_seg_en1 <=1'b1;
      Seven_seg_en2 <=1'b1;
      Seven_seg_en3 <=1'b0;
	 end
	 2'b01 : begin
		Seven_seg_display <= disp_output[15-:8];
      Seven_seg_en1 <=1'b1;
      Seven_seg_en2 <=1'b0;
      Seven_seg_en3 <=1'b1;
	 end
	 2'b10 : begin
		Seven_seg_display <= disp_output[0+:8];
      Seven_seg_en1 <=1'b0;
      Seven_seg_en2 <=1'b1;
      Seven_seg_en3 <=1'b1;
	 end
	 default: begin
	   Seven_seg_en1 <=1'b1;
      Seven_seg_en2 <=1'b1;
      Seven_seg_en3 <=1'b1;
		iterator <=0;
	 end
  endcase
 end
 else
   begin 
	letter_iterator<=0;
	  if(word_iterator >0)
	    begin
		   case (word_iterator)
            4'd11 : begin
	          disp_output<= phrase[87 -:24];
	        end
	        4'd10 : begin
	          disp_output<= phrase[79 -:24];
	        end
	        4'd9 : begin
	          disp_output<= phrase[71 -:24];
	        end
	        4'd8 : begin
	          disp_output<= phrase[63 -:24];
	        end
			4'd7 : begin
	          disp_output<= phrase[55 -:24];
	        end
	        4'd6 : begin
	          disp_output<= phrase[47 -:24];
	        end
	        4'd5 : begin
	          disp_output<= phrase[39 -:24];
	        end
	        4'd4 : begin
	          disp_output<= phrase[31 -:24];
	        end
			4'd3 : begin
	          disp_output<= phrase[23 -:24];
	        end
	        4'd2 : begin
	          disp_output<= {phrase[15 -:16],phrase[87 -:8]};
	        end
            4'd1 : begin
	          disp_output<= {phrase[7 -:8],phrase[87 -:16]};
	        end
	        // default: begin
	
	        // end
			endcase
			word_iterator <= word_iterator-1;

	    end
	  else
	    begin
			word_iterator<=11;
	    end
	
	end 
  end

endmodule
