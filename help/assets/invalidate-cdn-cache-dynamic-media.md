---
title: Annullamento della validità della cache CDN tramite Dynamic Media
description: L’annullamento della validità della rete CDN (Content Delivery Network) nei contenuti memorizzati nella cache consente di aggiornare rapidamente le risorse distribuite da Dynamic Media, anziché attendere la scadenza della cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 54645149dc4968c1c4f85eedb5ce4d71f80c3b64
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 1%

---


# Annullamento della validità della cache CDN tramite Dynamic Media {#invalidating-cdn-cache-for-dm-assets}

Le risorse per contenuti multimediali dinamici sono memorizzate nella cache dalla rete CDN (Content Delivery Network) per una distribuzione rapida dei contenuti ai clienti. Tuttavia, quando apportate gli aggiornamenti a tali risorse, potreste desiderare che le modifiche diventino attive immediatamente sul sito Web. Lo svuotamento o l’annullamento della validità della cache CDN consente di aggiornare rapidamente le risorse distribuite da Dynamic Media. Invece di aspettare che la cache scada utilizzando un valore TTL (Time To Live) (il valore predefinito è 10 ore), potete inviare una richiesta dall&#39;interfaccia utente di Dynamic Media affinché la cache scada in pochi minuti.

>[!IMPORTANT]
>
>I passaggi seguenti si applicano solo alla modalità Dynamic Media - Scene7 in AEM 6.5, Service Pack 6 (AEM 6.5.6) o versioni successive. Questa funzione di annullamento della validità CDN richiede anche l’utilizzo del CDN out-of-the-box fornito con AEM oggetto multimediale dinamico; qualsiasi altra CDN personalizzata non è supportata.<br>Se utilizzate Contenuti multimediali dinamici in AEM 6.5, Service Pack 5 (AEM 6.5.5) o versioni precedenti, attenetevi alla procedura descritta in [Invalidazione della cache CDN tramite Dynamic Media Classic.](/help/assets/invalidate-cdn-cache-dm-classic.md)

Consultate anche Panoramica sulla [memorizzazione nella cache dei file multimediali](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html)dinamici.

**Per annullare la validità del contenuto CDN memorizzato nella cache per le risorse Dynamic Media:**

*Parte 1 di 2: Creazione di un modello di annullamento validità CDN*

