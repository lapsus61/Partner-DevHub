---   
title:Integra/modifica un paragrafo nel file rd_hide.txt    
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Integra/modifica un paragrafo nel file rd_hide.txt 
Keywords  [RD_HIDE][DOC][INTEGRA][MODIFICA][PGM:suhide::sub_load_ps_build2][PGM:suhide::sub_load_ps_build3]

   
   
 >Cerco il paragrafo all'interno del file rd_hide.txt (per eventuale modifica)  
 T_FIND$=<2 asterischi>Controllo permessi [CW][PERMESSI][PRIVILEGI][PERMS][PGM:smd_cpw]"  
 CALL "suhide::sub_load_ps_build2",T_FIND$,T_PAR$,T_NOPAR$                  
 Qui ho ottenuto in t_par$ il testo del paragrafo (se trovato) e in t_nopar$ il contenuto del file TRANNE t_par$  
 >Integro : quindi ricrea il file rd_hide.txt con il contenuto di t_nopar$ e aggiunge in coda t_par$  
 ATTENZIONE : le righe di T_PAR$ devono contenere il terminatore $0D$  
 CALL "suhide::sub_merge_ps_build3",T_PAR$,T_NOPAR$                         
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:20 in ambiente Oblivion/ECHO*
