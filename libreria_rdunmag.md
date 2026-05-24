---   
title:Libreria rduNmag    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Libreria rduNmag 
Keywords  [N][MV2][OR2][LISTA][OR1][CODESTD]

   
 Questo progetto prevede la realizzazione di moduli con routine piu' semplici e che eseguano poche operazioni.   
 Quindi si lavora su una lista iniziale di articoli, si applicano i filtri, si sviluppa secondo le esigenze. Quello che accomuna   
 i moduli e' che lavorano sulla stessa lista step 37 composta da  
 <MVdt+MVnr+MVCTR><ORDtip+ORDdt+ORDnr+ORDctr>  
   
 Le routine rduNmag sono divise in   
    
## Routine INIT  
  Call "rduNmag::sub_get_step","",d_out$ Restituisce lo step con il quale la variabile di appoggio e' stata creata  
  call "rduNmag::sub_get_tmp","",d_out$ Restituisce la template utilizzata dalla variabile di appoggio  
## Routine di LOAD  
  call "rduNmag::sub_load_Lart"   Carica una lista di articoli applicando dei filtri   
      (questa e' una elaborazione iniziale, con lista step 18)   
  call "rduNmag::sub_load_Lor1"  Carica una lista di testata ordine fornendo cli/for   
## Routine di ELABORAZIONE  
  call "rduNmag::sub_load_Lmv2"  Carica una lista di TUTTI i movimenti relativi agli articoli  
  call "rduNmag::sub_load_Lor2"   Carica una lista degli ordini collegati agli articoli in lista  
  call "rduNmag::sub_load_Lor2_or1" Sviluppa una lista ordini testata OR1 in singole righe OR2  
## Routine di FILTRO  
  call "rduNmag::sub_filtro_Or2",  Filtra i movimenti in relazione allo stato di evasione degli ordini collegati  
  call "rduNmag::sub_filtro_Mv1",  Filtra i movimenti in relazione a Flg/Fat/Pag/Trp  
  call "rduNmag::sub_filtro_Mv2"  Filtra i movimenti in relazione a data scadenza,lotto,cella,dati supplementari UM  
## Routine di ESTRAPOLAZIONE  
  call "rwusdb::sub_load_Dbs"  Estrapola i componenti delle commesse collegate (solo righe)  
  call "rwusdb::sub_load_DbsT"  Restituisce la sola testata  
##  Routine SORT  
  call "rduNmag::sub_sort"  Esegue il sort della lista. Per il momento solo per data+nr+ctr movimento   
   
## Routine FORMATTAZIONE  
  call "rwusdb::sub_load_mv"  Formatta il contenuto restituito da LOAD_MV2  
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
## Esempi  
### Load di una lista di articoli rduNmag/ART all'interno di un range e con filtri [rduNmag]  
 call "rduNmag::SUB_LOAD_LART","x0|codart start|cod art end|",d_out$  
------------------D_IN  
 1 x0 Sysgui  Channel  
 2 codart start Codice articolo di partenza  
 3 codart end Codice articolo fine (se non passato assume inizio)  
-----------------D_OUT  
d_out$  Lista step 18 dei codici articoli selezionati e filtrati  
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
### Get LMV2  
 Elabora la lista rduNmag/ART e restituisce una lista rduNmag/MOV con movimenti mv2 e rord [rduNmag]  
   
   
 call "rduNmag::sub_load_lmv2"," |"+L_dep$+"|"+L_art$+"|"+Dtin$+"|"+Dtfn$+"|"+Rord$+"|", d_out$  
--------------D_IN  
 1 x0 Canale sysgui  
 2 L_dep Lista codici deposito da analizzare step 4  
 3 L_art Lista codici articoli da analizzare step 18  
 4 dtin Data di inizio  
 5 dtfn Data di fine  
 6 rord Riferimento ordine  
  se vuoto non esegue controlli  
  se valorizzato controlla il match con mv2.rord per la lunghezza in ingresso  
  se = all verifica che il campo sia valorizzato indipendentemte dal contenuto  
 7 tmv Lista codici tipo movimento step 3 - se vuota non esegue controlli  
   
-------------D_OUT  
D_out$ Lista movimenti considerati nella forma step 37 MV2.DTRG$+MV2.NRRF$+MV2.CTR$+MV2.RORD$  
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------   
### Get LOR2  
 Elabora la lista rduNmag/ART e restituisce una lista rduNmag/ORD con ordini or2 [rduNmag]  
    
 call "rduNmag::sub_load_lor2","x0|l_dep|tip|dtin|dtfn|l_art|", d_out$  
 NOTE  
 Poiche' non viene valorizzata la parte relativa ai movimenti, non e' possibile utilizzare le rduNmag relative   
--------------D_IN  
 1 x0 Canale sysgui  
 2 l_dep Lista codici deposito da analizzare step 4  
 3 tip Tipo ordine 1/2/3  
 4 dtin Data CONSEGNA di inizio  
 5 dtfn Data CONDEGNA di fine  
 6 l_art Lista codici articoli da analizzare step 18  
   
-------------D_OUT  
D_out$ Lista ordini considerati nella forma step 18 fill(18," ")+or2.tip$+or2.dtrg$+or2.nrrf$+or2.ctr$  
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
### Get Step  
 Restituisce lo step con il quale la variabile di appoggio e' stata creata [rduNmag]  
 Call "rduNmag::sub_get_step","",d_out$  
 Restituisce lo step con il quale la variabile di appoggio e' stata creata  
 Utile se aggiungiamo campi  
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
### Filtra OR2  
 Filtra la lista rduNmag/MOV e restituisce una lista FILTRATA sul campo or2.evs$ [rduNmag]    
 call "rduNmag::SUB_FILTRO_OR2","x0|tipoevaso|L_in|E_cfo|E_usr|e_td",d_out$  
--------------------------D_IN  
 1 x0 sysgui channel  
 2 tipoevaso  
  P Parzialmente e completamente evasi (or2.qta1<>0)  
  E Completamente evasi ( quindi or2.evs$=Y or or2.qta1>=or2.qta)  
 3 L_in Lista in ingresso step 37  
 4 E_cfo Lista step 5 dei cli/for da ESCLUDERE  
 5 E_usr Lista step 3 degli utenti da ESCLUDERE (ad esempio 000 o 999 sono prove)  
 6 e_td Lista step 3 tipo documento da escludere   
   
-------------------------D_OUT  
d_out$  Lista movimenti considerati nella forma step 37 della lista in ingresso ad esclusione dei risultati non   
  filtrati   
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
### Filtra MV1/MV3  
 Filtra la lista rduNmag/MOV su campo mv1$ e mv3$ [rduNmag]  
 call "rduNmag::SUB_FILTRO_MV1"," |"+mv1flg+"|"+fat$+"|"+mv3mpg$+"|"+trp$+"|"+L_in$+"|"+cfo$+"|"+td$+"|",d_out$  
 D_IN  
 1 x0 sysgui channel  
 2 mv1flg Lista step 1 valori MV1.FLG consentiti (se vuota tutti)  
 3 fat Lista step 1 valori determina fatturato consentiti Y/N/C (se vuota tutti)  
 4 mpg Lista step 3 valori 'codice pagamento' consentiti (se vuota tutti)  
 5 trp Lista step 3 valori 'trasportatore' consentiti (se vuota tutti)  
 6 L_in Lista in ingresso  
 7 cfo$ codice cliente da escludere nel formato nnnnn  
 8 td$ codice tipo documento da escludere - 3chr  
 D_OUT  
 d_out$ Lista movimenti considerati nella forma step 18 MV2.DTRG$+MV2.NRRF$+MV2.CTR$+MV2.RORD$  
------------------------------------------------------------------------------------------------------------------------------------------  
### Filtra MV2  
 Filtra la lista rduNmag/MOV su MV2 per data scadenza lotto, numero lotto, cella, dati supplememntari UM  
 D_IN  
 1 X0$  
 2 DTSCMN$  
 3 DTSCMX$  
 Ctl Lotti      ltmt0$ > 0=NoCtl 1=Inizia 2=Contiene 3=esatto    
 4 LTMT0$  
 5 LTMT$ CVS(REC_IN.CPO$[5],2)  
 Ctl Cella     cella0$ > 0=NoCtl 1=Inizia 2=Contiene 3=esatto    
 6 CELLA0$  
 7 CELLA$ CVS(REC_IN.CPO$[7],2)  
 Ctl MVU        prog0$ >  0=NoCtl 1=Ovunque 2=Ctl singolo prog   
 8 PROG0$  
 9 PROG1$ CVS(REC_IN.CPO$[9],2); REM  se 'Ovunque' va valorizzato  
 10 PROG2$ CVS(REC_IN.CPO$[10],2)                                   
 11 PROG3$ CVS(REC_IN.CPO$[11],2)                                   
 12 PROG4$=CVS(REC_IN.CPO$[12],2)        
-------------------------------------------------------------------------------------------------------------------------------------------------                             
### Sviluppa Mov  
 Sviluppa la lista generata da rduNmag generando l'elenco dei movimenti con diverse sequenze di colonne  
 call "rduNmag::SUB_LOAD_MV"," |"+tipo$+" | | | |"+L_in$+"|",d_out$  
 D_IN  
 1 x0 sysgui channel  
 2  tipo output  
 3 / 4 / 5  future espansioni  
 6 L_in Lista in ingresso  
 D_OUT  
 d_out$ Lista nella forma $09$0A  
 tipo$ =1  
  KeyMov-->088  
  Data-->091  
  Movimento  
  Dep-->000000000Iog:p36  
  Articolo-->000000000Iog:p12  
  Qta-->172  
  Cliente-->000000000Iogp05  
  RifDoc-->089          
 tipo$ = 2 "KeyMov-->088"+$09$+"Data-->091"+$09$+"Movimento"  
  +$09$+"Dep-->000000000Iog:p36"+$09$+"Articolo-->000000000Iog:p12"  
  +$09$+"Qta-->172"+$09$+"Colata"+$09$+"Cliente-->000000000Iog:pp05"  
  +$09$+"DocConsegna-->089"+$09$+"DocFRP-->089"+$09$+$0A$    
   
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
### Sort  
 Esegue il sort della lista lmov. Al momento solo per prima colonna dtrg+nrrf+ctr movimento.  
 Da utilizzare quando la lista contiene piu' articoli i cui movimenti vengono letti sequenzialmente  
 call "rduNmag::sub_sort"," |"+tipo$+" | | | |"+L_in$+"|",d_out$  
 D_IN  
 1 x0 sysgui channel  
 2  tipo output  
 3 / 4 / 5  future espansioni  
 6 L_in Lista in ingresso  
  tipo$  
   1 = Data + numero + ctr movimento  
   2 = da implementare  
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
### Sviluppa DiBa  
 Sviluppa la lista generata da rduNmag generando l'elenco dei componenti di commessa collegati  
   
 call "rwusdb::SUB_LOAD_DBS",d_in$,d_out$  
   
 D_IN$  Lista Generata da rduNmag   
 D_OUT$  Dati griglia in formato $09/$0A  
   
 call "rwusdb::sub_load_DbsT"  restituisce la sola testata  
  D_IN Null  
  D_OUT Testata  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:29 in ambiente Oblivion/ECHO*
