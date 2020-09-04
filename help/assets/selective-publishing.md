---
title: Utilizzo della pubblicazione selettiva nei file multimediali dinamici
description: Informazioni sull’utilizzo di Pubblicazione selettiva nei file multimediali dinamici.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 68e3e80b1c1dda8352ff30989f85f83e82bde261
workflow-type: tm+mt
source-wordcount: '2934'
ht-degree: 4%

---


# Configurazione della pubblicazione selettiva a livello di cartella in Contenuti multimediali dinamici {#selective-publish-configure-folder}

Potete scegliere di pubblicare o annullare la pubblicazione delle risorse su o da AEM o contenuti multimediali dinamici a livello di cartella, utilizzando **[!UICONTROL Gestisci pubblicazione]** o Pubblicazione **** rapida invece di affidarvi esclusivamente alla Configurazione **[!UICONTROL file multimediali]** dinamica le cui impostazioni sono globali per tutte le cartelle dell’istanza di supporto dinamico.

Ad esempio, con la pubblicazione selettiva potete lavorare sulle risorse per prodotti che non sono ancora live. In tal caso, un team marketing può accedere alle immagini di ritaglio avanzato e alle rappresentazioni dinamiche sincronizzate con i contenuti multimediali dinamici, in modo che possano creare materiali promozionali, il tutto senza dover pubblicare tali risorse su contenuti multimediali dinamici per la distribuzione globale.

>[!IMPORTANT]
>
>La pubblicazione selettiva è disponibile solo in modalità Dynamic Media - Scene7.

>[!NOTE]
>
>*Copiando* le risorse da e verso le cartelle, lo stato di pubblicazione di tali risorse viene cancellato. Tuttavia, quando *spostate* risorse da e verso le cartelle la cui proprietà cartella è impostata su Pubblica **** selettiva, viene mantenuto lo stato di pubblicazione di tali risorse.

Se successivamente decidete di modificare le impostazioni **[!UICONTROL Pubblicazione]** selettiva in una cartella, tali modifiche interesseranno solo le nuove risorse che caricate in tale cartella da quel momento in poi. Lo stato di pubblicazione delle risorse esistenti nella cartella rimane invariato finché non le modificate manualmente dalla finestra di dialogo Pubblicazione **** rapida o **[!UICONTROL Gestisci pubblicazione]** .

L’opzione della modalità **[!UICONTROL Pubblicazione file multimediali]** dinamici a livello di cartella corrisponde sempre per impostazione predefinita al valore trovato nell’impostazione **[!UICONTROL Pubblica risorse]** nella configurazione **[!UICONTROL elemento multimediale dinamico.]** I passaggi seguenti in questo argomento, tuttavia, mostrano come modificare manualmente questo valore predefinito a livello di cartella (come descritto nei passaggi seguenti) per ignorare il valore di Configurazione **[!UICONTROL elementi multimediali]** dinamici.

Indipendentemente dal valore **[!UICONTROL Pubblica risorse]** impostato in Configurazione **[!UICONTROL file multimediali]** dinamici o dal valore della modalità **[!UICONTROL Pubblicazione file multimediali]** dinamici impostato nelle proprietà a livello di cartella, potete comunque scegliere **[!UICONTROL Immediatamente]**, **[!UICONTROL Al momento dell’attivazione]****[!UICONTROL o Pubblicazione selettiva.]** Ad esempio, potete impostare il valore **[!UICONTROL Pubblica risorse]** nella configurazione **[!UICONTROL di contenuti multimediali]** dinamici su **[!UICONTROL Al momento dell’attivazione]**, ma impostare il valore della modalità di pubblicazione **[!UICONTROL di contenuti multimediali]** dinamici a livello di cartella su Pubblicazione **** selettiva, e viceversa.

Dopo aver configurato la pubblicazione selettiva in una cartella, potete effettuare una delle seguenti operazioni:

