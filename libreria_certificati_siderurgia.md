---   
title:Libreria certificati siderurgia    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Libreria certificati siderurgia 
Keywords  [N][SIDER][CERT][DBR][MV2][CFERR][g03][p18][p95][FERRIERE][rwusdb][g04][g05][NTC2018][g-rwusdb][CODESTD]

   
Questa libreria viene utilizzata per ottenere la rintracciabilita' dei materiali utilizzati nelle commesse di lavorazione siderurgia, gestire i verbali di prelievo e collegare i documenti allegati.  
Il flusso prevede  
   
- Ingresso merce da fornitore C01 o C02 con indicazione della COLATA  
- Registrazione nel DMS aziendale dei certificati allegati al carico  
- Inserimento degli ordini di lavorazione siderurgia del prodotto finito richiesto, con indicazione delle materie prime necessarie in qualita' e quantita'  
- Generazione dei verbali di prelievo per analisi  
- Registrazione, in fase di lavorazione, della ferriera/articolo/colata utilizzata per ogni commessa/materia prima lavorata  
- Vendita/Evasione ordine del prodotto finito  
- Emissione dei certificati collegati alle materie prime utilizzate  
   
## Elenco Template  
### g03  
La template g03 sul file w30/rfpg tipo record C contiene le relazione tra le righe di commessa e le righe del movimento di carico della materia prima utilizzata  
Posso quindi conoscere quali righe dei movimenti di carico MP (quindi ferriera/diametro/colata) ho utilizzato per la produzione di una commessa e,  
 viceversa, in quali commesse sono state utilizzate le le righe del movimento di carico della materia    
- key 0  Il collegamento tra la riga di commessa e i movimenti di carico C01. La riga di commessa 'KCOM' ha utilizzato la merce di cui al carico 'RIFMV'  
- key 1 non utile (serve a g01 per le fasi)  
- key 2 Il collegamento tra i movimenti di carico C01 e la riga di commessa. Il carico 'RIFMV' e' collegato alle righe di commessa 'KCOM'   
   
### g04   
La template g04 sul file w30/rfpg tipo record V contiene i dati di testata dei verbali di prelievo che accompagnano la merce al laboratorio di analisi esterno.  
La key e' <V(1)>+<anrf(4)>+<nrrf(6)>+<fill(17)>  
### g05   
La template g05 sul file w30/rfpg tipo record M contiene l'elenco dei movimenti di carico (quindi ferriera/diametro/colata) inviati al laboratorio di analisi con   
 relativo numero di verbali di prelievo ed esito  
- key 0 <M>+<movimento di carico aaaammggnnnnnncccc> righe inviate al laboratorio (da cui posso ricavare ferriera/diametro/colata/qta)  
- key 1 non utile  
- key 2 <M>+<anno e numero verbale di prelievo aaaannnnnn > mi permette di collegare il record al verbale di prelievo relativo    
   
## Elenco Routine  
   
 call "g-rwusdb::SUB_G03_FINDC01"," | dep | art | dtin | cfo  |  | ggpre |",d_out$ CERCA CARICHI PER SELEZIONE COLATA  
 call "g-rwusdb::SUB_G03_LCOM"," |keymovimento  | 1 |",d_out$   Restituisce  le righe di commessa collegate ad un carico di magazzino  
 call "rwusdb::SUB_G05_LVPRE",d_in$,d_out$    Restituisce gli articoli inseriti  in un verbale di prelievo   
 call "rwusdb::SUB_G03_MOVCTR"," | keycommessa | keymovimento |",d_out$ Fornita la key della riga di commessa e la key TRONCA  
          del movimento di magazzino, mancante cioe' del ctr,  
          restituisce la key magazzino completa eseguendo la ricerca  
          per codice articolo dbr.art uguale a mv2.art       
 call "rwusdb::SUB_G03_INS"," | keycommessa | key movimento |",d_out$  Fornita la key della riga di commessa e la key del movimento  
          di magazzino genera il record g03/w30  
 call "rwusdb::SUB_G03_DEL"," | keycommessa |",d_out$   Fornita la key della riga di commessa la cancella  
 call "rwusdb::SUB_G03_LMOV"," | keycommessa |",d_out$   Fornita la key della riga commessa completa (18+4+4)  
          restituisce i movimenti collegati e nei quali sono presenti  
          i certificati di materia prima  
 call "rwusdb::SUB_G03_LCOM"," |keymovimento  | 2 |",d_out$   Fornita la key del movimento di magazzino,restituisce la dbr.qta  
          totale delle righe comm collegate  
          
