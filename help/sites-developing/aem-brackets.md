---
title: Estensione AEM parentesi
seo-title: Estensione AEM parentesi
description: 'null'
seo-description: 'null'
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 2%

---


# Estensione AEM parentesi graffe{#aem-brackets-extension}

## Panoramica {#overview}

L&#39;estensione AEM Brackets offre un flusso di lavoro fluido per la modifica AEM componenti e librerie client e sfrutta la potenza dell&#39;editor di codici [Brackets](https://brackets.io/), che permette di accedere ai file e ai livelli Photoshop dall&#39;editor di codice. La semplice sincronizzazione fornita dall&#39;estensione (non è richiesto Maven o File Vault) aumenta l&#39;efficienza degli sviluppatori e aiuta gli sviluppatori front-end con AEM limitata conoscenza a partecipare ai progetti. Questa estensione fornisce anche il supporto per il [HTML Template Language (HTL)](https://docs.adobe.com/content/help/it-IT/experience-manager-htl/using/overview.html), che elimina la complessità della JSP per rendere lo sviluppo dei componenti più semplice e sicuro.

![chlimage_1-53](assets/chlimage_1-53a.png)

### Funzioni {#features}

Le caratteristiche principali dell&#39;estensione AEM parentesi sono:

* Sincronizzazione automatizzata dei file modificati nell&#39;istanza di sviluppo AEM.
* Sincronizzazione bidirezionale manuale di file e cartelle.
* Sincronizzazione completa del pacchetto di contenuti del progetto.
* Completamento del codice HTL per le espressioni e le istruzioni di blocco `data-sly-*`.

Inoltre, Bracket include molte funzionalità utili per AEM sviluppatori di font-end:

* Supporto di file Photoshop per estrarre informazioni da un file PSD, come livelli, misure, colori, font, testi, ecc.
* Suggerimenti per il codice dal file PSD, per riutilizzare facilmente le informazioni estratte nel codice.
* Supporto preprocessore CSS, come LESS e SCSS.
* E centinaia di ulteriori estensioni che coprono esigenze più specifiche.

## Installazione {#installation}

### Parentesi{#brackets}

L’estensione AEM parentesi quadre supporta le parentesi quadre versione 1.0 o successiva.

