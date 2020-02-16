---
title: Estensione AEM Bracket
seo-title: Estensione AEM Bracket
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

---


# Estensione AEM Bracket{#aem-brackets-extension}

## Panoramica {#overview}

AEM Brackets Extension fornisce un flusso di lavoro fluido per la modifica di componenti AEM e librerie di client e sfrutta la potenza dell’editor di codice [Brackets](https://brackets.io/) , che permette di accedere da un editor di codice a file e livelli Photoshop. La semplice sincronizzazione fornita dall’estensione (non è richiesto Maven o File Vault) aumenta l’efficienza degli sviluppatori e aiuta gli sviluppatori front-end con scarsa conoscenza di AEM a partecipare ai progetti. Questa estensione fornisce anche il supporto per il linguaggio HTL ( [HTML Template Language)](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html), che elimina la complessità della JSP per rendere lo sviluppo dei componenti più semplice e sicuro.

![chlimage_1-53](assets/chlimage_1-53a.png)

### Funzioni {#features}

Le caratteristiche principali di AEM Brackets Extension sono:

* Sincronizzazione automatizzata dei file modificati nell’istanza di sviluppo di AEM.
* Sincronizzazione bidirezionale manuale di file e cartelle.
* Sincronizzazione completa del pacchetto di contenuti del progetto.
* Completamento codice HTL per espressioni e istruzioni `data-sly-*` di blocco.

Inoltre, le parentesi quadre contengono molte utili funzioni per gli sviluppatori di font AEM:

* Supporto per file Photoshop per estrarre informazioni da un file PSD, come livelli, misure, colori, font, testi ecc.
* Suggerimenti per il codice dal file PSD, per riutilizzare facilmente le informazioni estratte nel codice.
* Supporto preprocessore CSS, come LESS e SCSS.
* E centinaia di ulteriori estensioni che coprono esigenze più specifiche.

## Installazione {#installation}

### Parentesi {#brackets}

L’estensione AEM Brackets supporta la versione 1.0 o successiva.

Scaricate la versione più recente di Brackets da [brackets.io](https://brackets.io/).

### Estensione {#the-extension}

Per installare l’estensione procedere come segue:

1. Aprite Le Parentesi. Nel menu **File**, selezionate **Extension Manager.**
1. Immettete **AEM** nella barra di ricerca e cercate **AEM Brackets Extension**.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. Fate clic su **Installa**.
1. Al termine dell’installazione, chiudete la finestra di dialogo e Extension Manager.

## Introduzione {#getting-started}

### Il progetto Content-Package {#the-content-package-project}

Dopo aver installato l’estensione, potete iniziare a sviluppare componenti AEM aprendo una cartella di pacchetto di contenuti dal file system con le parentesi quadre.

Il progetto deve contenere almeno:

1. una `jcr_root` cartella (ad esempio `myproject/jcr_root`)

1. un `filter.xml` file (ad esempio `myproject/META-INF/vault/filter.xml`); per ulteriori dettagli sulla struttura del `filter.xml` file, vedere la definizione [del filtro](https://jackrabbit.apache.org/filevault/filter.html)Workspace.

Nel menu **File** parentesi quadre, scegliete **Apri cartella...** e scegliete la `jcr_root` cartella o la cartella di progetto principale.

>[!NOTE]
>
>Se non disponete di un progetto con un pacchetto di contenuti, potete provare l’esempio [](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc)HTL TodoMVC. In GitHub, fate clic su **Scarica ZIP**, estraete i file localmente e, come indicato sopra, aprite la `jcr_root` cartella in Bracket. Seguite quindi i passaggi indicati di seguito per impostare le impostazioni **del** progetto e, infine, caricare l’intero pacchetto nell’istanza di sviluppo di AEM, eseguendo un pacchetto **di** esportazione dei contenuti come indicato più in basso nella sezione Sincronizzazione pacchetto di contenuti completi.
>
>Dopo questa procedura, devi essere in grado di accedere all’ `/content/todo.html` URL nell’istanza di sviluppo di AEM e puoi iniziare a modificare il codice in Bracket per vedere come, dopo aver effettuato un aggiornamento nel browser Web, le modifiche siano state immediatamente sincronizzate con il server AEM.

### Impostazioni progetto {#project-settings}

Per sincronizzare il contenuto con e da un’istanza di sviluppo AEM, è necessario definire le impostazioni del progetto. A tale scopo, dal menu **AEM** scegliete Impostazioni **progetto.**

![chlimage_1-55](assets/chlimage_1-55a.png)

Le impostazioni progetto consentono di definire:

1. L’URL del server (ad esempio `http://localhost:4502`)
1. Consente di tollerare i server che non dispongono di un certificato HTTPS valido (lasciare deselezionato, se necessario)
1. Nome utente utilizzato per la sincronizzazione del contenuto (ad esempio `admin`)
1. La password dell&#39;utente (ad esempio `admin`)

## Sincronizzazione del contenuto {#synchronizing-content}

AEM Brackets Extension fornisce i seguenti tipi di sincronizzazione del contenuto per file e cartelle consentiti dalle regole di filtro definite in `filter.xml`:

### Sincronizzazione Automatica Dei File Modificati {#automated-synchronization-of-changed-files}

Le modifiche verranno sincronizzate solo da Bracket all’istanza di AEM, ma non viceversa.

### Sincronizzazione bidirezionale manuale {#manual-bidirectional-synchronization}

In Esplora progetti, aprite il menu contestuale facendo clic con il pulsante destro del mouse su un file o una cartella, quindi è possibile accedere alle opzioni **Esporta sul server** o **Importa dal server** .

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>Se la voce selezionata è all&#39;esterno della `jcr_root` cartella, le voci di menu contestuali **Esporta nel server** e **Importa dal server** sono disattivate.

### Sincronizzazione completa dei pacchetti di contenuti {#full-content-package-synchronization}

Nel menu **AEM** , le opzioni **Esporta pacchetto** di contenuti o **Importa pacchetto** di contenuti consentono di sincronizzare l&#39;intero progetto con il server.

![chlimage_1-57](assets/chlimage_1-57a.png)

### Stato sincronizzazione {#synchronization-status}

AEM Brackets Extension dispone di un’icona di notifica nella barra degli strumenti, a destra della finestra Parentesi, che indica lo stato dell’ultima sincronizzazione:

* verde: tutti i file sono stati sincronizzati correttamente
* blue - È in corso un&#39;operazione di sincronizzazione
* giallo - alcuni dei file non erano sincronizzati
* rosso - nessuno dei file è stato sincronizzato

Facendo clic sull&#39;icona di notifica si aprirà la finestra di dialogo del rapporto Stato sincronizzazione in cui viene visualizzato l&#39;elenco di tutti gli stati per ciascun file sincronizzato.

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>Solo il contenuto contrassegnato come incluso dalle regole di filtro `filter.xml` verrà sincronizzato, indipendentemente dal metodo di sincronizzazione utilizzato.
>
>Inoltre, `.vltignore` i file sono supportati per escludere il contenuto dalla sincronizzazione con e dall’archivio.

## Modifica del codice HTL {#editing-htl-code}

L’estensione AEM Brackets offre anche il completamento automatico per semplificare la scrittura di attributi ed espressioni HTL.

### Completamento automatico attributi {#attribute-auto-completion}

1. In un attributo HTML, digitate `sly`. L&#39;attributo è completato automaticamente in `data-sly-`.
1. Selezionate l’attributo HTL nell’elenco a discesa.

### Completamento automatico espressione {#expression-auto-completion}

All&#39;interno di un&#39;espressione `${}`, i nomi delle variabili comuni vengono completati automaticamente.

## Ulteriori informazioni {#more-information}

AEM Brackets Extension è un progetto open-source, ospitato su GitHub dall&#39;organizzazione [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud) , con la licenza Apache, versione 2.0:

* Archivio codici: [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Licenza Apache, versione 2.0: [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

L’editor del codice Brackets è anche un progetto open-source, ospitato su GitHub dall’organizzazione [Adobe Systems Incorporated](https://github.com/adobe) :

* Archivio codici: [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

Sentiti libero di contribuire!
