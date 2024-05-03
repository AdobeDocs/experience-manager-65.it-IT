---
title: Visualizzazione e comprensione dei rapporti sulle transazioni
description: Utilizzare i report sulle transazioni per prendere una decisione informata sull'utilizzo del prodotto e sul ribilanciamento degli investimenti in hardware e software.
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Transaction Reports
exl-id: 3c7cbe1f-ac81-4df9-96b2-662cbc5f2075
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 0%

---

# Visualizzazione e informazioni sui rapporti sulle transazioni per AEM Forms su OSGi{#viewing-and-understanding-transaction-reports}

I rapporti sulle transazioni consentono di acquisire e registrare il numero di moduli inviati, documenti elaborati e documenti sottoposti a rendering. L&#39;obiettivo del tracciamento di queste transazioni è prendere una decisione informata sull&#39;utilizzo del prodotto e riequilibrare gli investimenti in hardware e software. Per ulteriori informazioni, consulta [Panoramica dei rapporti sulle transazioni di AEM Forms](../../forms/using/transaction-reports-overview.md).

## Impostazione dei rapporti sulle transazioni  {#setting-up-transaction-reports}

La funzione dei rapporti sulle transazioni è disponibile come parte del pacchetto aggiuntivo AEM forms. Per informazioni sull’installazione del pacchetto del componente aggiuntivo in tutte le istanze di authoring e pubblicazione, consulta [Installazione e configurazione di moduli AEM](/help/forms/using/installing-configuring-aem-forms-osgi.md). Dopo aver installato il pacchetto del componente aggiuntivo AEM Forms, eseguire le operazioni seguenti:

