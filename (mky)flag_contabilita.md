---   
title:(MKY)Flag Contabilita    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# (MKY)Flag Contabilita 
Keywords  [PN.FLG1][PN.FLG2][FLAG][CONTABILITA][EC][EC.FLG2]

PN_FlagFlag Contabilita [PN.FLG1][PN.FLG2][FLAG][CONTABILITA][EC][EC.FLG2]  
 ----------------------------------------------------------------------------------------- PN.FLG1 2,1 Dare/Avere 4,1 Iva Sospesa 5,1 Flag 770 6,1 Flag Estratto conto NLCY 7,3 Codice Tipo documento contabilita se operazione reverse charge - se si car  
ica anche 11,1 con "2" (vedi rcagiv) (va poi in mi.doc) 10,1 Tipo codice piano dei conti (pc.tip$) 11,1 Contiene identificatore registro 2 (vendit) se tipo documento reverse charge (vedi 7,3) (rcagiv va in mi.idf) 12,1 Segno Iva +/- (vedi rcagiv) (va  
 in mi.siva$) 15,1 A=Registrazione relativa ad apertura di bilancio (rcagpn) C=Registrazione relativa a chiusura di bilancio (rcagpn) ----------------------------------------------------------------------------------------- PN.FLG2 1,1 legato a rcdls  
3 2,1 codice valuta 3,1 legato a rcriac 4,1 legato a rcdlmk 8,1 Controllo registrazione automatica fatture acquisto smd_arx : Controllo di magazzino fattura/ddt 9,1 Controlli registrazione automatica fatture acquisto smd_arx *=Inserita da smd_arx 10,  
1 Controlli registrazione automatica fatture acquisto smd_arx Y = Cliente creato da smd_arx 11,1 Controlli registrazione automatica fatture acquisto smd_arx : Iva 12,1 Controlli registrazione automatica fatture acquisto smd_arx : Ordine 13,1 Controll  
i registrazione automatica fatture acquisto smd_arx : Contabilita generale 14,1 Controlli registrazione automatica fatture acquisto smd_arx : Contabilita analitica 15,1 Controlli registrazione automatica fatture acquisto smd_arx : E/C ---------------  
------------------------------------------------------------------------- EC.FLG2 - rcagec LET EC.FLG2$=PN.FLG1$(11,1); IF EC.FLG2$="6" THEN LET EC.FLG2$="2" LET EC.CVAL$=PN.FLG2$(2,1) IF EC.FLG2$=" " THEN LET EC.FLG2$=STR(POS(EC.FLG1$="AD")) -------  
--------------------------------------------------------------------------------------  
--  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:12 in ambiente Oblivion/ECHO*
