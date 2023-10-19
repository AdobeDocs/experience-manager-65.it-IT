---
title: Applicazione sandbox iniziale
description: Scopri come utilizzare il modello di contenuto utilizzato per creare pagine di contenuto e un componente e uno script utilizzati per il rendering delle pagine del sito web.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: cbf9ce36-53a2-4f4b-a96f-3b05743f6217
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 2%

---

# Applicazione sandbox iniziale {#initial-sandbox-application}

In questa sezione vengono creati i seguenti elementi:

* Il **[modello](#createthepagetemplate)** utilizzato per creare pagine di contenuto nel sito web di esempio.
* Il **[componente e script](#create-the-template-s-rendering-component)** utilizzato per eseguire il rendering delle pagine del sito web.

## Creare il modello di contenuto {#create-the-content-template}

Un modello definisce il contenuto predefinito di una nuova pagina. I siti web complessi possono utilizzare diversi modelli per creare i diversi tipi di pagine del sito. Inoltre, il set di modelli può diventare una blueprint utilizzata per distribuire le modifiche a un cluster di server.

In questo esercizio, tutte le pagine si basano su un modello semplice.

1. Nel riquadro Esplora risorse di CRXDE Liti:

   * Seleziona `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL Crea]** > **[!UICONTROL Crea modello]**

1. Nella finestra di dialogo Crea modello, digita i seguenti valori e fai clic su **[!UICONTROL Successivo]**:

   * Etichetta: `playpage`
   * Titolo: `An SCF Sandbox Play Template`
   * Descrizione: `An SCF Sandbox template for play pages`
   * Tipo risorsa: `an-scf-sandbox/components/playpage`
   * Classificazione: &lt;leave as=&quot;&quot; default=&quot;&quot;>

   L’etichetta viene utilizzata per il nome del nodo.

   Il Tipo di risorsa viene visualizzato sul `playpage`di `jcr:content` node come proprietà `sling:resourceType`. Identifica il componente (risorsa) che esegue il rendering del contenuto quando richiesto da un browser.

   In questo caso, tutte le pagine create utilizzando `playpage` il modello viene riprodotto da `an-scf-sandbox/components/playpage` componente. Per convenzione, il percorso del componente è relativo, consentendo a Sling di cercare la risorsa per prima nella `/apps` e, se non viene trovata, nella cartella `/libs` cartella.

   ![create-content-template](assets/create-content-template-1.png)

1. Se utilizzi Copia/Incolla, accertati che il valore Tipo risorsa non contenga spazi iniziali o finali.

   Fai clic su **[!UICONTROL Avanti]**.

1. &quot;Percorsi consentiti&quot; si riferisce ai percorsi delle pagine che utilizzano questo modello, in modo che il modello sia elencato per **[!UICONTROL Nuova pagina]** .

   Per aggiungere un percorso, fare clic sul pulsante più `+` e tipo `/content(/.&ast;)?` nella casella di testo visualizzata. Se si utilizza Copia/Incolla, verificare che non siano presenti spazi iniziali o finali.

   Nota: il valore della proprietà di percorso consentita è un *espressione regolare*. Le pagine di contenuto con un percorso che corrisponde all’espressione possono utilizzare il modello. In questo caso, l’espressione regolare corrisponde al percorso del **/content** cartella e tutte le relative pagine secondarie.

   Quando un autore crea una pagina di seguito `/content`, il `playpage` Il modello &quot;An SCF Sandbox Page Template&quot; (Modello di pagina sandbox SCF) viene visualizzato in un elenco di modelli disponibili da utilizzare.

   Dopo aver creato la pagina principale dal modello, l’accesso al modello potrebbe essere limitato a questo sito web modificando la proprietà in modo da includere il percorso principale nell’espressione regolare.

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. Fai clic su **[!UICONTROL Avanti]**.

   Clic **[!UICONTROL Successivo]** nel **[!UICONTROL Elementi padre consentiti]** pannello.

   Clic **[!UICONTROL Successivo]** nel **[!UICONTROL Elementi figlio consentiti]** pannello.

   Fai clic su **[!UICONTROL OK]**.

1. Dopo aver fatto clic su OK e completato la creazione del modello, notate i triangoli rossi visualizzati negli angoli della scheda Proprietà per il nuovo `playpage` modello. Questi triangoli rossi indicano modifiche che non sono state salvate.

   Clic **[!UICONTROL Salva tutto]** per salvare il nuovo modello nel repository.

   ![verify-content-template](assets/verify-content-template.png)

### Creare il componente Rendering del modello {#create-the-template-s-rendering-component}

Creare *componente* che definisce il contenuto ed esegue il rendering di tutte le pagine create in base al [modello playpage](#createthepagetemplate).

1. In CRXDE Liti, fai clic con il pulsante destro del mouse **`/apps/an-scf-sandbox/components`** e fai clic su **[!UICONTROL Crea > Componente]**.
1. Impostando il nome del nodo (Label) su *playpage*, il percorso del componente è

   `/apps/an-scf-sandbox/components/playpage`

   che corrisponde al tipo di risorsa del modello di pagina playlist (facoltativamente meno l’iniziale **`/apps/`** parte del percorso).

   In **[!UICONTROL Crea componente]** , digitare i seguenti valori di proprietà:

   * Etichetta: **playpage**
   * Titolo: **Un componente di riproduzione sandbox SCF**
   * Descrizione: **Questo è il componente che esegue il rendering del contenuto per una pagina Sandbox SCF.**
   * Super Type: *&lt;leave blank=&quot;&quot;>*
   * Gruppo: *&lt;leave blank=&quot;&quot;>*

   ![create-template-component](assets/create-template-component.png)

1. Clic **[!UICONTROL Successivo]** fino al **[!UICONTROL Elementi figlio consentiti]** viene visualizzato il pannello della finestra di dialogo:

   * Fai clic su **[!UICONTROL OK]**.
   * Clic **[!UICONTROL Salva tutto]**.

1. Verifica che il percorso del componente e il resourceType per il modello corrispondano.

   >[!CAUTION]
   >
   >La corrispondenza tra il percorso del componente Playpage e `sling:resourceType` proprietà del modello di playpage è fondamentale per il corretto funzionamento del sito web.

   ![verify-template-component](assets/verify-template-component.png)
