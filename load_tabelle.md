---   
title:Load tabelle    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Load tabelle 
Keywords  [usr][tab][sic][a7][txt][tpar][ope]

   
   
   
rbgled  gb__sysgui,TMP$,CWK,psg_id  
cwk = 0 - label$  
cwk = 1 - lfrom_tpar  
cwk = -1 LFROM_TAB  
cwk = -2 LFROM_SIC popola il list button indicato in psg_id  
cwk = -3 LFROM_A7  
cwk = -4 LFROM_USR (load tabella utenti)  
cwk = -5 LFROM_TXT  
   
   
## User  
ResBuilder : inserire nel nome del list button nf:iogUSR  
 per forzare il primo elemento <Elemento iniziale< (apparira' come prima voce)  
 per forzare l'ultimo elemento >Elemento finale> (apparira' come ultima voce)  
 <Elemento iniziale<>Elemento finale> appariranno rispettivamente  come prima e ultima voce  
   
GuiBuilder : rbgled  gb__sysgui,"",-4,ID  
   
## TAB  
   
   
## SIC  
 call "rbgled",gb__sysgui,"00000",-2,psg_id  
 gb__sysgui Canale sysgui  
 tmp$  Codice cliente formattato '00000' -  Se inizia con < aggiunge il '   nessuna selezione iniziale'  
 cwk  -2 questa opzione  
 psg_id  Oggetto list button che conterra' la lista delle destinazioni  
   
## A7  
   
## TXT  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:30 in ambiente Oblivion/ECHO*
