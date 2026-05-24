---   
title:Selezionare un elemento di un list button    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Selezionare un elemento di un list button 
Keywords  [LISTBUTTON[[LB][PGM:rbgsed][SEL]

   
   
 Inizializza la lista   call "rbgled",gb__SYSGUI,TMP$,CWK,ID  
 Legge l'elemento selezionato  APP$=CTRL(GB__SYSGUI,ID,1),APP=NUM(APP$(1,2))  
 Seleziona un elemento  CALL "rbgsed",GB__SYSGUI,ID,VALORE$,0  
 -----------------------------------------  
 Event Code / Flags  
 got focus  
 lost focus     
 list selection  l  
 list open  N 1 The user clicked the drop-down arrow on the list edit or list button control to display the list.  
 list select  N 2 The user selected an item from the displayed list.  
 LISTCLOSE N 3  List was closed, and is no longer displayed  
 LISTCANCEL N 4 The user canceled the selection process.  
 LISTCHANGE  N 5 Selected item(s) in the list were changed.  
   
   
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
INIZIALIZZA  
REM > psg_sysgui Canale X0                                              
REM > TMP$       Variabile con vari elementi separati da $0a$           
REM > CWK        0=Carica la variabile indicata in TMP$                 
REM >            1=dal param                                            
REM >           -1=da una tabella                                       
REM >           -2=da indirizzi supplementari                           
REM >           -3=from A7                                              
REM >           -4=from User                                            
REM >           -5=from file txt                                        
REM >           -6=from file banche ricezione crediti   con ########nn  
REM > PSG_ID     ID Oggetto                                             
call "rbgled",gb__SYSGUI,TMP$,CWK,ID  
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------   
Seleziona   
   
 CALL "rbgsed",GB__SYSGUI,1001,"00",ELE  
   
   
ENTER PSG_SYSGUI,PSG_ID,CODICE$,ELE                 
REM CODICE$=CVS(CODICE$,3)                          
REM Out : codice$ > codice da ricercare             
REM       ele     > posizione in cui si e' trovato  
REM               > -1= non trovato      
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:24 in ambiente Oblivion/ECHO*
