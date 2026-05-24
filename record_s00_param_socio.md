---   
title:Record s00 param socio   
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Record s00 param socio
Keywords  

REC_S00Record s00 param socio  
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------   
- 261,1 Estratto conto - rcepae - IF REC_S00$(261,1)="Y" AND POS(EC1.TIP$="CWA")>0 THEN GOTO 2670   
- 262,1 Estratto Conto - rcepae - REC_S00$(262,1)="Y" AND EC1.TIP$="*" AND EC1.CDPG$="399" THEN GOTO 2670   
- 263,1 Estratto Conto - recpae - 2750 IF REC_S00$(263,1)="Y" AND MP.TSC$="1" AND DTSC_RB$<DATAS$ AND EC1.FLG2$="1" THEN GOTO 2670 -----------------------------------------------------------------------------------------------------------------------  
-------------------------------------------------------------------------------------- 0 Filler  
-1 1 Esegue aggiornamento real time dei costi da movimento  
- 81 88 Data inizio ultimo aggiornamento maya Maya  
- 89 96 Data fine ultimo aggiornamento maya Maya  
- 97 104 Data nella quale e  stata eseguita l ultima elaborazione Maya  
- 105 105 Aggiormento file mensili per il periodo eseguito? (Y/N) Maya  
- 106 106 Aggiornemento file giornalieri avvenuto eseguito ? (Y/N) Maya  
- 107 107 Temporaneo per stand alone Maya  
- 121 129 Data trasmissione liquidazione iva 9 (sembra che da edil sia 121,5 numero mandato)  
- 131 140 Ultimo numero di analisi in g-rmvran per le singole voci di analisi certificato -   
- 141 150 Ultimo numero di analisi eseguito forme solide (T/D/1) omeo 10 / Se nessuna distinzione tra liquide e soldie, utilizzo questo per il certificato FINALE   
- 151 153 Versione ciclo di analisi collegato (nome file rfva::-nnn.txt) omeo 3   
- 161 170 Ultimo numero di analisi eseguito forme liquide (B/L/9/M) omeo 10   
- 171 176 Ultimo numero di odp assegnato Produzione 6 16/06/2015   
- 177 181 Ultimo numero di odp assegnato agli addendum Produzione 5 16/06/2015  
- 182 182 Sigla addendum (viene utilizzata come prefisso di 177-181) Produzione 1 16/06/2015   
- 200 200 Flag produzione: consente inserimento ordini destinati alla diluiteca Y=consente N=No omeo 1   
- 201 201 Flag produzione: consente inserimento ordini corriere 100destinati alla diluiteca Y=consente N=No omeo 1   
- 202 211 Numero progressivo lotto interno per ingresso materie prime ar.anli$= 1? magazzino 10   
- 251 251 Installazione con gestione OMEO 1 21/03/2017   
- 252 252 Y=il numero di LOTTO e la SCADENZA definitivi vengono assegnati in fase di autorizzazione QP Omeo 1 12/04/2017   
- 253 254 Colonna di rappresentazione del codice articolo in g-omgodp 2   
- 255 256 Colonna di rappresentazione della data di consegna in g-omgodp 2   
- 257 259 Codice deposito di default per produzione prodotti finiti 3 20/09/2018 g-omgodp   
- 260 260 Campo da visualizzare nella griglia di selezione ordini nella colonna odp blank/0 = or2.rord$(10,6) 1=or2.nrrf$ 1 20/09/2018 g-omgodp   
- 261 261 vedi smd_uec per variazioni :In elaborazione partite estratto conto se Y non considera i contrassegni (riconoscibili da TIP=C) da verificarne la attuale utilita:il nuovo controllo verifica mp.tsc$, quindi non il tip 1 21/09/2018 rcepae+s  m  
d_uec   
- 262 262 vedi smd_uec per variazioni :In elaborazione estratto conto, se Y non considera le compensazione note credito su riba (riconoscibili da TIP=* e Modalita di pagamento=399) 1 21/09/2018 rcepae+smd_uec   
- 263 263 vedi smd_uec per variazioni :Inelaborazione estratto conto, se Y considera chiuse anche le scadenze FORNITORE se riferite ad una riba con data scadenza trascorsa da verificarne la attuale utilita: il nuovo controllo verifica mp.tsc$ quindi  
non verifica se si tratta di una R mase legato ad una scadenza chiusa automaticamnete. Il parametro e utile perche agisce sulle scadenze fornitore, ma il controllo non e  su R 1 21/09/2018 rcepae+smd_uec   
- 264 266 Giorni anticipo su data elebarazione per definire data produzione inizio(or2.dtcs) 3 4/10/2018 g-omgodp   
- 267 269 Giorni posticipo su data elaborazione per definire data produzione inizio (or2.dtcs) 3 4/10/2018 g-omgodp   
- 270 272 Giorni anticipo su data di elaborazione per definire data inizio ordine 3 8/10/2018 g-omgodp   
- 273 276 Anno corrispondente all esercizio 1  
Viene considerato SEMPRE l anno solare come esercizio, quindi con inizio 1/1 e fine 31/12 dell anno.Se ad esempio il 2018 corrisponde ll esercizio numero 28, in questo elemento va inserito 1990. 4 8/10/20  18 rpucpc   
- 279 279 Accetta invii senza sdi ne pec ? (Y/N) fatturazione elettronica 1 18/12/2018 smd_fpa   
- 280 280 Versione completamento dati 0 #ipa #pec #cfipa 1 sac.csdi em Fatturazione elettronica 1 18/12/2018   
- 281 294 Contatore univoco pallet per multipallet (Rappresenta solo la parte fissa  08013901  piu sei caratteri del id pallet, viene poi completato con progressivo riga e progressivo pallet all interno della riga) maga 14 08013901nnnnnn   
- 301 400 Valorizzazione eseguita nell anno relativo Y=Si  
- 301=1991 302=1992  . 311=2001 maga 50 50   
- 401 408 Ultimo codice Prospect/Contatto attribuito Contatti 8   
- 409 416 Ultimo numero di richiesta hw/sw attribuito Richieste hw/sw 8   
- 417 418 ?? non so cosa sia   
- 445 447 Codice tipo documento di default associato al modulo ordini CLIENTI 12/04/2024   
- 448 450 Codice tipo documento di default associato al modulo ordini CLIENTI ESTERI 12/04/2024   
- 451 453 Codice tipo documento di default associato al modulo ordini fornitori ordini 3 30/08/2017   
- 454 456 Codice tipo documento di default associato al modulo ordini fornitori per le anagrafichecon zona iva diversa da IT ordini 3 30/08/2017   
- 457 459 Codice tipo documento per Proforma (solo Ordini Clienti ) (flag su Anagrafica Cli SAC$)   
- 461 520 Certificazione PEFC dell azienda. Inserire una nota esattamente cosi come si voglia appaia sui documenti.   
- 501 505 Ultimo codice paziente attribuito Medici 5 (sovrascitto da PEFC !!!..... qualcuno lo usa ??)   
- 601 630 Lista codici deposito   step 3   sui quali verificare la giacenza in add odp.  
NON PUO  ESSERE la lista restituita da rmuldp poiche, per la stessa societa, potrebbero essere di interesse codici deposito differenti. (Svas Ottaviano non vuole le  giacenze di Svas via Colle) 30 10/10/2018 g-omgodp   
- 631 660 Lista codici deposito   step 3   sui quali verificare la presenza di prodotti da rilasciare (quarantena) 30 10/10/2018 g-omgodp   
- 661 690 Lista codici deposito   step 3   sui quali verificare le scorte minime (di norma uno) 30 10/10/2018 g-omgodp   
- 990 991 Codice ditta per cassa comune (genera una prima nota di incasso nella ditta con codice indicato anche se movimento in altra ditta vedi smd_inc)   
- 992 992 Duplico in cassa comune i contanti ? Y=Si smd_inc   
- 993 993 Duplico in cassa comune i POS ? Y=Si smd_inc   
- 994 994 Duplico in cassa comune gli abbuoni ? Y=Si smd_inc  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:27 in ambiente Oblivion/ECHO*
