---
title: Sincronizzazione delle directory
description: Scopri come sincronizzare il database di User Management con le modifiche apportate ai server delle directory di origine tramite la sincronizzazione manuale o pianificata.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: cb642289-4137-4ba7-8bde-0e458c8c94fe
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# Sincronizzazione delle directory {#synchronizing-directories}

Per sincronizzare i domini, puoi scegliere di eseguire una sincronizzazione manuale o pianificata. A *sincronizzazione manuale* sincronizza tutti i domini selezionati. A *sincronizzazione pianificata* sincronizza tutti i domini.

La sincronizzazione della directory viene utilizzata per richiamare i dettagli dai server delle directory specificati nelle impostazioni della directory nel database di gestione utenti. In seguito, è possibile eseguire una sincronizzazione manuale anche se si verificano modifiche o aggiornamenti sui server delle directory. Ad esempio, puoi eseguire una sincronizzazione manuale se utenti e gruppi vengono aggiunti o se vengono apportate modifiche all’account di un utente.

È inoltre possibile impostare una pianificazione di sincronizzazione giornaliera per sincronizzare automaticamente il database di User Management con le modifiche o gli aggiornamenti ai server delle directory di origine. Tuttavia, questo processo utilizza risorse di rete e server. È possibile scegliere periodi di utilizzo ridotti ed evitare di pianificare sincronizzazioni non necessarie che bloccano le risorse di sistema e di rete. Per ridurre al minimo le sincronizzazioni non necessarie, utilizzare invece l&#39;opzione di sincronizzazione immediata.

È inoltre possibile specificare se inviare informazioni su utenti e gruppi al LiveCycle Adobe Content Services 9 (obsoleto) durante la sincronizzazione dei domini.

>[!NOTE]
>
>Non creare più utenti e gruppi locali mentre è in corso la sincronizzazione di una directory LDAP. Il tentativo di eseguire questo processo può causare errori.

>[!NOTE]
>
>Se il processo di sincronizzazione del dominio viene interrotto (ad esempio, il server applicazioni viene arrestato durante il processo), attendere qualche istante prima di tentare di sincronizzare il dominio. Per valutare lo stato della sincronizzazione, controllare lo stato. Se Gestione utenti ha acquisito un blocco prima dell&#39;arresto, attendere 10 minuti per il rilascio del blocco dopo il riavvio del server. Se lo stato di sincronizzazione è &quot;In corso&quot; ma la sincronizzazione è interrotta o bloccata, User Management ritenta la sincronizzazione dopo 3 minuti. Dopo tre tentativi non riusciti, User Management dichiara la sincronizzazione non riuscita e rilascia il blocco.

