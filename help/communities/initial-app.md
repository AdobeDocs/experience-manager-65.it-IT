---
title: Applicazione sandbox iniziale
description: Scopri come utilizzare il modello di contenuto utilizzato per creare pagine di contenuto e un componente e uno script utilizzati per il rendering delle pagine del sito web.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: cbf9ce36-53a2-4f4b-a96f-3b05743f6217
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 1%

---

# Applicazione sandbox iniziale {#initial-sandbox-application}

In questa sezione vengono creati i seguenti elementi:

* Il **[modello](#createthepagetemplate)** utilizzato per creare pagine di contenuto nel sito Web di esempio.
* Il **[componente e lo script](#create-the-template-s-rendering-component)** utilizzati per eseguire il rendering delle pagine del sito Web.

## Creare il modello di contenuto {#create-the-content-template}

Un modello definisce il contenuto predefinito di una nuova pagina. I siti web complessi possono utilizzare diversi modelli per creare i diversi tipi di pagine del sito. Inoltre, il set di modelli può diventare una blueprint utilizzata per distribuire le modifiche a un cluster di server.

In questo esercizio, tutte le pagine si basano su un modello semplice.

1. Nel riquadro Esplora risorse di CRXDE Lite:

   * Seleziona `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL Crea]** > **[!UICONTROL Crea modello]**

1. Nella finestra di dialogo Crea modello, digita i seguenti valori, quindi fai clic su **[!UICONTROL Avanti]**:

   * Etichetta: `playpage`
   * Titolo: `An SCF Sandbox Play Template`
   * Descrizione: `An SCF Sandbox template for play pages`
   * Tipo risorsa: `an-scf-sandbox/components/playpage`
   * Classificazione: &lt;lascia come predefinito>

   L’etichetta viene utilizzata per il nome del nodo.

   Il tipo di risorsa viene visualizzato nel nodo `jcr:content` di `playpage` come proprietà `sling:resourceType`. Identifica il componente (risorsa) che esegue il rendering del contenuto quando richiesto da un browser.

   In questo caso, tutte le pagine create utilizzando il modello `playpage` vengono sottoposte a rendering dal componente `an-scf-sandbox/components/playpage`. Per convenzione, il percorso del componente è relativo e Sling può cercare la risorsa prima nella cartella `/apps` e, se non la trova, nella cartella `/libs`.

   ![create-content-template](assets/create-content-template-1.png)

1. Se utilizzi Copia/Incolla, accertati che il valore Tipo risorsa non contenga spazi iniziali o finali.

   Fai clic su **[!UICONTROL Avanti]**.

1. &quot;Percorsi consentiti&quot; si riferisce ai percorsi delle pagine che utilizzano questo modello, in modo che il modello sia elencato per la finestra di dialogo **[!UICONTROL Nuova pagina]**.

   Per aggiungere un percorso, fare clic sul pulsante più `+` e digitare `/content(/.&ast;)?` nella casella di testo visualizzata. Se si utilizza Copia/Incolla, verificare che non siano presenti spazi iniziali o finali.

   Nota: il valore della proprietà di percorso consentita è una *espressione regolare*. Le pagine di contenuto con un percorso che corrisponde all’espressione possono utilizzare il modello. In questo caso, l&#39;espressione regolare corrisponde al percorso della cartella **/content** e di tutte le relative pagine secondarie.

   Quando un autore crea una pagina al di sotto di `/content`, il modello `playpage` denominato &quot;Modello di pagina sandbox SCF&quot; viene visualizzato in un elenco di modelli disponibili da utilizzare.

   Dopo aver creato la pagina principale dal modello, l’accesso al modello potrebbe essere limitato a questo sito web modificando la proprietà in modo da includere il percorso principale nell’espressione regolare.

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. Fai clic su **[!UICONTROL Avanti]**.

   Fai clic su **[!UICONTROL Avanti]** nel pannello **[!UICONTROL Padri consentiti]**.

   Fai clic su **[!UICONTROL Successivo]** nel pannello **[!UICONTROL Figli consentiti]**.

   Fai clic su **[!UICONTROL OK]**.

1. Dopo aver fatto clic su OK e aver completato la creazione del modello, notate i triangoli rossi visualizzati negli angoli della scheda Proprietà per il nuovo modello `playpage`. Questi triangoli rossi indicano modifiche che non sono state salvate.

   Fare clic su **[!UICONTROL Salva tutto]** per salvare il nuovo modello nel repository.

   ![verify-content-template](assets/verify-content-template.png)

### Creare il componente Rendering del modello {#create-the-template-s-rendering-component}

Crea il *componente* che definisce il contenuto ed esegue il rendering di tutte le pagine create in base al [modello di playpage](#createthepagetemplate).

1. In CRXDE Lite, fare clic con il pulsante destro del mouse su **`/apps/an-scf-sandbox/components`** e scegliere **[!UICONTROL Crea > Componente]**.
1. Impostando il nome del nodo (Etichetta) su *playpage*, il percorso del componente è

   `/apps/an-scf-sandbox/components/playpage`

   che corrisponde al tipo di risorsa del modello della pagina di riproduzione (facoltativamente meno la parte **`/apps/`** iniziale del percorso).

   Nella finestra di dialogo **[!UICONTROL Crea componente]**, digita i seguenti valori di proprietà:

   * Etichetta: **playpage**
   * Titolo: **Componente di riproduzione sandbox SCF**
   * Descrizione: **Questo è il componente che esegue il rendering del contenuto per una pagina Sandbox SCF.**
   * Super Type: *&lt;lasciare vuoto>*
   * Gruppo: *&lt;lasciare vuoto>*

   ![create-template-component](assets/create-template-component.png)

1. Fai clic su **[!UICONTROL Successivo]** finché non viene visualizzato il pannello **[!UICONTROL Figli consentiti]** della finestra di dialogo:

   * Fai clic su **[!UICONTROL OK]**.
   * Fare clic su **[!UICONTROL Salva tutto]**.

1. Verifica che il percorso del componente e il resourceType per il modello corrispondano.

   >[!CAUTION]
   >
   >La corrispondenza tra il percorso del componente Playpage e la proprietà `sling:resourceType` del modello Playpage è fondamentale per il corretto funzionamento del sito Web.

   ![verify-template-component](assets/verify-template-component.png)
