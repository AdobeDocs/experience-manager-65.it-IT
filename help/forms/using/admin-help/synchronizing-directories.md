---
title: Sincronizzazione delle directory
description: Scopri come sincronizzare il database di gestione utenti con le modifiche apportate ai server della directory di origine tramite la sincronizzazione manuale o pianificata.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: cb642289-4137-4ba7-8bde-0e458c8c94fe
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 0835dca60d8011ce8660f1e7fdefb2b14ccd6129
workflow-type: ht
source-wordcount: '1015'
ht-degree: 100%

---


# Sincronizzazione delle directory {#synchronizing-directories}

Per sincronizzare i domini, puoi scegliere di eseguire una sincronizzazione manuale o pianificata. Una *sincronizzazione manuale* sincronizza tutti i domini selezionati. Una *sincronizzazione pianificata* sincronizza tutti i domini.

La sincronizzazione della directory viene utilizzata per richiamare i dettagli dai server della directory specificati nelle impostazioni della directory nel database di gestione utenti. In seguito, puoi eseguire una sincronizzazione manuale anche in caso di modifiche o aggiornamenti sui server directory. Ad esempio, puoi eseguire una sincronizzazione manuale se utenti e gruppi vengono aggiunti o vengono apportate modifiche all’account di un utente.

Puoi inoltre impostare una pianificazione di sincronizzazione giornaliera per sincronizzare automaticamente il database di gestione utenti con le modifiche o gli aggiornamenti ai server delle directory di origine. Tuttavia, questo processo utilizza risorse di rete e server. Puoi scegliere periodi di utilizzo ridotti ed evitare di pianificare sincronizzazioni non necessarie che bloccano le risorse di sistema e di rete. Per ridurre al minimo le sincronizzazioni non necessarie, utilizza invece l’opzione di sincronizzazione immediata.

Puoi anche specificare se inviare le informazioni di utenti e gruppi in Adobe LiveCycle Content Services 9 (obsoleto) durante la sincronizzazione dei domini.

>[!NOTE]
>
>Non creare più utenti e gruppi locali mentre è in corso la sincronizzazione di una directory LDAP. Il tentativo di eseguire questo processo può causare errori.

