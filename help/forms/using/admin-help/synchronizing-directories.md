---
title: Sincronizzazione delle directory
seo-title: Synchronizing directories
description: Scopri come sincronizzare il database User Management con le modifiche ai server delle directory di origine utilizzando la sincronizzazione manuale o pianificata.
seo-description: Learn how to synchronize the User Management database with changes to the source directory servers using manual or scheduled synchronization.
uuid: 71cbc04d-6172-49b7-a490-ff3233c1b2bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7ec0698a-9e6e-48d4-bba2-5a6eee313900
exl-id: cb642289-4137-4ba7-8bde-0e458c8c94fe
source-git-commit: 2a2f8538b6554540b546f4d345c0b3c0d3e706f3
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---

# Sincronizzazione delle directory {#synchronizing-directories}

Per sincronizzare i domini, puoi scegliere di eseguire una sincronizzazione manuale o pianificata. A *sincronizzazione manuale* sincronizza tutti i domini selezionati. A *sincronizzazione pianificata* sincronizza tutti i domini.

La sincronizzazione della directory viene utilizzata per estrarre i dettagli dai server di directory specificati nelle impostazioni di directory nel database di Gestione utente. In seguito, è anche possibile eseguire una sincronizzazione manuale se si verificano modifiche o aggiornamenti sui server di directory. Ad esempio, puoi eseguire una sincronizzazione manuale se vengono aggiunti utenti e gruppi o se vengono apportate modifiche all’account di un utente.

È inoltre possibile impostare una pianificazione della sincronizzazione giornaliera per sincronizzare automaticamente il database User Management con le modifiche o gli aggiornamenti ai server delle directory di origine. Tuttavia, tenere presente che questo processo utilizza risorse di rete e server. Scegli periodi di tempo ridotti ed evita la pianificazione di sincronizzazioni non necessarie che collegano le risorse di sistema e di rete. Per ridurre al minimo le sincronizzazioni non necessarie, utilizza invece l’opzione di sincronizzazione immediata.

È inoltre possibile specificare se inviare le informazioni di utenti e gruppi in Adobe LiveCycle Content Services 9 (obsoleto) durante la sincronizzazione dei domini.

>[!NOTE]
>
>Non creare più utenti e gruppi locali mentre è in corso la sincronizzazione di una directory LDAP. Il tentativo di questo processo può causare errori.

