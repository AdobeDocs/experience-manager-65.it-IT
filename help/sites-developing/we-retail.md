---
title: Implementazione di riferimento di We.Retail
seo-title: We.Retail Reference Implementation
description: We.Retail è un'anteprima tecnologica di un'implementazione di riferimento che illustra il modo consigliato per configurare una presenza online con AEM
seo-description: We.Retail is a technology preview of a reference implementation that illustrates the recommended way of setting up an online presence with AEM
uuid: d8833192-b592-4812-bf9b-bd882e8ee7f0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: f50150af-deff-4c29-bfe0-1cfc67b29d51
exl-id: 504c61c7-dcd3-412c-9239-d24a2b78e4b9
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 11%

---

# Implementazione di riferimento di We.Retail{#we-retail-reference-implementation}

## Introduzione {#introduction}

We.Retail è un&#39;implementazione di riferimento e un contenuto di esempio che illustra il modo consigliato per impostare una presenza online con Adobe Experience Manager.

We.Retail si avvale delle tecnologie AEM più recenti, come HTL, layout reattivi, modelli modificabili, componenti core e molto altro ancora.

Mentre illustra un settore verticale, il modo in cui il sito viene configurato può essere applicato a qualsiasi verticale, e solo il catalogo dei prodotti e le caratteristiche del carrello sono specifiche per il settore retail.

## Funzioni {#features}

Come implementazione di riferimento standard AEM, We.Retail mostra alcune delle funzionalità più potenti di AEM.

| **Funzione obsoleta** | **Descrizione** | **Interessato?** |
|---|---|---|
| [Struttura del sito globale](/help/sites-administering/tc-bp.md) | We.Retail include schemi di lingua che vengono copiati in tempo reale in siti specifici per ciascun paese. | [Provatela!](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [Layout reattivo](/help/sites-authoring/responsive-layout.md) | Tutte le pagine dispongono di layout reattivo per adattarsi dinamicamente alle dimensioni dello schermo e del dispositivo. | [Provatela!](/help/sites-developing/we-retail-responsive-layout.md) |
| [Modelli modificabili](/help/sites-developing/page-templates-editable.md) | Tutte le pagine sono basate su modelli modificabili, che consentono agli sviluppatori di adattare e personalizzare i modelli. | [Provatela!](/help/sites-developing/we-retail-editable-templates.md) |
| [HTML Template Language ](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) | Tutti i componenti sono basati su HTL |  |
| [Funzionalità di eCommerce](/help/commerce/cif-classic/developing/ecommerce.md) | Caratteristiche di un catalogo di prodotti |  |
| [Siti community](/help/communities/overview.md) | Consentire ai visitatori di partecipare a discussioni della community, leggere blog e molto altro |  |
| [Componenti di base](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) | Tutti i componenti si basano sui nuovi componenti core e sono più utilizzabili e configurabili dall’utente | [Provatela!](/help/sites-developing/we-retail-core-components.md) |
| [Frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) | La sezione Esperienze We.Retail mostra la potenza del riutilizzo dei contenuti tramite frammenti di contenuto. | [Provatele!](/help/sites-developing/we-retail-content-fragments.md) |
| [Frammenti esperienza](/help/sites-authoring/experience-fragments.md) | Un Frammento esperienza è un gruppo di uno o più componenti, che include contenuto e layout, a cui è possibile fare riferimento tra le pagine. | [Provatele!](/help/sites-developing/we-retail-experience-fragments.md) |

## Guida introduttiva {#getting-started}

We.Retail viene fornito AEM contenuto di esempio. Per utilizzare, semplicemente [inizia AEM come si farebbe normalmente](/help/sites-deploying/deploy.md#getting-started), assicurandosi che il contenuto di esempio non sia disabilitato.

>[!CAUTION]
>
>We.Retail non deve essere installato nelle istanze di produzione. Le istanze di produzione devono essere avviate in `nosamplecontent` [modalità runmode](/help/sites-deploying/configure-runmodes.md).

>[!CAUTION]
>
>We.Retail si basa sulla tecnologia AEM più recente e pertanto non supporta [Authoring con interfaccia classica](/help/sites-classic-ui-authoring/home.md).

### Ultima versione {#latest-version}

Anche se We.Retail è distribuito con la versione AEM, gli aggiornamenti al contenuto e alle relative funzioni possono essere effettuati dopo la versione. Pertanto è possibile [scarica l’ultima versione da GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) e poi [caricare](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) e [installare](/help/sites-administering/package-manager.md#installing-packages) come pacchetto sulla tua istanza AEM.

### Primi passi {#first-steps}

1. Una volta avviato AEM (e/o installato We.Retail), il sito **We.Retail** è disponibile in [console siti](/help/sites-authoring/basic-handling.md#global-navigation).
1. Ad esempio, la pagina seguente può essere aperta e deve essere visualizzata come nella [appendice](#appendix) di seguito:

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail e Geometrixx {#we-retail-geometrixx}

Geometrixx e le sue numerose incarnazioni fungevano da contenuto di esempio nelle versioni precedenti di AEM. Dalla versione 6.3, We.Retail è il contenuto di esempio fornito con AEM e funge da nuova implementazione di riferimento standard.

We.Retail è tecnicamente più robusto e sfrutta la tecnologia AEM più recente per essere più flessibile e scalabile, dimostrando al contempo le nuove caratteristiche del prodotto.

### Confronto delle funzioni {#feature-comparison}

La tabella seguente offre una panoramica delle principali funzioni disponibili in We.Retail rispetto a Geometrixx.

* **Disponibile** significa che gli esempi della funzione si trovano nel contenuto di esempio.
* **Non disponibile** significa che gli esempi della funzione non sono disponibili nel contenuto di esempio, ma non significa che la funzione stessa non lo è.

| **Funzione obsoleta** | **We.Retail** | **Geometrixx** |
|---|---|---|
| Struttura del sito globale | I master lingua vengono copiati in tempo reale nei siti specifici del paese | Non disponibile |
| Frammenti di contenuto | Disponibile | Non disponibile |
| Frammenti di esperienza | Disponibile | Non disponibile |
| Layout reattivo | Per tutte le pagine | Solo Geometrixx Media |
| Modelli modificabili | Per tutte le pagine | Non disponibile |
| HTL | Tutti i componenti | Limitato |
| Impostazione destinazione | Per tutte le pagine | Solo Geometrixx Outdoors |
| Screens | Disponibile | Non disponibile |
| Mobile | Non disponibile | Disponibile |
| Manoscritti | Non disponibile | Disponibile |
| Carosello, download, componenti grafico | Non disponibile | Disponibile |
| Controllo colonna | Sostituito dal contenitore di layout | Disponibile |
| Forms | Non disponibile | Disponibile |
| Campaign | Nessun esempio di e-mail | Disponibile |

>[!NOTE]
>
>Questo elenco si prefigge di essere completo, ma non deve essere considerato esaustivo.

## Collaborare {#contribute}

We.Retail è stato rilasciato come progetto open-source e l’ultima versione del codice sorgente può essere scaricata da GitHub.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto aem-sample-we-retail su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* Scarica il progetto come [un file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/archive/master.zip)

L’ultima versione può essere [scaricato direttamente](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/latest) come pacchetto installabile.

Se riscontri dei problemi, ti preghiamo di inviare un file [Problemi relativi a GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues).

Sentiti libero di forchire o di contribuire con [richieste pull](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls).

## Anteprima {#preview}

Anteprima della pagina di benvenuto di We.Retail:

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
