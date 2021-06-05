---
title: Utilizzo della pubblicazione selettiva in Dynamic Media
description: Informazioni su come utilizzare Pubblicazione selettiva in Dynamic Media.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: Business Practitioner, Administrator
exl-id: cd025e9d-6fb1-436c-9e78-795f2daaf345
feature: Pubblicazione
source-git-commit: 1349d9929fc64ad46fc91f0d189bab54cca9de81
workflow-type: tm+mt
source-wordcount: '2944'
ht-degree: 4%

---

# Configurazione della pubblicazione selettiva a livello di cartella in Dynamic Media {#selective-publish-configure-folder}

Puoi scegliere di pubblicare o annullare la pubblicazione delle risorse su o da Adobe Experience Manager o Dynamic Media a livello di cartella. Puoi utilizzare **[!UICONTROL Gestisci pubblicazione]** o **[!UICONTROL Pubblicazione rapida]** invece di affidarti esclusivamente alla **[!UICONTROL Configurazione Dynamic Media]** le cui impostazioni sono globali per tutte le cartelle nell&#39;istanza Dynamic Media.

Ad esempio, con la pubblicazione selettiva puoi lavorare sulle risorse per i prodotti che non sono ancora in diretta. In questo caso, un team di marketing può accedere alle immagini di ritaglio avanzato e alle rappresentazioni dinamiche sincronizzate con Dynamic Media. Possono creare materiali promozionali senza dover pubblicare tali risorse in Dynamic Media per la distribuzione globale.

>[!IMPORTANT]
>
>La pubblicazione selettiva è disponibile solo in modalità Dynamic Media - Scene7.

>[!NOTE]
>
>** La copia delle risorse nelle cartelle e da esse cancella lo stato di pubblicazione di tali risorse. Tuttavia, quando *sposti* risorse in e da cartelle la cui proprietà della cartella è impostata su **[!UICONTROL Pubblicazione selettiva]**, viene mantenuto lo stato di pubblicazione di tali risorse.

Se decidi in un secondo momento di modificare le impostazioni di **[!UICONTROL Pubblicazione selettiva]** in una cartella, tali modifiche interesseranno solo le nuove risorse caricate in tale cartella da quel momento in poi. Lo stato di pubblicazione delle risorse esistenti nella cartella rimane invariato finché non le cambi manualmente dalla finestra di dialogo **[!UICONTROL Pubblicazione rapida]** o **[!UICONTROL Gestisci pubblicazione]**.

L&#39;opzione a livello di cartella **[!UICONTROL Modalità di pubblicazione Dynamic Media]** viene sempre impostata per impostazione predefinita sul valore trovato nell&#39;impostazione **[!UICONTROL Pubblica risorse]** nella **[!UICONTROL Configurazione Dynamic Media]**. I passaggi seguenti in questo argomento, tuttavia, mostrano come modificare manualmente questo valore predefinito a livello di cartella (come descritto nei passaggi seguenti) per sostituire il valore **[!UICONTROL Configurazione Dynamic Media]**.

