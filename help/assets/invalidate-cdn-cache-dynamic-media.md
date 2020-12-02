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


# Annullamento della validità della cache CDN per mezzo di elementi multimediali dinamici {#invalidating-cdn-cache-for-dm-assets}

Le risorse per contenuti multimediali dinamici sono memorizzate nella cache dalla rete CDN (Content Delivery Network) per una distribuzione rapida dei contenuti ai clienti. Tuttavia, quando apportate gli aggiornamenti a tali risorse, potreste desiderare che le modifiche diventino attive immediatamente sul sito Web. Lo svuotamento o l’annullamento della validità della cache CDN consente di aggiornare rapidamente le risorse distribuite da Dynamic Media. Invece di aspettare che la cache scada utilizzando un valore TTL (Time To Live) (il valore predefinito è 10 ore), potete inviare una richiesta dall&#39;interfaccia utente di Dynamic Media affinché la cache scada in pochi minuti.

>[!IMPORTANT]
>
>I passaggi seguenti si applicano solo alla modalità Dynamic Media - Scene7 in AEM 6.5, Service Pack 6 (AEM 6.5.6) o versioni successive. Questa funzione di annullamento della validità CDN richiede anche l’utilizzo del CDN out-of-the-box fornito con AEM oggetto multimediale dinamico; qualsiasi altra CDN personalizzata non è supportata.<br>Se utilizzate Contenuti multimediali dinamici in AEM 6.5, Service Pack 5 (AEM 6.5.5) o versioni precedenti, attenetevi alla procedura descritta in  [Invalidazione della cache CDN tramite Dynamic Media Classic.](/help/assets/invalidate-cdn-cache-dm-classic.md)

