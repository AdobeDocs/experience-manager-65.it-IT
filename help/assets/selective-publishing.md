---
title: Utilizzo della pubblicazione selettiva in Dynamic Media
description: Puoi scegliere di pubblicare o annullare la pubblicazione di risorse in o da Adobe Experience Manager o Dynamic Media a livello di cartella. Invece di affidarti esclusivamente alla configurazione di Dynamic Media, le cui impostazioni sono globali per tutte le cartelle nell’istanza di Dynamic Media, puoi utilizzare Gestisci pubblicazione o Pubblicazione rapida.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: Publishing
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '3000'
ht-degree: 3%

---

# Configurare la pubblicazione selettiva a livello di cartella in Dynamic Media {#selective-publish-configure-folder}

Puoi scegliere di pubblicare o annullare la pubblicazione di risorse in o da Adobe Experience Manager o Dynamic Media a livello di cartella. Puoi utilizzare **[!UICONTROL Gestisci pubblicazione]** o **[!UICONTROL Pubblicazione rapida]** invece di affidarti esclusivamente alla **[!UICONTROL configurazione di Dynamic Media]**, le cui impostazioni sono globali per tutte le cartelle nell&#39;istanza di Dynamic Media.

Ad esempio, con la pubblicazione selettiva è possibile lavorare su risorse per prodotti non ancora live. In questo caso, un team di marketing può accedere alle immagini con ritaglio avanzato e alle rappresentazioni dinamiche sincronizzate con Dynamic Media. Possono creare materiali promozionali senza dover pubblicare tali risorse in Dynamic Media per la distribuzione globale.

>[!IMPORTANT]
>
>La pubblicazione selettiva è disponibile solo in modalità Dynamic Media - Scene7.

>[!NOTE]
>
>*Se si copiano* risorse da e verso le cartelle, lo stato di pubblicazione di tali risorse viene cancellato. Tuttavia, quando *sposti* risorse in e da cartelle la cui proprietà cartella è impostata su **[!UICONTROL Pubblicazione selettiva]**, lo stato di pubblicazione di tali risorse viene mantenuto.

Se successivamente decidi di modificare le impostazioni di **[!UICONTROL Pubblicazione selettiva]** in una cartella, tali modifiche interesseranno solo le nuove risorse caricate in tale cartella da quel momento in poi. Lo stato di pubblicazione delle risorse esistenti nella cartella rimane invariato finché non le modifichi manualmente da **[!UICONTROL Pubblicazione rapida]** o dalla finestra di dialogo **[!UICONTROL Gestisci pubblicazione]**.

L&#39;opzione a livello di cartella **[!UICONTROL Modalità di pubblicazione Dynamic Media]** utilizza sempre per impostazione predefinita il valore presente nell&#39;impostazione **[!UICONTROL Pubblica Assets]** nella **[!UICONTROL Configurazione Dynamic Media]**. Nei passaggi seguenti di questo argomento viene tuttavia illustrato come modificare manualmente questo valore predefinito a livello di cartella (come descritto nei passaggi seguenti) per ignorare il valore **[!UICONTROL Configurazione elemento multimediale dinamico]**.

Indipendentemente dal fatto che ci si basi su uno dei seguenti elementi:

* **[!UICONTROL Pubblica valore Assets]** impostato in **[!UICONTROL Configurazione elemento multimediale dinamico]**.
* **[!UICONTROL Modalità di pubblicazione Dynamic Media]** impostata nelle proprietà a livello di cartella.