Indipendentemente dal valore **[!UICONTROL Pubblica risorse]** impostato in **[!UICONTROL Configurazione Dynamic Media]** o dal valore **[!UICONTROL Modalità pubblicazione Dynamic Media]** impostato nelle proprietà a livello di cartella, puoi scegliere **[!UICONTROL Immediatamente]**, **[!UICONTROL All&#39;attivazione]** o **[!UICONTROL Selettivo Pubblica]**. Ad esempio, puoi impostare il valore **[!UICONTROL Pubblica risorse]** nella **[!UICONTROL Configurazione Dynamic Media]** su **[!UICONTROL All&#39;attivazione]**, ma impostare il valore della modalità **[!UICONTROL Pubblicazione Dynamic Media]** a livello di cartella su **[!UICONTROL Pubblicazione selettiva]** e viceversa.

Dopo aver configurato la pubblicazione selettiva in una cartella, puoi effettuare una delle seguenti operazioni:

* [Pubblicare in modo selettivo le risorse in Dynamic Media o Experience Manager utilizzando Gestisci pubblicazione](#selective-publish-manage-publication).
* [Annulla la pubblicazione selettiva delle risorse da Dynamic Media o Experience Manager tramite Gestisci pubblicazione](#selective-unpublish-manage-publication).
* [Pubblicazione delle risorse in Dynamic Media o Experience Manager tramite Pubblicazione](#quick-publish-aem-dm) rapida.
* [Pubblicare o annullare selettivamente la pubblicazione delle risorse tramite i risultati](#selective-publish-unpublish-search-results) della ricerca.

**Per configurare la pubblicazione selettiva a livello di cartella in Dynamic Media:**

1. Ad Experience Manager, tocca il logo Experience Manager per accedere alla console di navigazione globale. A sinistra, tocca l’icona Navigazione (appena sopra l’icona Strumenti), quindi tocca **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. Effettua una delle operazioni seguenti:
   * Modifica le proprietà di una cartella esistente - In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]**, passa a una cartella di cui desideri modificare le proprietà. Seleziona la cartella, quindi tocca **[!UICONTROL Proprietà]** sulla barra degli strumenti.
   * Modifica le proprietà di una nuova cartella - In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]**, vicino all&#39;angolo superiore destro della pagina, tocca **[!UICONTROL Crea]** > **[!UICONTROL Cartella]**. Nella finestra di dialogo **[!UICONTROL Crea cartella]**, immetti un titolo (obbligatorio) per la cartella, quindi tocca **[!UICONTROL Crea]**. Seleziona la cartella, quindi tocca **[!UICONTROL Proprietà]** sulla barra degli strumenti.

1. Nell&#39;elenco a discesa **[!UICONTROL Modalità di sincronizzazione]** , seleziona una delle opzioni seguenti:

   | Modalità di sincronizzazione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Ereditato]** | Nessun valore di sincronizzazione esplicito sulla cartella; la cartella eredita invece il valore di sincronizzazione da una delle cartelle precedenti o la modalità predefinita impostata in **[!UICONTROL Configurazione Dynamic Media]**. Lo stato dettagliato di **[!UICONTROL Ereditato]** viene visualizzato tramite una descrizione comandi. |
   | **[!UICONTROL Sincronizza tutti gli elementi nella sottostruttura cartelle in Dynamic Media]** | Affinché la pubblicazione in Dynamic Media abbia successo, le risorse devono essere sincronizzate in Dynamic Media. Selezionando questa opzione vengono incluse tutte le risorse presenti nella sottostruttura per la sincronizzazione con Dynamic Media. Le impostazioni specifiche per la cartella sostituiscono le impostazioni predefinite in **[!UICONTROL Configurazione Dynamic Media]**. |
   | **[!UICONTROL Escludere tutto ciò che si trova nella sottostruttura della cartella dalla sincronizzazione Dynamic Media]** | Escludere tutte le risorse presenti in questa sottostruttura dalla sincronizzazione con Dynamic Media. |

   ![Pubblicazione selettiva a livello di cartella](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. Nell&#39;elenco a discesa **[!UICONTROL Modalità di pubblicazione Dynamic Media]** , seleziona un&#39;opzione. L&#39;opzione **[!UICONTROL Modalità di pubblicazione Dynamic Media]** viene sempre impostata per impostazione predefinita sul valore impostato in **[!UICONTROL Configurazione Dynamic Media]**. È tuttavia possibile ignorare manualmente questo valore predefinito **[!UICONTROL Configurazione Dynamic Media]** utilizzando una delle seguenti opzioni.

   >[!IMPORTANT]
   >
   >Indipendentemente dall’opzione della modalità di pubblicazione di Dynamic Media selezionata, eventuali aggiornamenti apportati successivamente a una risorsa *già* pubblicata, tali aggiornamenti vengono pubblicati immediatamente senza ulteriori azioni da parte dell’utente.

   | Opzione della modalità di pubblicazione Dynamic Media | Descrizione |
   | --- | --- |
   | **[!UICONTROL Immediatamente]** | Quando le risorse vengono caricate in questa cartella, il sistema le inserisce in Experience Manager e fornisce l’URL/Incorpora all’istante. Questa opzione è legata solo alla pubblicazione di Experienci Manager e non è necessario alcun intervento dell’utente per pubblicare le risorse.<br>Questa opzione  ** non è disponibile se nel passaggio precedente hai selezionato  **[!UICONTROL Escludi tutto ciò che si trova nella sottostruttura della cartella dalla]** modalità  **[!UICONTROL Sincronizza]** sincronizzazione di Dynamic Media. |
   | **[!UICONTROL All&#39;attivazione]** | Quando le risorse vengono caricate in questa cartella, devi pubblicare esplicitamente la risorsa prima di fornire un collegamento URL/Incorpora . Questa opzione è legata solo alla pubblicazione di Experienci Manager.<br>Questa opzione  ** non è disponibile se nel passaggio precedente hai selezionato  **[!UICONTROL Escludi tutto ciò che si trova nella sottostruttura della cartella dalla]** modalità  **[!UICONTROL Sincronizza]** sincronizzazione di Dynamic Media. |
   | **[!UICONTROL Pubblicazione selettiva]** | Le risorse vengono pubblicate come Experience Manager desiderato o su Dynamic Media per la distribuzione nel dominio pubblico. Entrambi i metodi di pubblicazione si escludono a vicenda. In altre parole, puoi pubblicare le risorse in DMS7 in modo da poter utilizzare funzioni quali Ritaglio avanzato o rappresentazioni dinamiche. Oppure puoi pubblicare le risorse esclusivamente in Experience Manager per un’anteprima sicura; le stesse risorse sono *non* pubblicate in DMS7 per la distribuzione nel dominio pubblico. Questa opzione non è disponibile se nel passaggio precedente hai selezionato **[!UICONTROL Escludi tutto ciò che si trova nella struttura secondaria della cartella da Dynamic Media sync]** in **[!UICONTROL Modalità di sincronizzazione]** . |

1. Nell’angolo in alto a destra della pagina, tocca **[!UICONTROL Salva e chiudi]**, quindi tocca **[!UICONTROL OK]** per tornare ad Experience Manager Assets.

## Pubblicare in modo selettivo le risorse in Dynamic Media o Experience Manager utilizzando Gestisci pubblicazione{#selective-publish-manage-publication}

Prima di poter utilizzare **[!UICONTROL Gestisci pubblicazione]** per pubblicare selettivamente le risorse in Dynamic Media o Experience Manager, assicurati di aver impostato uno dei seguenti valori:

* Opzione **[!UICONTROL Pubblica risorse]** in **[!UICONTROL Configurazione Dynamic Media]** in **[!UICONTROL Pubblicazione selettiva]**
* È stata configurata la pubblicazione selettiva a livello di cartella.

Consulta [Creazione di una configurazione Dynamic Media](#configuring-dynamic-media-cloud-services) o [Configurazione della pubblicazione selettiva a livello di cartella in Dynamic Media](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>La pubblicazione selettiva è disponibile solo in modalità Dynamic Media - Scene7.

>[!NOTE]
>
>** La copia delle risorse nelle cartelle e da esse cancella lo stato di pubblicazione di tali risorse. Tuttavia, quando *sposti* risorse in e da cartelle la cui proprietà della cartella è impostata su **[!UICONTROL Pubblicazione selettiva]**, viene mantenuto lo stato di pubblicazione di tali risorse.

**Per pubblicare selettivamente le risorse in Dynamic Media o Experience Manager utilizzando Gestisci pubblicazione:**

1. Ad Experience Manager, tocca il logo Experience Manager per accedere alla console di navigazione globale. A sinistra, tocca l’icona Navigazione (appena sopra l’icona Strumenti), quindi tocca **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]**, effettuare una delle seguenti operazioni:
   * Passa a una cartella di cui desideri pubblicare le risorse. Seleziona la cartella, quindi tocca **[!UICONTROL Gestisci pubblicazione]** sulla barra degli strumenti. Utilizza **[!UICONTROL Vista a elenco]** per controllare più facilmente lo stato di pubblicazione di una particolare cartella.
   * Passa a una cartella di cui desideri pubblicare le risorse. Apri la cartella, quindi seleziona una o più risorse. Sulla barra degli strumenti, tocca **[!UICONTROL Gestisci pubblicazione]**. Utilizza **[!UICONTROL Vista a elenco]** per controllare più facilmente lo stato di pubblicazione di una particolare risorsa.

      >[!NOTE]
      >
      >Se **[!UICONTROL Gestisci pubblicazione]** non è visualizzato nella barra degli strumenti, tocca invece il pulsante dei puntini di sospensione, quindi seleziona **[!UICONTROL Gestisci pubblicazione]** dal menu dell’elenco.

1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Opzioni]**, in **[!UICONTROL Azione]**, seleziona il tipo di attivazione desiderato.

   | Azione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Pubblica]**  (in Experience Manager) | Seleziona questa opzione per pubblicare le risorse in Experience Manager per l’anteprima protetta. |
   | **[!UICONTROL Pubblica in Dynamic Media]** | Seleziona questa opzione per pubblicare le risorse in Dynamic Media per la distribuzione nel dominio pubblico o per utilizzare funzioni quali Ritaglio avanzato o rappresentazioni dinamiche.<br>Questa opzione è disponibile solo se la modalità di pubblicazione  **[!UICONTROL Dynamic Media è]** impostata su  **[!UICONTROL Pubblicazione selettiva]** nelle proprietà della cartella. |

1. In **[!UICONTROL Schedule]**, imposta la tempistica della pubblicazione.

   | Pianificazione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Ora]** | Seleziona per pubblicare immediatamente le risorse. |
   | **[!UICONTROL Più tardi]** | Seleziona per pubblicare le risorse in una data e in un’ora specifiche. |

1. Nell’angolo in alto a destra della pagina **[!UICONTROL Gestisci pubblicazione]**, tocca **[!UICONTROL Avanti]**.
1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Ambito]** , effettua una delle seguenti operazioni:

   * Se necessario, seleziona una o più risorse da rimuovere dalla pubblicazione.
   * Nell’angolo in alto a destra della pagina **[!UICONTROL Gestisci pubblicazione - Ambito]**, tocca **[!UICONTROL Pubblica]** o **[!UICONTROL Pubblica in Dynamic Media]**.
