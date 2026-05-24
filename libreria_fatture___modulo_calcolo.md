---   
title:Libreria Fatture : Modulo calcolo    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Libreria Fatture : Modulo calcolo 
Keywords  [FRP][FAT][rmefat]

   
   
 rmeGrpl  
 Libreria Fatture : Modulo calcolo [FRP][FAT]  
   
## Calcolo fatture  
 Genera il record fattura TF$  
 Se la modalita' di pagamento prevede la chiusura automatica, genera anche il relativo record in c[27]/ecm$  
 call "rmefat",DAT$,NRDOC$,DOC$,DCN$,CLI$,MP$,ASSIVA$,TOTIMP[ALL],TOTIVA[ALL],TMRC,T$,C[ALL]   
  
Paremetri in ingresso  
  
- data documento da emettere  
- numero documento  
- tipo documento  
- documento per riporto in contabilita  
- codice cliente nella forma mmmccsssss  
- record modalita' di pagamento                  
- lista ssoggettamenti iva step 3  
- vettore totali imponibili per assoggettamento  
- vettore totali iva per assoggettamento  
- totale valore merce  
- record t$ (utilizza solo t.postel$)  
- vettore canali - utilizza 1, c[27],c[35]                                   
  
   
## Legge archivio fatture per cliente  
 call "rmefat::sub_setcommon","readcfo",d_in$,d_out$  
 da fare  
  
## Legge archivio fatture per documento  
 call "rmefat::sub_setcommon","readdoc",d_in$,d_out$  
 da fare  
  
   
   
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:26 in ambiente Oblivion/ECHO*
