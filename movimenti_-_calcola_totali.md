---   
title:Movimenti - Calcola Totali    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Movimenti - Calcola Totali 
Keywords  [MOV][TOTALE]

DIM ASSIVA$(21," "),TOTIMP[7],TOTIVA[7]; LET TMRC=0 ; rem Nel caso di documenti riepilogativi, eseguire questa linea solo sul primo  
CALL "rmempf",MV1$,SOC1$(52,1),TD.TOT,ASSIVA$,TOTIMP[ALL],TOTIVA[ALL],TMRC,C[ALL]  
FOR APP=1 TO 7; LET TOTIVA[APP]=INT((TOTIVA[APP]+.005)*100)/100; NEXT APP; REM ..arrotondamento iva.....  
##############################################################################################################  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:12 in ambiente Oblivion/ECHO*