* [Pubblicate le risorse in modo selettivo su file multimediali dinamici o AEM utilizzando Gestisci pubblicazione.](#selective-publish-manage-publication)
* [Annullamento selettivo della pubblicazione di risorse da elementi multimediali dinamici o AEM tramite Gestisci pubblicazione.](#selective-unpublish-manage-publication)
* [Pubblicazione di risorse su file multimediali dinamici o AEM tramite Pubblicazione rapida.](#quick-publish-aem-dm)
* [Pubblicare o annullare la pubblicazione delle risorse in modo selettivo tramite i risultati della ricerca.](#selective-publish-unpublish-search-results)

**Per configurare la pubblicazione selettiva a livello di cartella in Contenuti multimediali dinamici**

1. In AEM, toccate il logo AEM per accedere alla console di navigazione globale. A sinistra, tocca l&#39;icona Navigazione (appena sopra l&#39;icona Strumenti), quindi tocca **[!UICONTROL Risorse > File.]**
1. Effettua una delle operazioni seguenti:
   * Modificate le proprietà di una cartella esistente: in visualizzazione **[!UICONTROL a]** schede, in vista **** a colonne o in vista **** elenco, individuate la cartella di cui desiderate modificare le proprietà. Selezionate la cartella, quindi toccate **[!UICONTROL Proprietà sulla barra degli strumenti.]**
   * Modificate le proprietà di una nuova cartella: in visualizzazione **[!UICONTROL a]** schede, a **[!UICONTROL colonne]** o a **[!UICONTROL elenco]**, toccate **[!UICONTROL Crea > Cartella accanto all’angolo superiore destro della pagina.]** Nella finestra di dialogo **[!UICONTROL Crea cartella]** , immettete un titolo (obbligatorio) per la cartella, quindi toccate **[!UICONTROL Crea.]** Selezionate la cartella, quindi toccate **[!UICONTROL Proprietà sulla barra degli strumenti.]**

1. Nell’elenco a discesa Modalità **** sincronizzazione, selezionate una delle seguenti opzioni:

   | Modalità di sincronizzazione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Ereditato]** | Nessun valore di sincronizzazione esplicito sulla cartella; al contrario, la cartella eredita il valore di sincronizzazione da una delle cartelle antenate o dalla modalità predefinita impostata nella configurazione **[!UICONTROL Dynamic Media.]** Lo stato dettagliato per le **[!UICONTROL presentazioni]** ereditate viene visualizzato tramite una descrizione comandi. |
   | **[!UICONTROL Sincronizza tutto il contenuto di questo sottoalbero di cartelle in Dynamic Media]** | Affinché la pubblicazione possa essere eseguita correttamente, le risorse devono essere sincronizzate su elementi multimediali dinamici. Selezionando questa opzione verranno incluse tutte le risorse presenti in questo sottoalbero per la sincronizzazione con gli elementi multimediali dinamici. Le impostazioni specifiche per la cartella sostituiscono l’impostazione predefinita in Configurazione file multimediali **[!UICONTROL dinamici.]** |
   | **[!UICONTROL Escludere tutto ciò che si trova nella sottostruttura della cartella dalla sincronizzazione di contenuti multimediali dinamici]** | Escludete tutte le risorse in questo sottoalbero dalla sincronizzazione a Contenuti multimediali dinamici. |

   ![Pubblicazione selettiva a livello di cartella](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. Selezionate un’opzione dall’elenco a discesa Modalità **[!UICONTROL pubblicazione elemento multimediale]** dinamico. L’opzione Modalità **[!UICONTROL di pubblicazione file multimediali]** dinamici è sempre impostata per impostazione predefinita sul valore impostato in Configurazione file multimediali **[!UICONTROL dinamici.]** Tuttavia, potete ignorare manualmente questo valore predefinito per la configurazione **** di elementi multimediali dinamici utilizzando una delle seguenti opzioni.

   >[!IMPORTANT]
   >
   >A prescindere dall’opzione selezionata per la modalità di pubblicazione di file multimediali dinamici, eventuali aggiornamenti apportati successivamente a una risorsa *già* pubblicata verranno pubblicati immediatamente, senza ulteriori interventi da parte dell’utente.

   | Modalità Pubblicazione file multimediali dinamici | Descrizione |
   | --- | --- |
   | **[!UICONTROL Immediatamente]** | Quando le risorse vengono caricate in questa cartella, il sistema le assimila in AEM e fornisce l’URL/Incorpora immediatamente. Questa opzione è legata solo AEM pubblicazione e non è necessario alcun intervento da parte dell’utente per pubblicare le risorse.<br>Questa opzione *non* è disponibile se avete selezionato **[!UICONTROL Escludi tutto nella sottostruttura della cartella dalla sincronizzazione]** dei supporti dinamici in modalità **** Sinc nel passaggio precedente. |
   | **[!UICONTROL All&#39;attivazione]** | Quando le risorse vengono caricate in questa cartella, è necessario pubblicare esplicitamente la risorsa prima di fornire un collegamento URL/Incorpora. Questa opzione è legata solo AEM pubblicazione.<br>Questa opzione *non* è disponibile se avete selezionato **[!UICONTROL Escludi tutto nella sottostruttura della cartella dalla sincronizzazione]** dei supporti dinamici in modalità **** Sinc nel passaggio precedente. |
   | **[!UICONTROL Pubblicazione selettiva]** | Le risorse vengono pubblicate a scelta dell’AEM o su contenuti multimediali dinamici per la distribuzione nel dominio pubblico. Entrambi i metodi di pubblicazione si escludono a vicenda.  In altre parole, potete pubblicare le risorse su DMS7 in modo da poter utilizzare funzioni quali SmartCrop o rappresentazioni dinamiche. Oppure potete pubblicare le risorse esclusivamente per AEM per un’anteprima protetta; le stesse risorse *non* vengono pubblicate in DMS7 per la distribuzione nel dominio pubblico. Questa opzione non è disponibile se nel passaggio precedente avete selezionato **[!UICONTROL Escludi tutto ciò che si trova nella sottostruttura della cartella dalla sincronizzazione]** dei supporti dinamici in modalità **** sincronizzazione. |

1. Nell’angolo superiore destro della pagina, toccate **[!UICONTROL Salva e chiudi]**, quindi toccate **[!UICONTROL OK]** per tornare  AEM Assets.

## Pubblicare in modo selettivo le risorse su file multimediali dinamici o AEM tramite Gestisci pubblicazione{#selective-publish-manage-publication}

Prima di poter utilizzare **[!UICONTROL Gestisci pubblicazione]** per pubblicare selettivamente le risorse su file multimediali dinamici o per AEM, accertatevi di aver impostato l’opzione **[!UICONTROL Pubblica risorse]** in Configurazione **[!UICONTROL file multimediali]** dinamici su Pubblica **[!UICONTROL selettiva o su Pubblicazione]** selettiva configurata a livello di cartella.

Consultate [Creazione di una configurazione](#configuring-dynamic-media-cloud-services) per contenuti multimediali dinamici o [Configurazione della pubblicazione selettiva a livello di cartella in Contenuti multimediali dinamici](#selective-publish-configure-folder)

>[!IMPORTANT]
>
>La pubblicazione selettiva è disponibile solo in modalità Dynamic Media - Scene7.

>[!NOTE]
>
>*Copiando* le risorse da e verso le cartelle, lo stato di pubblicazione di tali risorse viene cancellato. Tuttavia, quando *spostate* risorse da e verso le cartelle la cui proprietà cartella è impostata su Pubblica **** selettiva, viene mantenuto lo stato di pubblicazione di tali risorse.

**Per pubblicare selettivamente le risorse su file multimediali dinamici o AEM tramite Gestisci pubblicazione**

1. In AEM, toccate il logo AEM per accedere alla console di navigazione globale. A sinistra, tocca l&#39;icona Navigazione (appena sopra l&#39;icona Strumenti), quindi tocca **[!UICONTROL Risorse > File.]**
1. Nelle viste **[!UICONTROL a]** schede, a **[!UICONTROL colonne]** o a **[!UICONTROL elenco]**, effettuate una delle seguenti operazioni:
   * Passate a una cartella di cui desiderate pubblicare le risorse. Selezionate la cartella, quindi toccate **[!UICONTROL Gestisci pubblicazione sulla barra degli strumenti.]**  È utile utilizzare la visualizzazione **** elenco per controllare più facilmente lo stato di pubblicazione di una determinata cartella.
   * Passate a una cartella di cui desiderate pubblicare le risorse. Aprite la cartella, quindi selezionate una o più risorse. Nella barra degli strumenti, toccate **[!UICONTROL Gestisci pubblicazione.]** Potrebbe essere utile usare la visualizzazione **** elenco per controllare più facilmente lo stato di pubblicazione di una particolare risorsa.

      >[!NOTE]
      >
      >Se **[!UICONTROL Gestisci pubblicazione]** non è visibile sulla barra degli strumenti, toccate il pulsante con i puntini di sospensione, quindi selezionate **[!UICONTROL Gestisci pubblicazione]** dal menu a discesa.

1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Opzioni]** , in **[!UICONTROL Azione]**, selezionate il tipo di attivazione desiderata.

   | Azione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Pubblica]** (su AEM) | Selezionate questa opzione per pubblicare le risorse da AEM per l&#39;anteprima protetta. |
   | **[!UICONTROL Pubblica in Dynamic Media]** | Selezionate questa opzione per pubblicare le risorse su file multimediali dinamici per la distribuzione nel pubblico dominio o per utilizzare funzioni quali SmartCrop o rappresentazioni dinamiche.<br>Questa opzione è disponibile solo se la modalità **[!UICONTROL Pubblicazione file multimediali]** dinamici è impostata su Pubblicazione **** selettiva nelle proprietà della cartella. |

1. In **[!UICONTROL Pianificazione]**, impostate la tempistica della pubblicazione.

   | Pianificazione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Ora]** | Selezionate questa opzione per pubblicare immediatamente le risorse. |
   | **[!UICONTROL Più tardi]** | Selezionate questa opzione per pubblicare le risorse in una data e in un’ora specifiche. |

1. Nell’angolo in alto a destra della pagina **[!UICONTROL Gestisci pubblicazione]** , toccate **[!UICONTROL Avanti.]**
1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Ambito]** , effettuate una delle seguenti operazioni:
   * Se necessario, selezionate una o più risorse da rimuovere dalla pubblicazione.
   * Nell’angolo in alto a destra della pagina **[!UICONTROL Gestisci pubblicazione - Ambito]** , tocca **[!UICONTROL Pubblica]** o **[!UICONTROL Pubblica su file multimediali dinamici.]**
1. Toccate **[!UICONTROL OK.]**

### Annullamento selettivo della pubblicazione di risorse da elementi multimediali dinamici o AEM tramite Gestisci pubblicazione {#selective-unpublish-manage-publication}

1. In AEM, toccate il logo AEM per accedere alla console di navigazione globale. A sinistra, tocca l&#39;icona Navigazione (appena sopra l&#39;icona Strumenti), quindi tocca **[!UICONTROL Risorse > File.]**
1. Nelle viste **[!UICONTROL a]** schede, a **[!UICONTROL colonne]** o a **[!UICONTROL elenco]**, effettuate una delle seguenti operazioni:
   * Individuate una cartella di cui desiderate annullare la pubblicazione. Selezionate la cartella, quindi toccate **[!UICONTROL Gestisci pubblicazione sulla barra degli strumenti.]**  È utile utilizzare la visualizzazione **** elenco per controllare più facilmente lo stato di pubblicazione di una determinata cartella.
   * Individuate una cartella di cui desiderate annullare la pubblicazione. Aprite la cartella, quindi selezionate una o più risorse. Nella barra degli strumenti, toccate **[!UICONTROL Gestisci pubblicazione.]** Potrebbe essere utile usare la visualizzazione **** elenco per controllare più facilmente lo stato di pubblicazione di una particolare risorsa.

      >[!NOTE]
      >
      >Se **[!UICONTROL Gestisci pubblicazione]** non è visibile sulla barra degli strumenti, toccate il pulsante con i puntini di sospensione, quindi selezionate **[!UICONTROL Gestisci pubblicazione]** dal menu a discesa.

1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Opzioni]** , in **[!UICONTROL Azione]**, selezionate il tipo di disattivazione desiderata.

   | Azione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Annulla pubblicazione]** (da AEM) | Selezionate questa opzione per annullare la pubblicazione delle risorse da AEM. |
   | **[!UICONTROL Annulla pubblicazione da Dynamic Media]** | Selezionate questa opzione per annullare la pubblicazione delle risorse da Contenuti multimediali dinamici.<br>Questa opzione è disponibile solo se la modalità **[!UICONTROL Pubblicazione file multimediali]** dinamici è impostata su Pubblicazione **** selettiva nelle proprietà della cartella. |

