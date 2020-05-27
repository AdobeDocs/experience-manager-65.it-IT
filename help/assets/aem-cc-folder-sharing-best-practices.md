---
title: Best practice per la condivisione di cartelle tra Adobe Experience Manager e Adobe Creative Cloud
description: Configura Adobe Experience Manager per consentire agli utenti di Experience Manager Assets di scambiare cartelle con utenti Adobe Creative Cloud (CC).
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 0%

---


# Condivisione di cartelle da Adobe Experience Manager ad Adobe Creative Cloud {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>La funzione Experience Manager per la condivisione delle cartelle di Creative Cloud è obsoleta. Adobe consiglia vivamente di utilizzare funzionalità più recenti, come [Adobe Asset Link](https://helpx.adobe.com/it/enterprise/using/adobe-asset-link.html) o l’app [desktop](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)Experience Manager. Scopri di più nelle best practice per l&#39;integrazione con [Experience Manager e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

Adobe Experience Manager può essere configurato per consentire agli utenti di Risorse di condividere cartelle con gli utenti delle app Adobe Creative Cloud, in modo che siano disponibili come cartelle condivise nel servizio Risorse Adobe Creative Cloud. La funzione può essere utilizzata per scambiare file tra team creativi e utenti di Risorse, soprattutto quando gli utenti creativi non hanno accesso all’istanza Risorse (non sono sulla rete aziendale).

Questo tipo di integrazione può essere utilizzato nei seguenti casi di utilizzo, soprattutto quando si lavora con utenti che non hanno accesso diretto alle risorse:

* Gli utenti delle risorse condividono una serie di risorse specifiche con gli utenti di Adobe Creative Cloud Files (ad esempio, una serie di risorse creative e approvate per il lavoro di progettazione di una nuova attività di marketing)
* Gli utenti delle risorse ricevono nuovi file creati dagli utenti delle app Adobe Creative Cloud.

>[!NOTE]
>
>Prima di leggere questo documento, puoi consultare le best practice [generali per l’integrazione con](/help/assets/aem-cc-integration-best-practices.md) Experience Manager e Creative Cloud per una panoramica di livello superiore dell’argomento.

## Panoramica {#overview}

Experience Manager per la condivisione di cartelle su Creative Cloud si basa sulla condivisione lato server di cartelle e file tra risorse e account Creative Cloud. I professionisti creativi, che utilizzano l’app desktop Creative Cloud sui propri desktop, possono inoltre rendere le cartelle condivise disponibili direttamente sui propri dischi utilizzando la tecnologia Adobe CreativeSync.

Il diagramma seguente fornisce una panoramica dell&#39;integrazione.

![chlimage_1-179](assets/chlimage_1-406.png)

L&#39;integrazione include i seguenti elementi:

* **Server** Experience Manager Assets implementato nella rete aziendale (servizi gestiti o locali): La condivisione delle cartelle viene avviata qui.
* **Servizio** di base di Adobe Marketing Cloud Assets: Agisce come intermediario tra i servizi di archiviazione Experience Manager e Creative Cloud. L&#39;amministratore della società che utilizza l&#39;integrazione deve stabilire una relazione di trust tra l&#39;organizzazione Marketing Cloud e l&#39;istanza Assets. Inoltre, [definiscono un elenco di collaboratori](https://marketing.adobe.com/resources/help/en_US/mcloud/t_admin_add_cc_user.html)di Creative Cloud approvati, che gli utenti di Assets possono condividere anche cartelle per ulteriore sicurezza.