Puoi scegliere **[!UICONTROL Immediatamente]**, **[!UICONTROL Al momento dell&#39;attivazione]** o **[!UICONTROL Pubblicazione selettiva]**. Ad esempio, puoi impostare il valore **[!UICONTROL Pubblica Assets]** nella **[!UICONTROL Configurazione Dynamic Media]** su **[!UICONTROL All&#39;attivazione]**, ma impostare il valore della modalità **[!UICONTROL Pubblicazione Dynamic Media]** a livello di cartella su **[!UICONTROL Pubblicazione selettiva]** e viceversa.

Dopo aver configurato la pubblicazione selettiva in una cartella, puoi effettuare una delle seguenti operazioni:

* [Pubblica selettivamente le risorse in Dynamic Media o Experience Manager tramite Gestisci pubblicazione](#selective-publish-manage-publication).
* [Annullamento selettivo della pubblicazione di risorse da Dynamic Media o Experience Manager tramite Gestisci pubblicazione](#selective-unpublish-manage-publication).
* [Pubblicare risorse in Dynamic Media o Experience Manager tramite Pubblicazione rapida](#quick-publish-aem-dm).
* [Pubblicare o annullare la pubblicazione selettiva delle risorse in base ai risultati della ricerca](#selective-publish-unpublish-search-results).

**Per configurare la pubblicazione selettiva a livello di cartella in Dynamic Media:**

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro, seleziona l&#39;icona Navigazione (appena sopra l&#39;icona Strumenti), quindi seleziona **[!UICONTROL Assets]** > **[!UICONTROL File]**.
1. Effettua una delle seguenti operazioni:
   * Modifica le proprietà di una cartella esistente. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]**, accedi a una cartella di cui desideri modificare le proprietà. Seleziona la cartella, quindi nella barra degli strumenti seleziona **[!UICONTROL Proprietà]**.
   * Modifica le proprietà di una nuova cartella. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]**, nell&#39;angolo superiore destro della pagina, seleziona **[!UICONTROL Crea]** > **[!UICONTROL Cartella]**. Nella finestra di dialogo **[!UICONTROL Crea cartella]**, immetti un titolo (obbligatorio) per la cartella, quindi seleziona **[!UICONTROL Crea]**. Seleziona la cartella, quindi nella barra degli strumenti seleziona **[!UICONTROL Proprietà]**.

1. Nell&#39;elenco a discesa **[!UICONTROL Modalità di sincronizzazione]** selezionare una delle opzioni seguenti:

   | Modalità di sincronizzazione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Ereditato]** | Nessun valore di sincronizzazione esplicito nella cartella. La cartella eredita invece il valore di sincronizzazione da una delle cartelle precedenti o dalla modalità predefinita impostata nella **[!UICONTROL configurazione di Dynamic Media]**. Lo stato dettagliato di **[!UICONTROL Ereditato]** viene visualizzato come descrizione comando. |
   | **[!UICONTROL Sincronizza tutto il contenuto di questa sottostruttura di cartelle con Dynamic Media]** | Affinché la pubblicazione in Dynamic Media abbia esito positivo, le risorse devono essere sincronizzate in Dynamic Media. Selezionando questa opzione vengono incluse tutte le risorse di questo sottoalbero per la sincronizzazione con Dynamic Media. Le impostazioni specifiche della cartella hanno la precedenza sull&#39;impostazione predefinita nella **[!UICONTROL configurazione elemento multimediale dinamico]**. |
   | **[!UICONTROL Escludi tutto il contenuto di questa sottostruttura di cartelle dalla sincronizzazione Dynamic Media]** | Escludi tutte le risorse in questa sottostruttura dalla sincronizzazione con Dynamic Media. |

   ![Pubblicazione selettiva a livello di cartella](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. Selezionare un&#39;opzione nell&#39;elenco a discesa **[!UICONTROL Modalità pubblicazione Dynamic Media]**. L&#39;opzione **[!UICONTROL Modalità pubblicazione Dynamic Media]** utilizza sempre per impostazione predefinita il valore impostato nella **[!UICONTROL configurazione Dynamic Media]**. È tuttavia possibile sovrascrivere manualmente il valore predefinito **[!UICONTROL Configurazione elemento multimediale dinamico]** utilizzando una delle opzioni seguenti.

   >[!IMPORTANT]
   >
   >Indipendentemente dall&#39;opzione selezionata per la modalità di pubblicazione Dynamic Media, qualsiasi aggiornamento apportato successivamente a una risorsa *già* pubblicata, verrà pubblicato immediatamente senza ulteriori azioni da parte dell&#39;utente.
   >
   >Se un video pubblicato viene aggiornato, deve essere pubblicato nuovamente per riflettere le modifiche alla consegna.

   | Opzione modalità di pubblicazione Dynamic Media | Descrizione |
   | --- | --- |
   | **[!UICONTROL Immediatamente]** | Quando le risorse vengono caricate in questa cartella, il sistema le acquisisce in Experience Manager e fornisce immediatamente l’URL/Incorpora. Questa opzione è associata solo alla pubblicazione in Experience Manager e non è necessario alcun intervento da parte dell’utente per pubblicare le risorse.<br>Questa opzione è *non* disponibile se hai selezionato **[!UICONTROL Escludi tutti gli elementi di questa sottostruttura di cartelle dalla sincronizzazione Dynamic Media]** in **[!UICONTROL Modalità di sincronizzazione]** nel passaggio precedente. |
   | **[!UICONTROL All&#39;attivazione]** | Quando le risorse vengono caricate in questa cartella, devi pubblicarle esplicitamente prima di fornire un URL o un collegamento di incorporamento. Questa opzione è associata solo alla pubblicazione in Experience Manager.<br>Questa opzione è *non* disponibile se hai selezionato **[!UICONTROL Escludi tutti gli elementi di questa sottostruttura di cartelle dalla sincronizzazione Dynamic Media]** in **[!UICONTROL Modalità di sincronizzazione]** nel passaggio precedente. |
   | **[!UICONTROL Pubblicazione selettiva]** | Assets vengono pubblicati su Experience Manager o Dynamic Media a tua scelta, per la distribuzione nel dominio pubblico. Entrambi i metodi di pubblicazione si escludono a vicenda. In altre parole, puoi pubblicare le risorse in DMS7 per utilizzare funzioni quali Ritaglio avanzato o rappresentazioni dinamiche. In alternativa, puoi pubblicare le risorse esclusivamente in Experience Manager per una visualizzazione protetta in anteprima; le stesse risorse sono *non* pubblicate in DMS7 per la distribuzione nel dominio pubblico. Questa opzione non è disponibile se hai selezionato **[!UICONTROL Escludi tutti gli elementi di questa sottostruttura di cartelle dalla sincronizzazione Dynamic Media]** in **[!UICONTROL Modalità di sincronizzazione]** nel passaggio precedente. |

1. Nell&#39;angolo superiore destro della pagina, seleziona **[!UICONTROL Salva e chiudi]**, quindi seleziona **[!UICONTROL OK]** per tornare a Experience Manager Assets.

## Pubblicare selettivamente le risorse in Dynamic Media o Experience Manager tramite Gestisci pubblicazione{#selective-publish-manage-publication}

Prima di poter utilizzare **[!UICONTROL Gestisci pubblicazione]** per pubblicare selettivamente le risorse in Dynamic Media o Experience Manager, assicurati di aver impostato una delle seguenti opzioni:

* Opzione **[!UICONTROL Pubblica Assets]** in **[!UICONTROL Configurazione elemento multimediale dinamico]** in **[!UICONTROL Pubblicazione selettiva]**
* È stata configurata la pubblicazione selettiva a livello di cartella.

Vedi [Creare una configurazione Dynamic Media](#configuring-dynamic-media-cloud-services) o [Configurare la pubblicazione selettiva a livello di cartella in Dynamic Media](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>La pubblicazione selettiva è disponibile solo in modalità Dynamic Media - Scene7.

>[!NOTE]
>
>*Se si copiano* risorse da e verso le cartelle, lo stato di pubblicazione di tali risorse viene cancellato. Tuttavia, quando *sposti* risorse in e da cartelle la cui proprietà cartella è impostata su **[!UICONTROL Pubblicazione selettiva]**, lo stato di pubblicazione di tali risorse viene mantenuto.

**Per pubblicare selettivamente le risorse in Dynamic Media o Experience Manager tramite Gestisci pubblicazione:**

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro, seleziona l&#39;icona Navigazione (appena sopra l&#39;icona Strumenti), quindi seleziona **[!UICONTROL Assets]** > **[!UICONTROL File]**.
1. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]**, eseguire una delle operazioni seguenti:
   * Passa a una cartella di cui desideri pubblicare le risorse. Seleziona la cartella, quindi nella barra degli strumenti seleziona **[!UICONTROL Gestisci pubblicazione]**. Utilizza **[!UICONTROL Vista a elenco]** per controllare più facilmente lo stato di pubblicazione di una determinata cartella.
   * Passa a una cartella di cui desideri pubblicare le risorse. Apri la cartella, quindi seleziona una o più risorse. Sulla barra degli strumenti, selezionare **[!UICONTROL Gestisci pubblicazione]**. Utilizza **[!UICONTROL Vista a elenco]** per controllare più facilmente lo stato di pubblicazione di una particolare risorsa.

     >[!NOTE]
     >
     >Se **[!UICONTROL Gestisci pubblicazione]** non è visualizzato nella barra degli strumenti, seleziona il pulsante con i puntini di sospensione, quindi seleziona **[!UICONTROL Gestisci pubblicazione]** dal menu elenco.

1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Opzioni]**, in **[!UICONTROL Azione]**, selezionare il tipo di attivazione desiderato.

   | Azione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Pubblica]** (in Experience Manager) | Seleziona questa opzione per pubblicare le risorse in Experience Manager per un’anteprima protetta. |
   | **[!UICONTROL Pubblica in Dynamic Media]** | Seleziona questa opzione per pubblicare le risorse in Dynamic Media per la distribuzione nel dominio pubblico o per utilizzare funzioni quali Ritaglio avanzato o rappresentazioni dinamiche.<br>Questa opzione è disponibile solo se **[!UICONTROL la modalità di pubblicazione Dynamic Media]** è impostata su **[!UICONTROL Pubblicazione selettiva]** nelle proprietà della cartella. |

1. In **[!UICONTROL Pianificazione]**, impostare la tempistica della pubblicazione.

   | Pianificazione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Ora]** | Seleziona questa opzione per pubblicare immediatamente le risorse. |
   | **[!UICONTROL Più tardi]** | Seleziona questa opzione per pubblicare le risorse in una data e un’ora specifiche. |

1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Gestisci pubblicazione]**, seleziona **[!UICONTROL Successivo]**.
1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Ambito]** eseguire una delle operazioni seguenti:

   * Se necessario, seleziona una o più risorse da rimuovere dalla pubblicazione.
   * Nell&#39;angolo superiore destro della pagina **[!UICONTROL Gestisci pubblicazione - Ambito]**, selezionare **[!UICONTROL Pubblica]** o **[!UICONTROL Pubblica in Dynamic Media]**.
