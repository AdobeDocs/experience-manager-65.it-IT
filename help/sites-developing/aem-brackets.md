---
title: Estensione Bracket AEM
seo-title: Estensione Bracket AEM
description: Estensione Bracket AEM
seo-description: 'null'
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 2%

---


# Estensione Brackets AEM{#aem-brackets-extension}

## Panoramica {#overview}

L&#39;estensione AEM Brackets fornisce un flusso di lavoro semplice per la modifica AEM componenti e librerie client e sfrutta la potenza dell&#39;editor di codice [Brackets](https://brackets.io/), che consente di accedere dall&#39;interno dell&#39;editor di codice a file e livelli Photoshop. La facile sincronizzazione fornita dall&#39;estensione (senza Maven o File Vault richiesti) aumenta l&#39;efficienza degli sviluppatori e aiuta gli sviluppatori front-end con limitata conoscenza AEM a partecipare ai progetti. Questa estensione fornisce anche un certo supporto per [HTML Template Language (HTL)](https://docs.adobe.com/content/help/it-IT/experience-manager-htl/using/overview.html), che toglie la complessità di JSP per rendere lo sviluppo dei componenti più facile e sicuro.

![chlimage_1-53](assets/chlimage_1-53a.png)

### Funzioni {#features}

Le caratteristiche principali dell&#39;estensione Brackets AEM sono:

* Sincronizzazione automatizzata dei file modificati nell&#39;istanza di sviluppo AEM.
* Sincronizzazione bidirezionale manuale di file e cartelle.
* Sincronizzazione completa del pacchetto di contenuti del progetto.
* Completamento del codice HTL per espressioni e istruzioni per blocchi `data-sly-*` .

Inoltre, Brackets viene fornito con molte funzioni utili per AEM sviluppatori di font-end:

* Supporto file Photoshop per estrarre informazioni da un file PSD, come livelli, misure, colori, caratteri, testi, ecc.
* Suggerimenti sul codice dal PSD, per riutilizzare facilmente queste informazioni estratte nel codice.
* Supporto preprocessore CSS, come LESS e SCSS.
* E centinaia di estensioni aggiuntive che soddisfano esigenze più specifiche.

## Installazione {#installation}

### Parentesi graffa {#brackets}

L&#39;estensione Brackets AEM supporta la versione 1.0 o successiva di Brackets.

