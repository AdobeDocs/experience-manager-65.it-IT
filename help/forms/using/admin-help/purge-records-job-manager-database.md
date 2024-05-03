---
title: Eliminare i record dal database di Gestione processi
description: Dati di processo di grandi dimensioni possono ridurre le prestazioni dei moduli AEM. È buona prassi eliminare i dati del processo quando i record non sono più necessari.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5279f6c3-5954-472c-9ea0-18e8a7ec860e
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Eliminare i record dal database di Gestione processi {#purge-records-from-the-job-manager-database}

I dati di processo generati quando si richiama un processo di lunga durata possono diventare troppo grandi, con conseguente riduzione delle prestazioni dei moduli AEM e utilizzo di spazio su disco non necessario. È buona prassi eliminare i dati del processo quando i record non sono più necessari.

È possibile utilizzare la console di amministrazione per eseguire una rimozione una tantum di record obsoleti o per pianificare eliminazioni automatiche regolari. Altri metodi per eliminare i record obsoleti sono descritti in [Rimozione dati processo](/help/forms/using/admin-help/purging-process-data.md#purging-process-data).

**Accedere alla pagina Utilità di pianificazione rimozione job**

1. In Administration Console, fare clic su Health Monitor nell&#39;angolo superiore destro della pagina.
1. Fare clic sulla scheda Pianificazione rimozione job.

Le informazioni sulle rimozioni attualmente pianificate vengono visualizzate nella casella Informazioni modulo di pianificazione rimozione OdL.

>[!NOTE]
>
>Facendo clic su Interrompi modulo di pianificazione vengono interrotte le rimozioni pianificate in futuro, ma non viene interrotto un processo di rimozione già in corso.

**Pianificare una rimozione una tantum**

1. Selezionare Solo una volta.
1. Nell&#39;area Filtro record completati rimozione specificare il numero di giorni o settimane dopo le quali un record viene considerato obsoleto e pronto per la rimozione.

   >[!NOTE]
   >
   >I record relativi a processi non completati non vengono eliminati, anche se sono più vecchi della data specificata.

1. Specifica quando avverrà l’eliminazione. Selezionare la casella di controllo Usa data e ora corrente oppure deselezionarla e fare clic sulle icone del calendario e dell&#39;orologio per specificare la data e l&#39;ora in cui verrà eseguita la rimozione.

   >[!NOTE]
   >
   >Se si specifica una data e un&#39;ora di inizio nel passato, la rimozione viene eseguita immediatamente quando si fa clic su Avvia modulo di pianificazione.

1. Fare clic su Avvia modulo di pianificazione. Tutte le impostazioni pianificate in precedenza vengono sostituite con le nuove impostazioni.

**Configurare una pianificazione di eliminazione automatica**

1. Selezionare Ripeti ogni e specificare il numero di giorni o settimane tra le eliminazioni.
1. Nell&#39;area Filtro record completati rimozione specificare il numero di giorni o settimane dopo le quali un record viene considerato obsoleto e pronto per la rimozione. Impossibile impostare il valore su `0`.

   >[!NOTE]
   >
   >I record relativi a processi non completati non vengono eliminati, anche se sono più vecchi della data specificata.

1. Specifica quando inizieranno le eliminazioni. Selezionare la casella di controllo Usa data e ora corrente oppure deselezionarla e fare clic sulle icone del calendario e dell&#39;orologio per specificare la data e l&#39;ora in cui verrà eseguita la rimozione.

   >[!NOTE]
   >
   >Se si specificano una data e un&#39;ora di inizio nel passato, i moduli AEM calcolano la data di inizio successiva logica in base alla data specificata. Ad esempio, se si pianifica che le eliminazioni del processo avvengano settimanalmente a partire dal 7 aprile e ora è il 9 aprile, la prima eliminazione avviene il 14 aprile.

1. Fare clic su Avvia modulo di pianificazione. Tutte le impostazioni pianificate in precedenza vengono sostituite con le nuove impostazioni.
