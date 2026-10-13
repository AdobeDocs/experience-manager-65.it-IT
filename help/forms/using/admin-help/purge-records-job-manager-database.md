---
title: Eliminare record dal database di Gestione processo
description: I dati dei processi di grandi dimensioni possono limitare le prestazioni dei moduli AEM. È buona norma eliminare i dati del processo quando i record non sono più necessari.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5279f6c3-5954-472c-9ea0-18e8a7ec860e
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
source-wordcount: '487'
ht-degree: 100%
---
# Eliminare record dal database di Gestione processo {#purge-records-from-the-job-manager-database}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

I dati di processo generati quando viene richiamato un processo di lunga durata possono assumere dimensioni eccessive, con conseguente riduzione delle prestazioni dei moduli AEM e utilizzo di spazio su disco non necessario. È buona norma eliminare i dati del processo quando i record non sono più necessari.

Puoi utilizzare la console di amministrazione per eseguire un’eliminazione una tantum di record obsoleti o per pianificare eliminazioni automatiche periodiche. Altri metodi per eliminare i record obsoleti sono descritti in [Eliminare i dati del processo](/help/forms/using/admin-help/purging-process-data.md#purging-process-data).

**Accedere alla pagina Modulo di pianificazione dell’eliminazione dei processi**

1. Nella console di amministrazione, fai clic su Health Monitor nell’angolo superiore destro della pagina.
1. Fai clic sulla scheda Modulo di pianificazione dell’eliminazione dei processi.

Le informazioni sulle eliminazioni attualmente pianificate vengono visualizzate nella casella Informazioni del Modulo di pianificazione dell’eliminazione dei processi.

>[!NOTE]
>
>Se fai clic su Interrompi modulo di pianificazione, le eliminazioni pianificate in futuro vengono interrotte, ma un processo di eliminazione già in corso non viene interrotto.

**Pianificare un’eliminazione una tantum**

1. Seleziona Solo una volta.
1. Nell’area Filtro per eliminare i record completati specifica il numero di giorni o settimane dopo le quali un record viene considerato obsoleto e risulta pronto per l’eliminazione.

   >[!NOTE]
   >
   >I record relativi a processi non completati non vengono eliminati, anche se sono precedenti alla data specificata.

1. Specifica quando avverrà l’eliminazione. Seleziona la casella di controllo Usa data e ora corrente oppure deselezionala e fai clic sulle icone del calendario e dell’orologio per specificare la data e l’ora in cui verrà eseguita l’eliminazione.

   >[!NOTE]
   >
   >Se specifichi una data e ora di inizio già trascorse, l’eliminazione viene eseguita immediatamente quando fai clic su Avvia modulo di pianificazione.

1. Fai clic su Avvia modulo di pianificazione. Tutte le impostazioni del modulo di pianificazione precedenti vengono sostituite dalle nuove impostazioni.

**Configurare una pianificazione di eliminazione automatica**

1. Seleziona Ripeti ogni e specifica il numero di giorni o settimane tra le eliminazioni.
1. Nell’area Filtro per eliminare i record completati specifica il numero di giorni o settimane dopo le quali un record viene considerato obsoleto e risulta pronto per l’eliminazione. Non puoi impostare il valore su `0`.

   >[!NOTE]
   >
   >I record relativi a processi non completati non vengono eliminati, anche se sono precedenti alla data specificata.

1. Specifica quando inizieranno le eliminazioni. Seleziona la casella di controllo Usa data e ora corrente oppure deselezionala e fai clic sulle icone del calendario e dell’orologio per specificare la data e l’ora in cui verrà eseguita l’eliminazione.

   >[!NOTE]
   >
   >Se specifichi una data e ora di inizio già trascorse, AEM Forms calcola la data di inizio logica successiva in base alla data che hai specificato. Se ad esempio pianifichi eliminazioni di processi con cadenza settimanale dal 7 aprile e oggi è il 9 aprile, la prima eliminazione avverrà il 14 aprile.

1. Fai clic su Avvia modulo di pianificazione. Tutte le impostazioni del modulo di pianificazione precedenti vengono sostituite dalle nuove impostazioni.
