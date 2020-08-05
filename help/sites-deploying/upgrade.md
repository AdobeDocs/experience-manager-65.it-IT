---
title: Aggiornamento a AEM 6.5
seo-title: Aggiornamento a AEM 6.5
description: Scoprite le nozioni di base per aggiornare un'installazione AEM precedente a AEM 6.5.
seo-description: Scoprite le nozioni di base per aggiornare un'installazione AEM precedente a AEM 6.5.
uuid: 45368056-273c-4f1a-9da6-e7ba5c2bbc0d
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: ebd99cc4-8762-4c28-a177-d62dac276afe
docset: aem65
targetaudience: target-audience upgrader
translation-type: tm+mt
source-git-commit: d3a69bbbc9c3707538be74fd05f94f20a688d860
workflow-type: tm+mt
source-wordcount: '729'
ht-degree: 4%

---


# Upgrading to AEM 6.5 {#upgrading-to-aem}

In questa sezione viene descritto l&#39;aggiornamento di un&#39;installazione AEM a AEM 6.5:

* [Pianificazione dell&#39;aggiornamento](/help/sites-deploying/upgrade-planning.md)
* [Valutazione della complessità dell&#39;aggiornamento con il rilevamento dei pattern](/help/sites-deploying/pattern-detector.md)
* [Compatibilità con le versioni precedenti della AEM 6.5](/help/sites-deploying/backward-compatibility.md)
* [Utilizzo della reindicizzazione offline per ridurre i tempi di inattività durante un aggiornamento](/help/sites-deploying/upgrade-offline-reindexing.md)
* [Procedura di aggiornamento](/help/sites-deploying/upgrade-procedure.md)
* [Aggiornamento di codice e personalizzazioni](/help/sites-deploying/upgrading-code-and-customizations.md)
* [Attività di manutenzione pre-aggiornamento](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [Esecuzione di un aggiornamento locale](/help/sites-deploying/in-place-upgrade.md)
* [Post Upgrade Checks e risoluzione dei problemi](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [Aggiornamenti sostenibili](/help/sites-deploying/sustainable-upgrades.md)
* [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md)
* [Ristrutturazione del repository nella AEM 6.5](/help/sites-deploying/repository-restructuring.md)

Per fare un riferimento più semplice alle istanze AEM coinvolte in queste procedure, in questi articoli vengono utilizzati i termini seguenti:

* L&#39;istanza *di origine* è l&#39;istanza AEM da cui si sta effettuando l&#39;aggiornamento.
* L’istanza *di destinazione* è quella a cui si sta effettuando l’aggiornamento.

>[!NOTE]
>
>Nell&#39;ambito degli sforzi volti a migliorare l&#39;affidabilità degli aggiornamenti, AEM ha subito una ristrutturazione esaustiva dei depositi. Per ulteriori informazioni su come allineare con la nuova struttura, vedere Ristrutturazione [repository in AEM.](/help/sites-deploying/repository-restructuring.md)

## Cos&#39;È Cambiato? {#what-has-changed}

Di seguito sono riportate le principali modifiche apportate alle note nelle ultime diverse versioni di AEM:

AEM 6.0 ha introdotto il nuovo repository Jackrabbit Oak. I Manager di persistenza sono stati sostituiti da [Micro Kernel](/help/sites-deploying/platform.md#contentbody_title_4). A partire dalla versione 6.1, CRX2 non è più supportato. È necessario eseguire uno strumento di migrazione denominato crx2oak per migrare i repository CRX2 dalle istanze 5.6.1. Per ulteriori informazioni, vedere [Utilizzo dello strumento](/help/sites-deploying/using-crx2oak.md)di migrazione CRX2OAK.

Se Asset Insights deve essere utilizzato e state effettuando l’aggiornamento da una versione precedente alla AEM 6.2, le risorse devono essere migrate e gli ID devono essere generati tramite un file JMX. Nei test interni, le risorse 125K in un ambiente TarMK sono state migrate in un&#39;ora, ma i risultati potrebbero variare.

6.3 ha introdotto un nuovo formato per il `SegmentNodeStore`, che è alla base dell&#39;implementazione TarMK. Se si sta effettuando l&#39;aggiornamento da una versione precedente alla AEM 6.3, sarà necessario effettuare una migrazione dell&#39;archivio nell&#39;ambito dell&#39;aggiornamento, con conseguente interruzione del sistema.

 Adobe Engineering stima che questo sia di circa 20 minuti. Si noti che la reindicizzazione non sarà necessaria. Inoltre, è stata rilasciata una nuova versione dello strumento crx2oak per lavorare con il nuovo formato del repository.

**Questa migrazione non è necessaria se si esegue l&#39;aggiornamento da AEM 6.3 a AEM 6.5.**

Le attività di manutenzione pre-aggiornamento sono state ottimizzate per supportare l&#39;automazione.

Le opzioni di utilizzo della riga di comando crx2oak sono state modificate per essere di facile automazione e supportare più percorsi di aggiornamento.

I controlli successivi all&#39;aggiornamento sono stati resi anche semplici da automazione.

La raccolta periodica dei rifiuti delle revisioni e la raccolta dei rifiuti nell&#39;archivio dati sono ora attività di manutenzione di routine che devono essere eseguite periodicamente. Con l&#39;introduzione di AEM 6.3,  Adobe supporta e consiglia la pulizia delle revisioni online. Per informazioni sulla configurazione di queste attività, vedere Pulizia [](/help/sites-deploying/revision-cleanup.md) revisioni.

AEM di recente è stato introdotto il [Rilevatore](/help/sites-deploying/pattern-detector.md) pattern per valutare la complessità dell&#39;aggiornamento quando si inizia la pianificazione per l&#39;aggiornamento. 6.5 ha anche una forte attenzione sulla compatibilità [](/help/sites-deploying/backward-compatibility.md) con le versioni precedenti. Infine, vengono aggiunte anche le best practice per gli aggiornamenti [](/help/sites-deploying/sustainable-upgrades.md) sostenibili.

Per ulteriori dettagli sulle modifiche apportate alle versioni AEM recenti, consulta le note sulla versione complete:

* [https://helpx.adobe.com/it/experience-manager/6-2/release-notes.html](https://helpx.adobe.com/it/experience-manager/6-2/release-notes.html)
* [https://helpx.adobe.com/it/experience-manager/6-3/release-notes.html](https://helpx.adobe.com/it/experience-manager/6-3/release-notes.html)
* [https://helpx.adobe.com/it/experience-manager/6-4/release-notes.html](https://helpx.adobe.com/it/experience-manager/6-4/release-notes.html)
* [https://helpx.adobe.com/it/experience-manager/6-5/release-notes.html](https://helpx.adobe.com/it/experience-manager/6-5/release-notes.html)

## Panoramica sull&#39;aggiornamento {#upgrade-overview}

L&#39;aggiornamento AEM è un processo a più fasi, a volte a più mesi. La struttura seguente è stata fornita come panoramica di ciò che è incluso in un progetto di aggiornamento e del contenuto che è stato incluso in questa documentazione:

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## Flusso di aggiornamento {#upgrade-overview-1}

Il diagramma seguente cattura il flusso complessivo raccomandato evidenziando l&#39;approccio di aggiornamento. Prendete nota del riferimento alle nuove funzioni introdotte. L&#39;aggiornamento dovrebbe iniziare con il rilevamento dei pattern (vedere [Valutazione della complessità dell&#39;aggiornamento con il rilevamento](/help/sites-deploying/pattern-detector.md)dei pattern), che dovrebbe consentire di decidere il percorso da seguire per compatibilità con AEM 6.4 in base ai pattern nel report generato.

In 6.5 è stata messa a fuoco una grande priorità per mantenere tutte le nuove funzioni compatibili con le versioni precedenti, ma nei casi in cui si verificano ancora alcuni problemi di compatibilità con le versioni precedenti, la modalità di compatibilità consente di posticipare temporaneamente lo sviluppo per mantenere il codice personalizzato conforme alla versione 6.5. Questo approccio consente di evitare lo sforzo di sviluppo subito dopo l’aggiornamento (consultate Compatibilità [con versioni precedenti nella AEM 6.5](/help/sites-deploying/backward-compatibility.md)).

Infine, nel tuo ciclo di sviluppo 6.5, le funzionalità introdotte in Aggiornamenti sostenibili (vedi Aggiornamenti [](/help/sites-deploying/sustainable-upgrades.md)sostenibili) ti aiutano a seguire le best practice per rendere gli aggiornamenti futuri ancora più efficienti e perfetti.

![6_4_upgrade_overviewflowchart-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)