1. Selezionare **[!UICONTROL OK]**.

### Annullare la pubblicazione selettiva delle risorse da Dynamic Media o Experience Manager tramite Gestisci pubblicazione {#selective-unpublish-manage-publication}

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro, seleziona l&#39;icona Navigazione (appena sopra l&#39;icona Strumenti), quindi seleziona **[!UICONTROL Assets]** > **[!UICONTROL File]**.
1. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]**, eseguire una delle operazioni seguenti:
   * Passa a una cartella di cui desideri annullare la pubblicazione delle risorse. Seleziona la cartella, quindi nella barra degli strumenti seleziona **[!UICONTROL Gestisci pubblicazione]**. Utilizza **[!UICONTROL Vista a elenco]** per controllare più facilmente lo stato di pubblicazione di una determinata cartella.
   * Passa a una cartella di cui desideri annullare la pubblicazione delle risorse. Apri la cartella, quindi seleziona una o più risorse. Sulla barra degli strumenti, selezionare **[!UICONTROL Gestisci pubblicazione]**. Utilizza **[!UICONTROL Vista a elenco]** per controllare più facilmente lo stato di pubblicazione di una particolare risorsa.

     >[!NOTE]
     >
     >Se **[!UICONTROL Gestisci pubblicazione]** non è visualizzato nella barra degli strumenti, seleziona il pulsante con i puntini di sospensione, quindi seleziona **[!UICONTROL Gestisci pubblicazione]** dal menu elenco.

