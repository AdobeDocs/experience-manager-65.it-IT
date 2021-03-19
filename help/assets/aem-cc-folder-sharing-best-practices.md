---
title: Best practice per la condivisione di cartelle su [!DNL Adobe Creative Cloud] best practice
description: Configura [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] per scambiare cartelle con utenti Adobe Creative Cloud (CC).
contentOwner: AG
role: Business Practices, amministratore
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] alla condivisione  [!DNL Adobe Creative Cloud] cartelle  {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>La funzione di condivisione cartelle da [!DNL Experience Manager] a [!DNL Creative Cloud] è obsoleta. Adobe consiglia vivamente di utilizzare funzionalità più recenti come [Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) o [app desktop Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). Ulteriori informazioni sono disponibili in [Best practice per l&#39;integrazione di Experienci Manager e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] può essere configurato per consentire agli utenti di  [!DNL Assets] condividere cartelle con gli utenti di  [!DNL Adobe Creative Cloud] app, in modo che siano disponibili come cartelle condivise nel servizio  [!DNL Adobe Creative Cloud] risorse. La funzione può essere utilizzata per scambiare file tra i team creativi e gli utenti [!DNL Assets], specialmente quando gli utenti creativi non hanno accesso alla distribuzione [!DNL Assets] (non sono sulla rete aziendale).

Questo tipo di integrazione può essere utilizzato nei seguenti casi d’uso, soprattutto quando si lavora con utenti che non hanno accesso diretto a [!DNL Assets]:

* [!DNL Assets] gli utenti condividono un set di risorse digitali specifiche con gli utenti di  [!DNL Adobe Creative Cloud] file (ad esempio, un breve riepilogo creativo e un set di risorse approvate per i lavori di progettazione per una nuova attività di marketing).
* [!DNL Assets] Gli utenti ricevono i nuovi file creati dagli utenti  [!DNL Adobe Creative Cloud] dell’app.

>[!NOTE]
>
>Prima di leggere questo documento, puoi consultare le [best practice generali sull&#39;integrazione di Experienci Manager e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) per una panoramica dell&#39;integrazione.

## Panoramica {#overview}

[!DNL Experience Manager] per la condivisione delle  [!DNL Creative Cloud] cartelle si basa sulla condivisione lato server di cartelle e file tra  [!DNL Assets] e  [!DNL Creative Cloud] account. I creativi professionisti, che utilizzano l&#39;app desktop [!DNL Creative Cloud] sul proprio desktop, possono inoltre rendere le cartelle condivise disponibili direttamente sui propri dischi utilizzando la tecnologia [!DNL Adobe CreativeSync].

Il diagramma seguente fornisce una panoramica dell’integrazione.

![chlimage_1-179](assets/chlimage_1-406.png)

L’integrazione include i seguenti elementi:

* **[!DNL Experience Manager Assets]** implementato nella rete aziendale (servizi gestiti o on-premise): La condivisione delle cartelle viene avviata qui.
* **[!DNL Adobe Marketing Cloud Assets]servizio** principale: Agisce come intermediario tra i servizi  [!DNL Experience Manager] di  [!DNL Creative Cloud] archiviazione e di archiviazione. Un amministratore di un&#39;organizzazione che utilizza l&#39;integrazione deve stabilire una relazione di trust tra l&#39;organizzazione del Marketing Cloud e la distribuzione [!DNL Assets]. Inoltre [definiscono un elenco di collaboratori di Creative Cloud approvati](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html), che gli utenti [!DNL Assets] possono condividere anche le cartelle per ulteriore sicurezza.

* **[!DNL Creative Cloud]Servizi Web Assets**  (interfaccia web per archiviazione e  [!DNL Creative Cloud] file): In questo caso, gli utenti specifici dell’app Creative Cloud con cui è stata condivisa una  [!DNL Assets] cartella possono accettare l’invito e visualizzare la cartella nell’archivio dell’account Creative Cloud.
* **Creative Cloud app** desktop: (Facoltativo) Consente l’accesso diretto a cartelle/file condivisi dal desktop dell’utente creativo tramite sincronizzazione con l’archiviazione  [!DNL Creative Cloud] Assets.

## Caratteristiche e limitazioni {#characteristics-and-limitations}

* **Propagazione unidirezionale delle modifiche:** le modifiche ai file vengono propagate in una sola direzione, dal sistema ([!DNL Experience Manager] o  [!DNL Creative Cloud Assets]), in cui la risorsa è stata originariamente creata (caricata). L’integrazione non fornisce una sincronizzazione bidirezionale completamente automatizzata tra i due sistemi.
* **Gestione versioni:**

   * [!DNL Experience Manager] crea le versioni di una risorsa sugli aggiornamenti solo se il file è stato creato in  [!DNL Experience Manager] e vi è stato aggiornato.
   * [!DNL Creative Cloud] Assets fornisce la propria  [funzione di ](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) controllo delle versioni, destinata agli aggiornamenti di Work In Progress (in pratica, archivia gli aggiornamenti per un massimo di 10 giorni)

* **Limitazioni dello spazio:** le dimensioni e i volumi dei file scambiati sono limitati dalla  [Creative Cloud specifica ](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) delle risorse per gli utenti creativi (dipende dal livello di abbonamento) e da un limite di 5 GB di dimensione massima del file. Lo spazio è inoltre limitato dalla quota di risorse di cui dispone l’organizzazione nel servizio di base Adobe Marketing Cloud Assets.

* **Requisiti di spazio:** Anche i file nelle cartelle condivise devono essere fisicamente memorizzati in  [!DNL Experience Manager] e poi nell&#39; [!DNL Creative Cloud] account, con una copia nella cache nel servizio  [!DNL Marketing Cloud Assets] core.
* **Rete e larghezza di banda:** i file in cartelle condivise e tutti gli aggiornamenti devono essere trasportati attraverso la rete tra i sistemi. Assicurati che siano condivisi solo i file e gli aggiornamenti pertinenti.
* **Tipo** cartella: La condivisione di una  [!DNL Assets] cartella del tipo  `sling:OrderedFolder`, non è supportata nel contesto della condivisione in  [!DNL Adobe Marketing Cloud]. Se desideri condividere una cartella, quando la crei in [!DNL Assets], non selezionare l&#39;opzione [!UICONTROL Ordinato].

## Best practice {#best-practices}

Le best practice per sfruttare la condivisione di cartelle da [!DNL Experience Manager] a [!DNL Creative Cloud] includono:

* **Considerazioni sul volume:** [!DNL Experience Manager] e  [!DNL Creative Cloud] Condivisione cartelle devono essere utilizzati per condividere un numero minore di file, ad esempio, relativi a una campagna o a un’attività specifica. Per condividere set di risorse più grandi, come tutte le risorse approvate nell’organizzazione, utilizza altri metodi di distribuzione (ad esempio, [!DNL Assets Brand Portal]) o [!DNL Experience Manager] app desktop.
* **Evita la condivisione di gerarchie profonde:** la condivisione funziona in modo ricorsivo e non consente la condivisione selettiva. In genere, per la condivisione è consigliabile considerare solo le cartelle prive di sottocartelle o con una gerarchia molto superficiale, ad esempio 1 livello di sottocartella.
* **Cartelle separate per la condivisione unidirezionale:** è necessario utilizzare cartelle separate per la condivisione delle risorse finali da  [!DNL Assets] a  [!DNL Creative Cloud] file e per la condivisione di risorse pronte per la creazione da  [!DNL Creative Cloud] file a  [!DNL Assets]. Insieme a una buona convenzione di denominazione per queste cartelle, crea un ambiente di lavoro facile da comprendere per gli utenti [!DNL Assets] e [!DNL Creative Cloud] allo stesso modo.
* **Evitare WIP nella cartella condivisa:** La cartella condivisa non deve essere utilizzata per Work in Progress. Utilizzare una cartella separata in Creative Cloud Files per eseguire un lavoro che richiede frequenti modifiche al file.
* **Avvia nuovo lavoro all&#39;esterno della cartella condivisa:** le nuove progettazioni (file creativi) devono essere avviate nella cartella WIP separata in File di Creative Cloud e, quando sono pronte per essere condivise con  [!DNL Assets] gli utenti, devono essere spostate o salvate nella cartella condivisa.
* **Semplificare la struttura di condivisione:** per una configurazione operativa più gestibile, pensa a semplificare la struttura di condivisione. Invece di condividere con tutti gli utenti creativi, le cartelle [!DNL Assets] devono essere condivise solo con i rappresentanti del team, come un direttore creativo o un responsabile del team. Il manager dal lato creativo riceverà le risorse finali, deciderà sulle assegnazioni di lavoro e quindi lascerà che i designer lavorino nei propri account di Creative Cloud sulle risorse WIP. È possibile utilizzare le funzioni di collaborazione Creative Cloud per coordinare il lavoro e infine selezionare e inserire le risorse pronte per la condivisione nella cartella condivisa creativa.[!DNL Assets]

Il diagramma seguente illustra una configurazione di esempio per la creazione di nuove progettazioni basate sulle risorse finali esistenti da [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
