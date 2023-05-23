---
title: Utilizzo della pubblicazione selettiva in Dynamic Media
description: Puoi scegliere di pubblicare o annullare la pubblicazione delle risorse su o da Adobe Experience Manager o Dynamic Media a livello di cartella. Puoi utilizzare Gestisci pubblicazione o Pubblicazione rapida invece di affidarti esclusivamente alla configurazione di Dynamic Media, le cui impostazioni sono globali per tutte le cartelle nell’istanza di Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: Publishing
source-git-commit: 664e22cc4c6acd74f285a4ec1a0dbd7d301240b7
workflow-type: tm+mt
source-wordcount: '3000'
ht-degree: 4%

---

# Configurare la pubblicazione selettiva a livello di cartella in Dynamic Media {#selective-publish-configure-folder}

Puoi scegliere di pubblicare o annullare la pubblicazione delle risorse su o da Adobe Experience Manager o Dynamic Media a livello di cartella. È possibile utilizzare **[!UICONTROL Gestisci pubblicazione]** o **[!UICONTROL Pubblicazione rapida]** invece di affidarsi esclusivamente al **[!UICONTROL Configurazione Dynamic Media]** le cui impostazioni sono globali per tutte le cartelle nell’istanza di Dynamic Media.

Ad esempio, con la pubblicazione selettiva è possibile lavorare su risorse per prodotti non ancora live. In questo caso, un team di marketing può accedere alle immagini con ritaglio avanzato e alle rappresentazioni dinamiche sincronizzate con Dynamic Media. Possono creare materiali promozionali senza dover pubblicare tali risorse su Dynamic Media per la distribuzione globale.

>[!IMPORTANT]
>
>La pubblicazione selettiva è disponibile solo in modalità Dynamic Media - Scene7.

>[!NOTE]
>
>*Copia* le risorse da e verso le cartelle cancellano lo stato di pubblicazione di tali risorse. Tuttavia, quando *sposta* risorse da e verso cartelle con proprietà cartella impostata su **[!UICONTROL Pubblicazione selettiva]**, lo stato di pubblicazione di tali risorse viene mantenuto.

Se in seguito decidi di modificare **[!UICONTROL Pubblicazione selettiva]** in una cartella, tali modifiche influiscono solo sulle nuove risorse caricate in tale cartella da quel momento in poi. Lo stato di pubblicazione delle risorse esistenti nella cartella rimane invariato finché non le modifichi manualmente da **[!UICONTROL Pubblicazione rapida]** o **[!UICONTROL Gestisci pubblicazione]** .

Livello della cartella **[!UICONTROL Modalità di pubblicazione Dynamic Media]** viene sempre impostato automaticamente sul valore presente nella **[!UICONTROL Pubblicare le risorse]** impostazioni in **[!UICONTROL Configurazione Dynamic Media]**. Nei passaggi seguenti di questo argomento, tuttavia, viene illustrato come modificare manualmente questo valore predefinito a livello di cartella (come descritto nei passaggi seguenti) per ignorare **[!UICONTROL Configurazione Dynamic Media]** valore.

Indipendentemente dal fatto che ci si basi su uno dei seguenti elementi:

* **[!UICONTROL Pubblicare le risorse]** valore impostato in **[!UICONTROL Configurazione Dynamic Media]**.
* **[!UICONTROL Modalità di pubblicazione Dynamic Media]** nelle proprietà a livello di cartella.

Puoi scegliere **[!UICONTROL Immediatamente]**, **[!UICONTROL Al momento dell’attivazione]**, o **[!UICONTROL Pubblicazione selettiva]**. Ad esempio, puoi impostare **[!UICONTROL Pubblicare le risorse]** valore nel tuo **[!UICONTROL Configurazione Dynamic Media]** a **[!UICONTROL Al momento dell’attivazione]**, ma imposta **[!UICONTROL Pubblicazione Dynamic Media]** valore di modalità a livello di cartella su **[!UICONTROL Pubblicazione selettiva]** e viceversa.

Dopo aver configurato la pubblicazione selettiva in una cartella, puoi effettuare una delle seguenti operazioni:

* [Pubblicare selettivamente le risorse in Dynamic Media o Experience Manager tramite Gestisci pubblicazione](#selective-publish-manage-publication).
* [Annullare la pubblicazione selettiva di risorse da Dynamic Media o Experience Manager tramite Gestisci pubblicazione](#selective-unpublish-manage-publication).
* [Pubblicare risorse in Dynamic Media o Experience Manager tramite Pubblicazione rapida](#quick-publish-aem-dm).
* [Pubblicare o annullare la pubblicazione selettiva delle risorse tramite i risultati della ricerca](#selective-publish-unpublish-search-results).

**Per configurare la pubblicazione selettiva a livello di cartella in Dynamic Media:**

1. In Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro, seleziona l’icona Navigazione (appena sopra l’icona Strumenti), quindi fai clic su **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. Effettua una delle operazioni seguenti:
   * Modificare le proprietà di una cartella esistente - In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]**, o **[!UICONTROL Vista a elenco]**, passa a una cartella di cui desideri modificare le proprietà. Seleziona la cartella, quindi nella barra degli strumenti seleziona **[!UICONTROL Proprietà]**.
   * Modificare le proprietà di una nuova cartella - In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]**, o **[!UICONTROL Vista a elenco]**, vicino all’angolo superiore destro della pagina, seleziona **[!UICONTROL Crea]** > **[!UICONTROL Cartella]**. In **[!UICONTROL Crea cartella]** , immettere un titolo (obbligatorio) per la cartella, quindi selezionare **[!UICONTROL Crea]**. Seleziona la cartella, quindi nella barra degli strumenti seleziona **[!UICONTROL Proprietà]**.

1. In **[!UICONTROL Modalità di sincronizzazione]** dall&#39;elenco a discesa, selezionare una delle opzioni seguenti:

   | Modalità di sincronizzazione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Ereditato]** | Nessun valore di sincronizzazione esplicito nella cartella. La cartella eredita invece il valore di sincronizzazione da una delle cartelle precedenti o dalla modalità predefinita impostata nel **[!UICONTROL Configurazione Dynamic Media]**. Stato dettagliato per **[!UICONTROL Ereditato]** viene visualizzato come descrizione comando. |
   | **[!UICONTROL Sincronizza tutto il contenuto di questa sottostruttura di cartelle con Dynamic Media]** | Affinché la pubblicazione in Dynamic Media venga eseguita correttamente, le risorse devono essere sincronizzate in Dynamic Media. Selezionando questa opzione vengono incluse tutte le risorse di questa sottostruttura per la sincronizzazione con Dynamic Media. Le impostazioni specifiche della cartella sovrascrivono l&#39;impostazione predefinita in **[!UICONTROL Configurazione Dynamic Media]**. |
   | **[!UICONTROL Escludi tutto il contenuto di questa sottostruttura di cartelle dalla sincronizzazione di Dynamic Media]** | Escludi tutte le risorse in questa sottostruttura dalla sincronizzazione con Dynamic Media. |

   ![Pubblicazione selettiva a livello di cartella](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. In **[!UICONTROL Modalità di pubblicazione Dynamic Media]** , selezionare un&#39;opzione. Il **[!UICONTROL Modalità di pubblicazione Dynamic Media]** viene sempre impostato automaticamente sul valore impostato nel **[!UICONTROL Configurazione Dynamic Media]**. Tuttavia, potete ignorare manualmente questo valore predefinito **[!UICONTROL Configurazione Dynamic Media]** utilizzando una delle opzioni seguenti.

   >[!IMPORTANT]
   >
   >Indipendentemente dall’opzione selezionata per la modalità Pubblicazione su Dynamic Media, qualsiasi aggiornamento apportato successivamente a una risorsa che è *già* pubblicati, questi aggiornamenti vengono pubblicati immediatamente senza ulteriori azioni da parte dell’utente.
   >
   >Se un video pubblicato viene aggiornato, deve essere pubblicato nuovamente per riflettere le modifiche alla consegna.

   | Opzione modalità di pubblicazione Dynamic Media | Descrizione |
   | --- | --- |
   | **[!UICONTROL Immediatamente]** | Quando le risorse vengono caricate in questa cartella, il sistema acquisisce le risorse in Experience Manager e fornisce immediatamente l’URL/Incorpora. Questa opzione è associata solo alla pubblicazione Experience Manager e non è necessario alcun intervento da parte dell’utente per pubblicare le risorse.<br>Questa opzione è *non* disponibile se hai selezionato **[!UICONTROL Escludi tutto il contenuto di questa sottostruttura di cartelle dalla sincronizzazione di Dynamic Media]** in **[!UICONTROL Modalità di sincronizzazione]** nel passaggio precedente. |
   | **[!UICONTROL All&#39;attivazione]** | Quando le risorse vengono caricate in questa cartella, devi pubblicarle esplicitamente prima di fornire un URL o un collegamento di incorporamento. Questa opzione è associata solo alla pubblicazione Experience Manager.<br>Questa opzione è *non* disponibile se hai selezionato **[!UICONTROL Escludi tutto il contenuto di questa sottostruttura di cartelle dalla sincronizzazione di Dynamic Media]** in **[!UICONTROL Modalità di sincronizzazione]** nel passaggio precedente. |
   | **[!UICONTROL Pubblicazione selettiva]** | Le risorse vengono pubblicate a scelta tra Experience Manager e Dynamic Media per la distribuzione nel dominio pubblico. Entrambi i metodi di pubblicazione si escludono a vicenda. In altre parole, puoi pubblicare le risorse in DMS7 per utilizzare funzioni quali Ritaglio avanzato o rappresentazioni dinamiche. In alternativa, puoi pubblicare le risorse esclusivamente in Experience Manager per una visualizzazione protetta in anteprima; le stesse risorse sono *non* pubblicato in DMS7 per la distribuzione nel dominio pubblico. Questa opzione non è disponibile se hai selezionato **[!UICONTROL Escludi tutto il contenuto di questa sottostruttura di cartelle dalla sincronizzazione di Dynamic Media]** in **[!UICONTROL Modalità di sincronizzazione]** nel passaggio precedente. |

1. Nell’angolo superiore destro della pagina, seleziona **[!UICONTROL Salva e chiudi]**, quindi seleziona **[!UICONTROL OK]** per tornare a Experience Manager Assets.

## Pubblicare selettivamente le risorse in Dynamic Media o Experience Manager tramite Gestisci pubblicazione{#selective-publish-manage-publication}

Prima di usare **[!UICONTROL Gestisci pubblicazione]** per pubblicare selettivamente le risorse su Dynamic Media o Experience Manager, assicurati di aver impostato una delle seguenti opzioni:

* Il **[!UICONTROL Pubblicare le risorse]** opzione in **[!UICONTROL Configurazione Dynamic Media]** a **[!UICONTROL Pubblicazione selettiva]**
* È stata configurata la pubblicazione selettiva a livello di cartella.

Consulta [Creare una configurazione Dynamic Media](#configuring-dynamic-media-cloud-services) o [Configurare la pubblicazione selettiva a livello di cartella in Dynamic Media](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>La pubblicazione selettiva è disponibile solo in modalità Dynamic Media - Scene7.

>[!NOTE]
>
>*Copia* le risorse da e verso le cartelle cancellano lo stato di pubblicazione di tali risorse. Tuttavia, quando *sposta* risorse da e verso cartelle con proprietà cartella impostata su **[!UICONTROL Pubblicazione selettiva]**, lo stato di pubblicazione di tali risorse viene mantenuto.

**Per pubblicare selettivamente le risorse su Dynamic Media o Experience Manager utilizzando Gestisci pubblicazione:**

1. In Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro, seleziona l’icona Navigazione (appena sopra l’icona Strumenti), quindi fai clic su **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. In entrata **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]**, o **[!UICONTROL Vista a elenco]**, eseguire una delle operazioni seguenti:
   * Passa a una cartella di cui desideri pubblicare le risorse. Seleziona la cartella, quindi nella barra degli strumenti seleziona **[!UICONTROL Gestisci pubblicazione]**. Utilizzare **[!UICONTROL Vista a elenco]** in modo da poter controllare più facilmente lo stato di pubblicazione di una particolare cartella.
   * Passa a una cartella di cui desideri pubblicare le risorse. Apri la cartella, quindi seleziona una o più risorse. Sulla barra degli strumenti, seleziona **[!UICONTROL Gestisci pubblicazione]**. Utilizzare **[!UICONTROL Vista a elenco]** in modo da poter controllare più facilmente lo stato di pubblicazione di una particolare risorsa.

      >[!NOTE]
      >
      >Se **[!UICONTROL Gestisci pubblicazione]** non è visibile sulla barra degli strumenti, seleziona il pulsante con i puntini di sospensione, quindi seleziona **[!UICONTROL Gestisci pubblicazione]** dal menu elenco.

1. In **[!UICONTROL Gestisci pubblicazione - Opzioni]** pagina, sotto **[!UICONTROL Azione]**, selezionare il tipo di attivazione desiderato.

   | Azione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Pubblica]** (all’Experience Manager) | Seleziona questa opzione per pubblicare le risorse su Experience Manager per un’anteprima protetta. |
   | **[!UICONTROL Pubblica in Dynamic Media]** | Seleziona questa opzione per pubblicare le risorse in Dynamic Media per la distribuzione nel dominio pubblico o per utilizzare funzioni quali Ritaglio avanzato o rappresentazioni dinamiche.<br>Questa opzione è disponibile solo se **[!UICONTROL Modalità di pubblicazione Dynamic Media]** è impostato su **[!UICONTROL Pubblicazione selettiva]** nelle proprietà della cartella. |

1. Sotto **[!UICONTROL Pianificazione]**, imposta la tempistica della pubblicazione.

   | Pianificazione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Ora]** | Seleziona questa opzione per pubblicare immediatamente le risorse. |
   | **[!UICONTROL Più tardi]** | Seleziona questa opzione per pubblicare le risorse in una data e un’ora specifiche. |

1. Nell&#39;angolo superiore destro del **[!UICONTROL Gestisci pubblicazione]** pagina, seleziona **[!UICONTROL Successivo]**.
1. In **[!UICONTROL Gestisci pubblicazione - Ambito]** eseguire una delle operazioni seguenti:

   * Se necessario, seleziona una o più risorse da rimuovere dalla pubblicazione.
   * Nell&#39;angolo superiore destro del **[!UICONTROL Gestisci pubblicazione - Ambito]** pagina, seleziona **[!UICONTROL Pubblica]** o **[!UICONTROL Pubblica su Dynamic Media]**.
1. Seleziona **[!UICONTROL OK]**.

### Annullare la pubblicazione selettiva di risorse da Dynamic Media o Experience Manager tramite Gestisci pubblicazione {#selective-unpublish-manage-publication}

1. In Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro, seleziona l’icona Navigazione (appena sopra l’icona Strumenti), quindi fai clic su **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. In entrata **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]**, o **[!UICONTROL Vista a elenco]**, eseguire una delle operazioni seguenti:
   * Passa a una cartella di cui desideri annullare la pubblicazione delle risorse. Seleziona la cartella, quindi nella barra degli strumenti seleziona **[!UICONTROL Gestisci pubblicazione]**. Utilizzare **[!UICONTROL Vista a elenco]** in modo da poter controllare più facilmente lo stato di pubblicazione di una particolare cartella.
   * Passa a una cartella di cui desideri annullare la pubblicazione delle risorse. Apri la cartella, quindi seleziona una o più risorse. Sulla barra degli strumenti, seleziona **[!UICONTROL Gestisci pubblicazione]**. Utilizzare **[!UICONTROL Vista a elenco]** in modo da poter controllare più facilmente lo stato di pubblicazione di una particolare risorsa.

      >[!NOTE]
      >
      >Se **[!UICONTROL Gestisci pubblicazione]** non è visibile sulla barra degli strumenti, seleziona il pulsante con i puntini di sospensione, quindi seleziona **[!UICONTROL Gestisci pubblicazione]** dal menu elenco.

