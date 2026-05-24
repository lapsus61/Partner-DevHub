---   
title:SQL - Libreria    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# SQL - Libreria 
Keywords  [smd_sql[SQL][QUERY][WHERE][TEMPLATE][BAKSHALI][MV2]

   
-------------------------------------------------------------------------------------------------------------------------------------------------------------------  
Configurazione  
 systak esegue "smd_sql::sub_set_bakshali" che legge la variabile globale 'bakshali'  
  se 0 o e' mancante     -> bakshali=0  
  se 1 ed il file FILENM$="bakshali_DB"+SOC$ e' raggiungibile -> stbl bakshali contiene il numero del canale SQL su cui il DB e' aperto  
 g-syctlp e susenv eseguono gli stessi controlli in caso di cambio societa'  
------------------------------------------------------------------------------------------------------------------------------------------------------------------  
## Esempio sequenza di utilizzo  
 CALL "smd_sql::sub_sql_def_temp",S_CH,S_DB$,"bks_mov",BKS_MOV$; rem Leggo struttura tabella DB  
 CALL "smd_sql::SUB_SQL_SVL_CPO_EXT",BKS_MOV$,CPO_MOV$;  rem Ottengo sequenza CAMPI    
 CALL "smd_sql::MAKE_UPDATE_STR",CPO_MOV$,UPD_STR_MOV$; rem Ottengo struttura clausola 'on duplicate key update'  
 loop_next:  
 --- popolo il record BKS_MOV.campi ----------   
 CALL "smd_sql::SUB_SQL_SVL_VAL_EXT",BKS_MOV$,SQL_VAL$;   rem Ottengo sequenza VALORI cosi come presenti in bks_mov$    
 SQLPREP$="insert into "+SQL_TBL$;     rem Insert in Tabella                             
 SQLPREP$=SQLPREP$+" ("+CPO_MOV$+") values("+SQL_VAL$+")",; rem Assegno alla sequenza CAMPI i VALORI  
 SQLPREP$=SQLPREP$+" ON DUPLICATE KEY UPDATE "+UPD_STR_MOV$; rem Aggiungo clausola  'on duplicate key update'   
 SQLPREP (S_CH)SQLPREP$; SQLEXEC (S_CH);   rem Eseguo  
 goto loop_next   
 loop_end:  
------------------------------------------------------------------------------------------------------------------------------------------------------------------  
## GET TEMPLATE  
 call "smd_sql::SUB_SQL_DEF_TEMP",SQL_CHN,SQL_DB$,SQL_TBL$,SQL_TMP$  
 >ENTER  
  sql_chn  Canale su cui e' aperto il database  
  sql_db$  Nome del database da prire se sql_chn=0  
  sql_tbl$  Tabella della quale si vuole la template  
  sql_tmp$  Struttura template da utilizzare nella fetch  
-------------------------------------------------------------------------------------------------------------------------------------------------------------------  
## GET STRUTTURA  
 Genera la stringa di assegnazione dei valori di tutti i campi della template nella sintassi corretta VPRO5/SQLODBC  
 Carica anche sql_dout con la struttura classica $09$/$0A$ (verificata 4/3/2020)                                                
 CALL "smd_sql::SUB_SQL_SVL_CPO_EXT",BKS_MOV$,CPO_MOV$  
 IN  
 >BKS_MOV$ Struttura tabella cosi come restituita da SUB_SQL_DEF_TEMP  
 OUT  
 >CPO_MOV$ Elenco campi con la sintassi Vpro5/OdBc  
------------------------------------------------------------------------------------------------------------------------------------------------------------------  
## GET CLAUSOLA 'ON DUPLICATE KEY UPDATE'  
 restituisce la sintassi corretta per la clausola ON DUPLICATE KEY UPDATE  
   
 CALL "smd_sql::MAKE_UPDATE_STR",CPO_MOV$,UPD_STR_MOV$  
 IN  
 >CPO_MOV$ Vpro5 sintax cosi come restituita da SUB_SQL_SVL_CPO_EXT  
 OUT  
 >STR_MOV$ Vpro5 Sintax per clausola  
-------------------------------------------------------------------------------------------------------------------------------------------------------------------  
## GET STRINGA WHERE  
Scopo di questa routine e' quello di evitare molti IF nei programmi per arrivare alla costruzione della  
clausola 'where'  
 call "smd_sql::SUB_SQL_QUERY_DEV",SQL_app$,SQL_QUERY$  
 >Enter  
 sql_app$  struttura where secondo i parametri indicati  
 >Out  
 sql_query$ where sviluppata   
 -Gli attributi dei diversi campi vanno separati con | (pipe, ascii 124)  
 -I diversi campi vanno separati con $0A (LineFeed,ascii 10)  
 -Campi Speciali  
  cfo viene formattato con 00000 e trattato come num nelle esclusioni  
   
 Esempio di call con, per ogni campo, la struttura da utilizzare  
  operatore logico | nomecampo | operatorediconfronto | valore | metodoesclusione |$0a$  
  dove MetodoEsclusione vale                     
   Y= escludi se vuoto                 
   y= escludi se zero per numerici     
   D= escludi se 00000000 o 99999999 per date   
   
 SQLPREP$="select * from "+SQL_TBL$                                      
 SQL_APP$="   |art|=|"+ART$+"|Y"+$0A$   
 +"and|dtrg|>=|"+DATAIN$+"|N"+$0A$  
 +"and|dtrg|<=|"+DATAFN$+"|N"+$0A$  
 +"and|dep|=|"+DEP$+"|Y"+$0A$  
 +"and|dtlt|=|"+DTLT$+"|Y"+$0A$  
 +"and|ltmt|=|"+APP_NLOT$+"|Y"+$0A$  
 +"and|cella|=|"+APP_CELLA$+"|Y"+$0A$  
 +"and|tmv|=|"+TMV$+"|Y"+$0A$  
 +"and|cfo|=|"+APP_CFO$+"|Y"+$0A$                      
 CALL "smd_sql::SUB_SQL_QUERY_DEV",SQL_APP$,SQL_PREP$                   
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
## QUERY   
 call "smd_sql::SUB_SQL_UTILITY"  
 Libreria SQL - esegue alcune query a carattere generale [SQL][SEARCH][FETCH][UTL]  
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
## QUERY Magazzino MV2  
 rem Gli elementi su cui posso intervenire sono quelli della tabella bks_mov  
 rem  > al 27/4/2026 12:30  
 rem   KEYMOV:C(18),DTRG:C(8),NRRF:C(6),CTR:C(4),DEP:C(3),ART:C(18),MCC:C(5),CFO:C(5),SIC:C(3),  
 rem  QTA:N(40),PRZ:N(40),VLR:N(40),PRZNET:N(40),CST:N(40),VLRCST:N(40),  
 rem  TMV:C(3),TDC:C(3),DETFATT:N(40),CMER:C(30),CIVA:C(30),  
 rem  OPE:C(3),RORD:C(19),CAP:C(8),ZIVA:C(2),  
 rem  DTLT:C(8),LTMT:C(18),CELLA:C(10),FLGT:C(1),  
 rem  RF1:C(17),RF2:C(17),FLG_ERR:C(1)         
   
 call "rwusdb::SUB_SQLPREP_MV2",d_in$,d_out$  
 D_IN  
 >1 X0  
 >2 Tipo elaborazione (campi da presentare e ordinamento)  
 >3 Valori di filtro  
 >4 Eventuale clausola order by  
 D_OUT  
 Risultato elaborazione nella forma $09/$0A   
 Il Tipo elaborazione rappresenta i vari output che si vogliono ottenere. 1 sara' ad esempio video skeda totale, 2 video venduto clienti etc  
   
   
 Lo sviluppo considera  
 > i campi  
 > il loro contenuto  
 > gli operatori logici che li collegano (and/or)  
 > le condizioni (= <> >= < etc)  
 > l'eventuale esclusione se vuoto o zero  
 I campi in ingresso vengono forniti tramite una stringa che deve essere VALORIZZATA  
 Esempio  
 " :cfo:>:paolo:Y:3"+$0A$           +"and:art:=:giuseppe&paolo"  
  +--------------------->  and / or  (non sul primo)  
     +------------------>  Nome campo nel database  
         +--------------->  operatore  
              +----------->  contenuto da filtrare  
+-------> escludi  
    Y=se vuoto  
    y=se zero per numerici  
    D=se 00000000 o 99999999  
+-----> step non piu' utilizzato (vedi &)  
               ---> separatore di campo   
 controlla che il campo cfo sia maggiore di paolo e lo esclude se 0  
 E (and) controlla che il campo art sia uguale a giuseppe oppure paolo (la & individua una lista di elementi. per ora gestiti solo = e <> )  
 Gli attributi dei diversi campi vanno separati con | (ascii 124)  
 I diversi campi vanno separati con $0A (ascii 10)  
 Campi Speciali  
 cfo viene formattato con 00000 e trattato come num nelle esclusioni  
   
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:30 in ambiente Oblivion/ECHO*
