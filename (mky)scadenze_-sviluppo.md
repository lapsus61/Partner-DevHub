---   
title:(MKY)Scadenze -Sviluppo    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# (MKY)Scadenze -Sviluppo 
Keywords  [EC][SCADENZE]

```  
 DIM DTSC$[30](8,"*"),IMSC[30]  
 CALL "rpclsc",NUM(MP.NUM$),PS_OGGI$,MP$,PS_T,PS_I,0,DTSC$[ALL],IMSC[ALL]  
 FOR APP=1 TO 30  
 IF DTSC$[APP](1,1)="*" THEN NEXT APP  
 MESSG$=MESSG$+TBL(STR(IMSC[APP]:"###,###,##0.00"),TBL=L65)  
 MESSG$=MESSG$+" al "+FND10$(DTSC$[APP])+$0A$  
 NEXT APP  
```  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:24 in ambiente Oblivion/ECHO*