1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Opzioni]**, in **[!UICONTROL Azione]**, selezionare il tipo di disattivazione desiderato.

   | Azione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Annulla pubblicazione]** (da Experience Manager) | Seleziona questa opzione se desideri annullare la pubblicazione delle risorse da Experience Manager. |
   | **[!UICONTROL Annulla pubblicazione da Dynamic Media]** | Seleziona questa opzione se desideri annullare la pubblicazione delle risorse da Dynamic Media.<br>Questa opzione è disponibile solo se **[!UICONTROL la modalità di pubblicazione Dynamic Media]** è impostata su **[!UICONTROL Pubblicazione selettiva]** nelle proprietà della cartella. |

1. In **[!UICONTROL Pianificazione]**, impostare la tempistica della disattivazione.

   | Pianificazione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Ora]** | Seleziona questa opzione per annullare subito la pubblicazione delle risorse. |
   | **[!UICONTROL Più tardi]** | Seleziona questa opzione per annullare la pubblicazione delle risorse in una data e un’ora specifiche. |

1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Gestisci pubblicazione]**, seleziona **[!UICONTROL Successivo]**.
1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Ambito]** eseguire una delle operazioni seguenti:
   * Seleziona una o più risorse da rimuovere per annullare la pubblicazione.
   * Nell&#39;angolo superiore destro della pagina **[!UICONTROL Gestisci pubblicazione - Ambito]**, selezionare **[!UICONTROL Annulla pubblicazione]** o **[!UICONTROL Annulla pubblicazione da Dynamic Media]**.
