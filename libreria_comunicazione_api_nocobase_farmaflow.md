---   
title:Libreria comunicazione API NocoBase FarmaFlow    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Libreria comunicazione API NocoBase FarmaFlow 
Keywords  [g-dmnFFA][API][FARMAFLOW]

   
 g-dmnFFA  
   
richiede : CALL "smd_s17::sub_load_s17","|91012"+$09$+"z00-tokenFF||D|",APP$  
   
## FILE  
Load STRUTTURA di Lista collezioni oppure Singola collezione. Genera il risultato in un file txt  
curl -k -H "Authorization: Bearer  %TOKEN%" https://app.farmaflow.it/api/collections -i>Listacollezioni.txt                                              
D_IN  
- [1] non utilizzato (X0?)  
- [2] collezione di cui si intende ricevere la struttura  
  collections tutte le collezioni  
  collections/users solo users  
D_OUT  
- Nome del file generato  
## FILE_REC_SINGLE                                               
 da fare seguendo quanto nel file  di esempio ConnectFarmaFlow.bat              
Load Records                                                             
curl -k -H "Authorization: Bearer  %TOKEN%" https://app.farmaflow.it/api/categorie?fields=id,nome -i > Rec_Categorie_Campi.txt   
---  
## WRITE_CPO     
 da fare seguendo quanto nel file  di esempio ConnectFarmaFlow.bat                                                                   
Write singolo campo singolo record                                   
curl -k -X PATCH -H "Authorization: Bearer  %TOKEN%" -H "Content-Type: application/json" https://app.farmaflow.it/api/categorie/1 -d "{\"nome\":\"AntiDolorificiC\"}" -i > WriteCategorieNome.txt  
--  
## PARSER_JSON  
Parser JSON1 - Sviluppa il contenuto di una risposta della API NocoBase e la restituisce in un formato Griglia $09$0A  
D_IN  
- [1] non utilizzato (X0?)  
- [2] non utilizzato  
- [3] Nome file completo di path cosi come restituito dalla subroutine 'FILE'  
     
D_OUT  
- Dati in formatio griglia standard completi di testata e campi  
    
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:25 in ambiente Oblivion/ECHO*
