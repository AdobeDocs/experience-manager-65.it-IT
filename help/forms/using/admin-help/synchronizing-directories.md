---
title: Sincronizzazione delle directory
seo-title: Sincronizzazione delle directory
description: Scoprite come sincronizzare il database Gestione utenti con le modifiche apportate ai server di directory di origine mediante la sincronizzazione manuale o pianificata.
seo-description: Scoprite come sincronizzare il database Gestione utenti con le modifiche apportate ai server di directory di origine mediante la sincronizzazione manuale o pianificata.
uuid: 71cbc04d-6172-49b7-a490-ff3233c1b2bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7ec0698a-9e6e-48d4-bba2-5a6eee313900
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 0%

---


# Sincronizzazione delle directory {#synchronizing-directories}

Per sincronizzare i domini, puoi scegliere di eseguire una sincronizzazione manuale o pianificata. Una *sincronizzazione manuale* sincronizza tutti i domini selezionati. Una *sincronizzazione pianificata* sincronizza tutti i domini.

La sincronizzazione della directory viene utilizzata per estrarre i dettagli dai server di directory specificati nelle impostazioni della directory nel database Gestione utente. In seguito, è inoltre possibile eseguire una sincronizzazione manuale in caso di modifiche o aggiornamenti sui server di directory. Ad esempio, potete eseguire una sincronizzazione manuale se vengono aggiunti utenti e gruppi o se vengono apportate modifiche all’account di un utente.

È inoltre possibile impostare una pianificazione di sincronizzazione giornaliera per sincronizzare automaticamente il database Gestione utente con le modifiche o gli aggiornamenti ai server di directory di origine. Tuttavia, tenete presente che questo processo utilizza risorse di rete e server. Scegliete periodi di tempo ridotti ed evitate di pianificare sincronizzazioni non necessarie che colleghino le risorse di rete e di sistema. Per ridurre al minimo le sincronizzazioni non necessarie, utilizzate invece l&#39;opzione di sincronizzazione immediata.

È inoltre possibile specificare se inviare le informazioni di utenti e gruppi  Adobe a Content Services 9 (obsoleto) durante la sincronizzazione dei domini.

>[!NOTE]
>
>Non create più utenti e gruppi locali mentre è in corso la sincronizzazione di una directory LDAP. Il tentativo di eseguire questo processo potrebbe causare errori.

>[!NOTE]
>
>Se il processo di sincronizzazione del dominio viene interrotto (ad esempio, il server applicazione viene arrestato durante il processo), attendere un po&#39; prima di tentare di sincronizzare il dominio. Per valutare lo stato della sincronizzazione, controllate lo stato. Se User Management ha acquisito un blocco prima dell&#39;arresto, attendere 10 minuti prima che il blocco venga rilasciato dopo il riavvio del server. Se lo stato di sincronizzazione è &quot;In corso&quot; ma la sincronizzazione viene interrotta o bloccata, Gestione utente riprova la sincronizzazione dopo 3 minuti. Dopo tre tentativi non riusciti, Gestione utente dichiara la sincronizzazione un errore e rilascia il blocco.

>[!NOTE]
>
> Adobe® Content Services ES (obsoleto) è un sistema di gestione dei contenuti installato con LiveCycle LiveCycle®. Consente agli utenti di progettare, gestire, monitorare e ottimizzare i processi incentrati sulle persone. Il supporto di Content Services (obsoleto) termina il 31/12/2014. Vedere [ documento sul ciclo di vita del prodotto del Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html). Per informazioni sulla configurazione di Content Services (obsoleto), vedere [Amministrazione di Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).

## Abilita sincronizzazione directory delta {#enable-delta-directory-synchronization}

La sincronizzazione delle directory Delta migliora l&#39;efficienza della sincronizzazione delle directory. Quando la sincronizzazione della directory delta è abilitata, Gestione utente sincronizza solo gli utenti e i gruppi che sono stati aggiunti o aggiornati dall&#39;ultima sincronizzazione.

Gestione utente esegue i seguenti passaggi quando la sincronizzazione della directory delta è abilitata:

* Recuperate tutti gli utenti dai server di directory, ma aggiornate il database di Gestione utente con solo gli utenti la cui marca temporale è cambiata.
* Recuperate tutti i gruppi ma aggiornate il database Gestione utenti con solo i gruppi la cui marca temporale è cambiata.
* Recupera i membri del gruppo solo per i gruppi le cui marche temporali sono cambiate e aggiorna il database Gestione utente con tali informazioni.