Vedere anche [Caching overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Per annullare la validità del contenuto CDN memorizzato nella cache per le risorse Dynamic Media:**

*Parte 1 di 2: Creazione di un modello di annullamento validità CDN*

1. In AEM 6.5.6 o versione successiva, toccare **[!UICONTROL Strumenti > Risorse > Annullamento validità CDN.]**

   ![Funzione di convalida CDN](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. Nella pagina **[!UICONTROL Modello di annullamento validità CDN]**, effettuare una delle seguenti operazioni in base allo scenario:

   | Scenario | Opzione |
   | --- | --- |
   | In passato ho già creato un modello di annullamento validità CDN utilizzando Dynamic Media Classic. | Il campo di testo **[!UICONTROL Crea modello]** viene precompilato con i dati del modello. In tal caso, potete modificare il modello oppure continuare con il passaggio successivo. |
   | Devo creare un modello. In cosa si entra? | Nel campo di testo **[!UICONTROL Crea modello]**, immettete un URL immagine (inclusi predefiniti immagine o modificatori) che faccia riferimento a `<ID>`, invece di un ID immagine specifico come nell&#39;esempio seguente:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Se il modello contiene solo `<ID>`, il supporto dinamico si riempie in `https://<publishserver_name>/is/image/<company_name>/<ID>` dove `<publishserver_name>` è il nome del server di pubblicazione definito in Impostazioni generali Classic; il `<company_name>` è il nome della directory principale della società associata a questa istanza AEM e `<ID>` è la risorsa selezionata tramite il selettore risorse da annullare.<br>Eventuali predefiniti/modificatori inseriti  `<ID>` vengono copiati così come sono nella definizione URL.<br>Solo le immagini  `/is/image` - ovvero - possono essere formate automaticamente in base al modello.<br>Ad  `/is/content/`esempio, l’aggiunta di risorse come video o PDF tramite il selettore delle risorse non genera automaticamente URL. Al contrario, dovete specificare tali risorse nel modello di annullamento validità CDN, oppure potete aggiungere manualmente l’URL a tali risorse in *Parte 2 di 2: Impostazione delle opzioni di annullamento validità CDN*.<br>**Esempi:**<br> In questo primo esempio, il modello di annullamento della validità contiene  `<ID>` insieme all’URL della risorsa  `/is/content`. Esempio, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Elemento multimediale dinamico crea l’URL in base a questo, con `<ID>` come risorse selezionate tramite il selettore delle risorse che desiderate annullare.<br>In questo secondo esempio, il modello di annullamento della validità contiene l’URL completo della risorsa utilizzata nelle proprietà Web con  `/is/content` (non dipendente dal selettore delle risorse). Ad esempio, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` dove lo zaino è l&#39;ID della risorsa.<br>I formati di risorse supportati in Contenuti multimediali dinamici possono essere annullati. I tipi di file di risorse *non* supportati per l&#39;annullamento della validità CDN includono Postscript, Encapsulated Postscript,  Adobe Illustrator,  Adobe InDesign, Microsoft Powerpoint, Microsoft Excel, Microsoft Word e Rich Text Format.<br>Quando create il modello, ma prestate attenzione alla sintassi e agli errori di battitura; Gli elementi multimediali dinamici non eseguono la convalida dei modelli.<br>Tenete presente che è necessario specificare gli URL per le raccolte avanzate immagine in questo modello di annullamento validità CDN o nel campo  **[!UICONTROL Aggiungi]** URL nella  *parte 2: Impostazione delle opzioni di annullamento validità CDN.*<br>**Importante:**ogni voce in un modello di annullamento validità CDN deve essere su una propria riga.<br>*L’esempio di modello riportato di seguito è solo a scopo illustrativo.* |

   ![Modello di annullamento validità CDN - Crea](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Modello di annullamento validità CDN]**, toccare **[!UICONTROL Salva]**, quindi toccare **[!UICONTROL OK.]**<br>

   *Parte 2 di 2: Impostazione delle opzioni di annullamento validità CDN*
   <br>

1. In AEM come Cloud Service, toccare **[!UICONTROL Strumenti > Risorse > Annullamento validità CDN.]**

   ![Funzione di convalida CDN](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. Nella pagina **[!UICONTROL Annullamento validità CDN - Aggiungi dettagli]**, selezionate le risorse per l&#39;annullamento della validità CDN.

   ![Annullamento validità CDN - Aggiungi dettagli](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Se decidete di lasciare deselezionate le opzioni **[!UICONTROL Annulla validità predefiniti immagine associati a risorse in CDN]** *e* **[!UICONTROL Annulla validità in base a modello]**, l&#39;URL di base delle risorse selezionate viene formato per l&#39;annullamento della validità. È consigliabile utilizzare questa disposizione di opzioni solo per le immagini.


   | Opzione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Annulla validità dei predefiniti immagine associati alla risorsa in CDN]** | (Facoltativo) Quando selezionate questa opzione, le risorse selezionate e tutti gli URL dei predefiniti per immagini associati vengono automaticamente formati per l’annullamento della validità della cache.<br>Le risorse e i relativi URL predefiniti preimpostati vengono formati automaticamente per l’annullamento della validità. Questa opzione funziona solo per le risorse di immagine. |
   | **[!UICONTROL Annullamento della convalida in base al modello]** | (Facoltativo) Selezionate questa opzione per utilizzare solo il modello definito per la formazione degli URL. |
   | **[!UICONTROL Aggiungi risorse]** | Usate il selettore delle risorse per selezionare le risorse da annullare. Potete selezionare risorse pubblicate o non pubblicate.<br>La memorizzazione nella cache del CDN è basata su URL, non su risorse. Pertanto, è necessario conoscere gli URL completi presenti sul sito Web. Dopo aver determinato tali URL, potete aggiungerli al modello. Potete quindi selezionare e aggiungere tali risorse e annullare la validità degli URL in un unico passaggio. <br>Usate questa opzione insieme ai predefiniti per immagini associati per risorse  **[!UICONTROL Annulla validità in CDN]**,  **[!UICONTROL Annulla validità in base al modello]** o a entrambi. |
   | **[!UICONTROL Aggiungi URL]** | Aggiungete o incollate manualmente i percorsi URL completi alle risorse per file multimediali dinamici la cui cache CDN desiderate annullare la validità. Utilizzate questa opzione se non avete creato un modello di annullamento validità CDN in ***Parte 1 di 2: Creazione di un modello di annullamento validità CDN*** e di poche risorse da annullare.<br>**Importante:** ogni URL aggiunto deve trovarsi su una propria riga.<br>Potete annullare la validità di un massimo di 1000 URL alla volta. Se il numero di URL nel campo di testo **[!UICONTROL Aggiungi URL]** è maggiore di 1000, non è possibile toccare **[!UICONTROL Next]**. In questi casi, toccate **[!UICONTROL X]** a destra di una risorsa selezionata oppure un URL aggiunto manualmente per eliminarla dall&#39;elenco di annullamento della validità.<br>Tenete presente che dovete specificare gli URL per le raccolte avanzate immagine nel modello di annullamento validità CDN o in questo campo di  **[!UICONTROL testo Aggiungi]** URL. |

1. Vicino all&#39;angolo superiore destro della pagina, toccare **[!UICONTROL Avanti.]**
1. Nella pagina **[!UICONTROL Annullamento validità CDN - Conferma]**, nella casella di riepilogo **[!UICONTROL URL]** verrà visualizzato un elenco di uno o più URL generati dal modello di annullamento validità CDN creato in precedenza e dalle risorse appena aggiunte.

   Ad esempio, utilizzando l’esempio CDN Modello di annullamento validità illustrato nei passaggi precedenti, supponiamo che sia stata aggiunta una singola risorsa denominata `spinset`. Toccando **[!UICONTROL Strumenti > Risorse > Annullamento validità CDN]** si ottengono i seguenti cinque URL generati nell&#39;interfaccia utente **[!UICONTROL Annullamento validità CDN - Conferma]**:

   ![Annullamento validità CDN - Conferma](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Se necessario, toccare **X** a destra di un URL per eliminarlo dal processo di annullamento della validità.

1. Vicino all&#39;angolo superiore destro della pagina, toccare **[!UICONTROL Invia]** per avviare il processo di annullamento della validità CDN.

## Risoluzione di errori di annullamento validità CDN

In tutti i casi, l&#39;intero batch viene elaborato per l&#39;annullamento della validità oppure l&#39;intero batch non riesce.

| Errore | Spiegazione |
| --- | --- |
| *Impossibile recuperare gli URL per le risorse selezionate.* | Si verifica se viene soddisfatta una delle seguenti situazioni:<br>- Non viene trovata una configurazione per contenuti multimediali dinamici.<br>- È presente un&#39;eccezione durante il recupero di un utente di servizio tramite il quale viene letta la configurazione Dynamic Media.<br>- Il server di pubblicazione o la directory principale della società utilizzata per creare gli URL non è presente nella configurazione per elementi multimediali dinamici. |
| *Alcuni URL non sono definiti correttamente. Correggi e invia di nuovo.* | Si verifica se l&#39;API di annullamento validità cache CDN IPS restituisce un errore che fa riferimento a un&#39;altra società o se l&#39;URL non è valido in base alla convalida eseguita dall&#39;API cdnCacheInvalidation IPS. |
| *Impossibile annullare la validità della cache CDN.* | Si verifica se la richiesta di annullamento della validità della cache CDN non riesce per altri motivi. |
| *Nessun URL immesso per essere invalidato.* | Si verifica se non sono presenti URL nella pagina **[!UICONTROL Annullamento validità CDN - Conferma]** e si tocca **[!UICONTROL Invia.]** |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