1. Selezionare **[!UICONTROL OK]**.

## Pubblicare risorse in Dynamic Media o Experience Manager tramite Pubblicazione rapida {#quick-publish-aem-dm}

Puoi utilizzare **[!UICONTROL Pubblicazione rapida]** per casi semplici di attivazione di risorse. **[!UICONTROL Pubblicazione rapida]** pubblica immediatamente le risorse selezionate senza ulteriore interazione da parte dell&#39;utente. A causa di questa azione, vengono pubblicati automaticamente anche tutti i riferimenti non pubblicati.

>[!NOTE]
>
>Per utilizzare la **[!UICONTROL Pubblicazione rapida]** per pubblicare risorse in Dynamic Media o Experience Manager, assicurati che la **[!UICONTROL Pubblicazione selettiva]** sia abilitata nella **[!UICONTROL Configurazione di Dynamic Media]** o nelle proprietà della cartella selezionata.

**Per pubblicare le risorse in Dynamic Media o Experience Manager tramite Pubblicazione rapida:**

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro della pagina, seleziona l&#39;icona Navigazione (appena sopra l&#39;icona Strumenti), quindi sul lato destro della pagina seleziona **[!UICONTROL Assets]** > **[!UICONTROL File]**.
1. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]**, eseguire una delle operazioni seguenti:
   * Passa a una cartella di cui desideri pubblicare le risorse. Seleziona la cartella, quindi sulla barra degli strumenti seleziona **[!UICONTROL Pubblicazione rapida]**. Utilizza **[!UICONTROL Vista a elenco]** per controllare più facilmente lo stato di pubblicazione di una determinata cartella.
   * Passa a una cartella di cui desideri pubblicare le risorse. Apri la cartella, quindi seleziona una o più risorse. Sulla barra degli strumenti, seleziona **[!UICONTROL Pubblicazione rapida]**. Utilizza **[!UICONTROL Vista a elenco]** per controllare più facilmente lo stato di pubblicazione di una particolare risorsa.

     >[!NOTE]
     >
     >Se **[!UICONTROL Pubblicazione rapida]** non è visualizzato nella barra degli strumenti, seleziona il pulsante con i puntini di sospensione, quindi seleziona **[!UICONTROL Pubblicazione rapida]** dal menu elenco.

     ![Pubblicazione rapida a livello di cartella in Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Selezionare una delle opzioni seguenti dall&#39;elenco del menu **[!UICONTROL Pubblicazione rapida]**.

   | Opzione Pubblicazione rapida | Effetto |
   | --- | --- |
   | Pubblica su Experience Manager | Pubblica immediatamente le risorse selezionate in Experience Manager. |
   | Pubblica su Brand Portal | Pubblica immediatamente le risorse selezionate in **[!UICONTROL Brand Portal]**.<br>Questa opzione è disponibile solo se nell&#39;istanza di Experience Manager Assets è già configurato **[!UICONTROL Brand Portal]**. |
   | Pubblica in Dynamic Media | Pubblica immediatamente le risorse selezionate in Dynamic Media.<br>Una risorsa deve essere sincronizzata in Dynamic Media. Se necessario, verificare che **[!UICONTROL Modalità di sincronizzazione]** nelle proprietà di una cartella sia già impostata su **[!UICONTROL Sincronizza tutto il contenuto di questa sottostruttura di cartelle in Dynamic Media]**. |

1. Seleziona **[!UICONTROL OK]**, quindi seleziona **[!UICONTROL Chiudi]**.

## Pubblicare o annullare la pubblicazione selettiva delle risorse tramite i risultati della ricerca {#selective-publish-unpublish-search-results}

I risultati della ricerca possono mostrare le risorse di più cartelle di risorse con impostazioni di pubblicazione di Dynamic Media diverse. Se dai risultati della ricerca selezioni più risorse e ciascuna risorsa ha impostazioni diverse per la modalità di pubblicazione Dynamic Media, puoi attivare **[!UICONTROL Gestisci pubblicazione]** dalla barra degli strumenti, per eseguire o annullare la pubblicazione.

Vedi anche [Cercare risorse in Experience Manager](/help/assets/search-assets.md).

**Per pubblicare o annullare la pubblicazione selettiva delle risorse tramite i risultati della ricerca:**

1. In Experience Manager, nell’angolo superiore sinistro della pagina, seleziona il logo Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro della pagina, seleziona l&#39;icona Navigazione (appena sopra l&#39;icona Strumenti), quindi seleziona **[!UICONTROL Assets]** > **[!UICONTROL File]**.
1. Sulla barra degli strumenti, nell&#39;angolo superiore destro della pagina, selezionare l&#39;icona Ricerca (lente di ingrandimento).
1. Nel campo di testo **[!UICONTROL Digitare per cercare]**, immettere una parola chiave, quindi premere **[!UICONTROL Invio]**.
1. Fai clic sull&#39;icona **[!UICONTROL Vista a elenco]** nell&#39;angolo superiore destro della pagina.
1. Seleziona l&#39;icona **[!UICONTROL Filtri]** nell&#39;angolo superiore sinistro della pagina.

   ![Visualizzazione elenco e filtri nei risultati di ricerca](/help/assets/assets-dm/select-publish-search-result.png)

1. Nel pannello a sinistra, espandi **[!UICONTROL Stato]**, quindi espandi il predicato di ricerca **[!UICONTROL Dynamic Media]**.
1. Utilizza le caselle di controllo **[!UICONTROL Pubblicato]** e **[!UICONTROL Non pubblicato]** per perfezionare ulteriormente i risultati della ricerca in base allo stato di pubblicazione delle risorse Dynamic Media.
Facoltativamente, puoi utilizzare queste caselle di controllo con il predicato di ricerca **[!UICONTROL Pubblica]** per perfezionare i risultati della ricerca delle risorse Experience Manager **[!UICONTROL Pubblicate]** e **[!UICONTROL Non pubblicate]**.
1. Effettua una delle seguenti operazioni:
   * Seleziona una o più risorse da pubblicare o di cui annullare la pubblicazione.
   * Selezionare **[!UICONTROL Seleziona tutto]** nell&#39;angolo superiore destro della pagina **[!UICONTROL Risultati ricerca]**.
1. Sulla barra degli strumenti, selezionare **[!UICONTROL Gestisci pubblicazione]**. Seleziona l&#39;icona con i puntini di sospensione sulla barra degli strumenti per aprire **[!UICONTROL Gestisci pubblicazione]**.
1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Opzioni]** selezionare l&#39;azione desiderata.

   | Azione selezionata | Impostazione di pubblicazione di Assets nella configurazione di Dynamic Media | Assets sono |
   | --- | --- | --- |
   | Pubblicazione | Immediatamente o Al momento dell&#39;attivazione | Pubblicato in Experience Manager e Dynamic Media. |
   | Pubblicazione | Pubblicazione selettiva | Pubblicato solo su Experience Manager. |
   | Annulla pubblicazione | Immediatamente o Al momento dell&#39;attivazione | Non più pubblicato su Experience Manager e Dynamic Media. |
   | Annulla pubblicazione | Pubblicazione selettiva | Pubblicazione annullata solo da Experience Manager. |
   | Pubblica in Dynamic Media | Immediatamente o Al momento dell&#39;attivazione | Non pubblicato in Experience Manager, Dynamic Media o entrambi. |
   | Pubblica in Dynamic Media | Pubblicazione selettiva | Pubblicato solo in Dynamic Media. |
   | Annulla pubblicazione da Dynamic Media | Immediatamente o Al momento dell&#39;attivazione | Non viene annullata la pubblicazione su Experience Manager, Dynamic Media o entrambi. |
   | Annulla pubblicazione da Dynamic Media | Pubblicazione selettiva | Pubblicazione annullata solo da Dynamic Media. |

