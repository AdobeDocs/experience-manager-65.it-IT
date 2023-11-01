---
title: Estensione parentesi AEM
seo-title: AEM Brackets Extension
description: Scopri come utilizzare l’estensione Adobe Experience Manager per Brackets.
seo-description: null
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
exl-id: 829d8256-b415-4a44-a353-455ac16950f3
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 2%

---

# Estensione parentesi AEM{#aem-brackets-extension}

## Panoramica {#overview}

L’estensione per Brackets AEM fornisce un flusso di lavoro fluido per modificare i componenti AEM e le librerie client e sfrutta la potenza della [Parentesi](https://brackets.io/) editor di codice, che consente l&#39;accesso ai file e ai livelli di Photoshop dall&#39;interno dell&#39;editor di codice. La facile sincronizzazione fornita dall’estensione (non è richiesto alcun Maven o File Vault) aumenta l’efficienza degli sviluppatori e aiuta anche gli sviluppatori front-end con conoscenze AEM limitate a partecipare ai progetti. Questa estensione fornisce anche un po’ di supporto per [HTL (HTML Template Language)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=it), che elimina la complessità di JSP per rendere lo sviluppo dei componenti più semplice e sicuro.

![chlimage_1-53](assets/chlimage_1-53a.png)

### Funzioni {#features}

Le caratteristiche principali dell’estensione per Brackets dell’AEM sono:

* Sincronizzazione automatizzata dei file modificati con l’istanza di sviluppo AEM.
* Sincronizzazione bidirezionale manuale di file e cartelle.
* Sincronizzazione completa del pacchetto di contenuti del progetto.
* Completamento del codice HTL per espressioni e `data-sly-*` istruzioni di blocco.

Brackets offre inoltre molte funzioni utili per gli sviluppatori di font-end AEM:

* Supporto di file Photoshop per estrarre informazioni da un file PSD, come livelli, misure, colori, font, testi, ecc.
* Suggerimenti sul codice dal PSD, per riutilizzare facilmente queste informazioni estratte nel codice.
* Supporto per il preprocessore CSS, come LESS e SCSS.
* E centinaia di estensioni aggiuntive che coprono esigenze più specifiche.

## Installazione {#installation}

### Parentesi {#brackets}

L&#39;estensione per Brackets AEM supporta Brackets versione 1.0 o successiva.

Scarica la versione più recente di Brackets da [parentesi.io](https://brackets.io/).

### Estensione {#the-extension}

Per installare l’estensione, procedi come segue:

1. Aprire Parentesi. Nel menu **File**, seleziona **Extension Manager:**
1. Invio **AEM** nella barra di ricerca e cerca **Estensione parentesi AEM**.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. Clic **Installa**.
1. Chiudere la finestra di dialogo e l&#39;Extension Manager al termine dell&#39;installazione.

## Guida introduttiva {#getting-started}

### Il progetto Content-Package {#the-content-package-project}

Una volta installata l’estensione, puoi iniziare a sviluppare componenti AEM aprendo una cartella di pacchetti di contenuti dal file system con Brackets.

Il progetto deve contenere almeno:

1. a `jcr_root` cartella (ad esempio, `myproject/jcr_root`)

1. a `filter.xml` file (ad esempio, `myproject/META-INF/vault/filter.xml`); per ulteriori dettagli sulla struttura del `filter.xml` consultare il file [Definizione filtro area di lavoro](https://jackrabbit.apache.org/filevault/filter.html).

Tra parentesi **File** menu, scegliere **Apri cartella...** e scegliere `jcr_root` o la cartella del progetto principale.

>[!NOTE]
>
>Se non disponi di un progetto con un pacchetto di contenuti, puoi provare la [Esempio HTL TodoMVC](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc). Su GitHub, fai clic su **Scarica ZIP**, estrarre i file localmente e, come indicato in precedenza, aprire `jcr_root` cartella in Brackets. Quindi seguire i passaggi riportati di seguito per impostare **Impostazioni progetto**, e infine caricare l’intero pacchetto nell’istanza di sviluppo AEM eseguendo un’ **Esporta pacchetto contenuti** come descritto più avanti nella sezione Sincronizzazione completa dei pacchetti di contenuti.
>
>Dopo questi passaggi, dovresti essere in grado di accedere al `/content/todo.html` URL nell’istanza di sviluppo dell’AEM e puoi iniziare a modificare il codice in Brackets e vedere come, dopo aver eseguito un aggiornamento nel browser web, le modifiche sono state immediatamente sincronizzate con il server AEM.

### Impostazioni progetto {#project-settings}

Per sincronizzare i contenuti con e da un’istanza di sviluppo AEM, devi definire le Impostazioni del progetto. Per eseguire questa operazione, vai al **AEM** menu e scelta **Impostazioni progetto...**

![chlimage_1-55](assets/chlimage_1-55a.png)

Le Impostazioni progetto consentono di definire:

1. L’URL del server (ad esempio, `http://localhost:4502`)
1. Tollerare i server che non dispongono di un certificato HTTPS valido (mantieni deselezionato, a meno che non sia necessario)
1. Il nome utente utilizzato per la sincronizzazione del contenuto (ad esempio, `admin`)
1. La password dell’utente (ad esempio, `admin`)

## Sincronizzazione dei contenuti {#synchronizing-content}

L’estensione per parentesi quadre AEM fornisce i seguenti tipi di sincronizzazione del contenuto per file e cartelle consentiti dalle regole di filtro definite in `filter.xml`:

### Sincronizzazione Automatizzata Dei File Modificati {#automated-synchronization-of-changed-files}

In questo modo verranno sincronizzate solo le modifiche da Brackets all’istanza AEM, ma mai il contrario.

### Sincronizzazione bidirezionale manuale {#manual-bidirectional-synchronization}

In Esplora progetti, apri il menu contestuale facendo clic con il pulsante destro del mouse su un file o una cartella e **Esporta su server** o **Importa dal server** è possibile accedere alle opzioni.

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>Se la voce selezionata è esterna al `jcr_root` cartella, la **Esporta su server** e **Importa dal server** le voci di menu contestuali sono disabilitate.

### Sincronizzazione completa dei pacchetti di contenuti {#full-content-package-synchronization}

In **AEM** menu, il **Esporta pacchetto contenuti** o **Importa pacchetto contenuti** Le opzioni consentono di sincronizzare l&#39;intero progetto con il server.

![chlimage_1-57](assets/chlimage_1-57a.png)

### Stato di sincronizzazione {#synchronization-status}

L&#39;estensione per parentesi quadre AEM presenta un&#39;icona di notifica nella barra degli strumenti a destra della finestra Parentesi quadre, che indica lo stato dell&#39;ultima sincronizzazione:

* verde - tutti i file sono stati sincronizzati correttamente
* blu: è in corso un’operazione di sincronizzazione
* giallo - alcuni file non sono stati sincronizzati
* rosso: nessuno dei file è stato sincronizzato

Facendo clic sull&#39;icona di notifica verrà aperta la finestra di dialogo del report Stato di sincronizzazione, in cui sono elencati tutti gli stati di ciascun file sincronizzato.

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>Solo il contenuto contrassegnato come incluso dalle regole di filtro da `filter.xml` verranno sincronizzati, indipendentemente dal metodo di sincronizzazione utilizzato.
>
>Inoltre, `.vltignore` i file sono supportati per escludere il contenuto dalla sincronizzazione con e dal repository.

## Modifica del codice HTL {#editing-htl-code}

L’estensione AEM Brackets dispone anche di un completamento automatico per facilitare la scrittura di attributi ed espressioni HTL.

### Completamento automatico attributo {#attribute-auto-completion}

1. In un attributo HTML, digita `sly`. L’attributo viene compilato automaticamente in `data-sly-`.
1. Seleziona l’attributo HTL nell’elenco a discesa.

### Completamento automatico espressione {#expression-auto-completion}

In un’espressione `${}`, i nomi delle variabili comuni vengono completati automaticamente.

## Ulteriori informazioni {#more-information}

L’estensione AEM Brackets è un progetto open-source, ospitato su GitHub da [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud) organizzazione, con licenza Apache, versione 2.0:

* Archivio del codice: [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Licenza Apache, versione 2.0: [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

L’editor di codice Brackets è anche un progetto open-source, ospitato su GitHub da [Adobe Systems Incorporated](https://github.com/adobe) organizzazione:

* Archivio del codice: [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

Sentiti libero di contribuire!
