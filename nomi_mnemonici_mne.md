---   
title:Nomi Mnemonici MNE    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Nomi Mnemonici MNE 
Keywords  [MNE][GRID][FIND][CERCA]

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
E' possibile gestire il nome mnemonico delle colonne cosi da trovarle anche se la posizione viene modificata rispetto alle altre. Se, per una implementazione successiva, decidiamo di modificare la sequanza delle colonne, con l'utilizzo del mnemonico  
non e necessario modificare il programma nel quale la griglia viene visualizzata/gestita. La colonna va intestata con l'indicatore 'Mne:' Ad esempio vogliamo intestare una colonna con il menmonico KeyF, scriveremo :   
   
 testata$="Codice"+$09$+"Ragione Sociale"+$09$+"Cod.Articolo"+$09$+"Descrizione"+$09$+"Mne:KeyF"+$09$+$0A$   
sara' quindi poi possibile accedere alla colonna KeyF anche se la testata dovesse diventare  
 testata$="Codice"+$09$+"Ragione Sociale"+$09$+"Cod.Articolo"+$09$+"Mne:KeyF"+$09$+"Descrizione"+$09$++$0A$   
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
Vedi Libreria griglia  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:25 in ambiente Oblivion/ECHO*