1. Toccare **[!UICONTROL OK]**.

### Annullare selettivamente la pubblicazione delle risorse da Dynamic Media o Experience Manager utilizzando Gestisci pubblicazione {#selective-unpublish-manage-publication}

1. Ad Experience Manager, tocca il logo Experience Manager per accedere alla console di navigazione globale. A sinistra, tocca l’icona Navigazione (appena sopra l’icona Strumenti), quindi tocca **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]**, effettuare una delle seguenti operazioni:
   * Passa a una cartella di cui desideri annullare la pubblicazione delle risorse. Seleziona la cartella, quindi tocca **[!UICONTROL Gestisci pubblicazione]** sulla barra degli strumenti. Utilizza **[!UICONTROL Vista a elenco]** per controllare più facilmente lo stato di pubblicazione di una particolare cartella.
   * Passa a una cartella di cui desideri annullare la pubblicazione delle risorse. Apri la cartella, quindi seleziona una o più risorse. Sulla barra degli strumenti, tocca **[!UICONTROL Gestisci pubblicazione]**. Utilizza **[!UICONTROL Vista a elenco]** per controllare più facilmente lo stato di pubblicazione di una particolare risorsa.

      >[!NOTE]
      >
      >Se **[!UICONTROL Gestisci pubblicazione]** non è visualizzato nella barra degli strumenti, tocca invece il pulsante dei puntini di sospensione, quindi seleziona **[!UICONTROL Gestisci pubblicazione]** dal menu dell’elenco.