## CERCA CARICHI PER SELEZIONE COLATA                                             
 Restituisce i carichi C01/C02 eseguiti in un arco temporale da oggi a oggi-p_dt sul range di articoli artin-artfn  
 call "rwusdb::SUB_G03_FINDC01"," | dep | art | artfn | cfo  | p_dt | p_out |",d_out$  
 Il d_out nella forma $09$0A viene restituito nella forma  
  Riferimento movimento-->088+$09$  
  Data Carico-->091+$09$  
  Codice Articolo-->000000000Iog:p12+$09$  
  Codice Ferriera-->000000000Iog:p05+$09$  
  Qta Movimento-->170+$09$  
  Colata+$09$  
  Nr verbale di prelievo+$09$  
  Residuo Qta+$09$  
  %Utilizzo-->122+$09$  
  $0A$  
DIN$  
- [1] X0$  
- [2] DEP$ Codice deposito - default 001  
- [3] ArtIn$ Codice articolo inizio  
- [4] ArtFn$ Codice articolo fine  
- [5] CFO$ Codice Ferriera - NON UTILIZZATO  
- [6] P_DT ggpre Giorni precedenti alla data indicata da cui iniziare il controllo - default 180  
- [7] P_out NON UTILIZZATO  
   
   
D_OUT$  
 Riferimenti movimenti dtrg+nrrf+ctr(088) Ferriera(Iog:p05) QtaMovimento(170) Cella  
   
## COMMESSE                                               
Fornita la key del movimento di magazzino,restituisce  le righe di commessa collegate   
   
 call "rwusdb::SUB_G03_LCOM"," |keymovimento  | 1 |",d_out$   
   
   
## VERBALI DI PRELIEVO  
Fornita il numero del verbale di prelievo, ne restituisce gli articoli inseriti                                     
 call "rwusdb::SUB_G05_LVPRE",d_in$,d_out$  
-1 LET X0$=REC_IN.CPO$[1]                                         
-2 LET ANRF$=STR(NUM(REC_IN.CPO$[2]):"0000")                      
-3 LET NRRF$=STR(NUM(REC_IN.CPO$[3]):"000000")     
   
d_out$="Articolo" "Descrizione" "Fornitore" "RagioneSociale" "Colata" "Esito"  
   
   
## CTR MOV                                   
Fornita la key della riga di commessa e la key TRONCA del movimento di magazzino, mancante cioe' del ctr, restituisce la key magazzino completa        
eseguendo la ricerca per codice articolo dbr.art uguale a mv2.art   
 call "rwusdb::SUB_G03_MOVCTR"," | keycommessa | keymovimento |",d_out$  
   
## INSERT                                  
Fornita la key della riga di commessa e la key del movimento di magazzino genera il record g03/w30  
   
 call "rwusdb::SUB_G03_INS"," | keycommessa | key movimento |",d_out$                 
   
## DELETE                                  
Fornita la key della riga di commessa la cancella  
    
 call "rwusdb::SUB_G03_DEL"," | keycommessa |",d_out$                          
   
## MOVIMENTI                                             
Fornita la key della riga commessa completa (18+4+4) restituisce i movimenti collegati e nei quali sono presenti i certificati di materia prima         
   
 call "rwusdb::SUB_G03_LMOV"," | keycommessa |",d_out$  
   
   
## QUANTITA                                               
Fornita la key del movimento di magazzino,restituisce la dbr.qta totale delle righe comm collegate   
   
 call "rwusdb::SUB_G03_LCOM"," |keymovimento  | 2 |",d_out$  
   
!!! info    "NOTA"  
    *se trova un record di START, un record quindi con commessa valorizzata a zero, questo viene considerato come qta=1 nella somma*  
   
## INIZIALIZZAZIONE  
 Per definire una data di 'START', una data cioe' per la quale siano stati generati i provini e da cui si vuole partire,  
 ad evitare quindi di utilizzare un movimento di carico C01 casuale, va inizializzato il file per ogni ferriera/diametro.  
 Per far cio', inserisco una riga nel file w30 relativa al carico C01 che mi interessa  con KCOM$ valorizzata a zero                  
   
 call "rwusdb:: SUB_G03_INIT","x0 | Key movimento aaaammggnnnnnnctr |  
!!! info "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:30 in ambiente Oblivion/ECHO*
