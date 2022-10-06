---
title: Manutenzione del registro di controllo in AEM 6
seo-title: Audit Log Maintenance in AEM 6
description: Scopri la Manutenzione del log di controllo in AEM.
seo-description: Lear about Audit Log Maintenance in AEM.
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
exl-id: 1e05faf5-619a-4ea3-acbf-2fd37c71e6d2
feature: Operations
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# Manutenzione del registro di controllo in AEM 6{#audit-log-maintenance-in-aem}

AEM eventi idonei per la registrazione di controllo generano molti dati archiviati. Questi dati possono crescere rapidamente nel tempo a causa di repliche, caricamenti di risorse e altre attività del sistema.

La manutenzione del registro di controllo include diverse parti di funzionalità che consentono di automatizzare la manutenzione del registro di controllo in base a criteri specifici.

Viene implementato come attività di manutenzione settimanale configurabile ed è accessibile tramite la console di monitoraggio di Operations Dashboard.

Per ulteriori informazioni, consulta la [Documentazione del dashboard delle operazioni](/help/sites-administering/operations-dashboard.md).

Sono disponibili tre tipi di opzioni di eliminazione del log di controllo:

1. [Pulizia del registro di controllo delle pagine](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [Rimozione del log di controllo DAM](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [Eliminazione del registro di controllo della replica](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

È possibile configurarle creando regole nella Console Web AEM. Una volta configurati, puoi attivarli selezionando **Strumenti - Operazioni - Manutenzione - Finestra Manutenzione settimanale** e l&#39;esecuzione del **Attività di manutenzione AuditLog**.

## Configurare l’eliminazione del log di controllo della pagina {#configure-page-audit-log-purging}

Segui questi passaggi per configurare l’eliminazione del registro di controllo:

1. Passa all’amministratore della console Web puntando il browser verso `http://localhost:4502/system/console/configMgr/`

1. Cerca un elemento denominato **Regola di eliminazione del registro di controllo delle pagine** e fai clic su di esso.

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. Quindi, configura la pianificazione della rimozione in base alle tue esigenze. Le opzioni disponibili sono:

   * **Nome regola:** il nome della regola della politica di audit;
   * **Percorso contenuto:** il percorso del contenuto a cui si applicherà la regola;
   * **Età minima:** il tempo in giorni necessario per mantenere i registri di audit;
   * **Tipo di registro di controllo:** il tipo di registro di controllo da eliminare.

   >[!NOTE]
   >
   >Il percorso del contenuto si applica solo agli elementi secondari del `/var/audit/com.day.cq.wcm.core.page` nel repository.

1. Salva la regola.
1. La regola appena creata deve essere esposta nel dashboard delle operazioni per eseguirla. Per fare questo, vai **Strumenti - Operazioni - Manutenzione** dalla schermata di benvenuto AEM.

1. Premere **Finestra Manutenzione settimanale** il Card.

1. Troverai l’attività di manutenzione già presente nella sezione **Attività di manutenzione AuditLog** il Card.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. È possibile controllare la data dell&#39;esecuzione successiva, configurarla o eseguirla manualmente premendo il pulsante di riproduzione.

In AEM 6.3, se la finestra di manutenzione programmata viene chiusa prima del completamento dell&#39;attività di eliminazione del log di controllo, l&#39;attività viene arrestata automaticamente. Viene ripreso quando si apre la prossima finestra di manutenzione.

**Con AEM 6.5**, puoi interrompere manualmente un&#39;attività di eliminazione del registro di controllo facendo clic su **Interrompi** icona. All&#39;esecuzione successiva l&#39;attività riprenderà in modo sicuro.

>[!NOTE]
>
>Per interrompere l’attività di manutenzione, sospenderne l’esecuzione senza perdere traccia del processo già in corso.

## Configurare l’eliminazione del log di controllo DAM {#configure-dam-audit-log-purging}

1. Passa alla console di sistema in *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Cerca **Eliminazione del registro di controllo DAM** e fai clic sul risultato.
1. Nella finestra successiva, configura di conseguenza la regola. Le opzioni sono:

   * **Nome regola:** il nome della regola della politica di audit;
   * **Percorso contenuto:** il percorso del contenuto a cui si applicherà la regola
   * **Età minima:** l’ora in giorni in cui i registri di controllo devono essere conservati
   * **Tipi di eventi Dam log di controllo:** i tipi di eventi di controllo DAM che devono essere eliminati.

1. Fai clic su **Salva** per salvare la configurazione

## Configurare l’eliminazione del log di controllo della replica  {#configure-replication-audit-log-purging}

1. Passa alla console di sistema in *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. Cerca **Utilità di pianificazione eliminazione registro di controllo replica** e clicca sul risultato
1. Nella finestra successiva, configura di conseguenza la regola. Le opzioni sono:

   * **Nome regola:** il nome della regola dei criteri di audit
   * **Percorso contenuto:** il percorso del contenuto a cui si applicherà la regola
   * **Età minima:** l’ora in giorni in cui i registri di controllo devono essere conservati
   * **Tipi di eventi di replica del registro di controllo:** i tipi di eventi di controllo della replica che devono essere eliminati

1. Fai clic su **Salva** per salvare la configurazione.