1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Opzioni]**, in **[!UICONTROL Azione]**, seleziona il tipo di disattivazione desiderato.

   | Azione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Annulla pubblicazione]**  (dall’Experience Manager) | Seleziona questa opzione se desideri annullare la pubblicazione delle risorse dall’Experience Manager. |
   | **[!UICONTROL Annulla pubblicazione da Dynamic Media]** | Seleziona questa opzione se desideri annullare la pubblicazione delle risorse da Dynamic Media.<br>Questa opzione è disponibile solo se la modalità di pubblicazione  **[!UICONTROL Dynamic Media è]** impostata su  **[!UICONTROL Pubblicazione selettiva]** nelle proprietà della cartella. |

1. In **[!UICONTROL Schedule]**, imposta il tempo di disattivazione.

   | Pianificazione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Ora]** | Seleziona per annullare immediatamente la pubblicazione delle risorse. |
   | **[!UICONTROL Più tardi]** | Seleziona per annullare la pubblicazione delle risorse in una data e in un’ora specifiche. |

1. Nell’angolo in alto a destra della pagina **[!UICONTROL Gestisci pubblicazione]**, tocca **[!UICONTROL Avanti]**.
1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Ambito]** , effettua una delle seguenti operazioni:
   * Seleziona una o più risorse da rimuovere dall’annullamento della pubblicazione.
   * Nell’angolo in alto a destra della pagina **[!UICONTROL Gestisci pubblicazione - Ambito]**, tocca **[!UICONTROL Annulla pubblicazione]** o **[!UICONTROL Annulla pubblicazione da Dynamic Media]**.
