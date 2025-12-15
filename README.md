# durvesh808
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
