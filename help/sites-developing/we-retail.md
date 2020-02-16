---
title: Implementazione di riferimento We.Retail
seo-title: Implementazione di riferimento We.Retail
description: We.Retail è un'anteprima tecnologica di un'implementazione di riferimento che illustra il modo consigliato per configurare una presenza online con AEM
seo-description: We.Retail è un'anteprima tecnologica di un'implementazione di riferimento che illustra il modo consigliato per configurare una presenza online con AEM
uuid: d8833192-b592-4812-bf9b-bd882e8ee7f0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: f50150af-deff-4c29-bfe0-1cfc67b29d51
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c

---


# Implementazione di riferimento We.Retail{#we-retail-reference-implementation}

## Introduzione {#introduction}

We.Retail è un&#39;implementazione di riferimento e un contenuto di esempio che illustra il modo consigliato per configurare una presenza online con Adobe Experience Manager.

We.Retail si avvale delle tecnologie AEM più recenti, come HTL, layout reattivi, modelli modificabili, componenti core e molto altro ancora.

Anche se illustra una vendita al dettaglio verticale, la modalità di configurazione del sito può essere applicata a qualsiasi verticale, e solo il catalogo prodotti e le funzioni del carrello sono specifiche per la vendita al dettaglio.

## Funzioni {#features}

Come implementazione di riferimento standard di AEM, We.Retail presenta alcune delle funzioni più potenti di AEM.

| **Funzione** | **Descrizione** | **Interessato?** |
|---|---|---|
| [Struttura del sito globale](/help/sites-administering/tc-bp.md) | We.Retail include master di lingua che vengono copiati in tempo reale in siti specifici per paese. | [Prova!](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [Layout reattivo](/help/sites-authoring/responsive-layout.md) | Tutte le pagine dispongono di un layout reattivo per adattarsi dinamicamente allo schermo e alle dimensioni del dispositivo. | [Prova!](/help/sites-developing/we-retail-responsive-layout.md) |
| [Modelli modificabili](/help/sites-developing/page-templates-editable.md) | Tutte le pagine sono basate su modelli modificabili, che consentono agli utenti non sviluppatori di adattare e personalizzare i modelli. | [Prova!](/help/sites-developing/we-retail-editable-templates.md) |
| [HTML Template Language](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) | Tutti i componenti sono basati su HTL |  |
| [Funzionalità eCommerce](/help/sites-developing/ecommerce.md) | Caratteristiche di un catalogo di prodotti |  |
| [Siti community](/help/communities/overview.md) | Consentire ai visitatori di partecipare alle discussioni della community, leggere blog e molto altro |  |
| [Componenti core](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) | Tutti i componenti sono basati sui nuovi componenti core e sono più utilizzabili e configurabili dall&#39;utente | [Prova!](/help/sites-developing/we-retail-core-components.md) |
| [Frammenti di contenuto](/help/assets/content-fragments.md) | La sezione Esperienze We.Retail mostra la potenza del riutilizzo dei contenuti tramite frammenti di contenuto. | [Provatele!](/help/sites-developing/we-retail-content-fragments.md) |
| [Frammenti esperienza](/help/sites-authoring/experience-fragments.md) | Un Frammento esperienza è un gruppo di uno o più componenti, che include contenuto e layout, a cui è possibile fare riferimento tra le pagine. | [Provatele!](/help/sites-developing/we-retail-experience-fragments.md) |

## Introduzione {#getting-started}

We.Retail viene distribuito come contenuto di esempio di AEM. Per utilizzarlo, [avviate AEM come di consueto](/help/sites-deploying/deploy.md#getting-started), accertatevi che il contenuto di esempio non sia disabilitato.

>[!CAUTION]
>
>We.Retail non deve essere installato nelle istanze di produzione. Le istanze di produzione devono essere avviate in `nosamplecontent` modalità [di esecuzione](/help/sites-deploying/configure-runmodes.md).

>[!CAUTION]
>
>We.Retail si basa sulla più recente tecnologia AEM e pertanto non supporta l’authoring [dell’interfaccia utente](/help/sites-classic-ui-authoring/home.md)classica.

### Ultima versione {#latest-version}

Anche se We.Retail è distribuito con la release di AEM, gli aggiornamenti al contenuto e alle sue funzioni possono essere effettuati dopo il rilascio. È quindi possibile [scaricare l’ultima versione da GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) , [caricare](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) e [installare](/help/sites-administering/package-manager.md#installing-packages) l’ultima versione come pacchetto nell’istanza di AEM.

### Primi passi {#first-steps}

1. Una volta avviato AEM (e/o installato We.Retail), il sito **We.Retail** è disponibile nella console [](/help/sites-authoring/basic-handling.md#global-navigation)Siti.
1. Ad esempio, è possibile aprire la pagina seguente e visualizzarla come illustrato nell’ [appendice](#appendix) seguente:

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.Retail e Geometrixx {#we-retail-geometrixx}

Geometrixx e le sue numerose incarnazioni erano contenuti campione nelle versioni precedenti di AEM. Dalla versione 6.3, We.Retail è il contenuto di esempio fornito con AEM e funge da nuova implementazione standard di riferimento.

We.Retail è tecnicamente più robusto e sfrutta la più recente tecnologia AEM per essere più flessibile e scalabile, dimostrando al contempo le nuove caratteristiche del prodotto.

### Confronto delle funzioni {#feature-comparison}

La tabella seguente fornisce una panoramica delle principali funzioni disponibili in We.Retail rispetto a Geometrixx.

* **Disponibile** significa che alcuni esempi della funzione sono disponibili nel contenuto di esempio.
* **Non disponibile** significa che alcuni esempi della funzione non sono disponibili nel contenuto di esempio, ma non significa che la funzione non sia disponibile.

| **Funzione** | **We.Retail** | **Geometrixx** |
|---|---|---|
| Struttura del sito globale | I master delle lingue vengono copiati in tempo reale nei siti specifici per ciascun paese | Non disponibile |
| Frammenti di contenuto | Disponibile | Non disponibile |
| Frammenti esperienza | Disponibile | Non disponibile |
| Layout reattivo | Per tutte le pagine | Solo Geometrixx Media |
| Modelli modificabili | Per tutte le pagine | Non disponibile |
| HTL | Tutti i componenti | Limitato |
| Impostazione destinazione | Per tutte le pagine | Solo Geometrixx Outdoors |
| Screens | Disponibile | Non disponibile |
| Mobile | Non disponibile | Disponibile |
| Manoscritti | Non disponibile | Disponibile |
| Carosello, download, componenti grafico | Non disponibile | Disponibile |
| Controllo colonna | Sostituito da Contenitore di layout | Disponibile |
| Forms | Non disponibile | Disponibile |
| Campaign | Nessun esempio di e-mail | Disponibile |

>[!NOTE]
>
>L&#39;elenco è completo, ma non esaustivo.

## Contribute {#contribute}

We.Retail è stato rilasciato come progetto open-source e l&#39;ultima versione del codice sorgente può essere scaricata da GitHub.

CODICE SU GITHUB

Puoi trovare il codice di questa pagina su GitHub

* [Apri progetto di vendita al dettaglio su GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* Scarica il progetto come [file ZIP](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/archive/master.zip)

L&#39;ultima versione può essere [scaricata direttamente](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/latest) come pacchetto installabile.

In caso di problemi, archiviate i problemi relativi a [GitHub](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues).

Sentitevi liberi di fork o di contribuire con le richieste [](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls)pull.

## Anteprima {#preview}

Anteprima della pagina di benvenuto We.Retail:

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)