1. In **[!UICONTROL Gestisci pubblicazione - Opzioni]** pagina, sotto **[!UICONTROL Azione]**, selezionare il tipo di disattivazione desiderato.

   | Azione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Annulla pubblicazione]** (da Experience Manager) | Seleziona questa opzione se desideri annullare la pubblicazione delle risorse da Experience Manager. |
   | **[!UICONTROL Annulla pubblicazione da Dynamic Media]** | Seleziona questa opzione se desideri annullare la pubblicazione delle risorse da Dynamic Media.<br>Questa opzione è disponibile solo se **[!UICONTROL Modalità di pubblicazione Dynamic Media]** è impostato su **[!UICONTROL Pubblicazione selettiva]** nelle proprietà della cartella. |

1. Sotto **[!UICONTROL Pianificazione]**, imposta la tempistica della disattivazione.

   | Pianificazione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Ora]** | Seleziona questa opzione per annullare subito la pubblicazione delle risorse. |
   | **[!UICONTROL Più tardi]** | Seleziona questa opzione per annullare la pubblicazione delle risorse in una data e un’ora specifiche. |

1. Nell&#39;angolo superiore destro del **[!UICONTROL Gestisci pubblicazione]** pagina, seleziona **[!UICONTROL Successivo]**.
1. In **[!UICONTROL Gestisci pubblicazione - Ambito]** eseguire una delle operazioni seguenti:
   * Seleziona una o più risorse da rimuovere per annullare la pubblicazione.
   * Nell&#39;angolo superiore destro del **[!UICONTROL Gestisci pubblicazione - Ambito]** pagina, seleziona **[!UICONTROL Annulla pubblicazione]** o **[!UICONTROL Annulla pubblicazione da Dynamic Media]**.
