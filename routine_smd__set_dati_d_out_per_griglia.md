---   
title:Routine SMD >SET DATI D_OUT PER GRIGLIA   
description:   
---   
![LogoRdep](./immagini/RDePPartnerEnterprise.png)
# Routine SMD >SET DATI D_OUT PER GRIGLIA
Keywords  

   
   
 Routine SMD  
 Routine SMD >SET DATI D_OUT PER GRIGLIA  
======================Caratteristiche Colonna======================== GCPS$[1]=x yy frc:zzzzzz bkc:wwwwww Bnf:Filenm_par:parnm Iog:xxx _____________________________________________________________ x Alignment 0=Sx (Alfa) 1=Dx (Num (<0 in rosso)) 2=C  
entro 3=Dx (Num (<0 in rosso)) % 4=Dx (Num (<0 in rosso =0 null) ____________________________________________________________ yy Style 4 checked box 8 unchecked box 91 data gg/mm/aaaa 92 data gg/mm/aa 96 data gg/mm/aaaa-hh:mm:ss 97 ora hh:mm:ss xy In  
teri + Decimali se numerico ____________________________________________________________ frc Color 3Byte forecolor ___________________________________________________________ bkc color 3byte backcolor _________________________________________________  
__________ Bnf Indicatore LB echo Filenm = Nome file _par: indicatore fisso di inizio nome paragrafo parnm = Nome paragrafo Iog____________________________________________________________ Key IOG ! ! ! ! ! ! +--------+-- + Color definire il valore di  
red/grn/blu in color map di un pgm carattere determinare il valore esadecimale con hta(chr(numero)) esempio grigio=128,128,128 hta(chr(128))=80 color = $808080$ ... altre .................................. Hide: Colonna non visibile e non stampabile  
(set larghezza 0) Mne:xxx Nome campo associato alla col (fino alla fine o next -->) ======================Caratteristiche Cella========================== Riconoscibile da '->' nella cella al termine dei dati 'img:' immagine associata 'frc:' colore fo  
reground 'bkc:' colore background 'rwh:' altezza riga in pixel (0 se invisibile) - va settato solo nella prima cella della riga  
--  
!!! info    "*Documentazione Partner - Developer kit*"
    *Specifica aggiornata il 24/05/2026 alle ore 20:59:24 in ambiente Oblivion/ECHO*
