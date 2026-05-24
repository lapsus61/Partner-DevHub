---   
title:Libreria rduGmov : Flusso    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Libreria rduGmov : Flusso 
Keywords  [CODESTD][MOV][MAG]

   
   
 rduGmov SuperMov           05/11/2024                 
 Genera un movimento di magazzino a partire da un file MKEYED                                   
 E' possibile lanciare il programma  
  come sessione separata utilizzando la sintassi definita in SUB_CMD        
  In questo caso NON restituisce info se non un messaggio a video se parametrizzato  
  (per evitare conflitti? Non ricordo perche' ho deciso di lanciarlo come sessione separata ed uscire con RELEASE)  
 come modulo esterno con D_IN/D_OUT                 
  ed il nome file va passato negli argomenti D_IN$   
  In uscita d_out contiene data e numero movimento generato                                          
  (vedi g-rmGmov per la getione del file temporaneo)                                       
   
Nota sulle griglie:  
La struttura del record di appoggio prevede che i dati di testata, piede e riga siano presenti su TUTTI i record. Questo determina la gestione di due distinte griglie.  
   
<INTERNA> TUTTI I DATI  
  La gestione dei dati avviene attraverso l'utilizzo di una griglia che contiene tutti i dati della template. Questa griglia e' definita INTERNA ed e' utilizzata  
  per una piu' semplice gestione dei dati  
<GESTIONE> SOLO DATI RIGHE PER MODIFICA  
  La gestione dei dati appaiano in g-rmgmov avviene attraverso l'utilizzo di una griglia che contiene SOLO i dati da presentare  
  a video e relativi alle RIGHE.Questa griglia e' definita GESTIONE  
--------------------------------------------------------------------------------------------------------------------------------------------------------  
## SEQUENZE TIPICHE  
   
### Generazione di un movimento di magazzino  
   
- call "rduGmov::sub_tmp",d_in$,d_out$  
- call "rduGmov::sub_cre",d_in$,d_out$  
- Loop  
- Alimento la variabile MKY_REC$ con i dati di interesse  
- call "rduGmov::SUB_WRITE_SIMPLE",D_IN$,MKY_REC$,D_OUT$  
- Goto Loop  
- Elaborazione  
-  (1) call "g-rmgmov",gb__arg$  
-  (2) call "rduGmov",d_in$,d_out$  
-  (3) call "rduGmov::SUB_CMD",d_in$,cmd$; Scall cmd$  
- call "rduGmov::sub_del",d_in$,""  
   
### Duplica Movimento di Magazzino  
Sequenza  
   
   
| Modulo | Utilizzo |  
| --------- | --------- |  
| call "rduGmov::SUB_LOAD_MOV_INT" | Legge un movimento di magazzino e restituisce la griglia INTERNO |  
| call "rduGmov::SUB_MOD_GRID_INT" | Permette di modificare i dati della griglia INTERNO |  
| call "rduGmov::sub_cre" | Crea il file di appoggio |  
| call "rduGmov::SUB_ADD_MKY_FROM_GRID" | Popola il file di appoggio leggendo i dati della griglia INTERNO |  
| Elaborazione | Tre diversi tipi di elaborazione del file di appoggio |  
|    | (1) call "g-rmgmov" |  
|  | (2) call "rduGmov"  |  
|   | (3) call "rduGmov::SUB_CMD"; Scall cmd$  |  
| call "rduGmov::sub_del" | Delete del file di appoggio |  
   
|---------------------------------------------------------------------------------------------------------------------------------------------------------  
### Template  
 [Ottenere la template standard utilizzata dal progetto]  
 [ call "rduGmov::sub_tmp",d_in$,d_out$ ]  
 Restituisce la template da utilizzare   
 (vedi 'Aggiorna singolo record per i dettagli di valorizzazione)  
   
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
   
## Tmp to Col  
 call "rduGmov::sub_tmp_col",d_in$,d_out$  
 Restituisce la relazione tra il campo della template e la relativa colonna nella griglia INTERNO  
 nel formato "<000><campo>;<000><campo>;<000><campo>;......."  
 quindi il campo 'campo' e' presente nella colonna '000' della griglia interna  
## Grid I to G  
 call "rduGmov::SUB_TMP_GRID_IG","",d_out$                                         
 Restituisce la tabella di relazione tra colonna griglia INTERNA e colonna griglia GESTIONE  
 nel formato "<000><nnn><campo>;<000><nnn><campo>;......"  
 quindi il campo presente nella colonna 000 della griglia interna  
  e' presente nella colonna nnn della griglia di gestione  
   
## Crea File  
 Creare il file di appoggio]  
 [ call "rduGmov::sub_cre",d_in$,d_out$ ]  
 Crea ed esegue open del file temporaneo per la memorizzazione dei movimenti  
 Il file viene creato di default nella directory c:\masbi-sun.  
 Se invce risulta valorizzata nel config la variabile globale 'tmpserver', viene utilizzata la path indicata in questa.  
 Il nome del file creato e' gmov_ seguito da un numero random  
 La routine verifica - in modo indipendente- la lunghezza della template e la utilizza per definire la lunghezza del record.  
 In questo modo se nelle varie implementazioni la lunghezza della template varia, la size del file si adegua.  
 D_out$ contiene il numero del canale su cui risulta aperto il file temporaneo  
   
## Insert Riga  
 [Alimentare il file di appoggio valorizzando la template dedicata e eseguendo la write nel file di appoggio per tutte le righe]  
 [call "rduGmov::SUB_WRITE_SIMPLE",D_IN$,MKY_REC$,D_OUT$ ]  
 Inserisce un record nel file di appoggio  
   
 D_in[2]  Deve contenere il nome del file di appoggio  
 MKY_REC$ Deve contenere il record valorizzato  
 D_OUT$  -1 Failed  
   1 OK  
 Note di compilazione del record mky_rec$  
 Campo Note    36 caratteri deve contenere                                     
  per le righe T e L > descrizione          (ele 26 grid_d) (cpo 31 di rmamvx)  
  per le righe 8 > eventuale riga di testo aggiuntiva (ele 26)    (cpo 59)  
 NoteExf 250 caratteri e' la descrizione exf per 8/T/L (ele 33)(cpo 58)                                                                    
   
## Genera  
 [Generare il movimento di magazzino]  
   
 (1)[ Se si desidera gestire il file temporaneo, modificandone eventualmente i dati contenuti]  
 [ call "g-rmgmov",gb__arg$]  
 La struttura della template in ingresso e' gb__arg$:"dtrg:c(8),nrrf:c(6),filenm:c(300),d_out:c(18)"  
 Il campo filenm$ deve contenere il nome del file temporaneo completo di Path  
 Il modulo contiene le call utili per le generazione del movimento   
   
 (2)[ Esecuzione immediata del file temporaneo in Modalita' classica]  
 [call "rduGmov",d_in$,d_out$ ]  
 Genera il movimento di magazzino a partire dai dati inseriti nel file di appoggio  
 Assume Organizzazione, Societa' e User dalle variabile globali      
 d_in$[2] deve contenere il nome del file temporaneo completo di path  
 Esegue EXIT  
   
 (3)[Esecuzione immediata del file temporaneo in Modalita' in BACKGROUND]  
 a) E' necessario ottenere la riga di comando (vedi GetCmdLine - Assume Organizzazione, Societa' e User dalle variabili globali, il file dai parametri in ingresso)  
 b) Eseguire SCALL della riga di comando  
 Esegue Release in chiusura  
   
