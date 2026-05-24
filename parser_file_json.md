---   
title:Parser file JSON   
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Parser file JSON
Keywords  

   
## converte un file JSON in un formato D_OUT classico [JSON][PARSER][CONVERT]  
   
 call "g-dmnFFA::PARSER_JSON"," | |c:\masbi-sun\StrutturaCollezioni.txt",d_out$  
   
 1 X0  
 2 Nome tag dati JSON  - se non passato assume CHR(34)+"data"+CHR(34)+":["    
 3 Nome file in formato JSON  
   
 D_OUT$ in formato classico $09/$0a$  
   
   
## converte un d_out$ classico in una stringa json  
   
 call "g-dmnFFA::PARSER_VPRO5_JSON",d_in$,d_out$  
 1 X0  
 2 stringa in formato classico $09$0A  
 3 stringa in formato JSON  
   
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:30 in ambiente Oblivion/ECHO*