Scaricate la versione più recente di Bracket da [brackets.io](https://brackets.io/).

### Estensione {#the-extension}

Per installare l’estensione procedere come segue:

1. Aprite Le Parentesi. Nel menu **File**, selezionare **Extension Manager...**
1. Immettere **AEM** nella barra di ricerca e cercare **AEM Estensione parentesi quadre**.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. Fare clic su **Installa**.
1. Chiudere la finestra di dialogo e  Extension Manager al termine dell&#39;installazione.

## Guida introduttiva {#getting-started}

### Il progetto Content-Package {#the-content-package-project}

Dopo aver installato l’estensione, potete iniziare a sviluppare AEM componenti aprendo una cartella di pacchetto di contenuti dal file system con parentesi quadre.

Il progetto deve contenere almeno:

1. una cartella `jcr_root` (ad esempio `myproject/jcr_root`)

1. un file `filter.xml` (ad esempio `myproject/META-INF/vault/filter.xml`); per ulteriori dettagli sulla struttura del file `filter.xml`, vedere la [definizione del filtro dell&#39;area di lavoro](https://jackrabbit.apache.org/filevault/filter.html).

Nel menu **File** delle parentesi quadre, scegliere **Apri cartella...** e scegliere la cartella `jcr_root` o la cartella di progetto principale.

>[!NOTE]
>
>Se non disponete di un progetto personalizzato con un pacchetto di contenuti, potete provare l&#39;esempio [HTL TodoMVC](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc). In GitHub, fate clic su **Scarica ZIP**, estraete i file localmente e, come indicato in precedenza, aprite la cartella `jcr_root` in Bracket. Seguite quindi i passaggi indicati di seguito per impostare le **Impostazioni progetto** e, infine, caricare l&#39;intero pacchetto nell&#39;istanza di sviluppo AEM, eseguendo un **Esporta pacchetto di contenuto** come indicato più in basso nella sezione Sincronizzazione pacchetto completo.
>
>Dopo questa procedura, è necessario poter accedere all&#39;URL `/content/todo.html` nell&#39;istanza di sviluppo AEM e iniziare a apportare modifiche al codice in Bracket, per vedere come, dopo aver effettuato un aggiornamento nel browser Web, le modifiche siano state immediatamente sincronizzate con il server di AEM.

### Impostazioni progetto {#project-settings}

Per sincronizzare il contenuto con e da un’istanza di sviluppo AEM, è necessario definire le impostazioni del progetto. A tale scopo, è possibile accedere al menu **AEM** e scegliere **Impostazioni progetto...**

![chlimage_1-55](assets/chlimage_1-55a.png)

Le impostazioni progetto consentono di definire:

1. L’URL del server (ad esempio `http://localhost:4502`)
1. Consente di tollerare i server che non dispongono di un certificato HTTPS valido (lasciare deselezionato, se necessario)
1. Nome utente utilizzato per la sincronizzazione del contenuto (ad esempio `admin`)
1. La password dell&#39;utente (ad esempio `admin`)

## Sincronizzazione del contenuto {#synchronizing-content}

L&#39;estensione AEM parentesi quadre offre i seguenti tipi di sincronizzazione del contenuto per file e cartelle consentiti dalle regole di filtro definite in `filter.xml`:

### Sincronizzazione Automatizzata Dei File Modificati {#automated-synchronization-of-changed-files}

Le modifiche verranno sincronizzate solo da Bracket all&#39;istanza AEM, ma non viceversa.

### Sincronizzazione bidirezionale manuale {#manual-bidirectional-synchronization}

In Esplora progetti, aprire il menu contestuale facendo clic con il pulsante destro del mouse su un file o una cartella, e accedere alle opzioni **Esporta in server** o **Importa da server**.

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>Se la voce selezionata è all&#39;esterno della cartella `jcr_root`, le voci di menu contestuali **Esporta nel server** e **Importa da server** sono disattivate.

### Sincronizzazione completa del pacchetto di contenuti {#full-content-package-synchronization}

Nel menu **AEM**, le opzioni **Esporta pacchetto di contenuti** o **Importa pacchetto di contenuti** consentono di sincronizzare l&#39;intero progetto con il server.

![chlimage_1-57](assets/chlimage_1-57a.png)

### Stato sincronizzazione {#synchronization-status}

L’estensione AEM parentesi quadre dispone di un’icona di notifica nella barra degli strumenti, a destra della finestra Parentesi, che indica lo stato dell’ultima sincronizzazione:

* verde: tutti i file sono stati sincronizzati correttamente
* blue - È in corso un&#39;operazione di sincronizzazione
* giallo - alcuni dei file non erano sincronizzati
* rosso - nessuno dei file è stato sincronizzato

Facendo clic sull&#39;icona di notifica si aprirà la finestra di dialogo del rapporto Stato sincronizzazione in cui viene visualizzato l&#39;elenco di tutti gli stati per ciascun file sincronizzato.

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>Solo il contenuto contrassegnato come incluso nelle regole di filtro di `filter.xml` verrà sincronizzato, indipendentemente dal metodo di sincronizzazione utilizzato.
>
>Inoltre, i file `.vltignore` sono supportati per escludere il contenuto dalla sincronizzazione con e dall&#39;archivio.

## Modifica del codice HTL {#editing-htl-code}

L’estensione AEM parentesi quadre include anche il completamento automatico per semplificare la scrittura di attributi ed espressioni HTL.

### Completamento automatico attributi {#attribute-auto-completion}

1. In un attributo HTML, digitate `sly`. L&#39;attributo viene completato automaticamente in `data-sly-`.
1. Selezionate l’attributo HTL nell’elenco a discesa.

### Completamento automatico espressione {#expression-auto-completion}

All&#39;interno di un&#39;espressione `${}`, i nomi delle variabili comuni vengono completati automaticamente.

## Ulteriori informazioni {#more-information}

L&#39;estensione AEM Brackets è un progetto open-source, ospitato su GitHub dall&#39;organizzazione [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud), con la licenza Apache, versione 2.0:

* Archivio codici: [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Licenza Apache, versione 2.0: [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

L&#39;editor del codice Brackets è anche un progetto open-source, ospitato su GitHub dall&#39;organizzazione [Adobe Systems Incorporated](https://github.com/adobe):

* Archivio codici: [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

Sentiti libero di contribuire!
