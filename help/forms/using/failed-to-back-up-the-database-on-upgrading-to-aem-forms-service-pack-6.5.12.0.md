---
title: Impossibile eseguire il backup del database precedente su AEM Forms 6.5.12.0.
description: Quando un utente esegue l’aggiornamento alla versione 6.5.12.0 dell’Experience Manager e fa clic su "Upgrade MySQL" (Aggiorna MySQL), il gestore della configurazione non riesce a eseguire il backup del database Experience Manager Forms precedente.
source-git-commit: d232bfdad7b8413eb015f6fe5dd3442cebf1001d
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 1%

---

# Problema (#issue)

Quando un utente esegue l’aggiornamento alla versione 6.5.12.0 dell’Experience Manager e fa clic su &quot;Upgrade MySQL&quot; (Aggiorna MySQL), il gestore della configurazione non riesce a eseguire il backup del database Experience Manager Forms precedente e viene visualizzato il messaggio di errore:

`Failed to backup the previous Adobe Experience Manager Forms Database`


## Si applica a {#applies-to}

* Experience Manager 6.5 Forms

## Soluzione {#solution}

Per risolvere il problema, aumentare il valore di max_packet_size del database a 100 M o come richiesto nel file my.ini che si trova in {AEM_HOME}/mysql.
