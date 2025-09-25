---
title: 'Database DB2®: esecuzione settimanale di un processo'
description: Scopri come migliorare le prestazioni di AEM Forms con il database DB2®.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '148'
ht-degree: 100%

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