1. In **[!UICONTROL Schedule (Pianificazione]**), impostate il tempo di disattivazione.

   | Pianificazione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Ora]** | Selezionate questa opzione per annullare immediatamente la pubblicazione delle risorse. |
   | **[!UICONTROL Più tardi]** | Selezionate questa opzione per annullare la pubblicazione delle risorse in una data e in un’ora specifiche. |

1. Nell’angolo in alto a destra della pagina **[!UICONTROL Gestisci pubblicazione]** , toccate **[!UICONTROL Avanti.]**
1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Ambito]** , effettuate una delle seguenti operazioni:
   * Selezionate una o più risorse da rimuovere dall’annullamento della pubblicazione.
   * Nell’angolo in alto a destra della pagina **[!UICONTROL Gestisci pubblicazione - Ambito]** , toccate **[!UICONTROL Annulla pubblicazione]** o **[!UICONTROL Annulla pubblicazione da Contenuti multimediali dinamici.]**
1. Toccate **[!UICONTROL OK.]**

## Pubblicazione di risorse su file multimediali dinamici o AEM tramite Pubblicazione rapida {#quick-publish-aem-dm}

Potete usare Pubblicazione **** rapida per casi di attivazione semplici delle risorse. **[!UICONTROL Pubblicazione]** rapida consente di pubblicare immediatamente le risorse selezionate senza ulteriori interazioni da parte dell’utente. Anche eventuali riferimenti non pubblicati vengono pubblicati automaticamente.

