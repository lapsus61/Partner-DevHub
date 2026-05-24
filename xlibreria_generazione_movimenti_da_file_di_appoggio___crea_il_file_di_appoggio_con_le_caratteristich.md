---   
title:xLibreria Generazione movimenti da file di appoggio : Crea il file di appoggio con le caratteristiche   
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# xLibreria Generazione movimenti da file di appoggio : Crea il file di appoggio con le caratteristiche
Keywords  [RDUGMOV]

   
   
[Creare il file di appoggio]  
 [ call "rduGmov::sub_cre",d_in$,d_out$ ]  
 Crea ed esegue open del file temporaneo per la memorizzazione dei movimenti  
 Il file viene creato di default nella directory c:\masbi-sun. SE invce risulta valorizzata nel config la  
 variabile globale 'tmpserver' viene utilizzata la path indicata in questa.  
 Il nome del file creato e' gmov_ seguito da un numero random  
 La routine verifica - in modo indipendente- la lunghezza della template e la utilizza per definire la lunghezza del record.  
 In questo modo se nelle varie implementazioni la lunghezza della template varia, la size del file si adegua.  
 D_out$ contiene il numero del canale su cui risulta aperto il file temporaneo  
   
   
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:28 in ambiente Oblivion/ECHO*