1. Seleziona **[!UICONTROL OK]**.

## Pubblicare risorse in Dynamic Media o Experience Manager tramite Pubblicazione rapida {#quick-publish-aem-dm}

È possibile utilizzare **[!UICONTROL Pubblicazione rapida]** per casi semplici di attivazione di risorse. **[!UICONTROL Pubblicazione rapida]** pubblica immediatamente le risorse selezionate senza ulteriori interazioni da parte dell&#39;utente. A causa di questa azione, vengono pubblicati automaticamente anche tutti i riferimenti non pubblicati.

>[!NOTE]
>
>Da utilizzare **[!UICONTROL Pubblicazione rapida]** per pubblicare risorse su Dynamic Media o Experience Manager, assicurati **[!UICONTROL Pubblicazione selettiva]** è abilitato in **[!UICONTROL Configurazione Dynamic Media]** o nelle proprietà della cartella selezionata.

**Per pubblicare le risorse su Dynamic Media o su Experience Manager utilizzando la Pubblicazione rapida:**

1. In Experience Manager, seleziona il logo di Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro della pagina, seleziona l’icona Navigazione (appena sopra l’icona Strumenti), quindi sul lato destro della pagina seleziona **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. In entrata **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]**, o **[!UICONTROL Vista a elenco]**, eseguire una delle operazioni seguenti:
   * Passa a una cartella di cui desideri pubblicare le risorse. Seleziona la cartella, quindi nella barra degli strumenti seleziona **[!UICONTROL Pubblicazione rapida]**. Utilizzare **[!UICONTROL Vista a elenco]** in modo da poter controllare più facilmente lo stato di pubblicazione di una particolare cartella.
   * Passa a una cartella di cui desideri pubblicare le risorse. Apri la cartella, quindi seleziona una o più risorse. Sulla barra degli strumenti, seleziona **[!UICONTROL Pubblicazione rapida]**. Utilizzare **[!UICONTROL Vista a elenco]** in modo da poter controllare più facilmente lo stato di pubblicazione di una particolare risorsa.

      >[!NOTE]
      >
      >Se **[!UICONTROL Pubblicazione rapida]** non è visibile sulla barra degli strumenti, seleziona il pulsante con i puntini di sospensione, quindi seleziona **[!UICONTROL Pubblicazione rapida]** dal menu elenco.

      ![Pubblicazione rapida in Dynamic Media a livello di cartella](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Seleziona una delle seguenti opzioni dalla **[!UICONTROL Pubblicazione rapida]** elenco dei menu.

   | Opzione Pubblicazione rapida | Effetto |
   | --- | --- | 
   | Pubblica su Experience Manager | Pubblica immediatamente su Experience Manager le risorse selezionate. |
   | Pubblica su Brand Portal | Pubblica immediatamente le risorse selezionate in **[!UICONTROL Brand Portal]**.<br>Questa opzione è disponibile solo se l’istanza di Experience Manager Assets **[!UICONTROL Brand Portal]** già configurato. |
   | Pubblica in Dynamic Media | Pubblica immediatamente le risorse selezionate in Dynamic Media.<br>Una risorsa deve essere sincronizzata con Dynamic Media. Se necessario, assicurarsi che **[!UICONTROL Modalità di sincronizzazione]** nelle proprietà di una cartella è già impostato su **[!UICONTROL Sincronizza tutto il contenuto di questa sottostruttura di cartelle con Dynamic Media]**. |

1. Seleziona **[!UICONTROL OK]**, quindi seleziona **[!UICONTROL Chiudi]**.

## Pubblicare o annullare la pubblicazione selettiva delle risorse tramite i risultati della ricerca {#selective-publish-unpublish-search-results}

I risultati della ricerca possono mostrare le risorse di più cartelle di risorse con impostazioni di pubblicazione di Dynamic Media diverse. Se selezioni più risorse dai risultati della ricerca e ciascuna risorsa ha impostazioni diverse della modalità di pubblicazione Dynamic Media, puoi attivare **[!UICONTROL Gestisci pubblicazione]** dalla barra degli strumenti, per pubblicare o annullare la pubblicazione.

Vedi anche [Cercare risorse in Experience Manager](/help/assets/search-assets.md).

**Per pubblicare o annullare la pubblicazione selettiva delle risorse tramite i risultati della ricerca:**

1. Ad Experience Manager, nell’angolo superiore sinistro della pagina, seleziona il logo di Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro della pagina, seleziona l’icona Navigazione (appena sopra l’icona Strumenti), quindi fai clic su **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. Sulla barra degli strumenti, nell&#39;angolo superiore destro della pagina, selezionare l&#39;icona Ricerca (lente di ingrandimento).
1. In **[!UICONTROL Digita per cercare]** testo, immettere una parola chiave, quindi premere **[!UICONTROL Invio]**.
1. Nell&#39;angolo superiore destro della pagina, seleziona la **[!UICONTROL Vista a elenco]** icona.
1. Nell&#39;angolo in alto a sinistra della pagina, seleziona la **[!UICONTROL Filtri]** icona.

   ![Visualizzazione elenco e filtri nei risultati di ricerca](/help/assets/assets-dm/select-publish-search-result.png)

1. Nel pannello a sinistra, espandi **[!UICONTROL Stato]**, quindi espandere **[!UICONTROL Dynamic Media]** predicato di ricerca.
1. Utilizza il **[!UICONTROL Pubblicato]** e **[!UICONTROL Non pubblicato]** caselle di controllo per perfezionare ulteriormente i risultati della ricerca in base allo stato di pubblicazione delle risorse Dynamic Media.
In alternativa, è possibile utilizzare queste caselle di controllo con **[!UICONTROL Pubblica]** predicato di ricerca per perfezionare i risultati della ricerca di **[!UICONTROL Pubblicato]** e **[!UICONTROL Non pubblicato]** Experience Manager di risorse.
1. Effettua una delle operazioni seguenti:
   * Seleziona una o più risorse da pubblicare o di cui annullare la pubblicazione.
   * Vicino all&#39;angolo superiore destro del **[!UICONTROL Risultati di ricerca]** pagina, seleziona **[!UICONTROL Seleziona tutto]**.
1. Sulla barra degli strumenti, seleziona **[!UICONTROL Gestisci pubblicazione]**. Seleziona l’icona con i puntini di sospensione sulla barra degli strumenti per aprire **[!UICONTROL Gestisci pubblicazione]**.
1. Il giorno **[!UICONTROL Gestisci pubblicazione - Opzioni]** , selezionare l&#39;azione desiderata.

   | Azione selezionata | Impostazione Publish Assets (Pubblica risorse) nella configurazione del Dynamic Media | Le risorse sono |
   | --- | --- | --- |
   | Pubblicazione | Immediatamente o Al momento dell&#39;attivazione | Pubblicato in Experience Manager e Dynamic Media. |
   | Pubblicazione | Pubblicazione selettiva | Pubblicato solo su Experience Manager. |
   | Annulla pubblicazione | Immediatamente o Al momento dell&#39;attivazione | Non più pubblicato su Experience Manager e Dynamic Media. |
   | Annulla pubblicazione | Pubblicazione selettiva | Pubblicazione annullata solo da Experience Manager. |
   | Pubblica in Dynamic Media | Immediatamente o Al momento dell&#39;attivazione | Non pubblicato su Experience Manager, Dynamic Media o entrambi. |
   | Pubblica in Dynamic Media | Pubblicazione selettiva | Pubblicato solo in Dynamic Media. |
   | Annulla pubblicazione da Dynamic Media | Immediatamente o Al momento dell&#39;attivazione | Pubblicazione non annullata da Experience Manager, Dynamic Media o entrambi. |
   | Annulla pubblicazione da Dynamic Media | Pubblicazione selettiva | Pubblicazione annullata solo da Dynamic Media. |

1. Sotto **[!UICONTROL Pianificazione]**, imposta la tempistica della disattivazione.

   | Pianificazione selezionata | Cosa succede |
   | --- | --- |
   | Ora | L&#39;azione selezionata viene eseguita immediatamente. |
   | Più tardi | L&#39;azione selezionata viene eseguita nella data e ora specifiche selezionate. |

1. Nell&#39;angolo superiore destro del **[!UICONTROL Gestisci pubblicazione - Opzioni]** pagina, seleziona **[!UICONTROL Successivo]**.
1. (Facoltativo) In **[!UICONTROL Gestisci pubblicazione - Ambito]** , controlla la **[!UICONTROL Destinazione pubblicazione]** nella tabella per le risorse selezionate.

   | Impostazione Publish Assets (Pubblica risorse) nella configurazione del Dynamic Media | Azione selezionata | Destinazione pubblicazione |
   | --- | --- | --- |
   | Immediatamente o <br>All&#39;attivazione | Pubblicazione | EXPERIENCE MANAGER e DYNAMIC MEDIA |
   | Immediatamente o <br>All&#39;attivazione | Pubblica in Dynamic Media | Nessuno |
   | Pubblicazione selettiva | Pubblicazione | Experience Manager |
   | Pubblicazione selettiva | Pubblica in Dynamic Media | Dynamic Media |
   | Immediatamente o <br>All&#39;attivazione | Annulla pubblicazione | EXPERIENCE MANAGER e DYNAMIC MEDIA |
   | Immediatamente o <br>All&#39;attivazione | Annulla pubblicazione da Dynamic Media | Nessuno |
   | Pubblicazione selettiva | Annulla pubblicazione | Experience Manager |
   | Pubblicazione selettiva | Annulla pubblicazione da Dynamic Media | Dynamic Media |

1. In **[!UICONTROL Gestisci pubblicazione - Ambito]** eseguire una delle operazioni seguenti:
   * Seleziona una o più risorse da rimuovere dalla pubblicazione o dall’annullamento della pubblicazione.
   * Nell&#39;angolo superiore destro del **[!UICONTROL Gestisci pubblicazione - Ambito]** pagina, seleziona **[!UICONTROL Pubblica]** o **[!UICONTROL Annulla pubblicazione]** per iniziare l’azione.
1. Seleziona **[!UICONTROL OK]**.

## Controllare lo stato di pubblicazione di una risorsa {#check-publish-status-of-asset}

È possibile utilizzare **[!UICONTROL Timeline]** con **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]**, o **[!UICONTROL Vista a elenco]** nell’Experience Manager per verificare rapidamente lo stato di pubblicazione di una risorsa.