>[!NOTE]
>
>Per utilizzare la pubblicazione **** rapida per pubblicare le risorse su file multimediali dinamici o AEM, accertatevi che la pubblicazione **** selettiva sia abilitata nella configurazione **[!UICONTROL dei file multimediali]** dinamici o nelle proprietà della cartella selezionata.

**Per pubblicare le risorse su file multimediali dinamici o AEM tramite Pubblicazione rapida**

1. In AEM, toccate il logo AEM per accedere alla console di navigazione globale. Sul lato sinistro della pagina, tocca l’icona Navigazione (appena sopra l’icona Strumenti), quindi sul lato destro della pagina tocca **[!UICONTROL Risorse > File.]**
1. Nelle viste **[!UICONTROL a]** schede, a **[!UICONTROL colonne]** o a **[!UICONTROL elenco]**, effettuate una delle seguenti operazioni:
   * Passate a una cartella di cui desiderate pubblicare le risorse. Selezionate la cartella, quindi toccate Pubblicazione **[!UICONTROL rapida sulla barra degli strumenti.]**  È utile utilizzare la visualizzazione **** elenco per controllare più facilmente lo stato di pubblicazione di una determinata cartella.
   * Passate a una cartella di cui desiderate pubblicare le risorse. Aprite la cartella, quindi selezionate una o più risorse. Nella barra degli strumenti, toccate Pubblicazione **[!UICONTROL rapida.]** Potrebbe essere utile usare la visualizzazione **** elenco per controllare più facilmente lo stato di pubblicazione di una particolare risorsa.

      >[!NOTE]
      >
      >Se **[!UICONTROL Pubblicazione]** rapida non viene visualizzata sulla barra degli strumenti, toccate il pulsante con i puntini di sospensione, quindi selezionate Pubblicazione **** rapida dal menu a discesa.

      ![Pubblicazione rapida a livello di cartella su file multimediali dinamici](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. Selezionate una delle seguenti opzioni dall’elenco del menu Pubblicazione **** rapida.

   | Opzione Pubblicazione rapida | Azioni |
   | --- | --- | 
   | Pubblica in AEM | Pubblica immediatamente le risorse selezionate da AEM. |
   | Pubblica su Brand Portal | Pubblica immediatamente le risorse selezionate sul **[!UICONTROL Brand Portal.]**<br>Questa opzione è disponibile solo se ’istanza di AEM Assets è già configurato**[!UICONTROL  Brand Portal ]**. |
   | Pubblica in Dynamic Media | Pubblica immediatamente le risorse selezionate in Contenuti multimediali dinamici.<br>Una risorsa deve essere già sincronizzata con un elemento multimediale dinamico. Se necessario, accertatevi che la modalità **** Sinc nelle proprietà di una cartella sia già impostata per **[!UICONTROL sincronizzare tutti gli elementi nella sottostruttura della cartella ai contenuti multimediali dinamici.]** |

1. Toccate **[!UICONTROL OK]**, quindi **[!UICONTROL Chiudi.]**

## Pubblicare o annullare la pubblicazione selettiva delle risorse tramite i risultati della ricerca {#selective-publish-unpublish-search-results}

I risultati della ricerca possono mostrare le risorse provenienti da più cartelle di risorse con diverse impostazioni di pubblicazione per contenuti multimediali dinamici. Se avete selezionato una o più risorse dai risultati della ricerca e le risorse dispongono di diverse impostazioni della modalità di pubblicazione per contenuti multimediali dinamici, potete attivare **[!UICONTROL Gestisci pubblicazione]** dalla barra degli strumenti per pubblicarla o annullarne la pubblicazione.

Consultate anche [Cercare le risorse in AEM.](/help/assets/search-assets.md)

**Per pubblicare o annullare la pubblicazione selettiva delle risorse tramite i risultati della ricerca**

1. In AEM, nell’angolo superiore sinistro della pagina, toccate il logo AEM per accedere alla console di navigazione globale. Sul lato sinistro della pagina, tocca l’icona Navigazione (appena sopra l’icona Strumenti), quindi tocca **[!UICONTROL Risorse > File.]**
1. Nella barra degli strumenti, accanto all’angolo superiore destro della pagina, toccate l’icona Ricerca (lente di ingrandimento).
1. Nel campo **[!UICONTROL Tipo per cercare]** testo, immettere una parola chiave, quindi premere **[!UICONTROL Invio.]**
1. Nell’angolo superiore destro della pagina, toccate l’icona Visualizzazione **** elenco.
1. Nell’angolo superiore sinistro della pagina, toccate l’icona **[!UICONTROL Filtri]** .

   ![Visualizzazione elenco e filtri nei risultati della ricerca](/help/assets/assets-dm/select-publish-search-result.png)

1. Nel pannello a sinistra, espandete **[!UICONTROL Stato]**, quindi espandete il predicato di ricerca per elementi multimediali **** dinamici.
1. Usate le caselle di controllo **[!UICONTROL Pubblicato]** e **[!UICONTROL Non pubblicato]** per perfezionare ulteriormente i risultati di ricerca in base allo stato pubblicato delle risorse Contenuti multimediali dinamici.
Facoltativamente, potete utilizzare queste caselle di controllo insieme al predicato di ricerca **[!UICONTROL Pubblica]** per perfezionare i risultati di ricerca delle risorse AEM **[!UICONTROL Pubblicato]** e **[!UICONTROL Non pubblicato]** .
1. Effettua una delle operazioni seguenti:
   * Selezionate una o più risorse da pubblicare o annullare la pubblicazione.
   * Nell’angolo in alto a destra della pagina Risultati **** ricerca, toccate **[!UICONTROL Seleziona tutto.]**
1. Nella barra degli strumenti, toccate **[!UICONTROL Gestisci pubblicazione.]** Potrebbe essere necessario toccare l&#39;icona con i puntini di sospensione sulla barra degli strumenti per visualizzare **[!UICONTROL Gestisci pubblicazione.]**
1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Opzioni]** , selezionate l’azione desiderata.

   | Azione selezionata | Impostazione Pubblica risorse in Configurazione elemento multimediale dinamico | Risorse |
   | --- | --- | --- |
   | Pubblicazione | Immediatamente o al momento dell&#39;attivazione | Pubblicato su AEM e contenuti multimediali dinamici. |
   | Pubblicazione | Pubblicazione selettiva | Pubblicato solo in AEM. |
   | Annulla pubblicazione | Immediatamente o al momento dell&#39;attivazione | Non pubblicato da AEM e contenuti multimediali dinamici. |
   | Annulla pubblicazione | Pubblicazione selettiva | Non pubblicato solo da AEM. |
   | Pubblica in Dynamic Media | Immediatamente o al momento dell&#39;attivazione | Non pubblicato su AEM, Contenuti multimediali dinamici o entrambi. |
   | Pubblica in Dynamic Media | Pubblicazione selettiva | Pubblicato solo su Contenuti multimediali dinamici. |
   | Annulla pubblicazione da Dynamic Media | Immediatamente o al momento dell&#39;attivazione | Non viene annullata la pubblicazione da AEM, Contenuti multimediali dinamici o entrambi. |
   | Annulla pubblicazione da Dynamic Media | Pubblicazione selettiva | Non pubblicato solo da Contenuti multimediali dinamici. |

