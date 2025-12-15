# durvesh808
1. Addition of two data.                          
C000 XRA A ; Clear the accumulator
 C001 MVI C , 00H ; Set Initial carry as Zero.
 C002 00
 C003 LXI H, C040H ; Initialize memory pointer at C040H 
 C004 40
 C005 C0
 C006 MOV A, M ; Copy first Byte into Reg.A
 C007 INX H ; Point towards Next Byte
 C008 ADD M ;Add first byte & Second byte
 C009 JNC NEXT ; If CY= 0 , GO TO Label NEXT
 C00A 0D
 C00B C0
 C00C INR C ; If CY = 1, Increment contents of Reg. C by 1
 C00D NEXT : INX H ;Point towards next memory location
 C00E MOV M , A ; Store Sum at next memory location 
 C00F INX H ; Point towards next memory location
 C010 MOV M , C ; Store Carry in next consecutive memory location
 C011 RST 1 ; Stop Program Execution





2. Subtraction of two data byte.                                    
C000 XRA A ; Clear the accumulator
 C001 LXI H , CO30H ; Initialize memory pointer to subtrahend
 C002 30
 C003 C0
 C004 MOV B , M ;Copy subtrahend to Reg. B
 C005 INX H ;Point towards next memory location
 C006 MOV A , M ; Copy minuend to Reg.A
 C007 SUB B ; Subtract contents of Reg. B from Contents of Reg. A 
 C008 JP DOWN ;If S=0,Transfer Program Control to Label DOWN
 C009 0E
 C00A C0
 C00B CMA ;Find 1’S Compliment of contents of Reg.A
 C00C ADI 01H ;ADD 01H into contents of Reg.A
 C00D 01
 C00E DOWN: INX H ;Point towards next memory location
 C00F MOV M , A ;Store absolute difference into memory location
 C010 CF RST 1 ;Stop Program Execution








Count of odd as well as even

C000 XRA A ;Clear accumulator.  
C001 MVI C ;Set Counter as Reg.C with 05H.   
C002 05.        
C003 MVI D ;Set Odd Counter as Reg.D as 00H.     
C004 00.     
C005 MVI E ;Set Even Counter as Reg.E as 00H.    
C006 00.     
C007 LXI H ;Initialize memory pointer at C040H.      
C008 40.      
C009 C0.    
C00A MOV AM ;Copy Data Byte in Reg.A
C00B RRC  ;Rotate contents of Reg.A towards Right
C00C JC ODD ;If CY = 1 , GO TO Label ODD
C00D 13
C00E C0
C00F INR E ;Increment Even Counter
C010 JMP ;GO TO Label NEXT
C011 14
C012 C0
C013 INR D ;Increment ODD Counter
C014 INX H ;Point towards next memory location
C015 DCR C ;Decrement contents of Reg.C
C016 JNZ ;If Z = 0 , GO TO Label UP
CO17 0A
C018 C0
C019 MOV MD ;If Z = 1,Copy ODD count in next memory location
C01A INX H ;Copy EVEN count in current memory location
C01B MOV ME
C01C RST 1 ;Stop Program Execution
