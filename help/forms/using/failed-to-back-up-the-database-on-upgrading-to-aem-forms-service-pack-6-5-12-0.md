---
title: Errore nel backup del database durante l'aggiornamento a 6.5.12.0 per MySQL.
description: Quando un utente esegue l’aggiornamento alla versione 6.5.12.0 dell’Experience Manager e fa clic su "Upgrade MySQL" (Aggiorna MySQL), il gestore della configurazione non riesce a eseguire il backup del database Experience Manager Forms precedente.
source-git-commit: a9d59e00efe8f0c2cbfca51901c441a2d65b70f2
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Errore durante il backup del database durante l&#39;aggiornamento a 6.5.12.0 per MySQL {#issue}

Quando un utente esegue l’aggiornamento alla versione 6.5.12.0 dell’Experience Manager e fa clic su &quot;Upgrade MySQL&quot; (Aggiorna MySQL), il gestore della configurazione non riesce a eseguire il backup del database Experience Manager Forms precedente e viene visualizzato il messaggio di errore:

`Failed to backup the previous Adobe Experience Manager Forms Database`


## Si applica a {#applies-to}

* Experience Manager 6.5 Forms

## Soluzione {#solution}

Per risolvere il problema, aumentare il valore di max_packet_size del database a 100 M o come richiesto nel file my.ini che si trova in {AEM_HOME}/mysql.
