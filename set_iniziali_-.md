---   
title:Set iniziali -    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Set iniziali - 
Keywords  [OPEN][DEF][DATA][DATE][INIT][INITIALIZATION][GRID]

   
   
 DIM C[80],WC[5],SC[3],JC[3],OC[3]  
 APP$="1YYY5YY8YY12345Y456789012Y4Y6789Y1Y3456789012345678901Y34567890123456789Yw123s12Yj123o123"  
 CALL "rbgopn",APP$,C[ALL],WC[ALL],SC[ALL],JC[ALL],OC[ALL]  
 call "smd_opn","p07",c7  
 def fnd10$(x$)=x$(7,2)+"/"+x$(5,2)+"/"+x$(1,4)  
 def fnd10r$(x$)=x$(7,4)+x$(4,2)+x$(1,2)  
 def fnd8r$(x$)=x$(5,4)+x$(3,2)+x$(1,2)  
 def fnd8$(x$)=x$(7,2)+x$(5,2)+x$(1,4)  
 def fnd_xml$(x$)=x$(5,4)+"-"+x$(3,2)+"-"+x$(1,2)  
 dim gar_dat[10,10]  
 gar_dat[1,1]=18001  
 gar_dat [1,2]=gb__current_context+1  
 gosub Sub_Init_Grid1  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:20 in ambiente Oblivion/ECHO*
