---
title: Condivisione di cartelle su [!DNL Adobe Creative Cloud] best practice
description: Configura [!DNL Adobe Experience Manager] per consentire agli utenti di [!DNL Experience Manager Assets] per scambiare cartelle con gli utenti Adobe Creative Cloud.
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: a76772b8761e35a828814ffe0ac3b019266ff008
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] a [!DNL Adobe Creative Cloud] condivisione cartelle {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>La [!DNL Experience Manager] a [!DNL Creative Cloud] La funzione Condivisione cartelle è obsoleta. Adobe consiglia vivamente di utilizzare funzionalità più recenti, come [Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) o [app desktop Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). Ulteriori informazioni in [Best practice per l’integrazione di Experience Manager e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] può essere configurato per consentire agli utenti di [!DNL Assets] per condividere cartelle con gli utenti di [!DNL Adobe Creative Cloud] app, in modo che siano disponibili come cartelle condivise nel [!DNL Adobe Creative Cloud] servizio assets. La funzione può essere utilizzata per scambiare file tra team creativi e [!DNL Assets] , specialmente quando gli utenti creativi non hanno accesso al [!DNL Assets] distribuzione (non presente nella rete aziendale).

Questo tipo di integrazione può essere utilizzato nei seguenti casi d’uso, specialmente quando si lavora con utenti che non hanno accesso diretto ad [!DNL Assets]:

* [!DNL Assets] gli utenti condividono un set di risorse digitali specifiche con gli utenti di [!DNL Adobe Creative Cloud] file (ad esempio, una descrizione creativa e un set di risorse approvate per il lavoro di progettazione per una nuova attività di marketing).
* [!DNL Assets] gli utenti ricevono nuovi file creati da [!DNL Adobe Creative Cloud] utenti dell’app.

>[!NOTE]
>
>Prima di leggere questo documento, è possibile esaminare il [Best practice per l’integrazione di Experience Manager e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) per una panoramica dell’integrazione.

## Panoramica {#overview}

[!DNL Experience Manager] a [!DNL Creative Cloud] la condivisione delle cartelle si basa sulla condivisione lato server di cartelle e file tra [!DNL Assets] e [!DNL Creative Cloud] conti. Professionisti creativi che utilizzano [!DNL Creative Cloud] app desktop sul desktop, può inoltre rendere le cartelle condivise disponibili direttamente sui dischi utilizzando [!DNL Adobe CreativeSync] tecnologia.

Il diagramma seguente fornisce una panoramica dell’integrazione.

![chlimage_1-179](assets/chlimage_1-406.png)

L’integrazione include i seguenti elementi:

* **[!DNL Experience Manager Assets]** implementato nella rete aziendale (servizi gestiti o on-premise): La condivisione delle cartelle viene avviata qui.
* **[!DNL Adobe Marketing Cloud Assets]servizio core**: Agisce come intermediario tra [!DNL Experience Manager] e [!DNL Creative Cloud] servizi di storage. Un amministratore di un&#39;organizzazione che utilizza l&#39;integrazione deve stabilire una relazione di trust tra l&#39;organizzazione del Marketing Cloud e [!DNL Assets] distribuzione. Inoltre [definire un elenco di collaboratori di Creative Cloud approvati](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html)che [!DNL Assets] gli utenti possono condividere anche le cartelle per ulteriore sicurezza.

* **[!DNL Creative Cloud]Servizi web Assets** (immagazzinamento e [!DNL Creative Cloud] file (interfaccia web): Questo è il punto in cui gli utenti specifici dell’app Creative Cloud utilizzano [!DNL Assets] cartella condivisa, potrebbe accettare l&#39;invito e visualizzare la cartella nell&#39;archivio dell&#39;account Creative Cloud.
* **Creative Cloud app desktop**: (Facoltativo) Consente l&#39;accesso diretto a cartelle/file condivisi dal desktop dell&#39;utente creativo tramite sincronizzazione con [!DNL Creative Cloud] Archiviazione delle risorse.

## Caratteristiche e limitazioni {#characteristics-and-limitations}

* **Propagazione unidirezionale delle modifiche:** Le modifiche ai file vengono propagate in una sola direzione, dal sistema ([!DNL Experience Manager] o [!DNL Creative Cloud Assets]), in cui la risorsa è stata originariamente creata (caricata). L’integrazione non fornisce una sincronizzazione bidirezionale completamente automatizzata tra i due sistemi.
* **Controllo delle versioni:**

   * [!DNL Experience Manager] crea solo versioni di una risorsa sugli aggiornamenti se il file ha avuto origine in [!DNL Experience Manager] e viene aggiornato qui.
   * [!DNL Creative Cloud] Risorse proprie [funzione di gestione delle versioni](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) destinato agli aggiornamenti di Work in Progress (in sostanza, memorizza gli aggiornamenti per un massimo di 10 giorni)

* **Limitazioni dello spazio:** Le dimensioni e i volumi dei file scambiati sono limitati dalle specifiche [Creative Cloud quota risorse](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) per gli utenti creativi (dipende dal livello di abbonamento) e da un limite di 5 GB di dimensione massima del file. Lo spazio è inoltre limitato dalla quota di risorse di cui dispone l’organizzazione nel servizio di base Adobe Marketing Cloud Assets.

* **Requisiti di spazio:** Anche i file in cartelle condivise devono essere fisicamente memorizzati in [!DNL Experience Manager] e poi [!DNL Creative Cloud] account, con una copia memorizzata nella cache [!DNL Marketing Cloud Assets] servizio di base.
* **Rete e larghezza di banda:** I file in cartelle condivise e tutti gli aggiornamenti devono essere trasportati attraverso la rete tra i sistemi. Assicurati che siano condivisi solo i file e gli aggiornamenti pertinenti.
* **Tipo di cartella**: Condivisione di un [!DNL Assets] cartella del tipo `sling:OrderedFolder`, non è supportato nel contesto della condivisione in [!DNL Adobe Marketing Cloud]. Per condividere una cartella, quando la si crea in [!DNL Assets], non selezionare [!UICONTROL Ordinato] opzione .

## Best practice {#best-practices}

Best practice per sfruttare [!DNL Experience Manager] a [!DNL Creative Cloud] la condivisione delle cartelle include:

* **Considerazioni sul volume:** [!DNL Experience Manager] e [!DNL Creative Cloud] La condivisione di cartelle deve essere utilizzata per condividere un numero inferiore di file, ad esempio relativi a una campagna o un’attività specifica. Per condividere set di risorse più grandi, come tutte le risorse approvate nell’organizzazione, utilizza altri metodi di distribuzione (ad esempio, [!DNL Assets Brand Portal]) o [!DNL Experience Manager] app desktop.
* **Evita di condividere gerarchie profonde:** La condivisione funziona in modo ricorsivo e non consente una condivisione selettiva. In genere, per la condivisione devono essere prese in considerazione solo le cartelle prive di sottocartelle o con una gerarchia molto superficiale, come 1 livello di sottocartella.
* **Cartelle separate per la condivisione unidirezionale:** È necessario utilizzare cartelle separate per la condivisione delle risorse finali da [!DNL Assets] a [!DNL Creative Cloud] e per la condivisione di risorse pronte per la creazione da [!DNL Creative Cloud] file in [!DNL Assets]. Insieme a una buona convenzione di denominazione per queste cartelle, crea un ambiente di lavoro più semplice per [!DNL Assets] e [!DNL Creative Cloud] utenti uguali.
* **Evitare WIP nella cartella condivisa:** La cartella condivisa non deve essere utilizzata per Work in Progress. Utilizzare una cartella separata in Creative Cloud Files per eseguire il lavoro che richiede frequenti modifiche al file.
* **Avvia nuovo lavoro all&#39;esterno della cartella condivisa:** Le nuove progettazioni (file creativi) devono essere avviate nella cartella WIP separata in File di Creative Cloud e quando sono pronte per essere condivise con [!DNL Assets] devono essere spostati o salvati nella cartella condivisa.
* **Semplificare la struttura di condivisione:** Per una configurazione operativa più gestibile, pensate a semplificare la struttura di condivisione. Invece di condividere con tutti gli utenti creativi, [!DNL Assets] le cartelle devono essere condivise solo con i rappresentanti del team, come un direttore creativo o un responsabile del team. Il manager dal lato creativo riceverà le risorse finali, deciderà sulle assegnazioni di lavoro e quindi lascerà che i designer lavorino nei propri account di Creative Cloud sulle risorse WIP. È possibile utilizzare le funzioni di collaborazione Creative Cloud per coordinare il lavoro e infine selezionare e mettere a disposizione risorse pronte per la condivisione [!DNL Assets] nella loro cartella condivisa pronta per la creazione.

Il diagramma seguente illustra una configurazione di esempio per la creazione di nuove progettazioni basate su risorse finali esistenti da [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