1. In **[!UICONTROL Schedule (Pianificazione]**), impostate il tempo di disattivazione.

   | Pianificazione selezionata | Cosa accade |
   | --- | --- |
   | Ora | L&#39;azione selezionata viene eseguita immediatamente. |
   | Più tardi | L&#39;azione selezionata viene eseguita in base alla data e all&#39;ora specifiche selezionate. |

1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Gestisci pubblicazione - Opzioni]** , tocca **[!UICONTROL Avanti.]**
1. (Facoltativo) Nella pagina **[!UICONTROL Gestisci pubblicazione - Ambito]** di applicazione, controlla la colonna Destinazione **[!UICONTROL di]** pubblicazione nella tabella relativa alle risorse selezionate.

   | Impostazione Pubblica risorse in Configurazione elemento multimediale dinamico | Azione selezionata | Destinazione pubblicazione |
   | --- | --- | --- |
   | Immediatamente o <br>al momento dell&#39;attivazione | Pubblicazione | AEM e contenuti multimediali dinamici |
   | Immediatamente o <br>al momento dell&#39;attivazione | Pubblica in Dynamic Media | Nessuno |
   | Pubblicazione selettiva | Pubblicazione | AEM |
   | Pubblicazione selettiva | Pubblica in Dynamic Media | Dynamic Media |
   | Immediatamente o <br>al momento dell&#39;attivazione | Annulla pubblicazione | AEM e contenuti multimediali dinamici |
   | Immediatamente o <br>al momento dell&#39;attivazione | Annulla pubblicazione da Dynamic Media | Nessuno |
   | Pubblicazione selettiva | Annulla pubblicazione | AEM |
   | Pubblicazione selettiva | Annulla pubblicazione da Dynamic Media | Dynamic Media |

