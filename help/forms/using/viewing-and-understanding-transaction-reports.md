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
translation-type: tm+mt
source-git-commit: 4ee3b99a3f0a5d37441eee76c3ec747afcf2e32e
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---


# Visualizzazione e comprensione dei rapporti sulle transazioni{#viewing-and-understanding-transaction-reports}

I rapporti sulle transazioni consentono di acquisire e tenere traccia del numero di moduli inviati, documenti elaborati e documenti sottoposti a rendering. L&#39;obiettivo dietro il monitoraggio di queste transazioni è quello di prendere una decisione informata sull&#39;utilizzo del prodotto e sul ribilanciamento degli investimenti in hardware e software. Per ulteriori informazioni, vedere [ AEM Forms Transaction Reports Overview](../../forms/using/transaction-reports-overview.md).

## Impostazione dei rapporti sulle transazioni {#setting-up-transaction-reports}

La funzione Report transazione è disponibile come parte del pacchetto del componente aggiuntivo AEM moduli. Per informazioni sull&#39;installazione del pacchetto del componente aggiuntivo in tutte le istanze di creazione e pubblicazione, vedere [Installazione e configurazione AEM moduli](/help/forms/using/installing-configuring-aem-forms-osgi.md). Dopo aver installato il pacchetto del componente aggiuntivo per i moduli AEM, effettuate le seguenti operazioni:

* Abilita replica inversa su tutte le istanze di pubblicazione
* Abilita rapporti sulle transazioni
* Fornire i diritti necessari per visualizzare un rapporto sulle transazioni
* (Facoltativo) Configurare il periodo di scaricamento delle transazioni e le caselle in uscita [](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>*  rapporti sulle transazioni AEM Forms non supportano topologie che contengono solo istanze di pubblicazione.
>* Prima di utilizzare il reporting delle transazioni, assicurarsi che la replica inversa sia abilitata per tutte le istanze di pubblicazione.
>* I dati della transazione vengono replicati in modo inverso da un&#39;istanza di pubblicazione solo all&#39;autore o all&#39;istanza di elaborazione corrispondente. L&#39;istanza di creazione o elaborazione non può replicare ulteriormente i dati in un&#39;altra istanza.

>



### Abilita replica inversa su tutte le istanze di pubblicazione {#enable-reverse-replication-on-all-the-publish-instances}

I rapporti sulle transazioni utilizzano la replica inversa per consolidare il conteggio delle transazioni dalle istanze di pubblicazione alle istanze di creazione. Configurate la replica inversa su tutte le istanze di pubblicazione. Per istruzioni dettagliate sulla configurazione della replica inversa, vedere [replica](/help/sites-deploying/replication.md).

### Abilita rapporti sulle transazioni {#enable-transaction-reports}

I rapporti sulle transazioni sono disattivati per impostazione predefinita. È possibile abilitare i rapporti da AEM console Web. per abilitare i rapporti sulle transazioni in un ambiente AEM Forms , eseguite i seguenti passaggi su tutte le istanze di creazione e pubblicazione:

1. Accedete a un&#39;istanza AEM come amministratore. Andate a **Strumenti** > **Operazioni** > **Console Web**.
1. Individuare e aprire il servizio **Forms Transaction Reporting**.
1. Selezionare la casella di controllo Registra transazioni. Fai clic su **Salva**.

   Ripetete i passaggi da 1 a 3 per tutte le istanze di creazione e pubblicazione.

### Fornire i diritti per visualizzare un report di transazione {#provide-rights-to-view-a-transaction-report}

Solo i membri del gruppo di amministratori di fd possono visualizzare i rapporti sulle transazioni. Per consentire a un utente di visualizzare i rapporti sulle transazioni, è necessario che gli utenti siano membri del gruppo di amministratori di fd. Per istruzioni su come rendere un utente membro di un gruppo di AEM, consultate [Amministrazione di utenti, gruppi e diritti di accesso](/help/sites-administering/user-group-ac-admin.md).

### (Facoltativo) Configurare il periodo di scaricamento delle transazioni e le caselle in uscita {#optional-configure-transaction-flush-period-and-outboxes}

Le transazioni vengono memorizzate nella cache prima di essere archiviate nella directory archivio. Per impostazione predefinita, il periodo di caching (Periodo di scaricamento transazione) è impostato su 60 secondi. Per modificare il periodo di memorizzazione nella cache predefinito, effettuate le seguenti operazioni:

1. Accedete per creare le istanze come amministratore. Andate a **Strumenti** > **Operazioni** > **Console Web**.
1. Individuare e aprire il servizio **Forms Transaction Repository Storage Provider**.
1. Specificare il numero di secondi nel campo **Periodo di scaricamento transazione**. Fai clic su **Salva**.

Inverti replica copia i dati delle transazioni nella casella in uscita predefinita delle istanze dell&#39;autore. È possibile inserire i dati della transazione in una casella in uscita personalizzata. Effettuate le seguenti operazioni per specificare una casella in uscita personalizzata:

1. Accedete per creare le istanze come amministratore. Andate a **Strumenti** > **Operazioni** > **Console Web**.
1. Individuare e aprire il servizio **Forms Transaction Repository Storage Provider**.
1. Specificate il nome della casella in uscita personalizzata nel campo **Outbox**. Fai clic su **Salva**. Su tutte le istanze dell’autore viene creata una casella in uscita con il nome specificato.

## Visualizzazione del report della transazione {#viewing-the-transaction-report}

Potete visualizzare i rapporti sulle transazioni sulle istanze di creazione o pubblicazione. Il rapporto sulle transazioni nell&#39;istanza di creazione fornisce una somma aggregata di tutte le transazioni che avvengono nelle istanze di creazione e pubblicazione configurate. Il rapporto sulle transazioni nell&#39;istanza di pubblicazione fornisce un conteggio delle transazioni che avvengono solo nell&#39;istanza di pubblicazione sottostante. Per visualizzare il rapporto, effettuate le seguenti operazioni:

1. Accedete al server AEM Forms  all&#39;indirizzo `https://[hostname]:'port'`.
1. Passare a **Strumenti** > **Forms**>**Visualizza rapporto transazione**.

## Informazioni sul rapporto {#understanding-the-report}

 AEM Forms visualizza i rapporti sulle transazioni a partire dalla data configurata, come mostrato in un rapporto di riepilogo seguente:

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* Utilizzare le opzioni **Reimposta la data su oggi** per ripristinare i record delle transazioni. Quando reimposti la data odierna, tutti i record di transazione precedenti vengono persi. Quando reimpostate la data su un’istanza di creazione, la modifica non influisce sui rapporti sulle transazioni nelle istanze di pubblicazione e viceversa.
* Utilizzate l&#39;opzione **Mostra transazioni solo delle istanze di Publish** per visualizzare tutte le transazioni che si sono verificate solo nell&#39;istanza di pubblicazione configurata o nella farm di pubblicazione.
* Utilizzare le categorie: **Documento elaborato**, **Documenti sottoposti a rendering** e **Forms inviato** per visualizzare le transazioni corrispondenti. Per il tipo di transazioni contabilizzate in queste categorie, vedere [Billable Transaction Reports APIs](../../forms/using/transaction-reports-billable-apis.md).

## Visualizza registri di reporting delle transazioni {#view-transaction-reporting-logs}

Il reporting delle transazioni inserisce tutte le informazioni visualizzate nel rapporto e alcune informazioni aggiuntive nei registri. Le informazioni fornite nei registri sono utili per gli utenti avanzati. Ad esempio, i registri dividono le transazioni in più categorie granulari rispetto a tre categorie consolidate visualizzate nel rapporto. I file di registro sono disponibili nel file `error.log` nella directory `/crx-repository/logs/`. I registri sono disponibili anche se non si abilitano i rapporti sulle transazioni da AEM console Web.

## Articoli correlati {#related-articles}

* [Panoramica dei report sulle transazioni](../../forms/using/transaction-reports-overview.md)
* [API fatturabili report transazioni](../../forms/using/transaction-reports-billable-apis.md)
* [Registrazione di una transazione per le implementazioni personalizzate](/help/forms/using/record-transaction-custom-implementation.md)