* Abilita replica inversa su tutte le istanze di pubblicazione
* Abilita rapporti sulle transazioni
* Fornire i diritti per visualizzare un report sulle transazioni
* (Facoltativo) Configurare il periodo di svuotamento delle transazioni e le caselle in uscita [](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* I rapporti sulle transazioni di AEM Forms non supportano topologie che contengono solo istanze di pubblicazione.
>* Prima di utilizzare la generazione rapporti sulle transazioni, assicurati che la replica inversa sia abilitata per tutte le istanze di pubblicazione.
>* I dati delle transazioni vengono replicati in modo inverso da un’istanza Publish all’unica istanza di authoring o elaborazione corrispondente. L’istanza di authoring o elaborazione non può replicare ulteriormente i dati in un’altra istanza.
>

### Abilita replica inversa su tutte le istanze di pubblicazione {#enable-reverse-replication-on-all-the-publish-instances}

I rapporti sulle transazioni utilizzano la replica inversa per consolidare il conteggio delle transazioni dalle istanze di pubblicazione alle istanze di authoring. Imposta la replica inversa su tutte le istanze di pubblicazione. Per istruzioni dettagliate sull’impostazione della replica inversa, consulta [replica](/help/sites-deploying/replication.md).

### Abilita rapporti sulle transazioni {#enable-transaction-reports}

I rapporti sulle transazioni sono disabilitati per impostazione predefinita. Puoi abilitare i rapporti dalla console web dell’AEM. per abilitare i rapporti sulle transazioni in un ambiente AEM Forms, effettua le seguenti operazioni su tutte le istanze di authoring e pubblicazione:

1. Accedi a un’istanza dell’AEM come amministratore. Vai a **Strumenti** > **Operazioni** > **Console web**.
1. Individuare e aprire **Generazione rapporti sulle transazioni Forms** servizio.
1. Selezionare la casella di controllo Registra transazioni. Fai clic su **Salva**.

   Ripeti i passaggi 1-3 su tutte le istanze di authoring e pubblicazione.

### Fornire i diritti per visualizzare un report sulle transazioni {#provide-rights-to-view-a-transaction-report}

Solo i membri del gruppo fd-administrator possono visualizzare i rapporti sulle transazioni. Per consentire a un utente di visualizzare i report sulle transazioni, rendere gli utenti membri del gruppo fd-administrator. Per istruzioni su come rendere un utente membro di un gruppo AEM, vedi [Amministrazione di utenti, gruppi e diritti di accesso](/help/sites-administering/user-group-ac-admin.md).

### (Facoltativo) Configurare il periodo di svuotamento delle transazioni e le caselle in uscita {#optional-configure-transaction-flush-period-and-outboxes}

Le transazioni vengono memorizzate nella cache prima di essere memorizzate nell&#39;archivio. Il processo viene seguito per garantire che non vi siano scritture frequenti nell’archivio. Per impostazione predefinita, il periodo di caching (periodo di scaricamento delle transazioni) è impostato su 60 secondi. Puoi modificare il periodo predefinito in base all’ambiente in uso. Per modificare il periodo di caching predefinito, effettua le seguenti operazioni:

1. Accedi alle istanze di authoring come amministratore. Vai a **Strumenti** > **Operazioni** > **Console web**.
1. Individuare e aprire **Provider archiviazione archivio transazioni Forms** servizio.
1. Specifica il numero di secondi nella **Periodo di scaricamento transazione** campo. Fai clic su **Salva**.

La replica inversa copia i dati della transazione nella casella in uscita predefinita delle istanze di authoring. È possibile inserire i dati delle transazioni in una casella in uscita personalizzata. Per specificare una casella in uscita personalizzata, effettuare le seguenti operazioni:

1. Accedi alle istanze di authoring come amministratore. Vai a **Strumenti** > **Operazioni** > **Console web**.
1. Individuare e aprire **Provider archiviazione archivio transazioni Forms** servizio.
1. Specifica il nome della casella in uscita personalizzata **Caselle in uscita** campo. Fai clic su **Salva**. Viene creata una casella in uscita con il nome specificato in tutte le istanze di authoring.

## Visualizzazione del report delle transazioni {#viewing-the-transaction-report}

Puoi visualizzare i rapporti sulle transazioni nelle istanze di authoring o pubblicazione. Il report delle transazioni sull’istanza di authoring fornisce una somma aggregata di tutte le transazioni che hanno luogo sulle istanze di authoring e pubblicazione configurate. Il report delle transazioni sull’istanza Publish fornisce un conteggio delle transazioni che vengono eseguite solo sull’istanza Publish sottostante. Per visualizzare il rapporto, effettua le seguenti operazioni:

1. Accedi al server AEM Forms all’indirizzo `https://[hostname]:'port'`.
1. Accedi a **Strumenti** > **Forms**>**Visualizza report transazioni**.

## Informazioni sul rapporto {#understanding-the-report}

AEM Forms visualizza i rapporti sulle transazioni dalla data configurata, come mostrato in un rapporto di riepilogo di seguito:

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* Utilizza il **Reimposta la data a oggi** opzioni per reimpostare i record delle transazioni. Quando si reimposta la data a oggi, tutti i record precedenti delle transazioni vengono persi. Quando reimposti la data su un’istanza Autore, la modifica non influisce sui rapporti sulle transazioni delle istanze Pubblica e viceversa.
* Utilizza il **Mostra transazioni solo delle istanze di pubblicazione** per visualizzare tutte le transazioni che si sono verificate solo nell’istanza o nella farm di pubblicazione configurata.
* Utilizza le categorie: **Documento elaborato**, **Documenti sottoposti a rendering**, e **Forms inviato** per visualizzare le transazioni corrispondenti. Per il tipo di transazioni contabilizzate in queste categorie, vedere [API per report transazioni fatturabili](../../forms/using/transaction-reports-billable-apis.md).

## Visualizzare i registri di reporting delle transazioni {#view-transaction-reporting-logs}

Nella generazione rapporti sulle transazioni vengono inserite tutte le informazioni visualizzate nel rapporto e alcune informazioni aggiuntive nei registri. Le informazioni fornite nei registri sono utili per gli utenti avanzati. Ad esempio, i registri suddividono le transazioni in più categorie granulari rispetto alle tre categorie consolidate visualizzate nel rapporto. I registri sono disponibili nel `error.log` file in corrispondenza di `/crx-repository/logs/` directory. I registri sono disponibili anche se non abiliti i rapporti sulle transazioni dalla console web AEM.

## Articoli correlati {#related-articles}

* [Panoramica dei rapporti sulle transazioni per AEM Forms su OSGi](../../forms/using/transaction-reports-overview.md)
* [Rapporti sulle transazioni API fatturabili per AEM Forms su OSGi](../../forms/using/transaction-reports-billable-apis.md)
* [Registrare una transazione per le implementazioni personalizzate per AEM Forms su OSGi](/help/forms/using/record-transaction-custom-implementation.md)
