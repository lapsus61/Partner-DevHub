---   
title:Manuale On Line -    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Manuale On Line - 
Keywords  [ToolButton 714][714][help][online][rbgres]

   
 La gestione del manuale on-line prevede la seguente configurazione  
- per la visualizzazione viene utilizzato il comando contenuto nella variabile globale 'objhelpshow'  
- se la variabile globale non risulta settata, viene utilizzato 'c:\masbi-sun\pdf_reader.bat'  
- se l'installazione prevede manuali personalizzati,   
 la variabile globale 'objhelpdir' dovra' contenere la path nella quale sono memorizzati  
 la variabile globale 'io_orgSU' dovra' contenere l'eventuale suffisso   
- se  'objhelpdir' e  'io_orgSu' risulktano entrambe non settate NON sara' possibile accedere ai manuali customizzati  
   
La variabile globale "io_orgSu", presente nel nome file, e' necessaria per i clienti che non utilizzano l'organizzazione, quindi differisce da o2b_org                                                        
      Obiettivo della Sequenza di ricerca                       
   >1 Trovare il nome del file customizzato per la io_org       
       Questo file e' unico, quindi non dipende dalla versione   
       L'organizzazione e' indicata in config  stbl("io_orgSu")  
       La path e' indicata in config stbl("objdochelp")          
   >2 Se non esiste il file customizzato,utilizzo il link       
       indicato nel permalink del programma    
   
- Il nome del file manuale standard e' composto da  
<'objHelpDir'> <nome programma> <_> <numeroprogramma> <_> <Build> <_ > <io_orgSU>  
   
- se l'organizzazione prevede file customizzati il nome diventa  
<'objHelpDir'> <nome programma> <_> <numeroprogramma> <_> <00> <_ > <io_orgSU>  
- se l'organizzazione non prevede file customizzati, oppure le variabili relative non risultano correttamente settate, il nome del programma e' rappresentato dal  
permalink indicato in gestione selettori.   
Tabella riassuntiva CMD  
| Caso | Comando |  
| xxxxx | xxxxxxxx |  
| Default | 'c:\masbi-sun\pdf_reader.bat' |  
| Custom | comando contenuto nella variabile globale objhelpshow |  
   
   
Tabella riassuntiva nome file  
| Caso          | path e nome file |  
| xxxxxxxxxx | xxxxxxxxxxxxxxxx |  
| File custom | <'objHelpDir'> <nome programma> <_> <numeroprogramma> <_> <Build> <_ > <io_orgSU> |  
| Standard    | permalink |  
| Custom ma variabili non settate | permalink |  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:28 in ambiente Oblivion/ECHO*
