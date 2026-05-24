---   
title:VPRO5    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# VPRO5 
Keywords  [bin][dec]

   
--  
BIN e DEC sono funzioni fondamentali in Business BASIC quando si vuole risparmiare memoria e creare strutture dati a "lunghezza fissa" (come la mappa che ti ho suggerito).  
In breve: servono a tradurre i numeri in caratteri macchina e viceversa. Ecco come funzionano, spiegati in modo semplice.  
   
  
## Il concetto base  
Immagina il numero 12345.  
Come Stringa (STR(12345)): Occupa 5 byte di memoria ("1", "2", "3", "4", "5").  
Come Binario (BIN(12345, 2)): Occupa solo 2 byte.  
Perche'? Perche' BIN non scrive le cifre leggibili, ma scrive direttamente il valore numerico dei byte in memoria (in esadecimale o ASCII).  
BIN(): Comprime un numero in una stringa di byte "raw".  
DEC(): Prende una stringa di byte "raw" e la riconverte in numero leggibile.  
   
  
## BIN (Binary)  
La sintassi e': X$ = BIN(numero, lunghezza_in_byte)  
Devi decidere quanti byte usare in base a quanto grande puo' essere il numero:  
1 Byte: Contiene numeri da 0 a 255.  
2 Byte: Contiene numeri da 0 a 65.535.  
3 Byte: Contiene numeri da 0 a 16.777.215.  
Esempio:  
LET A = 65  
LET A$ = BIN(A, 1)  
PRINT A$   
REM Stampa: "A" (perche' il codice ASCII di A e' 65)  
LET B = 12345  
LET B$ = BIN(B, 2)  
REM B$ conterra' due caratteri strani (non leggibili a occhio nudo),   
REM ma per il computer sono il valore 12345 compresso.  
   
  
## DEC (Decimal)  
La sintassi e': NUMERO = DEC(stringa_binaria)  
Fa l'operazione inversa. Legge i byte e ti rida' il numero.  
   
  
## Esempio:  
REM A$ contiene la versione BIN di 65  
PRINT DEC(A$)  
REM Stampa: 65  
REM B$ contiene la versione BIN di 12345  
PRINT DEC(B$)  
REM Stampa: 12345  
   
Perche' sono essenziali per la tua "Mappa"?  
Il tuo problema e' che se salvi le posizioni come numeri normali (es. "10", "150", "3045"), hanno lunghezze diverse.  
La stringa "10" e' lunga 2.  
La stringa "3045" e' lunga 4.  
Se le lunghezze sono variabili, non puoi usare la matematica per dire "vai direttamente al 50  elemento", perche' non sai dove inizia.  
Usando BIN, rendi tutto a lunghezza fissa.  
   
Applicazione pratica nel tuo caso:  
Vogliamo salvare:  
Posizione inizio (P_PS): Puo' essere un numero grande (fino a 16 milioni). Usiamo 3 byte.  
Lunghezza stringa (L_TMP): Diciamo che i tuoi codici sono max 255 caratteri. Usiamo 1 byte.  
Totale: Ogni record nella mappa e' sempre 4 byte.  
   
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
Vantaggi di questo approccio:  
Velocita' estrema: Il calcolo (N-1)*4 + 1 e' istantaneo per la CPU.  
Risparmio memoria: Se hai 10.000 articoli, una mappa di 40KB (10.000 * 4 byte) e' piccolissima e gestibilissima in memoria.  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:26 in ambiente Oblivion/ECHO*