1. In **[!UICONTROL Pianificazione]**, impostare la tempistica della disattivazione.

   | Pianificazione selezionata | Cosa succede |
   | --- | --- |
   | Adesso | L&#39;azione selezionata viene eseguita immediatamente. |
   | Più tardi | L&#39;azione selezionata viene eseguita nella data e ora specifiche selezionate. |

1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Gestisci pubblicazione - Opzioni]**, selezionare **[!UICONTROL Successivo]**.
1. (Facoltativo) Nella pagina **[!UICONTROL Gestisci pubblicazione - Ambito]**, controlla la colonna **[!UICONTROL Destinazione pubblicazione]** nella tabella per le risorse selezionate.

   | Impostazione di pubblicazione di Assets nella configurazione di Dynamic Media | Azione selezionata | Destinazione pubblicazione |
   | --- | --- | --- |
   | Immediatamente o <br>All&#39;attivazione | Pubblicazione | Experience Manager e Dynamic Media |
   | Immediatamente o <br>All&#39;attivazione | Pubblica in Dynamic Media | Nessuna |
   | Pubblicazione selettiva | Pubblicazione | Experience Manager |
   | Pubblicazione selettiva | Pubblica in Dynamic Media | Dynamic Media |
   | Immediatamente o <br>All&#39;attivazione | Annulla pubblicazione | Experience Manager e Dynamic Media |
   | Immediatamente o <br>All&#39;attivazione | Annulla pubblicazione da Dynamic Media | Nessuna |
   | Pubblicazione selettiva | Annulla pubblicazione | Experience Manager |
   | Pubblicazione selettiva | Annulla pubblicazione da Dynamic Media | Dynamic Media |

