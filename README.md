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



Count of occurrence of data byte

C000 XRA A ;Clear accumulator 
 C001 MVI B , 00H ;Set Count of Occurrence as 00H in Reg.B 
 C002 00
 C003 LXI H,C04FH ;Initialize memory pointer where block length is stored 
 C004 4F
 C005 C0
 C006 MOV C , M ;Copy block length into Reg.C
 C007 LOOP: INX H ;Point towards next memory location 
 C008 MOV A , M ;Copy Data Byte into Reg.A 
 C009 CPI ABH ;Compare contents of Reg.A with Data Byte ABH
 C00A AB
 C00B JNZ NEXT ;If Z = 0, GO TO Label NEXT
 C00C 0F
 C00D C0
 C00E INR B ;If Z = 1,Increment Count of Occurrence by 1
 C00F NEXT: DCR C ;Decrement Counter by 1
 C010 JNZ LOOP ;If Z = 0 , GO TO Label LOOP
 C011 07
 C012 C0
 C013 LXI H , C100H ; If Z = 1, Initialize memory pointer at C100H
 C014 00
 C015 C1
 C016 MOV M , B ; Copy Count of Occurrence at C100H
 C017 CF RST 1 ;Stop Program Execution
