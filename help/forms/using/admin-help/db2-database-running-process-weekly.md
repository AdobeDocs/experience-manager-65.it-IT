---
title: "Database DB2: esecuzione settimanale di un processo"
description: Scopri come migliorare le prestazioni del database DB2 dei moduli AEM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Database DB2: esecuzione settimanale di un processo{#db-database-running-a-process-weekly}

Se il database DB2 dei moduli AEM inizia a funzionare lentamente, l’esecuzione settimanale del seguente processo può migliorarne le prestazioni:

1. Avvia centro di controllo DB2:

   (Windows) Selezionare Start > Programmi > IBM DB2 > Strumenti di amministrazione generali > Centro controllo.

   (Linux e UNIX) Da un prompt dei comandi, digitare `db2jcc` comando.

1. Nell&#39;albero degli oggetti di DB2 Control Center fare clic su Tutti i database.
1. Fare clic sul database creato per i moduli AEM e quindi sulla cartella Tabelle.
1. Selezionare tutte le tabelle di database nel riquadro dei contenuti, fare clic con il pulsante destro del mouse su di esse e selezionare Esegui statistiche.
1. Vai a Statistiche > Statistiche indice.
1. Selezionare Raccogli statistiche per tutti gli indici, selezionare Raccogli statistiche per gli indici con statistiche dettagliate estese e quindi fare clic su OK.

Al termine del processo viene visualizzato un messaggio. Chiudi il messaggio.