1. Toccare **[!UICONTROL OK]**.

## Pubblicazione delle risorse in Dynamic Media o Experience Manager tramite Pubblicazione rapida {#quick-publish-aem-dm}

Puoi utilizzare **[!UICONTROL Pubblicazione rapida]** per casi semplici di attivazione delle risorse. **[!UICONTROL Pubblicazione rapida]** pubblica le risorse selezionate immediatamente senza ulteriore interazione da parte dell’utente. A causa di questa azione, vengono pubblicati automaticamente anche tutti i riferimenti non pubblicati.

>[!NOTE]
>
>Per utilizzare **[!UICONTROL Pubblicazione rapida]** per pubblicare le risorse in Dynamic Media o Experience Manager, assicurati che **[!UICONTROL Pubblicazione selettiva]** sia abilitata nelle **[!UICONTROL Configurazione Dynamic Media]** o nelle proprietà della cartella selezionata.

**Per pubblicare le risorse in Dynamic Media o Experience Manager utilizzando Pubblicazione rapida:**

1. Ad Experience Manager, tocca il logo Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro della pagina, tocca l’icona Navigazione (appena sopra l’icona Strumenti), quindi sul lato destro della pagina tocca **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]**, effettuare una delle seguenti operazioni:
   * Passa a una cartella di cui desideri pubblicare le risorse. Seleziona la cartella, quindi tocca **[!UICONTROL Pubblicazione rapida]** sulla barra degli strumenti. Utilizza **[!UICONTROL Vista a elenco]** per controllare più facilmente lo stato di pubblicazione di una particolare cartella.
   * Passa a una cartella di cui desideri pubblicare le risorse. Apri la cartella, quindi seleziona una o più risorse. Sulla barra degli strumenti, tocca **[!UICONTROL Pubblicazione rapida]**. Utilizza **[!UICONTROL Vista a elenco]** per controllare più facilmente lo stato di pubblicazione di una particolare risorsa.

      >[!NOTE]
      >
      >Se **[!UICONTROL Pubblicazione rapida]** non è visibile sulla barra degli strumenti, tocca invece il pulsante dei puntini di sospensione, quindi seleziona **[!UICONTROL Pubblicazione rapida]** dal menu dell’elenco.

      ![Pubblicazione rapida a livello di cartella in Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Selezionare una delle seguenti opzioni dall&#39;elenco del menu **[!UICONTROL Pubblicazione rapida]**.

   | Opzione Pubblicazione rapida | Funzionamento |
   | --- | --- | 
   | Pubblica in Experience Manager | Pubblica immediatamente ad Experience Manager le risorse selezionate. |
   | Pubblica su Brand Portal | Pubblica immediatamente le risorse selezionate in **[!UICONTROL Brand Portal]**.<br>Questa opzione è disponibile solo se l’istanza Risorse di Experience Manager ha già configurato  **[!UICONTROL Brand]** Portal. |
   | Pubblica in Dynamic Media | Pubblica immediatamente le risorse selezionate in Dynamic Media.<br>Una risorsa deve essere sincronizzata in Dynamic Media. Se necessario, assicurati che **[!UICONTROL Modalità di sincronizzazione]** nelle proprietà di una cartella sia già impostato su **[!UICONTROL Sincronizza tutti gli elementi della struttura secondaria di questa cartella su Dynamic Media]**. |

1. Tocca **[!UICONTROL OK]**, quindi tocca **[!UICONTROL Chiudi]**.

## Pubblicare o annullare selettivamente la pubblicazione delle risorse tramite i risultati della ricerca {#selective-publish-unpublish-search-results}

I risultati della ricerca possono mostrare risorse da più cartelle di risorse che hanno diverse impostazioni di pubblicazione di Dynamic Media. Se selezioni più risorse dai risultati della ricerca e ciascuna risorsa dispone di diverse impostazioni della modalità di pubblicazione di Dynamic Media, puoi attivare **[!UICONTROL Gestisci pubblicazione]** dalla barra degli strumenti per eseguire la pubblicazione o annullare la pubblicazione.

Consulta anche [Cercare risorse in Experience Manager](/help/assets/search-assets.md).

**Per pubblicare o annullare selettivamente la pubblicazione delle risorse tramite i risultati della ricerca:**

1. Ad Experience Manager, nell’angolo in alto a sinistra della pagina, tocca il logo Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro della pagina, tocca l’icona Navigazione (appena sopra l’icona Strumenti), quindi tocca **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. Nella barra degli strumenti, nell’angolo superiore destro della pagina, tocca l’icona Ricerca (lente di ingrandimento).
1. Nel campo di testo **[!UICONTROL Digitare per cercare]**, immettere una parola chiave, quindi premere **[!UICONTROL Invio]**.
1. Vicino all’angolo superiore destro della pagina, tocca l’icona **[!UICONTROL Vista a elenco]** .
1. Nell’angolo in alto a sinistra della pagina, tocca l’icona **[!UICONTROL Filtri]** .

   ![Visualizzazione a elenco e filtri nei risultati della ricerca](/help/assets/assets-dm/select-publish-search-result.png)

1. Nel pannello a sinistra, espandi **[!UICONTROL Stato]**, quindi espandi il predicato di ricerca **[!UICONTROL Dynamic Media]**.
1. Utilizza le caselle di controllo **[!UICONTROL Pubblicato]** e **[!UICONTROL Non pubblicato]** per perfezionare ulteriormente i risultati della ricerca in base allo stato pubblicato delle risorse Dynamic Media.
Facoltativamente, puoi utilizzare queste caselle di controllo con il predicato di ricerca **[!UICONTROL Pubblica]** per perfezionare i risultati della ricerca di risorse di Experience Manager **[!UICONTROL Pubblicato]** e **[!UICONTROL Non pubblicato]**.
1. Effettua una delle operazioni seguenti:
   * Seleziona una o più risorse da pubblicare o di cui annullare la pubblicazione.
   * Vicino all&#39;angolo superiore destro della pagina **[!UICONTROL Risultati ricerca]**, tocca **[!UICONTROL Seleziona tutto]**.
1. Sulla barra degli strumenti, tocca **[!UICONTROL Gestisci pubblicazione]**. Tocca l’icona dei puntini di sospensione nella barra degli strumenti per aprire **[!UICONTROL Gestisci pubblicazione]**.
1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Opzioni]** , seleziona l’azione desiderata.

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

