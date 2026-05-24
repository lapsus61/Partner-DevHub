---   
title:Libreria Generazione movimenti da file di appoggio : Generazione    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Libreria Generazione movimenti da file di appoggio : Generazione 
Keywords  [MV1][MV2][MV3][rduGmov]

   
   
 rduGmov  
 Libreria Generazione movimenti da file di appoggio  
 Generazione  
   
 (1)[Se si desidera gestire il file temporaneo]  
 [ call "g-rmgmov",gb__arg$]  
 La struttura della template in ingresso e' gb__arg$:"dtrg:c(8),nrrf:c(6),filenm:c(300),d_out:c(18)"  
 Il campo filenm$ deve contenere il nome del file temporaneo completo di Path  
 Il modulo contiene le call utili per le generazione del movimento   
   
 (2)[ Esecuzione immediata del file temporaneo in Modalita' classica]  
 [call "rduGmov",d_in$,d_out$ ]  
 Genera il movimento di magazzino a partire dai dati inseriti nel file di appoggio  
 d_in$[2] deve contenere il nome del file temporaneo completo di path  
 Esegue EXIT  
   
 (3)[Esecuzione immediata del file temporaneo in Modalita' in BACKGROUND]  
 Ottenere la riga di comando da eseguire  
 [call "rduGmov::sub_cmd",d_in$,d_out$ ]  
 Restituisce la riga di comando da eseguir con SCALL cosi da ottenere l'elaborazione in background  
 d_in$[2] deve contenere il nome del file temporaneo completo di path  
 La variabile globale 'cmdprompt' deve essere dichiarata nel config e contenere la completa riga di comando per l'esecuzione  
 dell'ambiente Partner  
 Eseguire SCALL della riga di comando  
 Esegue Release in chiusura  
--  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 28/02/2026 alle ore 19:30:25 in ambiente Oblivion/ECHO*
