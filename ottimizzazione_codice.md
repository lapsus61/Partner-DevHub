---   
title:Ottimizzazione codice    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Ottimizzazione codice 
Keywords  [VELOCITA][SPEED][OTTIMIZZAZIONE][TIPS][TRICKS]

   
## CARICAMENTO STRINGHE  
   
### LEN FISSA  
Se la stringa e' composta da porzioni con lunghezza fissa, per ottenere maggiore velocita'   
- P_MX=1000   Set numero massimo di elementi   
- P_ES=1000   Set numero di elementi da aggiungere ogni qual volta la stringa risulta completamente riempita   
- P_LN=18   Set lunghezza dei singoli elementi   
- P_PS=1     Set Posizione iniziale                                  
- D_OUT$=FILL(P_MX*P_LN," ") Dimensiona la stringa (numero elementi iniziali X lunghezza elemento)  
loop ....................................  
istruzione  
istruzione  
IF P_PS+P_LN>P_MX THEN LET D_OUT$=D_OUT$+FILL(P_ES," "),P_MX=P_MX+P_ES Controllo ed eventuale espansione  
D_OUT$(P_PS,P_LN)=AR.COD$      Popola stringa con elemento corrente  
P_PS=P_PS+P_LN        Set nuova posizione iniziale  
GOTO loop            
### LEN VARIABILE CON TERMINATORE DI RIGA  
LET P_MX=5000,P_ES=5000,P_PS=1,D_OUT$=FILL(P_MX," ")       
app$=testata con $09$0A  
LET P_LN=LEN(APP$)                                                      
LET D_OUT$(P_PS,P_LN)=APP$,P_PS=P_PS+P_LN                               
FOR X=1 TO ELE                                                          
LET KMV2$=L_IN$(X*N_STEP-(N_STEP-1),18)                                 
LET MV1$=FILL(LEN(MV1$)," ")                                            
LET MV3$=FILL(LEN(MV3$)," ")                                            
READ RECORD(709,KNUM=0,KEY=KMV2$,DOM=10360)MV2$                         
READ RECORD(709,KNUM=0,KEY=KMV2$(1,14)+"0000",DOM=10320)MV1$            
ON TIP GOSUB 0010,SUB_SUB_RG1  
app$=riga con $09$0A                                           
LET P_LN=LEN(APP$)                                                      
IF P_PS+P_LN>P_MX THEN LET D_OUT$=D_OUT$+FILL(P_ES," "),P_MX=P_MX+P_ES  
LET D_OUT$(P_PS,P_LN)=APP$,P_PS=P_PS+P_LN                               
REM ...                                                                 
NEXT X      
LET D_OUT$=CVS(D_OUT$,2)  
   
   
### LEN VARIABILE SENZA TERMINATORE DI RIGA  
Codice per scrivere nella mappa:  
REM P_PS e' la posizione (es. 1450)  
REM L_TMP e' la lunghezza (es. 12)  
REM Comprimo i due numeri in una stringa di 4 caratteri totali  
LET INFO$ = BIN(P_PS, 3) + BIN(L_TMP, 1)  
REM Ora INFO$ e' sempre lunga 4 byte, qualunque siano i numeri.  
LET K_MAP$(M_PS, 4) = INFO$  
Codice per leggere dalla mappa (il 5  elemento):  
REM Voglio il 5  elemento.  
REM Siccome ogni voce e' 4 byte, l'offset e' facile:  
LET OFFSET = (5 - 1) * 4 + 1  
REM Leggo esattamente 4 byte  
LET INFO$ = K_MAP$(OFFSET, 4)  
REM Estraggo i primi 3 byte e li riconverto in numero (Posizione)  
LET START_POS = DEC( INFO$(1,3) )   
REM Estraggo il 4  byte e lo riconverto in numero (Lunghezza)  
LET LEN_DATA  = DEC( INFO$(4,1) )  
REM Ora so dove andare a pescare nel buffer dei dati!  
PRINT D_OUT$(START_POS, LEN_DATA)  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:27 in ambiente Oblivion/ECHO*
