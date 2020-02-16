---
title: Manutenzione del registro di controllo in AEM 6
seo-title: Manutenzione del registro di controllo in AEM 6
description: Informazioni sulla manutenzione del registro di controllo in AEM.
seo-description: Informazioni sulla manutenzione del registro di controllo in AEM.
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# Manutenzione del registro di controllo in AEM 6{#audit-log-maintenance-in-aem}

Gli eventi AEM idonei per la registrazione del controllo generano molti dati archiviati. Questi dati possono crescere rapidamente nel tempo a causa di repliche, caricamenti di risorse e altre attività del sistema.

La manutenzione del registro di controllo include diverse parti di funzionalità che consentono di automatizzare la manutenzione del registro di controllo in base a criteri specifici.

È implementato come attività di manutenzione settimanale configurabile ed è accessibile tramite la console di monitoraggio di Operations Dashboard.

Per ulteriori informazioni, consulta la Documentazione [](/help/sites-administering/operations-dashboard.md)del dashboard delle operazioni.

Sono disponibili tre tipi di opzioni di rimozione log di controllo:

1. [Pulizia del registro di controllo delle pagine](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [Pulizia log di controllo DAM](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [Rimozione del registro di controllo della replica](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

Ciascuna di esse può essere configurata mediante la creazione di regole nella console Web di AEM. Una volta configurate, è possibile attivarle dalla finestra **Strumenti - Operazioni - Manutenzione - Manutenzione settimanale e dall&#39;esecuzione dell&#39;attività** di manutenzione **** AuditLog.

## Configurare lo scorrimento del registro di controllo delle pagine {#configure-page-audit-log-purging}

Per configurare lo scorrimento del registro di controllo, effettuate le seguenti operazioni:

1. Vai ad Admin Console Web indicando il browser `http://localhost:4502/system/console/configMgr/`

1. Cercare un elemento denominato Regola **rimozione registro controllo** pagine e fare clic su di esso.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. Quindi, configura il programma di eliminazione in base alle tue esigenze. Le opzioni disponibili sono:

   * **** Nome regola: il nome della regola della politica di audit;
   * **** Percorso contenuto: il percorso del contenuto a cui si applicherà la regola;
   * **** Età minima: l&#39;ora in giorni in cui i registri di controllo devono essere conservati;
   * **** Tipo registro di controllo: il tipo di registro di controllo da eliminare.
   >[!NOTE]
   >
   >Il percorso del contenuto si applica solo agli elementi secondari del `/var/audit/com.day.cq.wcm.core.page` nodo nella directory archivio.

1. Salva la regola.
1. La regola appena creata deve essere esposta nel Pannello operazioni per poterla eseguire. A questo scopo, andate **Strumenti - Operazioni - Manutenzione** dalla schermata introduttiva di AEM.

1. Premere la scheda Finestra **manutenzione** settimanale.

1. L&#39;attività di manutenzione è già presente nella scheda Attività **di manutenzione** AuditLog.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. È possibile controllare la data dell&#39;esecuzione successiva, configurarla o eseguirla manualmente premendo il pulsante di riproduzione.

In AEM 6.3, se la finestra di manutenzione pianificata viene chiusa prima del completamento dell’attività di rimozione del registro di controllo, l’attività viene arrestata automaticamente. Viene ripresa all’apertura della finestra di manutenzione successiva.

**Con AEM 6.5**, puoi arrestare manualmente un&#39;attività di rimozione log di controllo in esecuzione facendo clic sull&#39;icona **Interrompi** . Nella successiva esecuzione l&#39;attività riprenderà in modo sicuro.

>[!NOTE]
>
>Per interrompere l’attività di manutenzione si intende sospendere l’esecuzione senza perdere traccia del processo già in corso.

## Configurare lo scorrimento del registro di controllo DAM {#configure-dam-audit-log-purging}

1. Andate alla console di sistema all&#39;indirizzo *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Cercare la regola **DAM Audit Log Purge** e fare clic sul risultato.
1. Nella finestra successiva, configurate la regola di conseguenza. Le opzioni sono:

   * **** Nome regola: il nome della regola della politica di audit;
   * **** Percorso contenuto: percorso del contenuto a cui si applicherà la regola
   * **** Età minima: l&#39;ora in giorni i registri di controllo devono essere conservati
   * **** Tipi di evento Dam log di controllo: i tipi di eventi di controllo DAM da eliminare.

1. Fate clic su **Salva** per salvare la configurazione

## Configurare lo scorrimento del registro di controllo della replica {#configure-replication-audit-log-purging}

1. Andate alla console di sistema all&#39;indirizzo *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Cercare **Replication Audit Log Purge Scheduler** e fare clic sul risultato
1. Nella finestra successiva, configurate la regola di conseguenza. Le opzioni sono:

   * **** Nome regola: nome della regola del criterio di controllo
   * **** Percorso contenuto: percorso del contenuto a cui si applicherà la regola
   * **** Età minima: l&#39;ora in giorni i registri di controllo devono essere conservati
   * **** Tipi di eventi di replica del registro di controllo: i tipi di eventi di controllo della replica che devono essere eliminati

1. Fate clic su **Salva** per salvare la configurazione.