Scarica la versione più recente di Brackets da [brackets.io](https://brackets.io/).

### Estensione {#the-extension}

Per installare l&#39;estensione procedi come segue:

1. Parentesi aperte. Nel menu **File**, selezionare **Extension Manager...**
1. Inserisci **AEM** nella barra di ricerca e cerca **AEM Estensione parentesi**.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. Fare clic su **Installa**.
1. Chiudi la finestra di dialogo e l’Extension Manager al termine dell’installazione.

## Guida introduttiva {#getting-started}

### Progetto Content-Package {#the-content-package-project}

Dopo aver installato l’estensione, puoi iniziare a sviluppare componenti AEM aprendo una cartella di pacchetti di contenuti dal file system con Brackets.

Il progetto deve contenere almeno:

1. una cartella `jcr_root` (ad es. `myproject/jcr_root`)

1. un file `filter.xml` (ad es. `myproject/META-INF/vault/filter.xml`); per ulteriori dettagli sulla struttura del file `filter.xml`, consulta la [Definizione del filtro area di lavoro](https://jackrabbit.apache.org/filevault/filter.html).

Nel menu **File** di Brackets, scegliere **Apri cartella...** e scegliere la cartella `jcr_root` o la cartella di progetto principale.

>[!NOTE]
>
>Se non hai un progetto personalizzato con un pacchetto di contenuti, puoi provare l&#39; [HTL TodoMVC Example](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc). Su GitHub, fai clic su **Scarica ZIP**, estrai i file localmente e, come indicato in precedenza, apri la cartella `jcr_root` in Brackets. Quindi segui i passaggi seguenti per configurare le **Impostazioni progetto** e infine carica l&#39;intero pacchetto nella tua istanza di sviluppo AEM facendo un **Export Content Package** come indicato più in basso nella sezione Full Content-Package Synchronization .
>
>Dopo questi passaggi, dovresti essere in grado di accedere all’ URL `/content/todo.html` nell’istanza di sviluppo AEM e puoi iniziare a apportare modifiche al codice in Brackets e vedere come, dopo un aggiornamento nel browser Web, le modifiche siano state immediatamente sincronizzate con il server AEM.

### Impostazioni progetto {#project-settings}

Per sincronizzare il contenuto con e da un’istanza di sviluppo AEM, devi definire le impostazioni del progetto. Per farlo, vai al menu **AEM** e scegli **Impostazioni progetto...**.

![chlimage_1-55](assets/chlimage_1-55a.png)

Le impostazioni del progetto consentono di definire:

1. L’URL del server (ad esempio `http://localhost:4502`)
1. È possibile tollerare i server privi di un certificato HTTPS valido (mantieni deselezionato, se necessario)
1. Nome utente utilizzato per la sincronizzazione del contenuto (ad esempio `admin`)
1. Password dell’utente (ad esempio `admin`)

## Sincronizzazione del contenuto {#synchronizing-content}

L&#39;estensione Brackets AEM fornisce i seguenti tipi di sincronizzazione del contenuto per file e cartelle consentiti dalle regole di filtro definite in `filter.xml`:

### Sincronizzazione Automatizzata Dei File Modificati {#automated-synchronization-of-changed-files}

Questo sincronizzerà solo le modifiche da Brackets all&#39;istanza AEM, ma mai viceversa.

### Sincronizzazione bidirezionale manuale {#manual-bidirectional-synchronization}

In Esplora progetti, aprire il menu contestuale facendo clic con il pulsante destro del mouse su un file o una cartella e accedere alle opzioni **Esporta sul server** o **Importa dal server**.

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>Se la voce selezionata è all&#39;esterno della cartella `jcr_root`, le voci di menu contestuali **Esporta nel server** e **Importa dal server** sono disabilitate.

### Sincronizzazione completa del pacchetto di contenuti {#full-content-package-synchronization}

Nel menu **AEM**, le opzioni **Export Content Package** o **Import Content Package** consentono di sincronizzare l&#39;intero progetto con il server.

![chlimage_1-57](assets/chlimage_1-57a.png)

### Stato sincronizzazione {#synchronization-status}

L&#39;estensione Brackets AEM presenta un&#39;icona di notifica nella barra degli strumenti a destra della finestra Brackets, che indica lo stato dell&#39;ultima sincronizzazione:

* verde: tutti i file sono stati sincronizzati correttamente
* blu: è in corso un’operazione di sincronizzazione
* giallo - alcuni dei file non sono stati sincronizzati
* rosso - nessuno dei file è stato sincronizzato

Facendo clic sull’icona di notifica si aprirà la finestra di dialogo Rapporto stato sincronizzazione in cui viene visualizzato l’elenco di tutti gli stati per ogni file sincronizzato.

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>Solo il contenuto contrassegnato come incluso dalle regole di filtro di `filter.xml` verrà sincronizzato, indipendentemente dal metodo di sincronizzazione utilizzato.
>
>Inoltre, i file `.vltignore` sono supportati per escludere il contenuto dalla sincronizzazione con e dall’archivio.

## Modifica del codice HTL {#editing-htl-code}

L’estensione AEM Brackets dispone anche di un certo completamento automatico per facilitare la scrittura di attributi ed espressioni HTL.

### Completamento automatico attributi {#attribute-auto-completion}

1. In un attributo HTML, digita `sly`. L’attributo viene completato automaticamente in `data-sly-`.
1. Seleziona l’attributo HTL nell’elenco a discesa.

### Completamento automatico espressione {#expression-auto-completion}

All&#39;interno di un&#39;espressione `${}`, i nomi delle variabili comuni vengono completati automaticamente.

## Ulteriori informazioni {#more-information}

L’estensione Brackets AEM è un progetto open source ospitato su GitHub dall’organizzazione [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud), con la licenza Apache, versione 2.0:

* Archivio del codice: [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Licenza Apache, versione 2.0: [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

L’editor di codice Brackets è anche un progetto open source ospitato su GitHub dall’organizzazione [Adobe Systems Incorporated](https://github.com/adobe) :

* Archivio del codice: [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

Sentiti libero di contribuire!