1. In AEM 6.5.6 o versioni successive, toccate **[!UICONTROL Strumenti > Risorse > Annullamento validità CDN.]**

   ![Funzione di convalida CDN](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. Nella pagina del modello **[!UICONTROL di annullamento validità]** CDN, effettuate una delle seguenti operazioni in base allo scenario:

   | Scenario | Opzione |
   | --- | --- |
   | In passato ho già creato un modello di annullamento validità CDN utilizzando Dynamic Media Classic. | Il campo di testo **[!UICONTROL Crea modello]** è precompilato con i dati del modello. In tal caso, potete modificare il modello oppure continuare con il passaggio successivo. |
   | Devo creare un modello. In cosa si entra? | Nel campo di testo **[!UICONTROL Crea modello]** , immettete un URL immagine (con predefiniti per immagini o modificatori) che faccia riferimento `<ID>`, invece di un ID immagine specifico come nell’esempio seguente:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Se il modello contiene solo `<ID>`, Dynamic Media compila il `https://<publishserver_name>/is/image/<company_name>/<ID>` percorso in cui `<publishserver_name>` corrisponde al nome del server di pubblicazione definito in Impostazioni generali in Dynamic Media Classic; il nome `<company_name>` è il nome della directory principale della società associata a questa istanza AEM ed `<ID>` è la risorsa selezionata tramite il selettore risorse da annullare.<br>Eventuali predefiniti/modificatori inseriti `<ID>` vengono copiati così come sono nella definizione URL.<br>Solo le immagini, ovvero `/is/image` , possono essere formate automaticamente in base al modello.<br>Ad `/is/content/`esempio, l’aggiunta di risorse come video o PDF tramite il selettore delle risorse non genera automaticamente URL. Al contrario, dovete specificare tali risorse nel modello di annullamento validità CDN, oppure potete aggiungere manualmente l’URL a tali risorse nella *Parte 2 di 2: Impostazione delle opzioni* di annullamento validità CDN.<br>**Esempi:**<br> In questo primo esempio, il modello di annullamento della validità contiene `<ID>` insieme all’URL della risorsa `/is/content`. Esempio, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Elemento multimediale dinamico crea l’URL in base a questo criterio, con `<ID>` le risorse selezionate tramite il selettore delle risorse da annullare.<br>In questo secondo esempio, il modello di annullamento della validità contiene l’URL completo della risorsa utilizzata nelle proprietà Web con `/is/content` (non dipendente dal selettore delle risorse). Ad esempio, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` dove backpack è l’ID della risorsa.<br>I formati di risorse supportati in Contenuti multimediali dinamici possono essere annullati. I tipi di file di risorse *non* supportati per l’annullamento della validità CDN includono Postscript, Encapsulated Postscript,  Adobe Illustrator,  Adobe InDesign, Microsoft Powerpoint, Microsoft Excel, Microsoft Word e Rich Text Format.<br>Quando create il modello, ma prestate attenzione alla sintassi e agli errori di battitura; Gli elementi multimediali dinamici non eseguono la convalida dei modelli.<br>È necessario specificare gli URL per gli smart crop delle immagini in questo modello di annullamento validità CDN o nel campo di testo **[!UICONTROL Aggiungi URL]** nella *parte 2: Impostazione delle opzioni di annullamento validità CDN.*<br>**Importante:**Ogni voce in un modello di annullamento validità CDN deve essere su una propria riga.<br>*L’esempio di modello riportato di seguito è solo a scopo illustrativo.* |

   ![Modello di annullamento validità CDN - Crea](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. Nell&#39;angolo superiore destro della pagina del modello **[!UICONTROL di annullamento validità]** CDN, tocca **[!UICONTROL Salva]**, quindi tocca **[!UICONTROL OK.]**<br>   *Parte 2 di 2: Impostazione delle opzioni di annullamento validità CDN*
   <br>

1. In AEM come Cloud Service, toccate **[!UICONTROL Strumenti > Risorse > Annullamento validità CDN.]**

   ![Funzione di convalida CDN](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. Nella pagina **[!UICONTROL Annullamento validità CDN - Aggiungi dettagli]** , selezionate le risorse per l’annullamento della validità CDN.

   ![Annullamento validità CDN - Aggiungi dettagli](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Se decidete di lasciare deselezionata l’opzione **[!UICONTROL Annulla validità predefiniti immagine associati alla risorsa in CDN]** *e* Annulla validità in base al modello **** , l’URL di base delle risorse selezionate viene formato per l’annullamento della validità. È consigliabile utilizzare questa disposizione di opzioni solo per le immagini.


   | Opzione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Annulla validità dei predefiniti immagine associati alla risorsa in CDN]** | (Facoltativo) Quando selezionate questa opzione, le risorse selezionate e tutti gli URL dei predefiniti per immagini associati vengono automaticamente formati per l’annullamento della validità della cache.<br>Le risorse e i relativi URL predefiniti preimpostati vengono formati automaticamente per l’annullamento della validità. Questa opzione funziona solo per le risorse di immagine. |
   | **[!UICONTROL Annullamento della convalida in base al modello]** | (Facoltativo) Selezionate questa opzione per utilizzare solo il modello definito per la formazione degli URL. |
   | **[!UICONTROL Aggiungi risorse]** | Usate il selettore delle risorse per selezionare le risorse da annullare. Potete selezionare risorse pubblicate o non pubblicate.<br>La memorizzazione nella cache del CDN è basata su URL, non su risorse. Pertanto, è necessario conoscere gli URL completi presenti sul sito Web. Dopo aver determinato tali URL, potete aggiungerli al modello. Potete quindi selezionare e aggiungere tali risorse e annullare la validità degli URL in un unico passaggio. <br>Usate questa opzione insieme ai predefiniti per immagini associati per risorse **[!UICONTROL Annulla validità in CDN]**, **[!UICONTROL Annulla validità in base al modello]** o a entrambi. |
   | **[!UICONTROL Aggiungi URL]** | Aggiungete o incollate manualmente i percorsi URL completi alle risorse per file multimediali dinamici la cui cache CDN desiderate annullare la validità. Utilizzate questa opzione se non avete creato un modello di annullamento validità CDN nella ***parte 1 di 2: Creazione di un modello*** di annullamento validità CDN e di poche risorse da annullare.<br>**Importante:** Ogni URL aggiunto deve trovarsi su una propria riga.<br>Potete annullare la validità di un massimo di 1000 URL alla volta. Se il numero di URL nel campo di testo **[!UICONTROL Aggiungi URL]** è maggiore di 1000, non è possibile toccare **[!UICONTROL Avanti]**. In questi casi, toccate **[!UICONTROL X]** a destra di una risorsa selezionata o un URL aggiunto manualmente per eliminarla dall&#39;elenco di annullamento della validità.<br>Tenete presente che dovete specificare gli URL per le raccolte avanzate immagine nel modello di annullamento validità CDN o in questo campo di testo **[!UICONTROL Aggiungi URL]** . |

1. Near the upper-right corner of the page, tap **[!UICONTROL Next.]**
1. Nella pagina Annullamento validità **[!UICONTROL CDN - Conferma]** , nella casella di riepilogo **[!UICONTROL URL]** viene visualizzato uno o più URL generati dal modello di annullamento validità CDN precedentemente creato e dalle risorse appena aggiunte.

   Ad esempio, utilizzando l’esempio CDN Modello di annullamento validità illustrato nei passaggi precedenti, supponiamo che sia stata aggiunta una singola risorsa denominata `spinset`. Toccando **[!UICONTROL Strumenti > Risorse > Annullamento validità]** CDN si ottengono i seguenti cinque URL generati nell’interfaccia **[!UICONTROL Annulla validità CDN - Conferma]** utente:

   ![Annullamento validità CDN - Conferma](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Se necessario, toccate **X** a destra di un URL per eliminarlo dal processo di annullamento della validità.

1. Nell’angolo superiore destro della pagina, toccate **[!UICONTROL Invia]** per avviare il processo di annullamento della validità della CDN.

## Risoluzione di errori di annullamento validità CDN

In tutti i casi, l&#39;intero batch viene elaborato per l&#39;annullamento della validità oppure l&#39;intero batch non riesce.

| Errore | Spiegazione |
| --- | --- |
| *Impossibile recuperare gli URL per le risorse selezionate.* | Si verifica se vengono soddisfatti i seguenti scenari:<br>- Non viene trovata una configurazione per contenuti multimediali dinamici.<br>- È presente un&#39;eccezione durante il recupero di un utente di servizio tramite il quale viene letta la configurazione Dynamic Media.<br>- Il server di pubblicazione o la directory principale della società utilizzata per creare gli URL non è presente nella configurazione per elementi multimediali dinamici. |
| *Alcuni URL non sono definiti correttamente. Correggere e inviare di nuovo.* | Si verifica se l&#39;API di annullamento validità cache CDN IPS restituisce un errore che fa riferimento a un&#39;altra società o se l&#39;URL non è valido in base alla convalida eseguita dall&#39;API cdnCacheInvalidation IPS. |
| *Impossibile annullare la validità della cache CDN.* | Si verifica se la richiesta di annullamento della validità della cache CDN non riesce per altri motivi. |
| *Nessun URL immesso per essere invalidato.* | Si verifica se non sono presenti URL nella pagina **[!UICONTROL Annulla validità CDN - Conferma]** e si tocca **[!UICONTROL Invia.]** |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
