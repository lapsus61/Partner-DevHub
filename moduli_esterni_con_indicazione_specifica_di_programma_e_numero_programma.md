---   
title:Moduli esterni con INDICAZIONE specifica di programma e numero programma    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Moduli esterni con INDICAZIONE specifica di programma e numero programma 
Keywords  [rbg28N][28000][ResBuilder][brc]

   
   
Se la call ha necessita' di parametri, questi possono essere acquisiti dalla form/child o passati da codice  
>I dati da passare SONO PRESENTI nella form/child  
Indicare nel name dell'oggetto la sequenza 28_cpo:0000100100101050,pgm:yyyyyy,nrpgm:abc_28  
Il programma eseguira' il pgm/nrpgm passando utilizzando come parametri il contenuto dell'id 1001 del ctx 0 PIU' il contenuto  
dell'id 1050 del contesto 1  
ATTENZIONE: per questo tipo di utilizzo, NESSUNA routine deve essere attivata sul tasto interessato, neanche vuota.  
>I dati da passare NON sono presenti nella form/child (per esempio in una o piu' celle della griglia)  
Indicare nel name dell'oggetto la sequenza 28_cpo:00000000,pgm:yyyyyy,nrpgm:abc_28  
Nell'evento desiderato, settare il valore della variabile globale 'rbg28n_name' con il valore richiesto   
Il programma eseguira' il pgm/nrpgm utilizzando come parametri il contenuto della variabile globale 'rbg28n_name'  
>ALCUNI dati sono presenti nella form/child ed altri NON lo sono  
Indicare nel name dell'oggetto la sequenza 28_cpo:0000000000001001,pgm:yyyyyy,nrpgm:abc_28  
Nell'evento desiderato, settare il valore della variabile globale 'rbg28n_name' con il valore richiesto  
Il programma eseguira' il pgm/nrpgm utilizzando come parametri il contenuto della variabile globale 'rbg28n_name' PIU'  
il contenuto dell'id 1001 del ctx 0  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:20 in ambiente Oblivion/ECHO*
