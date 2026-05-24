---   
title:(MKY)CALL > Enter Classico   
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# (MKY)CALL > Enter Classico
Keywords  

   
   
 EnterCALL > Enter Classico  
 10000 REM 10000,5  
 10005 SUB_LOAD_KNUM4:  
 10010 REM =========================================================  
 10015 REM === Restituisce gli ordini inevasi ======================  
 10020 REM === se passato codice articolo va per key num 2  
 10025 REM === altrimenti per key num 4 10030 REM D_IN  
 0035 REM ->1 X0  
 10040 rem>2 TIP0070 REM D_OUT 10075 REM ->Elenco $09/$0a  
 1080 REM  
 085 SETERR SUBERR 10090 ENTER D_IN$,D_OUT$ 10095 CALL "sm2_utl:  
:Sub_Set_Din",D_IN$,REC_IN$ 10100 GOSUB SUB_INIT 10105 LET X0$=REC_IN.CPO$[1] 10110 LET TIP$=REC_IN.CPO$[2] 10140 REM ........................................................... 10145 LET D_OUT$="Codice articolo-->000000000Iog:p12"+$09$+"Data Consegn  
a-->091" +$09$+"Qta Inevasa-->172"+$09$+$0A$ 10150 REM ...........................................................  
--  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:21 in ambiente Oblivion/ECHO*
