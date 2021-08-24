---
title: Visualizzazione e comprensione dei rapporti sulle transazioni
seo-title: Visualizzazione e comprensione dei rapporti sulle transazioni
description: Utilizzare i rapporti sulle transazioni per prendere una decisione informata sull'utilizzo del prodotto e sul ribilanciamento degli investimenti in hardware e software.
seo-description: Utilizzare i rapporti sulle transazioni per prendere una decisione informata sull'utilizzo del prodotto e sul ribilanciamento degli investimenti in hardware e software.
uuid: 56d9f01d-4778-47c9-bbb2-6650a73a3f59
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c04c488b-73f3-49ba-9e89-f97497965757
docset: aem65
exl-id: 3c7cbe1f-ac81-4df9-96b2-662cbc5f2075
source-git-commit: 75e1697c301dca3a649833a45caa1753fdc81514
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 0%

---

# Visualizzazione e comprensione dei rapporti sulle transazioni{#viewing-and-understanding-transaction-reports}

I rapporti sulle transazioni consentono di acquisire e tenere traccia del numero di moduli inviati, documenti elaborati e documenti sottoposti a rendering. L&#39;obiettivo del monitoraggio di queste transazioni è quello di prendere una decisione informata sull&#39;utilizzo del prodotto e sul ribilanciamento degli investimenti in hardware e software. Per ulteriori informazioni, consulta [Panoramica dei rapporti sulle transazioni AEM Forms](../../forms/using/transaction-reports-overview.md).

## Impostazione dei rapporti sulle transazioni  {#setting-up-transaction-reports}

La funzione Report transazioni è disponibile come parte del pacchetto aggiuntivo dei moduli AEM. Per informazioni sull&#39;installazione del pacchetto aggiuntivo su tutte le istanze di authoring e pubblicazione, vedere [Installazione e configurazione di moduli AEM](/help/forms/using/installing-configuring-aem-forms-osgi.md). Una volta installato il pacchetto aggiuntivo per i moduli AEM, procedi come segue:

* Abilita replica inversa su tutte le istanze di pubblicazione
* Abilita rapporti sulle transazioni
* Fornire i diritti per visualizzare un rapporto sulle transazioni
* (Facoltativo) Configura il periodo di scaricamento delle transazioni e le caselle in uscita [](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* I rapporti sulle transazioni di AEM Forms non supportano topologie che contengono solo istanze di pubblicazione.
>* Prima di utilizzare la generazione di rapporti sulle transazioni, assicurati che la replica inversa sia abilitata per tutte le istanze di pubblicazione.
>* I dati della transazione vengono replicati inversamente da un&#39;istanza di pubblicazione solo all&#39;autore o all&#39;istanza di elaborazione corrispondente. L&#39;istanza di authoring o di elaborazione non può replicare ulteriormente i dati in un&#39;altra istanza.

>



### Abilita replica inversa su tutte le istanze di pubblicazione {#enable-reverse-replication-on-all-the-publish-instances}

I rapporti sulle transazioni utilizzano la replica inversa per consolidare il conteggio delle transazioni dalle istanze di pubblicazione alle istanze di creazione. Imposta la replica inversa su tutte le istanze di pubblicazione. Per istruzioni dettagliate su come impostare la replica inversa, vedere [replica](/help/sites-deploying/replication.md).

### Abilita rapporti sulle transazioni {#enable-transaction-reports}

I rapporti sulle transazioni sono disabilitati per impostazione predefinita. È possibile abilitare i rapporti da AEM console Web. per abilitare i rapporti sulle transazioni in un ambiente AEM Forms, esegui i seguenti passaggi su tutte le istanze di authoring e pubblicazione:

1. Accedi a un&#39;istanza AEM come amministratore. Vai a **Strumenti** > **Operazioni** > **Console web**.
1. Individua e apri il servizio **Report transazioni Forms** .
1. Selezionare la casella di controllo Registra transazioni. Fai clic su **Salva**.

   Ripeti i passaggi 1-3 su tutte le istanze di authoring e pubblicazione.

### Fornire i diritti per visualizzare un rapporto sulle transazioni {#provide-rights-to-view-a-transaction-report}

Solo i membri del gruppo fd-administrator possono visualizzare i rapporti sulle transazioni. Per consentire a un utente di visualizzare i rapporti sulle transazioni, rendi gli utenti membri del gruppo fd-administrator. Per istruzioni su come rendere un utente membro di un gruppo di AEM, consulta [Amministrazione di utenti, gruppi e diritti di accesso](/help/sites-administering/user-group-ac-admin.md).

### (Facoltativo) Configura il periodo di scaricamento delle transazioni e le caselle in uscita {#optional-configure-transaction-flush-period-and-outboxes}

Le transazioni vengono memorizzate nella cache prima di essere memorizzate nel repository. Il processo viene seguito per garantire che non vi siano scritture frequenti nell’archivio. Per impostazione predefinita, il periodo di memorizzazione in cache (Periodo di scaricamento transazione) è impostato su 60 secondi. Puoi modificare il periodo predefinito in base all’ambiente. Per modificare il periodo di memorizzazione in cache predefinito, effettua le seguenti operazioni:

1. Accedi alle istanze dell’autore come amministratore. Vai a **Strumenti** > **Operazioni** > **Console web**.
1. Individua e apri il servizio **Forms Transaction Repository Storage Provider** .
1. Specifica il numero di secondi nel campo **Periodo di scaricamento transazione** . Fai clic su **Salva**.

La replica inversa copia i dati delle transazioni nella casella in uscita predefinita delle istanze dell’autore. È possibile inserire i dati delle transazioni in una casella in uscita personalizzata. Esegui i seguenti passaggi per specificare una casella in uscita personalizzata:

1. Accedi alle istanze dell’autore come amministratore. Vai a **Strumenti** > **Operazioni** > **Console web**.
1. Individua e apri il servizio **Forms Transaction Repository Storage Provider** .
1. Specifica il nome della casella in uscita personalizzata nel campo **Outboxes** . Fai clic su **Salva**. Viene creata una casella in uscita con il nome specificato su tutte le istanze dell’autore.

## Visualizzazione del rapporto sulle transazioni {#viewing-the-transaction-report}

Puoi visualizzare i rapporti sulle transazioni nelle istanze di creazione o pubblicazione. Il rapporto sulle transazioni nell’istanza di authoring fornisce una somma aggregata di tutte le transazioni che avvengono sulle istanze di authoring e pubblicazione configurate. Il report delle transazioni sull&#39;istanza di pubblicazione fornisce un conteggio delle transazioni che avvengono solo sull&#39;istanza di pubblicazione sottostante. Esegui i seguenti passaggi per visualizzare il rapporto:

1. Accedi al server AEM Forms all&#39;indirizzo `https://[hostname]:'port'`.
1. Passa a **Strumenti** > **Forms****Visualizza rapporto transazione**.

## Informazioni sul rapporto {#understanding-the-report}

AEM Forms visualizza i rapporti sulle transazioni a partire dalla data configurata, come mostrato in un rapporto di riepilogo di seguito:

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* Utilizza le opzioni **Reimposta la data su oggi** per reimpostare i record delle transazioni. Quando si reimposta la data su oggi, tutti i record di transazione precedenti vengono persi. Quando reattivi la data in un’istanza dell’autore, la modifica non influisce sui rapporti sulle transazioni nelle istanze di pubblicazione e viceversa.
* Utilizza le **Mostra transazioni solo delle istanze di pubblicazione** per visualizzare tutte le transazioni che si sono verificate solo nell&#39;istanza di pubblicazione configurata o nella farm di pubblicazione.
* Utilizza le categorie: **Documento elaborato**, **Documenti sottoposti a rendering** e **Forms inviato** per visualizzare le transazioni corrispondenti. Per il tipo di transazioni contabilizzate in queste categorie, vedere [API per rapporti sulle transazioni fatturabili](../../forms/using/transaction-reports-billable-apis.md).

## Visualizza registri di reporting delle transazioni {#view-transaction-reporting-logs}

Nel reporting delle transazioni vengono inserite tutte le informazioni visualizzate nel report e alcune informazioni aggiuntive nei registri. Le informazioni fornite nei registri sono utili per gli utenti avanzati. Ad esempio, i registri suddividono le transazioni in più categorie granulari rispetto a tre categorie consolidate visualizzate nel rapporto. I registri sono disponibili nel file `error.log` nella directory `/crx-repository/logs/` . I registri sono disponibili anche se non si abilitano i rapporti sulle transazioni da AEM Web Console.

## Articoli correlati {#related-articles}

* [Panoramica dei rapporti sulle transazioni](../../forms/using/transaction-reports-overview.md)
* [API fatturabili per report transazioni](../../forms/using/transaction-reports-billable-apis.md)
* [Registra una transazione per implementazioni personalizzate](/help/forms/using/record-transaction-custom-implementation.md)
