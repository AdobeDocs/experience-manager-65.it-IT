---
title: 'Condivisione delle cartelle con le procedure ottimali [!DNL Adobe Creative Cloud] '
description: Configurare [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] per scambiare cartelle con utenti Adobe Creative Cloud (CC).
contentOwner: AG
translation-type: tm+mt
source-git-commit: 18e62f8fb46de20e1668b2dcdcedf68fe4622b50
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] per la condivisione  [!DNL Adobe Creative Cloud] delle cartelle  {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>La funzione [!DNL Experience Manager] per [!DNL Creative Cloud] Condivisione cartelle è obsoleta.  Adobe consiglia vivamente di utilizzare funzionalità più recenti come [ collegamento risorsa Adobe](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) o [ Experience Manager app desktop di ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). Ulteriori informazioni sono disponibili in [ procedure ottimali per l&#39;integrazione di Experienci Manager e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] può essere configurato per consentire  [!DNL Assets] agli utenti di condividere cartelle con gli utenti di  [!DNL Adobe Creative Cloud] app, in modo che siano disponibili come cartelle condivise nel servizio  [!DNL Adobe Creative Cloud] Risorse. La funzione può essere utilizzata per scambiare file tra team creativi e utenti [!DNL Assets], soprattutto quando gli utenti creativi non hanno accesso alla [!DNL Assets] distribuzione (non sono sulla rete aziendale).

Questo tipo di integrazione può essere utilizzato nei seguenti casi di utilizzo, soprattutto quando si lavora con utenti che non hanno accesso diretto a [!DNL Assets]:

* [!DNL Assets] gli utenti condividono una serie di risorse digitali specifiche con gli utenti di  [!DNL Adobe Creative Cloud] file (ad esempio, una breve e una serie di risorse approvate per lavori di progettazione per una nuova attività di marketing).
* [!DNL Assets] gli utenti ricevono nuovi file creati dagli utenti  [!DNL Adobe Creative Cloud] dell&#39;app.

>[!NOTE]
>
>Prima di leggere questo documento, è possibile esaminare le procedure ottimali per l&#39;integrazione di Experienci Manager e Creative Cloud ](/help/assets/aem-cc-integration-best-practices.md) nel complesso per una panoramica dell&#39;integrazione.[

## Panoramica {#overview}

[!DNL Experience Manager] per condividere le  [!DNL Creative Cloud] cartelle, la condivisione si basa sulla condivisione lato server di cartelle e file tra  [!DNL Assets] e  [!DNL Creative Cloud] account. I creativi professionisti, che utilizzano l&#39;app desktop [!DNL Creative Cloud] sui propri desktop, possono inoltre rendere disponibili le cartelle condivise direttamente sui propri dischi utilizzando la tecnologia [!DNL Adobe CreativeSync].

Il diagramma seguente fornisce una panoramica dell&#39;integrazione.

![chlimage_1-179](assets/chlimage_1-406.png)

L&#39;integrazione include i seguenti elementi:

* **[!DNL Experience Manager Assets]** implementato nella rete aziendale (servizi gestiti o in sede): La condivisione delle cartelle viene avviata qui.
* **[!DNL Adobe Marketing Cloud Assets]servizio** di base: funge da intermediario tra i servizi  [!DNL Experience Manager] di  [!DNL Creative Cloud] storage e di storage. L&#39;amministratore di un&#39;organizzazione che utilizza l&#39;integrazione deve stabilire una relazione di trust tra l&#39;organizzazione del Marketing Cloud e la distribuzione [!DNL Assets]. Inoltre [definiscono un elenco di collaboratori di Creative Cloud approvati](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html), che gli utenti [!DNL Assets] possono condividere anche le cartelle per una maggiore sicurezza.

* **[!DNL Creative Cloud]Servizi**  Web risorse (interfaccia utente Web archivio e  [!DNL Creative Cloud] file): Questo è il punto in cui gli utenti dell&#39;app di Creative Cloud specifici, con cui è stata condivisa una  [!DNL Assets] cartella, potrebbero accettare l&#39;invito e visualizzare la cartella nell&#39;archivio dell&#39;account di Creative Cloud.
* **Creative Cloud app** desktop: (Facoltativo) Consente l’accesso diretto alla cartella o ai file condivisi dal desktop dell’utente creativo tramite sincronizzazione con l’archiviazione  [!DNL Creative Cloud] Risorse.

## Caratteristiche e limitazioni {#characteristics-and-limitations}

* **Propagazione unidirezionale delle modifiche: le modifiche ai** file vengono propagate in una sola direzione, dal sistema ([!DNL Experience Manager] o  [!DNL Creative Cloud Assets]), dove la risorsa è stata creata originariamente (caricata). L&#39;integrazione non fornisce una sincronizzazione bidirezionale completamente automatizzata tra i due sistemi.
* **Gestione versioni:**

   * [!DNL Experience Manager] crea versioni di una risorsa sugli aggiornamenti solo se il file è stato creato  [!DNL Experience Manager] e vi viene aggiornato.
   * [!DNL Creative Cloud] Assets offre una propria  [funzione ](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) di controllo delle versioni, con targeting per gli aggiornamenti di Work in Progress (praticamente, memorizza gli aggiornamenti fino a 10 giorni)

* **Limiti di spazio:** Dimensioni e volumi di file scambiati sono limitati dalle  [Creative Cloud specifiche Risorse ](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) per gli utenti creativi (dipende dal livello di iscrizione) e un limite di 5 GB di dimensione massima per i file. Lo spazio è inoltre limitato dalla quota di risorse di cui dispone l’organizzazione nel servizio di base di Adobe Marketing Cloud Assets.

* **Requisiti di spazio:** Anche i file nelle cartelle condivise devono essere memorizzati fisicamente in  [!DNL Experience Manager] e poi nell&#39; [!DNL Creative Cloud] account, con una copia memorizzata nella cache nel servizio  [!DNL Marketing Cloud Assets] di base.
* **Rete e larghezza di banda:** I file nelle cartelle condivise e tutti gli aggiornamenti devono essere trasportati attraverso la rete tra i sistemi. Devi accertarti che siano condivisi solo i file e gli aggiornamenti rilevanti.
* **Tipo** cartella: La condivisione di una  [!DNL Assets] cartella del tipo  `sling:OrderedFolder`, non è supportata nel contesto della condivisione in  [!DNL Adobe Marketing Cloud]. Se desiderate condividere una cartella, quando la create in [!DNL Assets], non selezionate l&#39;opzione [!UICONTROL Ordinato].

## Best practice {#best-practices}

Le best practice per sfruttare la condivisione delle cartelle da [!DNL Experience Manager] a [!DNL Creative Cloud] includono:

* **Considerazioni sul volume:** [!DNL Experience Manager] e condivisione delle  [!DNL Creative Cloud] cartelle devono essere utilizzate per condividere un numero minore di file, ad esempio, relativi a una campagna o attività specifica. Per condividere set di risorse più grandi, come tutte le risorse approvate nell&#39;organizzazione, utilizzate altri metodi di distribuzione (ad esempio, [!DNL Assets Brand Portal]) o l&#39;app desktop [!DNL Experience Manager].
* **Evitate la condivisione di gerarchie profonde:** la condivisione funziona in modo ricorsivo e non consente la condivisione selettiva. In genere, per la condivisione devono essere considerate solo le cartelle prive di sottocartelle o con una gerarchia molto bassa, come 1 livello di sottocartella.
* **Cartelle separate per la condivisione unidirezionale:** Le cartelle separate devono essere utilizzate per condividere le risorse finali da  [!DNL Assets] a  [!DNL Creative Cloud] file e per condividere le risorse pronte per la creazione da  [!DNL Creative Cloud] file a  [!DNL Assets]. Insieme a una buona convenzione di denominazione per queste cartelle, crea un ambiente di lavoro più semplice per gli utenti [!DNL Assets] e [!DNL Creative Cloud].
* **Evitare WIP nella cartella condivisa: la cartella** condivisa non deve essere utilizzata per Work in Progress. Utilizzare una cartella separata in Creative Cloud File per eseguire il lavoro che richiede frequenti modifiche al file.
* **Avvia nuovo lavoro all&#39;esterno della cartella condivisa:** È necessario avviare nuove progettazioni (file creativi) nella cartella WIP separata in File Creative Cloud e, quando sono pronte per essere condivise con  [!DNL Assets] gli utenti, spostarle o salvarle nella cartella condivisa.
* **Semplificare la struttura di condivisione:** Per una configurazione operativa più gestibile, pensate a semplificare la struttura di condivisione. Invece di condividere con tutti gli utenti creativi, le cartelle [!DNL Assets] devono essere condivise solo con i rappresentanti del team, come un direttore creativo o un responsabile del team. Dal lato creativo, il manager riceve le risorse finali, decide sulle assegnazioni di lavoro e quindi lascia che i progettisti lavorino nei propri conti di Creative Cloud sulle risorse WIP. Possono usare le funzioni di collaborazione Creative Cloud per coordinare il lavoro, e infine selezionare e inserire le risorse pronte per essere condivise in [!DNL Assets] nella cartella condivisa pronta per la creazione.

Nel diagramma seguente è illustrata una configurazione di esempio per la creazione di nuove progettazioni basate sulle risorse finali esistenti da [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