>[!NOTE]
>
>Se il processo di sincronizzazione del dominio viene interrotto (ad esempio, il server applicazioni viene arrestato durante il processo), attendi qualche istante prima di tentare di sincronizzare il dominio. Per valutare lo stato della sincronizzazione, controlla lo stato. Se la gestione utenti ha acquisito un blocco prima dell’arresto, attendi 10 minuti per il rilascio del blocco dopo il riavvio del server. Se lo stato di sincronizzazione è “In corso” ma la sincronizzazione è interrotta o bloccata, gestione utenti ritenta la sincronizzazione dopo 3 minuti. Dopo tre tentativi non riusciti, gestione utenti dichiara la sincronizzazione non riuscita e rilascia il blocco.

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (obsoleto) è un sistema di gestione dei contenuti installato con LiveCycle. Consente agli utenti di progettare, gestire, monitorare e ottimizzare i processi incentrati sulla persona. Il supporto di Content Services (obsoleto) termina il 31/12/2014. Consulta il [documento sul ciclo di vita del prodotto Adobe](https://helpx.adobe.com/it/support/programs/eol-matrix.html).

## Abilitare la sincronizzazione directory delta {#enable-delta-directory-synchronization}

La sincronizzazione delle directory delta migliora l’efficienza della sincronizzazione della directory. Quando abiliti la sincronizzazione della directory delta, gestione utenti sincronizza solo gli utenti e i gruppi che sono stati aggiunti o aggiornati dopo l’ultima sincronizzazione.

Quando abiliti la sincronizzazione della directory delta, gestione utenti esegue le seguenti operazioni:

* Recupera tutti gli utenti dai server delle directory, ma aggiorna il database di gestione utenti con solo gli utenti la cui marca temporale è stata modificata.
* Recupera tutti i gruppi ma aggiorna il database di gestione utenti con solo i gruppi la cui marca temporale è stata modificata.
* Recupera i membri del gruppo solo per i gruppi le cui marche temporali sono state modificate e aggiorna il database di gestione utenti con tali informazioni.

>[!NOTE]
>
> * Gli utenti e i gruppi che sono stati rimossi dalla directory non vengono eliminati dal database di gestione utenti fino a quando non viene eseguita una sincronizzazione completa della directory.
> * Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.


1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione dominio.
2. In Sincronizzazione delta, seleziona la casella di controllo e fai clic su Salva.
3. Modifica le impostazioni della directory per ciascuno dei domini Enterprise che utilizzeranno la funzione di sincronizzazione della directory delta. Nelle pagine Impostazioni utente e Impostazioni gruppo individua l’impostazione Modifica marca temporale e immetti `modify TimeStamp` come valore. Per informazioni dettagliate sulla modifica dei domini Enterprise, consulta [Modifica e conversione di domini esistenti](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).

## Abilitare o disabilitare la registrazione dettagliata durante la sincronizzazione {#enable-or-disable-detailed-logging-during-synchronization}

Per impostazione predefinita, gestione utenti registra le statistiche dettagliate durante il processo di sincronizzazione.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Configurazione > Configura attributi di sistema avanzati.
1. In Registrazione statistiche di sincronizzazione, deseleziona la casella di controllo per disabilitare la registrazione dettagliata o selezionala per abilitare la registrazione, quindi fai clic su Salva.

## Configurare l’opzione di esecuzione di un nuovo tentativo di sincronizzazione della directory {#configure-the-directory-synchronization-retry-option}

Puoi configurare gestione utenti per verificare periodicamente la presenza di eventuali tentativi di sincronizzazione della directory non riusciti. Gestione utenti tenta quindi di completare le sincronizzazioni non riuscite.

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Configurazione > Configura attributi di sistema avanzati.
1. In Configura l’espressione Cron del completamento della sincronizzazione, immetti un’espressione Cron che rappresenta l’intervallo di tempo in cui gestione utenti ritenta le sincronizzazione non riuscite. L’utilizzo dell’espressione Cron si basa sul sistema di pianificazione dei processi open source Quartz, versione 1.4.0.

   Il valore predefinito è 0 0/13 &amp;ast; ? &amp;ast; , il che significa che il controllo viene eseguito ogni 13 minuti.

## Sincronizzazione manuale delle directory {#manually-synchronize-directories}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione dominio.
1. (Facoltativo) Per inviare le informazioni di utenti e gruppi a Content Services (obsoleto), seleziona l’opzione “Seleziona questa opzione per inviare utenti e gruppi a provider registrati esterni di archiviazione per entità principali. Questa opzione si applica anche quando aggiungi nuovi utenti e gruppi tramite la pagina Utenti e gruppi.
1. Seleziona la casella di controllo relativa a ciascun dominio enterprise da sincronizzare e fai clic su Sincronizza.

   Se selezioni più domini, la sincronizzazione del dominio per tutti i domini può essere eseguita contemporaneamente. Tuttavia, se selezioni i domini separatamente, può essere eseguita una sola sincronizzazione di dominio alla volta.

## Pianificare la sincronizzazione della directory {#schedule-directory-synchronization}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione dominio.
1. Pianifica sincronizzazione:

   * Per abilitare la sincronizzazione automatica su base giornaliera, in Modulo di pianificazione, seleziona Occorrenza. Seleziona Giornaliero dall’elenco e digita l’ora nel formato 24 ore nella casella corrispondente. Una volta salvate le impostazioni, questo valore viene convertito in un’espressione Cron, visualizzata nella casella Espressione Cron.
   * Per pianificare la sincronizzazione in un giorno specifico della settimana o del mese oppure in un mese specifico, seleziona Espressione Cron e digita l’espressione appropriata nella casella. Ad esempio, esegui la sincronizzazione all’1:30 dell’ultimo venerdì del mese.

L’utilizzo dell’espressione Cron si basa sul sistema di pianificazione dei processi open source Quartz, versione 1.4.0.

* Per disattivare la sincronizzazione automatica, seleziona Occorrenza e seleziona Mai dall’elenco.
* (Facoltativo) Per inviare le informazioni di utenti e gruppi a Content Services (obsoleto), seleziona l’opzione “Seleziona questa opzione per inviare utenti e gruppi a provider registrati esterni di archiviazione per entità principali. Questa opzione si applica anche quando aggiungi nuovi utenti e gruppi tramite la pagina Utenti e gruppi.
* Fai clic su Salva.

## Arresta tutte le sincronizzazioni della directory attualmente in corso {#stop-all-directory-synchronizations-currently-in-progress}

1. Nella console di amministrazione, fai clic su Impostazioni > Gestione utenti > Gestione dominio.
1. Fai clic su Annulla. Questo pulsante viene visualizzato solo quando è in corso la sincronizzazione della directory.