>[!NOTE]
>
>Adobe ® LiveCycle® Content Services ES (obsoleto) è un sistema di gestione dei contenuti installato con LiveCycle. Consente agli utenti di progettare, gestire, monitorare e ottimizzare i processi incentrati sulla persona. Il supporto di Content Services (obsoleto) termina il 12/31/2014. Consulta [Adobe di documento sul ciclo di vita del prodotto](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

## Abilita sincronizzazione directory delta {#enable-delta-directory-synchronization}

La sincronizzazione delle directory Delta migliora l&#39;efficienza della sincronizzazione delle directory. Quando è abilitata la sincronizzazione della directory delta, Gestione utenti sincronizza solo gli utenti e i gruppi che sono stati aggiunti o aggiornati dopo l’ultima sincronizzazione.

Quando è abilitata la sincronizzazione della directory delta, User Management esegue le seguenti operazioni:

* Recupera tutti gli utenti dai server delle directory, ma aggiorna il database di Gestione utenti con solo gli utenti la cui marca temporale è stata modificata.
* Recupera tutti i gruppi ma aggiorna il database di Gestione utente con solo i gruppi la cui marca temporale è stata modificata.
* Recupera i membri del gruppo solo per i gruppi i cui timestamp sono stati modificati e aggiorna il database di Gestione utente con tali informazioni.

>[!NOTE]
>
>Gli utenti e i gruppi che sono stati rimossi dalla directory non vengono eliminati dal database di User Management fino a quando non viene eseguita una sincronizzazione completa della directory.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. In Sincronizzazione delta selezionare la casella di controllo e fare clic su Salva.
1. Modificare le impostazioni della directory per ciascuno dei domini enterprise che utilizzeranno la funzione di sincronizzazione della directory delta. Nelle pagine Impostazioni utente e Impostazioni gruppo, individua l’impostazione Modifica marca temporale e immetti `modify TimeStamp` come valore. Per informazioni dettagliate sulla modifica dei domini aziendali, consulta [Modifica e conversione di domini esistenti](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).

## Attiva o disattiva la registrazione dettagliata durante la sincronizzazione {#enable-or-disable-detailed-logging-during-synchronization}

Per impostazione predefinita, Gestione utenti registra le statistiche dettagliate durante il processo di sincronizzazione.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Configura attributi di sistema avanzati.
1. In Registrazione statistiche di sincronizzazione deselezionare la casella di controllo per disattivare la registrazione dettagliata o selezionarla per attivare la registrazione e quindi fare clic su Salva.

## Configurare l&#39;opzione di esecuzione di un nuovo tentativo di sincronizzazione della directory {#configure-the-directory-synchronization-retry-option}

È possibile configurare Gestione utenti per verificare periodicamente la presenza di eventuali tentativi di sincronizzazione della directory non riusciti. Gestione utenti tenta quindi di completare le sincronizzazioni non riuscite.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Configura attributi di sistema avanzati.
1. In Espressione cron Synch Finisher immettere un&#39;espressione cron che rappresenta l&#39;intervallo di tempo in cui i tentativi di sincronizzazione non sono riusciti da parte di Gestione utente. L’utilizzo delle espressioni cron si basa sul sistema di pianificazione dei processi open source Quartz, versione 1.4.0.

   Il valore predefinito è 0 0/13 &amp;ast; ? &amp;ast; , il che significa che il controllo viene eseguito ogni 13 minuti.

## Sincronizzare manualmente le directory {#manually-synchronize-directories}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. (Facoltativo) Per inviare le informazioni di utenti e gruppi a Content Services (obsoleto), selezionare l&#39;opzione Seleziona questa opzione per inviare utenti e gruppi a provider di archiviazione principali esterni registrati. Questa opzione si applica anche quando si aggiungono nuovi utenti e gruppi tramite la pagina Utenti e gruppi.
1. Selezionare la casella di controllo relativa a ciascun dominio enterprise da sincronizzare e fare clic su Sincronizza.

   Se selezioni più domini, la sincronizzazione del dominio per tutti i domini può essere eseguita contemporaneamente. Tuttavia, se selezioni i domini separatamente, può essere eseguita una sola sincronizzazione di dominio alla volta.

## Pianificare la sincronizzazione della directory {#schedule-directory-synchronization}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Pianificazione sincronizzazione:

   * Per abilitare la sincronizzazione automatica su base giornaliera, in Scheduler, selezionare Occurs. Seleziona Giornaliero dall’elenco e digita l’ora nel formato 24 ore nella casella corrispondente. Quando si salvano le impostazioni, questo valore viene convertito in un&#39;espressione cron, visualizzata nella casella Espressione cron.
   * Per pianificare la sincronizzazione in un giorno specifico della settimana o del mese oppure in un mese specifico, selezionare Espressione corona e digitare l&#39;espressione appropriata nella casella. Ad esempio, esegui la sincronizzazione alle 01:30 dell’ultimo venerdì del mese.

L’utilizzo delle espressioni cron si basa sul sistema di pianificazione dei processi open source Quartz, versione 1.4.0.

* Per disattivare la sincronizzazione automatica, selezionare Si verifica e selezionare Mai dall&#39;elenco.
* (Facoltativo) Per inviare le informazioni di utenti e gruppi a Content Services (obsoleto), selezionare l&#39;opzione Seleziona questa opzione per inviare utenti e gruppi a provider di archiviazione principali esterni registrati. Questa opzione si applica anche quando si aggiungono nuovi utenti e gruppi tramite la pagina Utenti e gruppi.
* Fai clic su Salva.

## Arresta tutte le sincronizzazioni di directory attualmente in corso {#stop-all-directory-synchronizations-currently-in-progress}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic su Interrompi. Questo pulsante viene visualizzato solo quando è in corso la sincronizzazione della directory.