## Delete File  
 [Cancella il file di appoggio]  
 call "rduGmov::sub_del",d_in$,""  
 La variabile D_IN$ deve contenere il numero del canale sul quale il file temporaneo risulta aperto  
 Attenzione : d_in$ e' una semplice variabile, quindi non delimitata come $09/$0A   
   
## GetCmdLine  
 Restituisce la riga di comando da eseguir con SCALL cosi da ottenere l'elaborazione in background - Vedi Genera3  
 call "rduGmov::SUB_CMD",d_in$,d_out$  
 d_in$[2] deve contenere il nome del file temporaneo completo di path  
 La variabile globale 'cmdprompt' deve essere dichiarata nel config e contenere la completa riga di comando per l'esecuzione  
 dell'ambiente Partner  
 Assume Organizzazione, Societa' e User dalle variabile globali   
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------   
## Read Riga  
 Restituisce una singola riga con la struttura della template  
 call "rduGmov::SUB_read_simple",d_in$,d_out$  
 D_IN$ [2] File name  
  [3] Numero riga  
 D_OUT$ Record riga con la struttura della template dedicata  
## Read Riga C  
 Legge il file di appoggio generato secondo le specifiche di rduGmov e restituisce la riga con flag 'C' relativa ai certificati generali,  
 quindi collegati all'intero movimento e non ad una singola riga. Questa riga puo' avere qualsiasi contatore            
 call "rduGmov::SUB_GET_RIGAC","",d_out$     
   
 d_out$ Record C con struttura mky_rec$                                                        
   
   