* **Servizi** Web Creative Cloud Assets (interfaccia utente Web per l&#39;archiviazione e Creative Cloud Files): Questo è il punto in cui gli utenti specifici dell&#39;app Creative Cloud, con cui è stata condivisa una cartella Assets, possono accettare l&#39;invito e visualizzare la cartella nell&#39;archivio del loro account Creative Cloud.
* **App** desktop Creative Cloud: (Facoltativo) Consente l&#39;accesso diretto a cartelle/file condivisi dal desktop dell&#39;utente creativo tramite sincronizzazione con l&#39;archiviazione Creative Cloud Assets.

## Caratteristiche e limitazioni {#characteristics-and-limitations}

* **Propagazione unidirezionale delle modifiche:** Le modifiche ai file vengono propagate in una sola direzione, dal sistema (Experience Manager o Creative Cloud Assets), in cui la risorsa è stata creata originariamente (caricata). L&#39;integrazione non fornisce una sincronizzazione bidirezionale completamente automatizzata tra i due sistemi.
* **Gestione versioni:**

   * Experience Manager crea solo versioni di una risorsa sugli aggiornamenti se il file è stato creato in Experience Manager e vi viene aggiornato.
   * Creative Cloud Assets offre una propria funzione [di controllo delle](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) versioni, con targeting per gli aggiornamenti di Work In Progress (praticamente, memorizza gli aggiornamenti fino a 10 giorni)

* **Limiti di spazio:** Le dimensioni e i volumi di file scambiati sono limitati dalla quota [specifica di Risorse](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) Creative Cloud per gli utenti creativi (dipende dal livello di iscrizione) e da un limite di 5 GB per la dimensione massima dei file. Lo spazio è inoltre limitato dalla quota di risorse di cui dispone l’organizzazione nel servizio di base Risorse di Adobe Marketing Cloud.

* **Requisiti di spazio:** Anche i file nelle cartelle condivise devono essere memorizzati fisicamente in Experience Manager e quindi nell&#39;account Creative Cloud, con una copia memorizzata nella cache nel servizio di base Marketing Cloud Assets.
* **Rete e larghezza di banda:** I file in cartelle condivise e tutti gli aggiornamenti devono essere trasportati attraverso la rete tra i sistemi. Devi accertarti che siano condivisi solo i file e gli aggiornamenti rilevanti.
* **Tipo** cartella: La condivisione di una cartella di risorse di tipo `sling:OrderedFolder`non è supportata nel contesto della condivisione in Adobe Marketing Cloud. Se desiderate condividere una cartella, quando la create in Risorse, non selezionate l’opzione Ordinato.

## Best practices {#best-practices}

Le best practice per sfruttare Experience Manager per la condivisione di cartelle di Creative Cloud includono:

* **Considerazioni sul volume:** La condivisione delle cartelle Experience Manager/Creative Cloud deve essere utilizzata per condividere un numero minore di file, ad esempio relativi a una campagna o un&#39;attività specifica. Per condividere set di risorse più grandi, come tutte le risorse approvate nell’organizzazione, utilizzate altri metodi di distribuzione (ad esempio, Assets Brand Portal) o l’app desktop Experience Manager.

* **Evitate la condivisione di gerarchie profonde:** La condivisione funziona in modo ricorsivo e non consente la condivisione selettiva. In genere, per la condivisione devono essere considerate solo le cartelle prive di sottocartelle o con una gerarchia molto bassa, come 1 livello di sottocartella.
* **Cartelle separate per la condivisione unidirezionale:** Le cartelle devono essere utilizzate separatamente per condividere le risorse finali da Risorse ai file di Creative Cloud e per condividere le risorse pronte per la creazione da file di Creative Cloud a risorse. Insieme a una buona convenzione di denominazione per queste cartelle, crea un ambiente di lavoro facile da capire per Risorse e utenti Creative Cloud.
* **Evitare WIP nella cartella condivisa:** La cartella condivisa non deve essere utilizzata per Work in Progress. Per eseguire il lavoro che richiede frequenti modifiche al file, usate una cartella separata in Creative Cloud Files.
* **Avvia nuovo lavoro all&#39;esterno della cartella condivisa:** Le nuove progettazioni (file creativi) devono essere avviate nella cartella WIP separata in Creative Cloud Files e, quando sono pronte per essere condivise con gli utenti di Assets, devono essere spostate o salvate nella cartella condivisa.
* **Semplificazione della struttura di condivisione:** Per una configurazione operativa più gestibile, pensate a semplificare la struttura di condivisione. Invece di condividere con tutti gli utenti creativi, le cartelle Risorse devono essere condivise solo con i rappresentanti del team, come un direttore creativo o un manager del team. Dal lato creativo, il manager riceve le risorse finali, decide sulle assegnazioni di lavoro e lascia che i progettisti lavorino nei propri account Creative Cloud sulle risorse WIP. Possono utilizzare le funzioni di collaborazione di Creative Cloud per coordinare il lavoro, e infine selezionare e inserire le risorse pronte per la condivisione nelle proprie cartelle condivise pronte per la creazione.

Nel diagramma seguente è illustrata una configurazione di esempio per la creazione di nuove progettazioni basate sulle risorse finali esistenti da Assets.

![chlimage_1-180](assets/chlimage_1-407.png)
