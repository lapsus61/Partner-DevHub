---   
title:Verifica se documenti gia' esistenti nel mese per il cliente/fornitore    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Verifica se documenti gia' esistenti nel mese per il cliente/fornitore 
Keywords  [mov][unico][cfo][dtrg][esi]

 call "rmagab::SUB_CTL_S3_EXT","x0|mmmccsssss|dtrg|nrrf|listadocumenti|tipodocumneto|",d_out$  
 Il confronto viene eseguito tra documenti 'simili'. Questo vuol dire che sia il documento che sto analizzando che quelli con i quali eseguo il confronto  
 devono essere presenti nella stessa lista l_doc$                                
 Quindi se L_DOC$="" vuol dire che non intendo eseguire controlli, e se T_DOC$="" azzero quindi anche L_DOC$    
 Esempio1: Se il documento e' una nota debito non mi interessa eseguire il controllo                                   
 Esempio2: Se il documento e' un D,D1,F,FS mi interessa ed il controllo lo devo eseguire se trovo altri D,D1,F,FS    
  
D_IN  
  
- [1] x0  
- [2] codice cli/for nella forma mmmccsssss  
- [3] data registrazione (il controllo viene eseguito a partire dal primo giorno del mese relativo)  
- [4] numero movimento di magazzino (se indicato lo esclude dal controllo)  
- [5] lista codici tipo documento da considerare step 3  
- [6] codice tipo documento da emettere  
  
D_OUT  
- 0 Non trovato            
- 1 Trovato                
- -1 Scartato non in lista  
  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:26 in ambiente Oblivion/ECHO*
