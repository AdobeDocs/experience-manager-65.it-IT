---
title: Applicazione sandbox iniziale
seo-title: Applicazione sandbox iniziale
description: Creare un modello, un componente e uno script
seo-description: Creare un modello, un componente e uno script
uuid: b0d03376-d8bc-4e98-aea2-a01744c64ccd
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: f74d225e-0245-4d5a-bb93-0ee3f31557aa
translation-type: tm+mt
source-git-commit: 33c3126fbba4b324941338ee4d2a418d216408cd
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 2%

---


# Applicazione sandbox iniziale {#initial-sandbox-application}

In questa sezione, creerete i seguenti elementi:

* Il **[modello](#createthepagetemplate)**che verrà utilizzato per creare pagine di contenuto nel sito Web di esempio.
* Il **[componente e lo script](#create-the-template-s-rendering-component)**da utilizzare per il rendering delle pagine del sito Web.

## Creare il modello di contenuto {#create-the-content-template}

Un modello definisce il contenuto predefinito di una nuova pagina. I siti Web complessi possono utilizzare diversi modelli per la creazione di diversi tipi di pagine nel sito. Inoltre, il set di modelli potrebbe diventare un blueprint utilizzato per il rollout delle modifiche a un cluster di server.

In questo esercizio, tutte le pagine sono basate su un modello semplice.

1. Nel riquadro di esplorazione di CRXDE Lite:

   * Seleziona `/apps/an-scf-sandbox/templates`
   * **[!UICONTROL Crea]** > **[!UICONTROL Crea modello]**

1. Nella finestra di dialogo Crea modello, digitate i seguenti valori e fate clic su **[!UICONTROL Avanti]**:

   * Etichetta: `playpage`
   * Titolo: `An SCF Sandbox Play Template`
   * Descrizione: `An SCF Sandbox template for play pages`
   * Tipo risorsa: `an-scf-sandbox/components/playpage`
   * Classificazione: &lt;lasciare come predefinito>

   Etichetta utilizzata per il nome del nodo.

   Il tipo di risorsa viene visualizzato sul nodo jcr:content `playpage`come proprietà `sling:resourceType`. Identifica il componente (risorsa) che esegue il rendering del contenuto quando richiesto da un browser.

   In questo caso, tutte le pagine create utilizzando il `playpage` modello vengono sottoposte a rendering dal `an-scf-sandbox/components/playpage` componente. Per convenzione, il percorso del componente è relativo, consentendo a Sling di cercare la risorsa prima nella `/apps` cartella e, se non trovata, nella `/libs` cartella.

   ![create-content-template](assets/create-content-template-1.png)

1. Se si utilizza Copia/Incolla, assicurarsi che il valore Tipo risorsa non contenga spazi iniziali o finali.

   Fai clic su **[!UICONTROL Avanti]**.

1. Per &quot;Percorsi consentiti&quot; si intendono i percorsi delle pagine che utilizzano questo modello, in modo che il modello sia elencato per la finestra di dialogo **[!UICONTROL Nuova pagina]** .

   Per aggiungere un tracciato, fate clic sul pulsante più `+` e digitate `/content(/.&ast;)?` nella casella di testo visualizzata. Se usate Copia/Incolla, accertatevi che non vi siano spazi iniziali o finali.

   Nota: Il valore della proprietà path consentita è un&#39;espressione ** regolare. Le pagine di contenuto con un percorso che corrisponde all&#39;espressione possono utilizzare il modello. In questo caso, l&#39;espressione regolare corrisponde al percorso della cartella **/content** e di tutte le relative sottopagine.

   Quando un autore crea una pagina sotto `/content`, il `playpage` modello denominato &quot;An SCF Sandbox Page Template&quot; viene visualizzato in un elenco di modelli disponibili da utilizzare.

   Una volta creata la pagina principale dal modello, l&#39;accesso al modello potrebbe essere limitato a questo sito Web modificando la proprietà per includere il percorso principale nell&#39;espressione regolare, ovvero

   `/content/an-scf-sandbox(/.&ast;)?`

   ![configure-template-path](assets/configure-template-path.png)

1. Fai clic su **[!UICONTROL Avanti]**.

   Fate clic su **[!UICONTROL Avanti]** nel pannello Genitori **** consentiti.

   Fate clic su **[!UICONTROL Avanti]** nei pannelli Figli **** consentiti.

   Fai clic su **[!UICONTROL OK]**.

1. Dopo aver fatto clic su OK e aver completato la creazione del modello, agli angoli dei valori della scheda Proprietà per il nuovo `playpage` modello vengono visualizzati triangoli rossi. Questi triangoli rossi indicano le modifiche che non sono state salvate.

   Fate clic su **[!UICONTROL Salva tutto]** per salvare il nuovo modello nella directory archivio.

   ![verify-content-template](assets/verify-content-template.png)

### Creare il componente di rendering del modello {#create-the-template-s-rendering-component}

Create il *componente* che definisce il contenuto ed esegue il rendering di tutte le pagine create in base al modello [della](#createthepagetemplate)pagina di riproduzione.

1. In CRXDE Lite, fare clic con il pulsante destro del mouse **`/apps/an-scf-sandbox/components`** e scegliere **[!UICONTROL Crea > Componente]**.
1. Impostando il nome del nodo (Etichetta) sulla pagina di *riproduzione*, il percorso del componente è

   `/apps/an-scf-sandbox/components/playpage`

   che corrisponde al Tipo risorsa del modello della pagina di riproduzione (facoltativamente meno la **`/apps/`** parte iniziale del percorso).

   Nella finestra di dialogo **[!UICONTROL Crea componente]** , digitare i seguenti valori di proprietà:

   * Etichetta: **playpage**
   * Titolo: **Componente di riproduzione sandbox SCF**
   * Descrizione: **È il componente che esegue il rendering del contenuto per una pagina sandbox SCF.**
   * Super Type: *&lt;lasciare vuoto>*
   * Gruppo: *&lt;lasciare vuoto>*

   ![create-template-component](assets/create-template-component.png)

1. Fate clic su **[!UICONTROL Avanti]** fino a visualizzare il pannello **[!UICONTROL Elementi figlio]** consentiti nella finestra di dialogo:

   * Fai clic su **[!UICONTROL OK]**.
   * Fate clic su **[!UICONTROL Salva tutto]**.

1. Verifica che il percorso del componente e il resourceType per il modello corrispondano.

   >[!CAUTION]
   >
   >La corrispondenza tra il percorso del componente della pagina di riproduzione e la proprietà sling:resourceType del modello della pagina di riproduzione è fondamentale per il corretto funzionamento del sito Web.

   ![verify-template-component](assets/verify-template-component.png)