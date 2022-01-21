---
title: Utilizzo della pubblicazione selettiva in Dynamic Media
description: Puoi scegliere di pubblicare o annullare la pubblicazione delle risorse su o da Adobe Experience Manager o Dynamic Media a livello di cartella. Puoi utilizzare Gestisci pubblicazione o Pubblicazione rapida invece di affidarti esclusivamente alla configurazione Dynamic Media le cui impostazioni sono globali per tutte le cartelle nell’istanza Dynamic Media.
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

Puoi scegliere di pubblicare o annullare la pubblicazione delle risorse su o da Adobe Experience Manager o Dynamic Media a livello di cartella. Puoi utilizzare **[!UICONTROL Gestisci pubblicazione]** o **[!UICONTROL Pubblicazione rapida]** invece di affidarsi esclusivamente al **[!UICONTROL Configurazione Dynamic Media]** le cui impostazioni sono globali per tutte le cartelle nell’istanza di Dynamic Media.

Ad esempio, con la pubblicazione selettiva puoi lavorare sulle risorse per i prodotti che non sono ancora in diretta. In questo caso, un team di marketing può accedere alle immagini di ritaglio avanzato e alle rappresentazioni dinamiche sincronizzate con Dynamic Media. Possono creare materiali promozionali senza dover pubblicare tali risorse in Dynamic Media per la distribuzione globale.

>[!IMPORTANT]
>
>La pubblicazione selettiva è disponibile solo in modalità Dynamic Media - Scene7.

>[!NOTE]
>
>*Copia* le risorse in e da cartelle cancellano lo stato di pubblicazione di tali risorse. Tuttavia, quando *spostare* risorse da e verso le cartelle la cui proprietà di cartella è impostata su **[!UICONTROL Pubblicazione selettiva]**, lo stato di pubblicazione di tali risorse viene mantenuto.

Se decidi successivamente di modificare il **[!UICONTROL Pubblicazione selettiva]** in una cartella, queste modifiche influiscono solo sulle nuove risorse caricate in tale cartella da quel momento in poi. Lo stato di pubblicazione delle risorse esistenti nella cartella rimane invariato finché non le cambi manualmente da **[!UICONTROL Pubblicazione rapida]** o **[!UICONTROL Gestisci pubblicazione]** finestra di dialogo.

Livello della cartella **[!UICONTROL Modalità di pubblicazione Dynamic Media]** l&#39;opzione viene sempre impostata come predefinita sul valore trovato nella **[!UICONTROL Pubblicare le risorse]** impostazione nella **[!UICONTROL Configurazione Dynamic Media]**. I passaggi seguenti in questo argomento, tuttavia, mostrano come modificare manualmente questo valore predefinito a livello di cartella (come descritto nei passaggi seguenti) per sostituire il **[!UICONTROL Configurazione Dynamic Media]** valore.

Indipendentemente dal fatto che vi affidate a uno dei seguenti elementi:

* **[!UICONTROL Pubblicare le risorse]** valore impostato in **[!UICONTROL Configurazione Dynamic Media]**.
* **[!UICONTROL Modalità di pubblicazione Dynamic Media]** impostato nelle proprietà a livello di cartella.

