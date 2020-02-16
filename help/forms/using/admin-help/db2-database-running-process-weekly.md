---
title: '"Database DB2: Esecuzione settimanale di un processo"'
seo-title: '"Database DB2: Esecuzione settimanale di un processo"'
description: Scopri come migliorare le prestazioni del database DB2 dei moduli AEM.
seo-description: Scopri come migliorare le prestazioni del database DB2 dei moduli AEM.
uuid: 36070087-c250-41df-a841-aa922e777697
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc0e8183-5d50-4fc0-997a-5f3168ba0d70
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Database DB2: Esecuzione settimanale di un processo{#db-database-running-a-process-weekly}

Se il database DB2 di AEM Forms inizia a essere eseguito lentamente, l’esecuzione settimanale del seguente processo può migliorare le prestazioni:

1. Avvia DB2 Control Center:

   (Windows) Selezionate Start > Programmi > IBM DB2 > Strumenti di amministrazione generale > Centro di controllo.

   (Linux e UNIX) Da un prompt dei comandi, digitare il `db2jcc` comando.

1. Nella struttura degli oggetti DB2 Control Center fare clic su Tutti i database.
1. Fate clic sul database creato per i moduli AEM e fate clic sulla cartella Tables.
1. Selezionare tutte le tabelle del database nel riquadro dei contenuti, fare clic con il pulsante destro del mouse su di esse e selezionare Esegui statistiche.
1. Vai a Statistiche > Statistiche indice.
1. Selezionate Raccogli statistiche per tutti gli indici, selezionate Raccogli statistiche per indici con statistiche dettagliate estese, quindi fate clic su OK.

Al termine del processo viene visualizzato un messaggio. Chiudi il messaggio.
