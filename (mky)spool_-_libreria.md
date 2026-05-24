---   
title:(MKY)SPOOL - Libreria   
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# (MKY)SPOOL - Libreria
Keywords  

SPOOLSPOOL - Libreria  
 omsopl contiene una chiamata 51000 REM ===================================================================== 51010 SUB_PSPOOL: 51020 LET STP_PRELIEVO$=CVS(DP.STPR$,3) 51109 CALL "susenv","000","01"; OPEN (104)"tfil01" 51110 LET D_IN$="|"+STP_PRELIEV  
O$+"|Stampa lista di prelievo"+"|" 51120 CALL "smd_spl::sub_open",D_IN$,D_OUT$ 51178 LET CSTP=NUM(D_OUT$) 51180 CALL "smd_opn","k03",CSTP 51182 READ (101,KEY="348")REC$; DIM SPOOL_T$:REC$ 51184 READ (101,KEY="348")REC$; DIM SPOOL_R$:REC$ 51185 BREAK  
51188 SWEND  
--  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:12 in ambiente Oblivion/ECHO*
