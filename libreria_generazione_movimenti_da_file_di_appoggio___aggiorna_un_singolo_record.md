---   
title:Libreria Generazione movimenti da file di appoggio : Aggiorna un singolo record    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Libreria Generazione movimenti da file di appoggio : Aggiorna un singolo record 
Keywords  [MV1][MV2][MV3][rduGmov]

   
   
 CALL "sm2_utl::SUB_WRITE_SIMPLE",D_IN$,MKY_REC$,D_OUT$  
   
   
 D_in[2]  Deve contenere il nome del file di appoggio  
 MKY_REC$ Deve contenere il record valorizzato  
 D_OUT$  -1 Failed  
   1 OK  
   
   
 ctr:c(4)  Contatore riga  
 dtrg:c(8)  Data movimento  
 msg:c(1)    
 par:c(20)    
 dep:c(3)  Codice deposito  
 tmv:c(3)  Codice tipo movimento  
 dp1:c(3)  Codice deposito 1  
 tm1:c(3)  Codice tipo movimento 1  
 mcc:c(5)  Mastro/Conto da utilizzare  
 cfo:c(5)  Codice Cli/For  
 is:c(3)  Codice destinazione  
 flg:c(1)  Flag  
 art:c(18)  Codice Articolo  
 qta:f  Quantita  
 prz:f  Prezzo Unitario  
 sc1:f  Sconto 1  
 sc2:f  Sconto 2  
 sc3:f  Sconto 3  
 vlr:f  Valore Riga al netto degli sconti  
 dtsc:c(8)  Data Scadenza Lotto  
 ltmt:c(18)  Numero Lotto/Matricola  
 cella:c(10) Numero Cella  
 rord:c(19)  Riferimento Ordine collegato  
 civa:c(3)  Codice Iva  
 cmer:c(3)  Codice conto merce  
 note:c(36) Note  
 tdc:c(3)  Codice Tipo documento da generare  
 trp:c(3)  Codice trasportatore  
 mpg:c(3)  Codice modalita' di pagamento  
 cs:c(3)  Codice causale trasporto  
 ap:c(3)  Codice aspetto esteriore  
 ncol:f  Numero colli  
 noteExf:c(250) Note estese riga  
 noteEstese:c(360) Note estese documento  
   
 Note di compilazione del record mky_rec$  
 Campo Note    36 caratteri deve contenere                                     
  per le righe T e L > descrizione          (ele 26 grid_d) (cpo 31 di rmamvx)  
  per le righe 8 > eventuale riga di testo aggiuntiva (ele 26)    (cpo 59)  
 NoteExf 250 caratteri e' la descrizione exf per 8/T/L (ele 33)(cpo 58)                                                                    
   
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 28/02/2026 alle ore 19:30:25 in ambiente Oblivion/ECHO*
