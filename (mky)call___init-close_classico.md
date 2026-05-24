---   
title:(MKY)CALL > INIT-CLOSE Classico   
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# (MKY)CALL > INIT-CLOSE Classico
Keywords  

   
   
 Init-CloseCALL > INIT-CLOSE Classico  
 40000 REM 40000  
 40010 SUB_INIT:  
 40020 LET ACC$=STBL("acc")  
 40050 LET S_TBL$=$FF000102030405060708090A0B0C0D0E0F101112131415161718191A1B1C1D1E1F202122232425262728292A2B2E2D2C2F$  
 40070 DEF FND10$(X$)=X$(7,2)+"/"+X$(5,2)+"/"+X$(1,4)  
 40090 READ (101,KEY="p05")REC$; DIM AC$:REC$  
 40130 C2=702  
 40140 C9=709  
 40150 CALL "smd_opn","p70",C70  
 40180 RETURN  
   
 40190 SUB_CLOSE:  
 40220 CLOSE (C70)  
 40250 RETURN  
   
 54000 REM 54000  
 54010 SUBERR:  
 54020 LET MSG$="Errore "+STR(ERR)+" linea "+STR(TCB(5))  
 54030 LET X=MSGBOX(MSG$,48,"smd_inc")  
 54040 RETURN  
--  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:20 in ambiente Oblivion/ECHO*
