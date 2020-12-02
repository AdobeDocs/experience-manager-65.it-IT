---
title: Eliminare i record dal database di Gestione processi
seo-title: Eliminare i record dal database di Gestione processi
description: I dati di elaborazione di grandi dimensioni possono ridurre le prestazioni dei moduli AEM. È buona norma eliminare i dati di processo quando i record non sono più necessari.
seo-description: I dati di elaborazione di grandi dimensioni possono ridurre le prestazioni dei moduli AEM. È buona norma eliminare i dati di processo quando i record non sono più necessari.
uuid: cf214498-36e9-4dcc-b4d4-e7c46f80dbab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 69a406f2-4fa8-40bb-b671-7b0f5b6a2c4c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---


# Eliminare i record dal database di Job Manager {#purge-records-from-the-job-manager-database}

I dati di processo generati quando viene richiamato un processo di lunga durata possono diventare troppo grandi, riducendo le prestazioni dei moduli AEM e l&#39;uso di spazio su disco non necessario. È buona norma eliminare i dati di processo quando i record non sono più necessari.

È possibile utilizzare la console di amministrazione per eseguire una rimozione una tantum di record obsoleti, oppure per pianificare regolarmente le eliminazioni automatiche. Altri metodi per eliminare i record obsoleti sono descritti in [Rimozione dei dati del processo](/help/forms/using/admin-help/purging-process-data.md#purging-process-data).

**Accesso alla pagina Utilità di pianificazione rimozione processo**

1. In Admin Console, fai clic su Health Monitor nell’angolo superiore destro della pagina.
1. Fate clic sulla scheda Utilità di pianificazione rimozione processo.

Le informazioni sulle eventuali eliminazioni pianificate al momento vengono visualizzate nella casella Informazioni sull&#39;utilità di pianificazione per la rimozione dei processi.

>[!NOTE]
>
>Se si fa clic su Interrompi pianificatore, le eliminazioni pianificate in futuro verranno interrotte, ma non verrà interrotto un processo di eliminazione già in corso.

**Pianificazione di una rimozione una tantum**

1. Selezionate Solo Una Volta.
1. Nell&#39;area Rimuovi filtro record completati, specificare il numero di giorni o settimane dopo i quali un record viene considerato obsoleto e pronto per l&#39;eliminazione.

   >[!NOTE]
   >
   >I record relativi ai processi che non sono stati completati non vengono eliminati, anche se sono più vecchi della specifica età.

1. Specificate quando verrà effettuata la rimozione. Selezionate la casella di controllo Usa data e ora correnti oppure deselezionate la casella di controllo e fate clic sulle icone del calendario e dell’orologio per specificare la data e l’ora in cui verrà eseguita l’eliminazione.

   >[!NOTE]
   >
   >Se si specifica una data e un&#39;ora di inizio che è in passato, l&#39;eliminazione si verifica immediatamente quando si fa clic su Avvia pianificazione.

1. Fate clic su Avvia pianificazione. Eventuali impostazioni pianificate in precedenza vengono sostituite con le nuove.

**Configurare una pianificazione di eliminazione automatica**

1. Selezionate Ripeti ogni e specificate il numero di giorni o settimane tra le eliminazioni.
1. Nell&#39;area Rimuovi filtro record completati, specificare il numero di giorni o settimane dopo i quali un record viene considerato obsoleto e pronto per l&#39;eliminazione. Non è possibile impostare il valore su `0`.

   >[!NOTE]
   >
   >I record relativi ai processi che non sono stati completati non vengono eliminati, anche se sono più vecchi della specifica età.

1. Specificate quando inizierà la rimozione. Selezionate la casella di controllo Usa data e ora correnti oppure deselezionate la casella di controllo e fate clic sulle icone del calendario e dell’orologio per specificare la data e l’ora in cui verrà eseguita l’eliminazione.

   >[!NOTE]
   >
   >Se si specifica una data e un&#39;ora di inizio che è passata, AEM moduli calcola la data di inizio successiva logica in base alla data specificata. Ad esempio, se pianificate l’eliminazione settimanale dei processi a partire dal 7 aprile ed è ora il 9 aprile, la prima eliminazione verrà eseguita il 14 aprile.

1. Fate clic su Avvia pianificazione. Eventuali impostazioni pianificate in precedenza vengono sostituite con le nuove.