1. In **[!UICONTROL Schedule]**, imposta il tempo di disattivazione.

   | Pianificazione selezionata | Cosa accade |
   | --- | --- |
   | Ora | L’azione selezionata viene eseguita immediatamente. |
   | Più tardi | L’azione selezionata viene eseguita alla data e all’ora specifiche selezionate. |

1. Nell’angolo in alto a destra della pagina **[!UICONTROL Gestisci pubblicazione - Opzioni]**, tocca **[!UICONTROL Avanti]**.
1. (Facoltativo) Nella pagina **[!UICONTROL Gestisci pubblicazione - Ambito]** , controlla la colonna **[!UICONTROL Pubblica destinazione]** nella tabella per le risorse selezionate.

   | Impostazione Publish Assets in Dynamic Media Configuration | Azione selezionata | Destinazione pubblicazione |
   | --- | --- | --- |
   | Immediatamente o <br>All&#39;attivazione | Pubblicazione | Experience Manager e Dynamic Media |
   | Immediatamente o <br>All&#39;attivazione | Pubblica in Dynamic Media | Nessuna |
   | Pubblicazione selettiva | Pubblicazione | Experience Manager |
   | Pubblicazione selettiva | Pubblica in Dynamic Media | Dynamic Media |
   | Immediatamente o <br>All&#39;attivazione | Annulla pubblicazione | Experience Manager e Dynamic Media |
   | Immediatamente o <br>All&#39;attivazione | Annulla pubblicazione da Dynamic Media | Nessuna |
   | Pubblicazione selettiva | Annulla pubblicazione | Experience Manager |
   | Pubblicazione selettiva | Annulla pubblicazione da Dynamic Media | Dynamic Media |