>[!NOTE]
>
>Se il processo di sincronizzazione del dominio viene interrotto (ad esempio, l&#39;application server viene arrestato durante il processo), attendere un po&#39; prima di provare a sincronizzare il dominio. Per valutare lo stato della sincronizzazione, guarda lo stato . Se User Management ha acquisito un blocco prima dello spegnimento, attendere 10 minuti per il rilascio del blocco dopo il riavvio del server. Se lo stato di sincronizzazione è &quot;In corso&quot; ma la sincronizzazione viene interrotta o bloccata, Gestione utente ritenta la sincronizzazione dopo 3 minuti. Dopo tre tentativi non riusciti, Gestione utente dichiara la sincronizzazione un errore e rilascia il blocco.

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (obsoleto) è un sistema di gestione dei contenuti installato con il LiveCycle. Consente agli utenti di progettare, gestire, monitorare e ottimizzare processi incentrati sulle persone. Il supporto per Content Services (obsoleto) termina il 31/12/2014. Vedi [Adobe del documento sul ciclo di vita del prodotto](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

## Abilita sincronizzazione directory delta {#enable-delta-directory-synchronization}

La sincronizzazione della directory Delta migliora l&#39;efficienza della sincronizzazione della directory. Quando la sincronizzazione della directory delta è abilitata, User Management sincronizza solo gli utenti e i gruppi aggiunti o aggiornati dall’ultima sincronizzazione.

Quando la sincronizzazione della directory delta è abilitata, la gestione utente esegue i seguenti passaggi:

* Recupera tutti gli utenti dai server delle directory ma aggiorna il database di Gestione utente con solo gli utenti la cui marca temporale è cambiata.
* Recupera tutti i gruppi ma aggiorna il database di Gestione utente con solo i gruppi la cui marca temporale è stata modificata.
* Recupera i membri del gruppo solo per i gruppi i cui timestamp sono cambiati e aggiorna il database di Gestione utente con tali informazioni.

>[!NOTE]
>
>Gli utenti e i gruppi rimossi dalla directory non vengono eliminati dal database di Gestione utente fino a quando non si esegue una sincronizzazione completa della directory.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. In Sincronizzazione delta selezionare la casella di controllo e fare clic su Salva.
1. Modifica le impostazioni della directory per ciascuno dei domini aziendali che utilizzeranno la funzione di sincronizzazione della directory delta. Nelle pagine Impostazioni utente e Impostazioni gruppo, individua l’impostazione Modifica timestamp e immetti . `modify TimeStamp` come valore. Per informazioni sulla modifica dei domini aziendali, consulta [Modifica e conversione di domini esistenti](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).

## Attiva o disattiva la registrazione dettagliata durante la sincronizzazione {#enable-or-disable-detailed-logging-during-synchronization}

Per impostazione predefinita, Gestione utente registra statistiche dettagliate durante il processo di sincronizzazione.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Configura attributi di sistema avanzati.
1. In Sincronizza registrazione statistiche deselezionare la casella di controllo per disabilitare la registrazione dettagliata o selezionarla per abilitare la registrazione, quindi fare clic su Salva.

## Configurare l’opzione di esecuzione di un nuovo tentativo di sincronizzazione della directory {#configure-the-directory-synchronization-retry-option}

È possibile configurare Gestione utenti per verificare periodicamente la presenza di eventuali tentativi di sincronizzazione della directory non riusciti. Gestione utente cerca quindi di completare le sincronizzazioni non riuscite.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Configurazione > Configura attributi di sistema avanzati.
1. In Espressione cron di Synch Finisher immettere un&#39;espressione cron che rappresenta l&#39;intervallo in cui la Gestione utente tenta di eseguire sincronizzazioni non riuscite. L&#39;utilizzo dell&#39;espressione cron si basa sul sistema di programmazione dei processi open source Quartz, versione 1.4.0.

   Il valore predefinito è 0/13 &amp;ast; ? &amp;ast; , il che significa che il controllo si verifica ogni 13 minuti.

## Sincronizza manualmente le directory {#manually-synchronize-directories}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. (Facoltativo) Per inviare le informazioni di utenti e gruppi in Content Services (obsoleto), selezionare l&#39;opzione Seleziona questa opzione per l&#39;invio di utenti e gruppi in provider di archiviazione entità esterni registrati. Questa opzione si applica anche quando si aggiungono nuovi utenti e gruppi tramite la pagina Utenti e gruppi .
1. Selezionare la casella di controllo per ogni dominio enterprise da sincronizzare e fare clic su Sincronizza ora.

   Se selezioni più domini, puoi eseguire contemporaneamente la sincronizzazione del dominio per tutti i domini. Tuttavia, se selezioni i domini separatamente, è possibile eseguire una sola sincronizzazione di dominio alla volta.

## Sincronizzazione della directory {#schedule-directory-synchronization}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Sincronizzazione programmata:

   * Per abilitare la sincronizzazione automatica su base giornaliera, in Scheduler selezionare Generato. Selezionare Giornaliero dall’elenco e digitare l’ora nel formato 24 ore nella casella corrispondente. Quando salvi le impostazioni, questo valore viene convertito in un’espressione cron, visualizzata nella casella Espressione Cron.
   * Per pianificare la sincronizzazione in un giorno specifico della settimana o del mese, o in un mese particolare, selezionare Espressione Cron e digitare l&#39;espressione appropriata nella casella. Ad esempio, effettua la sincronizzazione alle 00:30 dell’ultimo venerdì del mese.

L&#39;utilizzo dell&#39;espressione cron si basa sul sistema di programmazione dei processi open source Quartz, versione 1.4.0.

* Per disattivare la sincronizzazione automatica, selezionare Generato e selezionare Mai dall’elenco.
* (Facoltativo) Per inviare le informazioni di utenti e gruppi in Content Services (obsoleto), selezionare l&#39;opzione Seleziona questa opzione per l&#39;invio di utenti e gruppi in provider di archiviazione entità esterni registrati. Questa opzione si applica anche quando si aggiungono nuovi utenti e gruppi tramite la pagina Utenti e gruppi .
* Fai clic su Salva.

## Interrompi tutte le sincronizzazioni delle directory attualmente in corso {#stop-all-directory-synchronizations-currently-in-progress}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fare clic su Interrompi. Questo pulsante viene visualizzato solo mentre è in corso la sincronizzazione di una directory.