Puoi scegliere **[!UICONTROL Immediatamente]**, **[!UICONTROL All&#39;attivazione]** oppure **[!UICONTROL Pubblicazione selettiva]**. Ad esempio, puoi impostare la **[!UICONTROL Pubblicare le risorse]** nella **[!UICONTROL Configurazione Dynamic Media]** a **[!UICONTROL All&#39;attivazione]**, ma imposta **[!UICONTROL Pubblicazione Dynamic Media]** valore della modalità a livello di cartella su **[!UICONTROL Pubblicazione selettiva]** e viceversa.

Dopo aver configurato la pubblicazione selettiva in una cartella, puoi effettuare una delle seguenti operazioni:

* [Pubblicare in modo selettivo le risorse in Dynamic Media o Experience Manager utilizzando Gestisci pubblicazione](#selective-publish-manage-publication).
* [Annullare selettivamente la pubblicazione delle risorse da Dynamic Media o Experience Manager tramite Gestisci pubblicazione](#selective-unpublish-manage-publication).
* [Pubblicare risorse in Dynamic Media o Experience Manager tramite Pubblicazione rapida](#quick-publish-aem-dm).
* [Pubblicare o annullare selettivamente la pubblicazione delle risorse tramite i risultati della ricerca](#selective-publish-unpublish-search-results).

**Per configurare la pubblicazione selettiva a livello di cartella in Dynamic Media:**

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro, seleziona l’icona Navigazione (appena sopra l’icona Strumenti ), quindi seleziona **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. Effettua una delle operazioni seguenti:
   * Modifica le proprietà di una cartella esistente - In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** oppure **[!UICONTROL Vista a elenco]**, passa a una cartella di cui desideri modificare le proprietà. Seleziona la cartella, quindi seleziona nella barra degli strumenti **[!UICONTROL Proprietà]**.
   * Modifica le proprietà di una nuova cartella - In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** oppure **[!UICONTROL Vista a elenco]**, nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Crea]** > **[!UICONTROL Cartella]**. In **[!UICONTROL Crea cartella]** immettere un titolo (obbligatorio) per la cartella, quindi selezionare **[!UICONTROL Crea]**. Seleziona la cartella, quindi seleziona nella barra degli strumenti **[!UICONTROL Proprietà]**.

1. In **[!UICONTROL Modalità di sincronizzazione]** dall’elenco a discesa, selezionare una delle opzioni seguenti:

   | Modalità di sincronizzazione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Ereditato]** | Nessun valore di sincronizzazione esplicito sulla cartella; la cartella eredita invece il valore di sincronizzazione da una delle cartelle precedenti o dalla modalità predefinita impostata nel **[!UICONTROL Configurazione Dynamic Media]**. Lo stato dettagliato di **[!UICONTROL Ereditato]** viene visualizzato tramite una descrizione comandi. |
   | **[!UICONTROL Sincronizza tutti gli elementi nella sottostruttura cartelle in Dynamic Media]** | Affinché la pubblicazione in Dynamic Media abbia successo, le risorse devono essere sincronizzate in Dynamic Media. Selezionando questa opzione vengono incluse tutte le risorse presenti nella sottostruttura per la sincronizzazione con Dynamic Media. Le impostazioni specifiche per la cartella sostituiscono l’impostazione predefinita nella **[!UICONTROL Configurazione Dynamic Media]**. |
   | **[!UICONTROL Escludere tutto ciò che si trova nella sottostruttura della cartella dalla sincronizzazione Dynamic Media]** | Escludere tutte le risorse presenti in questa sottostruttura dalla sincronizzazione con Dynamic Media. |

   ![Pubblicazione selettiva a livello di cartella](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. In **[!UICONTROL Modalità di pubblicazione Dynamic Media]** dall’elenco a discesa, seleziona un’opzione. La **[!UICONTROL Modalità di pubblicazione Dynamic Media]** viene sempre impostato il valore predefinito nel **[!UICONTROL Configurazione Dynamic Media]**. È tuttavia possibile ignorare manualmente questa impostazione predefinita **[!UICONTROL Configurazione Dynamic Media]** utilizzando una delle opzioni seguenti.

   >[!IMPORTANT]
   >
   >Indipendentemente dall’opzione della modalità di pubblicazione di Dynamic Media selezionata, eventuali aggiornamenti apportati successivamente a una risorsa che è *già* pubblicati, tali aggiornamenti vengono pubblicati immediatamente senza ulteriori azioni da parte dell’utente.
   >
   >Se un video pubblicato viene aggiornato, deve essere pubblicato di nuovo per riflettere le modifiche alla consegna.

   | Opzione della modalità di pubblicazione Dynamic Media | Descrizione |
   | --- | --- |
   | **[!UICONTROL Immediatamente]** | Quando le risorse vengono caricate in questa cartella, il sistema le inserisce in Experience Manager e fornisce l’URL/Incorpora all’istante. Questa opzione è legata solo alla pubblicazione di Experienci Manager e non è necessario alcun intervento dell’utente per pubblicare le risorse.<br>Questa opzione è *not* disponibile se hai selezionato **[!UICONTROL Escludere tutto ciò che si trova nella sottostruttura della cartella dalla sincronizzazione Dynamic Media]** in **[!UICONTROL Modalità di sincronizzazione]** nel passaggio precedente. |
   | **[!UICONTROL All&#39;attivazione]** | Quando le risorse vengono caricate in questa cartella, devi pubblicare esplicitamente la risorsa prima di fornire un collegamento URL/Incorpora . Questa opzione è legata solo alla pubblicazione di Experienci Manager.<br>Questa opzione è *not* disponibile se hai selezionato **[!UICONTROL Escludere tutto ciò che si trova nella sottostruttura della cartella dalla sincronizzazione Dynamic Media]** in **[!UICONTROL Modalità di sincronizzazione]** nel passaggio precedente. |
   | **[!UICONTROL Pubblicazione selettiva]** | Le risorse vengono pubblicate come Experience Manager desiderato o su Dynamic Media per la distribuzione nel dominio pubblico. Entrambi i metodi di pubblicazione si escludono a vicenda. In altre parole, puoi pubblicare le risorse in DMS7 in modo da poter utilizzare funzioni quali Ritaglio avanzato o rappresentazioni dinamiche. Oppure puoi pubblicare le risorse esclusivamente in Experience Manager per un’anteprima sicura; le stesse attività *not* pubblicato in DMS7 per la distribuzione nel dominio pubblico. Questa opzione non è disponibile se è selezionata **[!UICONTROL Escludere tutto ciò che si trova nella sottostruttura della cartella dalla sincronizzazione Dynamic Media]** in **[!UICONTROL Modalità di sincronizzazione]** nel passaggio precedente. |

1. Nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Salva e chiudi]**, quindi seleziona **[!UICONTROL OK]** per tornare a Experience Manager Assets.

## Pubblicare in modo selettivo le risorse in Dynamic Media o Experience Manager utilizzando Gestisci pubblicazione{#selective-publish-manage-publication}

Prima di utilizzare **[!UICONTROL Gestisci pubblicazione]** per pubblicare selettivamente le risorse in Dynamic Media o Experience Manager, accertati di aver impostato una delle seguenti opzioni:

* La **[!UICONTROL Pubblicare le risorse]** opzione in **[!UICONTROL Configurazione Dynamic Media]** a **[!UICONTROL Pubblicazione selettiva]**
* È stata configurata la pubblicazione selettiva a livello di cartella.

Vedi [Creare una configurazione Dynamic Media](#configuring-dynamic-media-cloud-services) o [Configurare la pubblicazione selettiva a livello di cartella in Dynamic Media](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>La pubblicazione selettiva è disponibile solo in modalità Dynamic Media - Scene7.

>[!NOTE]
>
>*Copia* le risorse in e da cartelle cancellano lo stato di pubblicazione di tali risorse. Tuttavia, quando *spostare* risorse da e verso le cartelle la cui proprietà di cartella è impostata su **[!UICONTROL Pubblicazione selettiva]**, lo stato di pubblicazione di tali risorse viene mantenuto.

**Per pubblicare selettivamente le risorse in Dynamic Media o Experience Manager utilizzando Gestisci pubblicazione:**

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro, seleziona l’icona Navigazione (appena sopra l’icona Strumenti ), quindi seleziona **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** oppure **[!UICONTROL Vista a elenco]**, effettua una delle seguenti operazioni:
   * Passa a una cartella di cui desideri pubblicare le risorse. Seleziona la cartella, quindi seleziona nella barra degli strumenti **[!UICONTROL Gestisci pubblicazione]**. Utilizzo **[!UICONTROL Vista a elenco]** puoi controllare più facilmente lo stato di pubblicazione di una particolare cartella.
   * Passa a una cartella di cui desideri pubblicare le risorse. Apri la cartella, quindi seleziona una o più risorse. Sulla barra degli strumenti, seleziona **[!UICONTROL Gestisci pubblicazione]**. Utilizzo **[!UICONTROL Vista a elenco]** puoi controllare più facilmente lo stato di pubblicazione di una particolare risorsa.

      >[!NOTE]
      >
      >Se **[!UICONTROL Gestisci pubblicazione]** non visualizzato sulla barra degli strumenti, seleziona il pulsante con i puntini di sospensione, quindi seleziona **[!UICONTROL Gestisci pubblicazione]** dal menu elenco.

1. In **[!UICONTROL Gestisci pubblicazione - Opzioni]** pagina, sotto **[!UICONTROL Azione]**, seleziona il tipo di attivazione desiderato.

   | Azione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Pubblica]** (all&#39;Experience Manager) | Seleziona questa opzione per pubblicare le risorse in Experience Manager per l’anteprima protetta. |
   | **[!UICONTROL Pubblica in Dynamic Media]** | Seleziona questa opzione per pubblicare le risorse in Dynamic Media per la distribuzione nel dominio pubblico o per utilizzare funzioni quali Ritaglio avanzato o rappresentazioni dinamiche.<br>Questa opzione è disponibile solo se **[!UICONTROL Modalità di pubblicazione Dynamic Media]** è impostato su **[!UICONTROL Pubblicazione selettiva]** nelle proprietà della cartella. |

1. Sotto **[!UICONTROL Pianificazione]**, imposta la tempistica della pubblicazione.

   | Pianificazione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Ora]** | Seleziona per pubblicare immediatamente le risorse. |
   | **[!UICONTROL Più tardi]** | Seleziona per pubblicare le risorse in una data e in un’ora specifiche. |

1. Nell&#39;angolo in alto a destra del **[!UICONTROL Gestisci pubblicazione]** pagina, seleziona **[!UICONTROL Successivo]**.
1. In **[!UICONTROL Gestisci pubblicazione - Ambito]** eseguire una delle operazioni seguenti:

   * Se necessario, seleziona una o più risorse da rimuovere dalla pubblicazione.
   * Nell&#39;angolo in alto a destra del **[!UICONTROL Gestisci pubblicazione - Ambito]** pagina, seleziona **[!UICONTROL Pubblica]** o **[!UICONTROL Pubblicare su Dynamic Media]**.
1. Seleziona **[!UICONTROL OK]**.

### Annullare selettivamente la pubblicazione delle risorse da Dynamic Media o Experience Manager tramite Gestisci pubblicazione {#selective-unpublish-manage-publication}

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro, seleziona l’icona Navigazione (appena sopra l’icona Strumenti ), quindi seleziona **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** oppure **[!UICONTROL Vista a elenco]**, effettua una delle seguenti operazioni:
   * Passa a una cartella di cui desideri annullare la pubblicazione delle risorse. Seleziona la cartella, quindi seleziona nella barra degli strumenti **[!UICONTROL Gestisci pubblicazione]**. Utilizzo **[!UICONTROL Vista a elenco]** puoi controllare più facilmente lo stato di pubblicazione di una particolare cartella.
   * Passa a una cartella di cui desideri annullare la pubblicazione delle risorse. Apri la cartella, quindi seleziona una o più risorse. Sulla barra degli strumenti, seleziona **[!UICONTROL Gestisci pubblicazione]**. Utilizzo **[!UICONTROL Vista a elenco]** puoi controllare più facilmente lo stato di pubblicazione di una particolare risorsa.

      >[!NOTE]
      >
      >Se **[!UICONTROL Gestisci pubblicazione]** non visualizzato sulla barra degli strumenti, seleziona il pulsante con i puntini di sospensione, quindi seleziona **[!UICONTROL Gestisci pubblicazione]** dal menu elenco.

1. In **[!UICONTROL Gestisci pubblicazione - Opzioni]** pagina, sotto **[!UICONTROL Azione]**, seleziona il tipo di disattivazione desiderato.

   | Azione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Annulla pubblicazione]** (dall&#39;Experience Manager) | Seleziona questa opzione se desideri annullare la pubblicazione delle risorse dall’Experience Manager. |
   | **[!UICONTROL Annulla pubblicazione da Dynamic Media]** | Seleziona questa opzione se desideri annullare la pubblicazione delle risorse da Dynamic Media.<br>Questa opzione è disponibile solo se **[!UICONTROL Modalità di pubblicazione Dynamic Media]** è impostato su **[!UICONTROL Pubblicazione selettiva]** nelle proprietà della cartella. |

1. Sotto **[!UICONTROL Pianificazione]**, imposta la tempistica della disattivazione.

   | Pianificazione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Ora]** | Seleziona per annullare immediatamente la pubblicazione delle risorse. |
   | **[!UICONTROL Più tardi]** | Seleziona per annullare la pubblicazione delle risorse in una data e in un’ora specifiche. |

1. Nell&#39;angolo in alto a destra del **[!UICONTROL Gestisci pubblicazione]** pagina, seleziona **[!UICONTROL Successivo]**.
1. In **[!UICONTROL Gestisci pubblicazione - Ambito]** eseguire una delle operazioni seguenti:
   * Seleziona una o più risorse da rimuovere dall’annullamento della pubblicazione.
   * Nell&#39;angolo in alto a destra del **[!UICONTROL Gestisci pubblicazione - Ambito]** pagina, seleziona **[!UICONTROL Annulla pubblicazione]** o **[!UICONTROL Annulla pubblicazione da Dynamic Media]**.
1. Seleziona **[!UICONTROL OK]**.

## Pubblicare risorse in Dynamic Media o Experience Manager tramite Pubblicazione rapida {#quick-publish-aem-dm}

È possibile utilizzare **[!UICONTROL Pubblicazione rapida]** per casi semplici di attivazione delle risorse. **[!UICONTROL Pubblicazione rapida]** pubblica immediatamente le risorse selezionate senza ulteriore interazione da parte dell’utente. A causa di questa azione, vengono pubblicati automaticamente anche tutti i riferimenti non pubblicati.

>[!NOTE]
>
>Per utilizzare **[!UICONTROL Pubblicazione rapida]** per pubblicare risorse in Dynamic Media o Experience Manager, assicurati **[!UICONTROL Pubblicazione selettiva]** è abilitato nella **[!UICONTROL Configurazione Dynamic Media]** o nelle proprietà della cartella selezionata.

**Per pubblicare le risorse in Dynamic Media o Experience Manager utilizzando Pubblicazione rapida:**

1. In Experience Manager, seleziona il logo Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro della pagina, seleziona l’icona Navigazione (appena sopra l’icona Strumenti ), quindi sul lato destro della pagina seleziona **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** oppure **[!UICONTROL Vista a elenco]**, effettua una delle seguenti operazioni:
   * Passa a una cartella di cui desideri pubblicare le risorse. Seleziona la cartella, quindi seleziona nella barra degli strumenti **[!UICONTROL Pubblicazione rapida]**. Utilizzo **[!UICONTROL Vista a elenco]** puoi controllare più facilmente lo stato di pubblicazione di una particolare cartella.
   * Passa a una cartella di cui desideri pubblicare le risorse. Apri la cartella, quindi seleziona una o più risorse. Sulla barra degli strumenti, seleziona **[!UICONTROL Pubblicazione rapida]**. Utilizzo **[!UICONTROL Vista a elenco]** puoi controllare più facilmente lo stato di pubblicazione di una particolare risorsa.

      >[!NOTE]
      >
      >Se **[!UICONTROL Pubblicazione rapida]** non visualizzato sulla barra degli strumenti, seleziona il pulsante con i puntini di sospensione, quindi seleziona **[!UICONTROL Pubblicazione rapida]** dal menu elenco.

      ![Pubblicazione rapida a livello di cartella in Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Seleziona una delle seguenti opzioni dalla **[!UICONTROL Pubblicazione rapida]** elenco menu.

   | Opzione Pubblicazione rapida | Effetto |
   | --- | --- | 
   | Pubblica in Experience Manager | Pubblica immediatamente ad Experience Manager le risorse selezionate. |
   | Pubblica su Brand Portal | Pubblica immediatamente le risorse selezionate in **[!UICONTROL Brand Portal]**.<br>Questa opzione è disponibile solo se l’istanza di Experience Manager Assets ha **[!UICONTROL Brand Portal]** già configurato. |
   | Pubblica in Dynamic Media | Pubblica immediatamente le risorse selezionate in Dynamic Media.<br>Una risorsa deve essere sincronizzata in Dynamic Media. Se necessario, assicurati che **[!UICONTROL Modalità di sincronizzazione]** nelle proprietà di una cartella è già impostato su **[!UICONTROL Sincronizza tutti gli elementi nella sottostruttura cartelle in Dynamic Media]**. |

1. Seleziona **[!UICONTROL OK]**, quindi seleziona **[!UICONTROL Chiudi]**.

## Pubblicare o annullare selettivamente la pubblicazione delle risorse tramite i risultati della ricerca {#selective-publish-unpublish-search-results}

I risultati della ricerca possono mostrare risorse da più cartelle di risorse che hanno diverse impostazioni di pubblicazione di Dynamic Media. Quando selezioni più risorse dai risultati della ricerca e ogni risorsa ha diverse impostazioni della modalità di pubblicazione di Dynamic Media, puoi attivare **[!UICONTROL Gestisci pubblicazione]** dalla barra degli strumenti, per pubblicare o annullare la pubblicazione.

Vedi anche [Cercare risorse in Experience Manager](/help/assets/search-assets.md).

**Per pubblicare o annullare selettivamente la pubblicazione delle risorse tramite i risultati della ricerca:**

1. Ad Experience Manager, nell’angolo in alto a sinistra della pagina, seleziona il logo Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro della pagina, seleziona l’icona Navigazione (appena sopra l’icona Strumenti ), quindi seleziona **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. Nella barra degli strumenti, nell’angolo superiore destro della pagina, seleziona l’icona Ricerca (lente di ingrandimento).
1. In **[!UICONTROL Digitare per cercare]** campo di testo, immettere una parola chiave, quindi premere **[!UICONTROL Invio]**.
1. Seleziona l’ **[!UICONTROL Vista a elenco]** icona.
1. Seleziona l’ **[!UICONTROL Filtri]** icona.

   ![Visualizzazione a elenco e filtri nei risultati della ricerca](/help/assets/assets-dm/select-publish-search-result.png)

1. Nel pannello a sinistra, espandi **[!UICONTROL Stato]**, quindi espandi la **[!UICONTROL Dynamic Media]** predicato di ricerca.
1. Utilizza la **[!UICONTROL Pubblicato]** e **[!UICONTROL Non pubblicato]** caselle di controllo per perfezionare ulteriormente i risultati della ricerca in base allo stato pubblicato delle risorse Dynamic Media.
Facoltativamente, è possibile utilizzare queste caselle di controllo con **[!UICONTROL Pubblica]** predicato di ricerca per perfezionare i risultati di ricerca di **[!UICONTROL Pubblicato]** e **[!UICONTROL Non pubblicato]** Experience Manager di risorse.
1. Effettua una delle operazioni seguenti:
   * Seleziona una o più risorse da pubblicare o di cui annullare la pubblicazione.
   * Vicino all&#39;angolo superiore destro del **[!UICONTROL Risultati ricerca]** pagina, seleziona **[!UICONTROL Seleziona tutto]**.
1. Sulla barra degli strumenti, seleziona **[!UICONTROL Gestisci pubblicazione]**. Seleziona l’icona dei puntini di sospensione nella barra degli strumenti per aprire **[!UICONTROL Gestisci pubblicazione]**.
1. Sulla **[!UICONTROL Gestisci pubblicazione - Opzioni]** , seleziona l’azione desiderata.

   | Azione selezionata | Impostazione Publish Assets in Dynamic Media Configuration | Risorse |
   | --- | --- | --- |
   | Pubblicazione | Immediatamente o al momento dell&#39;attivazione | Pubblicato in Experience Manager e Dynamic Media. |
   | Pubblicazione | Pubblicazione selettiva | Pubblicato solo in Experience Manager. |
   | Annulla pubblicazione | Immediatamente o al momento dell&#39;attivazione | Non pubblicato da Experience Manager e Dynamic Media. |
   | Annulla pubblicazione | Pubblicazione selettiva | Non pubblicato solo da Experience Manager. |
   | Pubblica in Dynamic Media | Immediatamente o al momento dell&#39;attivazione | Non pubblicato in Experience Manager, Dynamic Media o entrambi. |
   | Pubblica in Dynamic Media | Pubblicazione selettiva | Pubblicato solo in Dynamic Media. |
   | Annulla pubblicazione da Dynamic Media | Immediatamente o al momento dell&#39;attivazione | Non viene annullata la pubblicazione da Experience Manager, Dynamic Media o entrambi. |
   | Annulla pubblicazione da Dynamic Media | Pubblicazione selettiva | Non pubblicato solo da Dynamic Media. |

1. Sotto **[!UICONTROL Pianificazione]**, imposta la tempistica della disattivazione.

   | Pianificazione selezionata | Cosa accade |
   | --- | --- |
   | Ora | L’azione selezionata viene eseguita immediatamente. |
   | Più tardi | L’azione selezionata viene eseguita alla data e all’ora specifiche selezionate. |

1. Nell&#39;angolo in alto a destra del **[!UICONTROL Gestisci pubblicazione - Opzioni]** pagina, seleziona **[!UICONTROL Successivo]**.
1. (Facoltativo) In **[!UICONTROL Gestisci pubblicazione - Ambito]** pagina, controlla **[!UICONTROL Pubblicare Target]** nella tabella per le risorse selezionate.

   | Impostazione Publish Assets in Dynamic Media Configuration | Azione selezionata | Destinazione pubblicazione |
   | --- | --- | --- |
   | Immediatamente o <br>All&#39;attivazione | Pubblicazione | Experience Manager e Dynamic Media |
   | Immediatamente o <br>All&#39;attivazione | Pubblica in Dynamic Media | Nessuno |
   | Pubblicazione selettiva | Pubblicazione | Experience Manager |
   | Pubblicazione selettiva | Pubblica in Dynamic Media | Dynamic Media |
   | Immediatamente o <br>All&#39;attivazione | Annulla pubblicazione | Experience Manager e Dynamic Media |
   | Immediatamente o <br>All&#39;attivazione | Annulla pubblicazione da Dynamic Media | Nessuno |
   | Pubblicazione selettiva | Annulla pubblicazione | Experience Manager |
   | Pubblicazione selettiva | Annulla pubblicazione da Dynamic Media | Dynamic Media |

1. In **[!UICONTROL Gestisci pubblicazione - Ambito]** eseguire una delle operazioni seguenti:
   * Seleziona una o più risorse da rimuovere dalla pubblicazione o dall’annullamento della pubblicazione.
   * Nell&#39;angolo in alto a destra del **[!UICONTROL Gestisci pubblicazione - Ambito]** pagina, seleziona **[!UICONTROL Pubblica]** o **[!UICONTROL Annulla pubblicazione]** per iniziare l&#39;azione.
1. Seleziona **[!UICONTROL OK]**.

## Controllare lo stato di pubblicazione di una risorsa {#check-publish-status-of-asset}

È possibile utilizzare **[!UICONTROL Timeline]** con **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** oppure **[!UICONTROL Vista a elenco]** in Experience Manager per controllare rapidamente lo stato di pubblicazione di una risorsa.

**Per controllare lo stato di pubblicazione di una risorsa:**

1. Ad Experience Manager, nell’angolo in alto a sinistra della pagina, seleziona il logo Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro della pagina, seleziona l’icona Navigazione (appena sopra l’icona Strumenti ), quindi seleziona **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** oppure **[!UICONTROL Vista a elenco]** (la schermata sottostante mostra **[!UICONTROL Vista a elenco]**), apri una cartella contenente le risorse pubblicate o di cui hai annullato la pubblicazione.
1. Seleziona una risorsa in modo che venga visualizzata con un segno di spunta. Vedi la schermata sottostante per esempio.
1. Seleziona dal menu a discesa accanto all’angolo superiore sinistro della pagina. **[!UICONTROL Timeline]**. La **[!UICONTROL Stato]** nel pannello a sinistra mostra lo stato di pubblicazione della risorsa selezionata.
Quando utilizzi **[!UICONTROL Vista a elenco]**, una colonna aggiuntiva per **[!UICONTROL Dynamic Media]** viene visualizzato lo stato di pubblicazione.
   * In una cartella configurata per la sincronizzazione con Dynamic Media viene visualizzata la **[!UICONTROL Dynamic Media]** per impostazione predefinita.
   * Una cartella *not* configurato per la sincronizzazione con Dynamic Media non visualizza la colonna Dynamic Media.
      ![Vista a elenco e Timeline](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Risolvere i problemi relativi alla pubblicazione selettiva {#selective-publish-troubleshoot}

Una risorsa che non è sincronizzata con Dynamic Media ma su cui è attivata un’azione di pubblicazione Dynamic Media restituisce il seguente messaggio di errore e soluzione:

![Errore di pubblicazione selettiva](/help/assets/assets-dm/selective-publish-error.png)
