---
title: Eliminare i record dal database di Job Manager
seo-title: Purge records from the Job Manager database
description: Dati di processo di grandi dimensioni possono comportare prestazioni di moduli AEM inferiori. È buona prassi eliminare i dati del processo quando i record non sono più necessari.
seo-description: Large process data can result in lower AEM forms performance. It is good practice to purge process data when records are no longer necessary.
uuid: cf214498-36e9-4dcc-b4d4-e7c46f80dbab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 69a406f2-4fa8-40bb-b671-7b0f5b6a2c4c
exl-id: 5279f6c3-5954-472c-9ea0-18e8a7ec860e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Eliminare i record dal database di Job Manager {#purge-records-from-the-job-manager-database}

I dati del processo generati quando viene richiamato un processo di lunga durata possono diventare troppo grandi, con conseguente riduzione delle prestazioni dei moduli AEM e utilizzo di spazio su disco non necessario. È buona prassi eliminare i dati del processo quando i record non sono più necessari.

È possibile utilizzare la console di amministrazione per eseguire un&#39;eliminazione una tantum di record obsoleti o per pianificare regolarmente l&#39;eliminazione automatica. Altri metodi per eliminare i record obsoleti sono descritti in [Rimozione dei dati del processo](/help/forms/using/admin-help/purging-process-data.md#purging-process-data).

**Accedere alla pagina Utilità di pianificazione rimozione processo**

1. In Console di amministrazione, fai clic su Monitoraggio integrità nell’angolo in alto a destra della pagina.
1. Fare clic sulla scheda Utilità di pianificazione eliminazione processo.

Le informazioni su eventuali eliminazioni attualmente pianificate vengono visualizzate nella casella Informazioni pianificazione rimozione processo.

>[!NOTE]
>
>Se si fa clic su Interrompi pianificazione, tutte le operazioni di pulizia pianificate in futuro verranno interrotte, ma non verrà interrotto un processo di eliminazione già in corso.

**Pianificare una rimozione una tantum**

1. Selezionare Solo una volta.
1. Nell&#39;area Rimuovi filtro record completato specificare il numero di giorni o settimane dopo i quali un record viene considerato obsoleto e pronto per l&#39;eliminazione.

   >[!NOTE]
   >
   >I record relativi a processi che non sono stati completati non vengono eliminati, anche se sono più vecchi dell&#39;età specificata.

1. Specifica quando verrà effettuata l&#39;eliminazione. Selezionare la casella di controllo Usa data e ora corrente oppure deselezionare la casella di controllo e fare clic sulle icone del calendario e dell&#39;orologio per specificare la data e l&#39;ora in cui verrà eseguita l&#39;eliminazione.

   >[!NOTE]
   >
   >Se specifichi una data e un&#39;ora di inizio che sono in passato, l&#39;eliminazione si verifica immediatamente quando fai clic su Avvia pianificazione.

1. Fai clic su Avvia pianificazione. Tutte le impostazioni precedentemente pianificate vengono sostituite con le nuove impostazioni.

**Configurare una pianificazione di eliminazione automatica**

1. Seleziona Ripeti ogni e specifica il numero di giorni o settimane tra le eliminazioni.
1. Nell&#39;area Rimuovi filtro record completato specificare il numero di giorni o settimane dopo i quali un record viene considerato obsoleto e pronto per l&#39;eliminazione. Non è possibile impostare il valore su `0`.

   >[!NOTE]
   >
   >I record relativi a processi che non sono stati completati non vengono eliminati, anche se sono più vecchi dell&#39;età specificata.

1. Specifica quando inizierà la pulizia. Selezionare la casella di controllo Usa data e ora corrente oppure deselezionare la casella di controllo e fare clic sulle icone del calendario e dell&#39;orologio per specificare la data e l&#39;ora in cui verrà eseguita l&#39;eliminazione.

   >[!NOTE]
   >
   >Se si specifica una data e un&#39;ora di inizio precedenti, AEM forms calcola la data di inizio successiva logica in base alla data specificata. Ad esempio, se pianifichi l’eliminazione dei processi con cadenza settimanale a partire dal 7 aprile ed è ora il 9 aprile, la prima eliminazione avrà luogo il 14 aprile.

1. Fai clic su Avvia pianificazione. Tutte le impostazioni precedentemente pianificate vengono sostituite con le nuove impostazioni.