## Get MV1/2/3  
 [Legge il file di appoggio e restituisce MV1$,MV3$ piu' una matrice griglia INTERNA]  
 Restituisce un MV1 ed un MV3 parzialmente compilati, piu un d_out con le righe [MV1][MV2][MV3]  
 d_in$[2] deve contenere il nome del file temporaneo  
 call "rduGmov::sub_load",d_in$,d_out$,mv1$,mv3$,grid_d$[all]  
   
## Get GridFile  
 Trasforma la matrice griglia dal formato INTERNO, in un d_out nel formato GESTIONE, cosi come utilizzato da g-rmgmov (Vedi Genera/1)  
 call "rduGmov::sub_load_grid",d_in$,d_out$,grid_d$[all]  
 d_in$  Non utilizzato  
 d_out$  in OUT restituisce la matrice griglia GESTIONE  
 grid_d$[all] in INPUT deve contenere la matrice griglia INTERNA  
   
## Get Grid GESTIONE   
 Restituisce una griglia GESTIONE - quindi con la sequenza colonne utilizzata da  g-rmgmov- a partire da un data/numero movimento di magazzino  
 [Legge un movimento di magazzino e ne converte le righe in una griglia (leggere prima MV1$ e MV3$)]  
 call "rduGmov::sub_load_mov","|"+mv1.dtrg$+"|"+mv1.nrrf$,d_out$  
   
## Get Grid INTERNA  
 call "rduGmov::SUB_LOAD_MOV_INT","|"+"aaaammgg"+"|"+"nnnnnn",d_out$,grid_d$[all]  
 Legge un movimento di magazzino  
 Restituisce un d_out con le righe presenti nel movimento con il formato griglia INTERNO                            
 (utile per duplica movimento)   
   
## Mod Grid Interna  
 call "rduGmov::SUB_MOD_GRID_INT",d_in$,d_out$,grid_d$[all]  
 Permette di modificare SU TUTTE LE RIGHE della griglia INTERNA, una o piu' colonne  
Il numero elemento del d_in deve essere relativo al numero colonna della griglia INTERNA                   
 Se voglio modificare il TMV, poiche' nella griglia INTERNA questo corrisponde alla colonna 6, il valore deve essere valorizzato in d_IN$[6]                                            
   
## Import Grid  
 [Trasforma una griglia nel file di appoggio ]  
 Aggiorna il file di appoggio a partire dalla griglia grid_d INTERNA [GRID_D][MV1][MV3] [MV2]  
 La griglia deve contenere tutti i dati compresi nella template e nella esatta sequenza  
 call "rduGmov::SUB_ADD_MKY_FROM_GRID"," |"+filenm$,d_out$,grid_d$[all]  
 D_IN$  [1] X0  
   [2] Filename  
 D_OUT$  Non utilizzato  
 GRID_D$[all] in INPUT deve contenere la matrice griglia INTERNA  
   
   
   
## GF  
 call "rduGmov::SUB_MOV_ODP",SGP$[ALL],SGP,OR2$,D_OUT$  
 Routinescarico ODP di Commessa da picking list di materie prime  
 Chiama il programma di gestione g-rmgmov  
 Aggiorna lo status dell'ODP in ingresso    (20 o 45 )  
 Elimina il file di appoggio     
 Riceve in ingresso:                            
 SGP$(ALL) Matrice dati stampa picking    
 SGP  Righe totali                   
 OR2$  Intero record OR2$             
  Struttura SGP$                                 
  SGP$(SGP,12) = Lotto                  
  SGP$(SGP,0)  = Data Scadenza          
  SGP$(SGP,4)  = Cella                  
  SGP$(SGP,32) = Qta                    
  SGP$(SGP,1)  = Art                    
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:29 in ambiente Oblivion/ECHO*
