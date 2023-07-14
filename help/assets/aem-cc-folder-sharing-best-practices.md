---
title: Condivisione cartella in [!DNL Adobe Creative Cloud] best practice
description: Configura [!DNL Adobe Experience Manager] per consentire agli utenti di [!DNL Experience Manager Assets] per scambiare cartelle con utenti di Adobe Creative Cloud.
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] a [!DNL Adobe Creative Cloud] condivisione cartelle {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>Il [!DNL Experience Manager] a [!DNL Creative Cloud] La funzione Condivisione cartella è obsoleta. L’Adobe consiglia di utilizzare funzionalità più recenti, come [Adobe collegamento risorsa](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) o [app desktop Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). Ulteriori informazioni in [Best practice per l’integrazione di Experience Manager e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] può essere configurato per consentire agli utenti di [!DNL Assets] per condividere cartelle con gli utenti di [!DNL Adobe Creative Cloud] , in modo che siano disponibili come cartelle condivise in [!DNL Adobe Creative Cloud] servizio assets. Questa funzione può essere utilizzata per scambiare file tra team creativi e [!DNL Assets] utenti, in particolare quando gli utenti creativi non hanno accesso al [!DNL Assets] distribuzione (non si trovano nella rete aziendale).

Questo tipo di integrazione può essere utilizzato nei seguenti casi d’uso, in particolare quando si lavora con utenti che non hanno accesso diretto a [!DNL Assets]:

* [!DNL Assets] gli utenti condividono un set di risorse digitali specifiche con gli utenti di [!DNL Adobe Creative Cloud] file (ad esempio, un resoconto creativo e un insieme di risorse approvate per il lavoro di progettazione di una nuova attività di marketing).
* [!DNL Assets] gli utenti ricevono i nuovi file creati da [!DNL Adobe Creative Cloud] utenti dell’app.

>[!NOTE]
>
>Prima di leggere questo documento, puoi rivedere [Best practice per l’integrazione di Experience Manager e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) per una panoramica dell’integrazione.

## Panoramica {#overview}

[!DNL Experience Manager] a [!DNL Creative Cloud] la condivisione delle cartelle si basa sulla condivisione lato server di cartelle e file tra [!DNL Assets] e [!DNL Creative Cloud] account. Professionisti creativi che utilizzano [!DNL Creative Cloud] sull&#39;app desktop, possono anche rendere le cartelle condivise disponibili direttamente sui loro dischi utilizzando [!DNL Adobe CreativeSync] tecnologia.

Il diagramma seguente fornisce una panoramica dell’integrazione.

![chlimage_1-179](assets/chlimage_1-406.png)

L’integrazione include i seguenti elementi:

* **[!DNL Experience Manager Assets]** distribuito nella rete aziendale (Managed Services o on-premise): la condivisione delle cartelle viene avviata qui.
* **[!DNL Adobe Experience Cloud Assets]servizio core**: funge da intermediario tra [!DNL Experience Manager] e [!DNL Creative Cloud] servizi di storage. L’amministratore di un’organizzazione che utilizza l’integrazione deve stabilire una relazione di affidabilità tra l’organizzazione Experience Cloud e [!DNL Assets] distribuzione. Inoltre, [definire un elenco di collaboratori Creative Cloud approvati](https://experienceleague.adobe.com/docs/core-services/interface/services/assets/t-admin-add-cc-user.html), che [!DNL Assets] gli utenti possono condividere le cartelle per una maggiore sicurezza.

* **[!DNL Creative Cloud]Servizi web di Assets** (archiviazione e [!DNL Creative Cloud] file (interfaccia web): è il luogo in cui vengono specificati gli utenti dell’app Creative Cloud, con cui un utente [!DNL Assets] la cartella è stata condivisa, è stato in grado di accettare l’invito e di visualizzare la cartella nell’archivio dell’account di Creative Cloud.
* **Creative Cloud app desktop**: (facoltativo) consente l’accesso diretto a cartelle e file condivisi dal desktop dell’utente creativo tramite sincronizzazione con [!DNL Creative Cloud] Archiviazione delle risorse.

## Caratteristiche e limitazioni {#characteristics-and-limitations}

* **Propagazione unidirezionale delle modifiche:** Le modifiche apportate ai file vengono propagate in una sola direzione, ovvero dal sistema ([!DNL Experience Manager] o [!DNL Creative Cloud Assets]), dove la risorsa è stata originariamente creata (caricata). L&#39;integrazione non fornisce una sincronizzazione bidirezionale completamente automatizzata tra i due sistemi.
* **Controllo delle versioni:**

   * [!DNL Experience Manager] crea versioni di una risorsa solo al momento degli aggiornamenti se il file ha avuto origine in [!DNL Experience Manager] e viene aggiornato lì.
   * [!DNL Creative Cloud] Assets fornisce risorse proprie [funzione di controllo delle versioni](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) con targeting per gli aggiornamenti Work in Progress (in pratica, memorizza gli aggiornamenti fino a dieci giorni)

* **Limiti di spazio:** Le dimensioni e i volumi dei file scambiati sono limitati dalle [Creative Cloud quota risorse](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) per gli utenti creativi (a seconda del livello di abbonamento) e un limite di 5 GB di dimensione massima del file. Lo spazio è inoltre limitato dalla quota di risorse di cui dispone l’organizzazione nel servizio core Assets di Adobe Experience Cloud.

* **Spazio richiesto:** Anche i file nelle cartelle condivise devono essere fisicamente memorizzati in [!DNL Experience Manager] e quindi in [!DNL Creative Cloud] con una copia memorizzata nella cache in [!DNL Experience Cloud Assets] servizio core.
* **Rete e larghezza di banda:** I file contenuti nelle cartelle condivise e tutti gli aggiornamenti devono essere trasportati in rete tra i sistemi. Assicurati che solo i file e gli aggiornamenti pertinenti siano condivisi.
* **Tipo di cartella**: condivisione di un [!DNL Assets] cartella del tipo `sling:OrderedFolder`, non è supportato nel contesto della condivisione in [!DNL Adobe Experience Cloud]. Se desideri condividere una cartella, quando la crei in [!DNL Assets], non selezionare [!UICONTROL Ordinato] opzione.

## Best practice {#best-practices}

Best practice per l’utilizzo di [!DNL Experience Manager] a [!DNL Creative Cloud] la condivisione delle cartelle include:

* **Considerazioni sul volume:** [!DNL Experience Manager] e [!DNL Creative Cloud] La condivisione cartelle deve essere utilizzata per condividere un numero inferiore di file, ad esempio relativi a una campagna o attività specifica. Per condividere set di risorse più grandi, come tutte le risorse approvate nell’organizzazione, utilizza altri metodi di distribuzione (ad esempio, [!DNL Assets Brand Portal]) o [!DNL Experience Manager] app desktop.
* **Evita la condivisione di gerarchie profonde:** La condivisione funziona in modo ricorsivo e non consente l’annullamento selettivo della condivisione. In genere, solo le cartelle senza sottocartelle o con una gerarchia superficiale, come un livello di sottocartelle, devono essere considerate per la condivisione.
* **Cartelle separate per la condivisione unidirezionale:** Per condividere le risorse finali da, utilizza cartelle separate [!DNL Assets] a [!DNL Creative Cloud] e per la condivisione di risorse pronte per la creazione da [!DNL Creative Cloud] file in [!DNL Assets]. Insieme a una buona convenzione di denominazione per queste cartelle, crea un ambiente di lavoro più facile da comprendere per [!DNL Assets] e [!DNL Creative Cloud] utenti.
* **Evita WIP nella cartella condivisa:** La cartella condivisa non deve essere utilizzata per Work in Progress. Utilizzare una cartella separata in File di Creative Cloud per eseguire operazioni che richiedono modifiche frequenti al file.
* **Avvia nuovo lavoro all&#39;esterno della cartella condivisa:** I nuovi progetti (file creativi) devono essere avviati nella cartella WIP separata in File di Creative Cloud e quando sono pronti per essere condivisi con [!DNL Assets] utenti, devono essere spostati o salvati nella cartella condivisa.
* **Semplificare la struttura di condivisione:** Per una configurazione operativa più gestibile, è consigliabile semplificare la struttura di condivisione. Invece di condividere con tutti gli utenti creativi, [!DNL Assets] le cartelle devono essere condivise solo con i rappresentanti del team, come un direttore creativo o un manager del team. Il manager dal lato creativo riceverà i cespiti finali, deciderà le assegnazioni di lavoro e quindi lascerà che i designer lavorino sui cespiti WIP nel proprio account di Creative Cloud. Possono utilizzare le funzioni di collaborazione Creative Cloud per coordinare il lavoro e infine selezionare e reinserire le risorse pronte per la condivisione [!DNL Assets] nella cartella condivisa pronta per la creazione.

Il diagramma seguente illustra un esempio di configurazione per la creazione di progetti basati sulle risorse finali esistenti da [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
