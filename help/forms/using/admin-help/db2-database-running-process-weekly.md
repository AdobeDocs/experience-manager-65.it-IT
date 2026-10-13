---
title: 'Database DB2&reg;: esecuzione settimanale di un processo'
description: Scopri come migliorare le prestazioni del tuo database AEM Forms DB2&reg;.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 85%
---
# Database DB2®: esecuzione settimanale di un processo{#db-database-running-a-process-weekly}

Se il database DB2® di AEM Forms inizia a funzionare lentamente, l’esecuzione settimanale del seguente processo può migliorare le prestazioni:

1. Avviare il Centro controllo DB2®:

   (Windows) Seleziona Start > Programmi > IBM® DB2® > Strumenti di amministrazione generale > Centro di controllo.

   (Linux® e UNIX®) Dal prompt dei comandi digita il comando `db2jcc`.

1. Nella struttura degli oggetti del Centro di controllo DB2®, fai clic su Tutti i database.
1. Fai clic sul database creato per AEM Forms e quindi sulla cartella Tabelle.
1. Seleziona tutte le tabelle di database nel riquadro dei contenuti, fai clic con il pulsante destro del mouse su di esse, quindi seleziona Esegui statistiche.
1. Passa a Statistiche > Statistiche indice.
1. Seleziona Raccogli statistiche per tutti gli indici, seleziona Raccogli statistiche per gli indici con statistiche dettagliate estese e quindi fai clic su OK.

Al termine del processo viene visualizzato un messaggio. Chiudi il messaggio.
