---   
title:Rileva programmi duplicati nelle directory Partner    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Rileva programmi duplicati nelle directory Partner 
Keywords  [DUP][PGM][VER]

   
 "sm2_utl::SUB_PGM_DUP",d_in$,d_out$  
 LET X0$=REC_IN.CPO$[1]    
 LET DIR1$=REC_IN.CPO$[2]  
 LET DIR2$=REC_IN.CPO$[3]  
   
 Le directory devono essere complete con il backslash finale (esempio C:\Partner_AAS\prog\"  
 Al momento esegue solo show  
   
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:30 in ambiente Oblivion/ECHO*