1. Nella pagina **[!UICONTROL Gestisci pubblicazione - Ambito]** , effettuate una delle seguenti operazioni:
   * Selezionate una o più risorse da rimuovere dalla pubblicazione o dall’annullamento della pubblicazione.
   * Nell’angolo in alto a destra della pagina **[!UICONTROL Gestisci pubblicazione - Ambito]** , toccate **[!UICONTROL Pubblica]** o **[!UICONTROL Annulla pubblicazione]** per avviare l’azione.
1. Toccate **[!UICONTROL OK.]**

## Verifica dello stato di pubblicazione di una risorsa {#check-publish-status-of-asset}

Potete usare la **[!UICONTROL timeline]** con la vista **[!UICONTROL a]** schede, la vista **[!UICONTROL a]** colonne o la vista **[!UICONTROL a]** elenco in AEM per controllare rapidamente lo stato di pubblicazione di una risorsa.

**Per verificare lo stato di pubblicazione di una risorsa**

1. In AEM, nell’angolo superiore sinistro della pagina, toccate il logo AEM per accedere alla console di navigazione globale. Sul lato sinistro della pagina, tocca l’icona Navigazione (appena sopra l’icona Strumenti), quindi tocca **[!UICONTROL Risorse > File.]**
1. In vista **[!UICONTROL a]** schede, in vista **** a colonne o in vista **** elenco (la schermata seguente mostra la vista **[!UICONTROL a]** elenco), aprite una cartella che contiene le risorse pubblicate o non pubblicate.
1. Selezionate una risorsa in modo che venga visualizzata con un segno di spunta. Vedete, ad esempio, la schermata sottostante.
1. Near the upper-left corner of the page, from the drop-down menu, select **[!UICONTROL Timeline.]** L’area **[!UICONTROL Stato]** nel pannello a sinistra mostra lo stato di pubblicazione della risorsa selezionata.
Quando usate la vista **** Elenco, viene visualizzata una colonna aggiuntiva per lo stato di pubblicazione di file multimediali **** dinamici.
   * Per impostazione predefinita, una cartella configurata per la sincronizzazione con gli elementi multimediali dinamici presenta la colonna Contenuti multimediali **** dinamici.
   * Una cartella *non* configurata per la sincronizzazione con gli elementi multimediali dinamici non visualizzerà la colonna Contenuti multimediali dinamici.
      ![Visualizzazione a elenco e Timeline](/help/assets/assets-dm/selective-publish-status-timeline.png)

## Risoluzione dei problemi relativi alla pubblicazione selettiva {#selective-publish-troubleshoot}

Una risorsa che non è sincronizzata con un elemento multimediale dinamico ma che dispone di un’azione di pubblicazione elemento multimediale dinamico attivata, genera il seguente messaggio di errore e la seguente soluzione:

![Errore di pubblicazione selettiva](/help/assets/assets-dm/selective-publish-error.png)