**Per verificare lo stato di pubblicazione di una risorsa:**

1. Ad Experience Manager, nell’angolo superiore sinistro della pagina, seleziona il logo di Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro della pagina, seleziona l’icona Navigazione (appena sopra l’icona Strumenti), quindi fai clic su **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. In entrata **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]**, o **[!UICONTROL Vista a elenco]** (la schermata seguente mostra **[!UICONTROL Vista a elenco]**), apri una cartella contenente le risorse pubblicate o di cui hai annullato la pubblicazione.
1. Seleziona una risorsa affinché venga visualizzata con un segno di spunta. Vedi la schermata seguente, ad esempio.
1. Nell’angolo in alto a sinistra della pagina, dal menu a discesa, seleziona **[!UICONTROL Timeline]**. Il **[!UICONTROL Stato]** nel pannello a sinistra, l’area mostra lo stato di pubblicazione della risorsa selezionata.
Quando si utilizza **[!UICONTROL Vista a elenco]**, una colonna aggiuntiva per **[!UICONTROL Dynamic Media]** stato di pubblicazione.
   * Una cartella configurata per la sincronizzazione con Dynamic Media visualizza **[!UICONTROL Dynamic Media]** per impostazione predefinita.
   * Una cartella che è *non* configurato per la sincronizzazione con Dynamic Media non visualizza la colonna Dynamic Media.
      ![Vista a elenco e timeline](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Risoluzione dei problemi di pubblicazione selettiva {#selective-publish-troubleshoot}

Una risorsa non sincronizzata in Dynamic Media ma su cui è attivata un’azione di pubblicazione Dynamic Media genera il messaggio di errore e la soluzione seguenti:

![Errore di pubblicazione selettiva](/help/assets/assets-dm/selective-publish-error.png)