1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Ambito]** , effettua una delle seguenti operazioni:
   * Seleziona una o più risorse da rimuovere dalla pubblicazione o dall’annullamento della pubblicazione.
   * Nell&#39;angolo in alto a destra della pagina **[!UICONTROL Gestisci pubblicazione - Ambito]**, tocca **[!UICONTROL Pubblica]** o **[!UICONTROL Annulla pubblicazione]** per iniziare l&#39;azione.
1. Toccare **[!UICONTROL OK]**.

## Verifica dello stato di pubblicazione di una risorsa {#check-publish-status-of-asset}

Per controllare rapidamente lo stato di pubblicazione di una risorsa, puoi utilizzare **[!UICONTROL Timeline]** con **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]** in Experience Manager.

**Per controllare lo stato di pubblicazione di una risorsa:**

1. Ad Experience Manager, nell’angolo in alto a sinistra della pagina, tocca il logo Experience Manager per accedere alla console di navigazione globale. Sul lato sinistro della pagina, tocca l’icona Navigazione (appena sopra l’icona Strumenti), quindi tocca **[!UICONTROL Risorse]** > **[!UICONTROL File]**.
1. In **[!UICONTROL Vista a schede]**, **[!UICONTROL Vista a colonne]** o **[!UICONTROL Vista a elenco]** (la schermata seguente mostra la **[!UICONTROL Vista a elenco]**), apri una cartella contenente le risorse pubblicate o non pubblicate.
1. Seleziona una risorsa in modo che venga visualizzata con un segno di spunta. Vedi la schermata sottostante per esempio.
1. Nell’angolo in alto a sinistra della pagina, dal menu a discesa, seleziona **[!UICONTROL Timeline]**. L’area **[!UICONTROL Stato]** nel pannello a sinistra mostra lo stato di pubblicazione della risorsa selezionata.
Quando utilizzi **[!UICONTROL Vista a elenco]**, viene visualizzata una colonna aggiuntiva per lo stato di pubblicazione **[!UICONTROL Dynamic Media]**.
   * Per impostazione predefinita, in una cartella configurata per la sincronizzazione con Dynamic Media viene visualizzata la colonna **[!UICONTROL Dynamic Media]** .
   * Una cartella *non* configurata per la sincronizzazione con Dynamic Media non visualizza la colonna Dynamic Media.
      ![Vista a elenco e Timeline](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Risoluzione dei problemi Pubblicazione selettiva {#selective-publish-troubleshoot}

Una risorsa che non è sincronizzata con Dynamic Media ma su cui è attivata un’azione di pubblicazione Dynamic Media restituisce il seguente messaggio di errore e soluzione:

![Errore di pubblicazione selettiva](/help/assets/assets-dm/selective-publish-error.png)