>[!NOTE]
>
>Gli utenti e i gruppi che sono stati rimossi dalla directory non vengono eliminati dal database Gestione utenti fino a quando non viene eseguita la sincronizzazione completa della directory.

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. In Delta Synch (Sincronizzazione delta), selezionate la casella di controllo e fate clic su Save (Salva).
1. Modificate le impostazioni di directory per ciascuno dei domini aziendali che utilizzeranno la funzione di sincronizzazione della directory delta. Nelle pagine Impostazioni utente e Impostazioni gruppo, individuate l&#39;impostazione Modifica marca temporale e immettete `modify TimeStamp` come valore. Per informazioni dettagliate sulla modifica dei domini enterprise, vedere [Modifica e conversione di domini esistenti](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).

## Attivare o disattivare la registrazione dettagliata durante la sincronizzazione {#enable-or-disable-detailed-logging-during-synchronization}

Per impostazione predefinita, Gestione utenti registra statistiche dettagliate durante il processo di sincronizzazione.

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Configurazione > Configura attributi di sistema avanzati.
1. In Sincronizza registrazione statistiche, deselezionate la casella di controllo per disattivare la registrazione dettagliata o selezionatela per abilitare la registrazione, quindi fate clic su Salva.

## Configurare l&#39;opzione dei tentativi di sincronizzazione della directory {#configure-the-directory-synchronization-retry-option}

È possibile configurare Gestione utente per controllare periodicamente la presenza di eventuali tentativi di sincronizzazione delle directory non riusciti. Gestione utente tenta quindi di completare le sincronizzazioni non riuscite.

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Configurazione > Configura attributi di sistema avanzati.
1. In Espressione cron Synch Finisher, immettere un&#39;espressione cron che rappresenta l&#39;intervallo in cui i tentativi di gestione utente non sono riusciti a eseguire la sincronizzazione. L&#39;utilizzo dell&#39;espressione cron si basa sul sistema di programmazione dei processi open source Quartz, versione 1.4.0.

   Il valore predefinito è 0/13 &amp;ast; ? &amp;ast; , che significa che il controllo viene effettuato ogni 13 minuti.

## Sincronizzazione manuale delle directory {#manually-synchronize-directories}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. (Facoltativo) Per inviare le informazioni di utenti e gruppi in Content Services (obsoleto), selezionate l&#39;opzione Seleziona questa opzione per inviare utenti e gruppi nei provider di archiviazione principale esterni registrati. Questa opzione si applica anche quando si aggiungono nuovi utenti e gruppi tramite la pagina Utenti e gruppi.
1. Selezionate la casella di controllo per ciascun dominio Enterprise da sincronizzare e fate clic su Sincronizza ora.

   Se selezionate più domini, la sincronizzazione del dominio per tutti i domini può essere eseguita contemporaneamente. Tuttavia, se si selezionano i domini separatamente, è possibile eseguire una sola sincronizzazione di dominio alla volta.

## Pianificare la sincronizzazione della directory {#schedule-directory-synchronization}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. Pianificare la sincronizzazione:

   * Per abilitare la sincronizzazione automatica su base giornaliera, in Scheduler selezionare Generato. Selezionare Giornaliero dall&#39;elenco e digitare l&#39;ora nel formato 24 ore nella casella corrispondente. Quando salvate le impostazioni, questo valore viene convertito in un&#39;espressione cron, che viene visualizzata nella casella Espressione cron.
   * Per pianificare la sincronizzazione in un giorno particolare della settimana o del mese, oppure in un mese particolare, selezionate Espressione cursore e digitate l&#39;espressione appropriata nella casella. Ad esempio, eseguire la sincronizzazione alle 1:30 di mattina. l&#39;ultimo venerdì del mese.

L&#39;utilizzo dell&#39;espressione cron si basa sul sistema di programmazione dei processi open source Quartz, versione 1.4.0.

* Per disattivare la sincronizzazione automatica, selezionare Si verifica e selezionare Mai dall&#39;elenco.
* (Facoltativo) Per inviare le informazioni di utenti e gruppi in Content Services (obsoleto), selezionate l&#39;opzione Seleziona questa opzione per inviare utenti e gruppi nei provider di archiviazione principale esterni registrati. Questa opzione si applica anche quando si aggiungono nuovi utenti e gruppi tramite la pagina Utenti e gruppi.
* Fate clic su Salva.

## Interrompi tutte le sincronizzazioni di directory attualmente in corso {#stop-all-directory-synchronizations-currently-in-progress}

1. Nella console di amministrazione, fate clic su Impostazioni > Gestione utente > Gestione dominio.
1. Fate clic su Interrompi. Questo pulsante viene visualizzato solo mentre è in corso la sincronizzazione di una directory.