1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Ambito]** eseguire una delle operazioni seguenti:
   * Seleziona una o più risorse da rimuovere dalla pubblicazione o dall’annullamento della pubblicazione.
   * Nell&#39;angolo superiore destro della pagina **[!UICONTROL Gestisci pubblicazione - Ambito]**, selezionare **[!UICONTROL Pubblica]** o **[!UICONTROL Annulla pubblicazione]** per avviare l&#39;azione.
1. Selezionare **[!UICONTROL OK]**.

## Controllare lo stato di pubblicazione di una risorsa {#check-publish-status-of-asset}

Puoi utilizzare **[!UICONTROL Timeline]** con **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]** in Experience Manager per verificare rapidamente lo stato di pubblicazione di una risorsa.

**Per verificare lo stato di pubblicazione di una risorsa:**

1. In Experience Manager, nell’angolo superiore sinistro della pagina, seleziona il logo Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro della pagina, seleziona l&#39;icona Navigazione (appena sopra l&#39;icona Strumenti), quindi seleziona **[!UICONTROL Assets]** > **[!UICONTROL File]**.
1. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]** (la schermata seguente mostra la **[!UICONTROL Vista a elenco]**), apri una cartella contenente le risorse pubblicate o non pubblicate.
1. Seleziona una risorsa affinché venga visualizzata con un segno di spunta. Vedi la schermata seguente, ad esempio.
1. Seleziona **[!UICONTROL Timeline]** dal menu a discesa nell&#39;angolo superiore sinistro della pagina. L&#39;area **[!UICONTROL Stato]** nel pannello a sinistra mostra lo stato di pubblicazione della risorsa selezionata.
Quando si utilizza **[!UICONTROL Vista a elenco]**, viene visualizzata una colonna aggiuntiva per lo stato di pubblicazione **[!UICONTROL Dynamic Media]**.
   * Una cartella configurata per la sincronizzazione con Dynamic Media visualizza la colonna **[!UICONTROL Dynamic Media]** per impostazione predefinita.
   * Una cartella *non* configurata per la sincronizzazione con Dynamic Media non visualizza la colonna Dynamic Media.
     ![Visualizzazione elenco e sequenza temporale](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Risoluzione dei problemi di pubblicazione selettiva {#selective-publish-troubleshoot}

Una risorsa non sincronizzata in Dynamic Media ma su cui è attivata un’azione di pubblicazione Dynamic Media genera il messaggio di errore e la soluzione seguenti:

![Errore di pubblicazione selettiva](/help/assets/assets-dm/selective-publish-error.png)
