---
title: Invalidare la cache di rete per la distribuzione dei contenuti tramite Dynamic Media
description: Annulla validità della rete CDN (Content Delivery Network) memorizzata in cache consente di aggiornare rapidamente le risorse distribuite da Dynamic Media, invece di attendere la scadenza della cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
feature: CDN Cache
exl-id: 23d3c274-0736-49f7-8d44-a56a55cfd06d
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '1372'
ht-degree: 1%

---


# Invalidare la cache CDN tramite Dynamic Media {#invalidating-cdn-cache-for-dm-assets}

Le risorse Dynamic Media vengono memorizzate nella cache dalla rete CDN (Content Delivery Network) per velocizzare la distribuzione ai clienti. Tuttavia, quando apporti aggiornamenti a tali risorse, desideri che le modifiche diventino effettive immediatamente sul sito web. La rimozione o l’annullamento della validità della cache CDN consente di aggiornare rapidamente le risorse distribuite da Dynamic Media. Invece di attendere la scadenza della cache utilizzando un valore TTL (Time To Live) (il valore predefinito è dieci ore), puoi inviare una richiesta dall’interno di Dynamic Media affinché la cache scada in pochi minuti.



>[!IMPORTANT]
>
>I passaggi seguenti sono validi solo per la modalità Dynamic Media - Scene7 in Adobe Experience Manager 6.5, Service Pack 6 (Experience Manager 6.5.6) o versione successiva. Questa funzione di annullamento della validità della CDN richiede anche l’utilizzo della CDN preconfigurata inclusa in Adobe Experience Manager - Dynamic Media. Qualsiasi altra rete CDN personalizzata non è supportata con questa funzione.<br>Se utilizzi Dynamic Media in Experience Manager 6.5, Service Pack 5 (Experience Manager 6.5.5) o versioni precedenti, segui i passaggi descritti in [Annullamento della validità della cache CDN tramite Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md).

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Caching overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Per annullare la validità del contenuto CDN memorizzato nella cache per le risorse Dynamic Media:**

*Parte 1 di 2: creazione di un modello di annullamento validità CDN*

1. In Experience Manager 6.5.6 o versione successiva, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Annullamento validità CDN]**.

   ![Funzione di convalida CDN](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. Nella pagina **[!UICONTROL Modello di annullamento validità CDN]** eseguire una delle opzioni seguenti in base allo scenario:

   | Scenario | Opzione |
   | --- | --- |
   | In passato ho già creato un modello di annullamento della validità CDN utilizzando Dynamic Media Classic. | Il campo di testo **[!UICONTROL Crea modello]** è precompilato con i dati del modello. In questo caso, puoi modificare il modello o continuare con il passaggio successivo. |
   | Devo creare un modello. Cosa si immette? | Nel campo di testo **[!UICONTROL Crea modello]**, immettere un URL immagine (inclusi predefiniti immagine o modificatori) che faccia riferimento a `<ID>`, invece di un ID immagine specifico come nell&#39;esempio seguente:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Se il modello contiene solo `<ID>`, Dynamic Media compila `https://<publishserver_name>/is/image/<company_name>/<ID>`, dove `<publishserver_name>` è il nome del server di pubblicazione definito in Impostazioni generali in Dynamic Media Classic. `<company_name>` è il nome della directory principale della tua società associata a questa istanza di Experience Manager e `<ID>` sono le risorse selezionate tramite il selettore risorse da invalidare.<br>Eventuali predefiniti/modificatori post `<ID>` vengono copiati così come sono nella definizione dell&#39;URL.<br>Solo le immagini, ovvero `/is/image`, possono essere formate automaticamente in base al modello.<br>Per `/is/content/`, l&#39;aggiunta di risorse come video o PDF tramite il selettore risorse non genera automaticamente gli URL. È invece necessario specificare tali risorse nel modello di annullamento validità CDN oppure è possibile aggiungere manualmente l&#39;URL a tali risorse in *Parte 2 di 2: Impostazione delle opzioni di annullamento validità CDN*.<br>**Esempi:**<br> In questo primo esempio, il modello di invalidazione contiene `<ID>` insieme all&#39;URL della risorsa con `/is/content`. Ad esempio, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media forma l&#39;URL in base a questo percorso; `<ID>` sono le risorse selezionate tramite il selettore risorse che desideri invalidare.<br>In questo secondo esempio, il modello di annullamento della validità contiene l&#39;URL completo della risorsa utilizzata nelle proprietà Web con `/is/content` (non dipendente dal selettore risorse). Ad esempio, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` dove zaino è l&#39;ID risorsa.<br>I formati di risorse supportati in Dynamic Media possono essere invalidati. I tipi di file di risorse *non* supportati per l&#39;annullamento della validità CDN includono PostScript®, Encapsulated PostScript®, Adobe Illustrator, Adobe InDesign, Microsoft® Powerpoint, Microsoft® Excel, Microsoft® Word e Rich Text Format.<br><br>· Durante la creazione del modello, prestare particolare attenzione alla sintassi e agli errori di battitura; Dynamic Media non esegue alcuna convalida del modello.<br>· Il modello di annullamento validità CDN può salvare il testo fino a 2500 caratteri.<br>· Specificare gli URL per le ritagli avanzati immagine in questo modello di annullamento validità CDN o nel campo di testo **[!UICONTROL Aggiungi URL]** in *Parte 2: impostazione delle opzioni di annullamento validità CDN.*<br>· Ogni voce in un modello di annullamento della validità CDN deve trovarsi sulla propria riga.<br>· Il seguente esempio di modello di annullamento della validità CDN è solo a scopo dimostrativo. |

   ![Modello di annullamento validità CDN - Crea](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >Il modello di annullamento validità CDN può salvare il testo fino a 2500 caratteri.

1. Nell&#39;angolo superiore destro della pagina **[!UICONTROL Modello di annullamento validità CDN]**, selezionare **[!UICONTROL Salva]**, quindi selezionare **[!UICONTROL OK]**.<br>
   *Parte 2 di 2: impostazione delle opzioni di annullamento della validità CDN*
   <br>

1. In Experience Manager as a Cloud Service, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Annullamento validità CDN]**.

   ![Funzione di convalida CDN](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. Nella pagina **[!UICONTROL Annullamento validità CDN - Aggiungi dettagli]**, seleziona le risorse per l&#39;annullamento della validità CDN.

   ![Annullamento validità CDN - Aggiungi dettagli](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Se decidi di lasciare deselezionate le opzioni **[!UICONTROL Annulla validità predefiniti immagine associati alla risorsa in CDN]** *e* **[!UICONTROL Annulla validità in base al modello]**, viene creato l&#39;URL di base delle risorse selezionate per l&#39;annullamento della validità. Utilizzare questa disposizione di opzioni solo per le immagini.


   | Opzione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Annulla validità dei predefiniti immagine associati alla risorsa in CDN]** | (Facoltativo) Quando selezioni questa opzione, le risorse selezionate e tutti gli URL predefiniti immagine associati vengono automaticamente formattati per l’annullamento della validità della cache.<br>Assets e i relativi URL predefiniti associati vengono automaticamente formati per l&#39;annullamento della validità. Questa opzione funziona solo per le risorse immagini. |
   | **[!UICONTROL Annullamento della validità in base al modello]** | (Facoltativo) Seleziona questa opzione per utilizzare solo il modello definito per la formazione degli URL. |
   | **[!UICONTROL Aggiungi Assets]** | Utilizza il Selettore risorse per selezionare le risorse da invalidare. Puoi selezionare risorse pubblicate o non pubblicate.<br>La memorizzazione in cache nella rete CDN è basata su URL e non su risorse. Pertanto, è necessario essere a conoscenza degli URL completi presenti sul sito web. Dopo aver determinato tali URL, puoi aggiungerli al modello. Quindi puoi selezionare e aggiungere tali risorse e annullare la validità degli URL in un unico passaggio. <br>Utilizzare questa opzione con **[!UICONTROL Invalidare i predefiniti immagine associati alla risorsa in CDN]**, **[!UICONTROL Invalidare in base al modello]** o entrambi. |
   | **[!UICONTROL Aggiungi URL]** | Aggiungi o incolla manualmente i percorsi URL completi per le risorse Dynamic Media di cui desideri annullare la validità della cache CDN. Utilizzare questa opzione se non è stato creato un modello di annullamento validità CDN in ***Parte 1 di 2: Creazione di un modello di annullamento validità CDN*** e sono disponibili solo alcune risorse da annullare la validità.<br>**Importante:** ogni URL aggiunto deve trovarsi sulla propria riga.<br>È possibile annullare la validità di un massimo di 1000 URL alla volta. Se il numero di URL nel campo di testo **[!UICONTROL Aggiungi URL]** è maggiore di 1000, non è possibile selezionare **[!UICONTROL Avanti]**. In questi casi, è necessario selezionare **[!UICONTROL X]** a destra di una risorsa selezionata o un URL aggiunto manualmente per eliminarla dall&#39;elenco di invalidazione.<br>Specifica gli URL per le ritagli avanzati immagine nel modello di annullamento della validità CDN o in questo campo di testo **[!UICONTROL Aggiungi URL]**. |

1. Seleziona **[!UICONTROL Avanti]** nell&#39;angolo superiore destro della pagina.
1. Nella pagina **[!UICONTROL Annullamento validità CDN - Conferma]**, nella casella di riepilogo **[!UICONTROL URL]** è disponibile un elenco di uno o più URL generati dal modello di annullamento validità CDN creato in precedenza e dalle risorse appena aggiunte.

   Ad esempio, utilizzando l&#39;esempio del modello di invalidazione CDN illustrato nei passaggi precedenti, si supponga di aver aggiunto una singola risorsa denominata `spinset`. Quando si passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Assets]** > **[!UICONTROL Annullamento validità CDN]**, vengono generati i seguenti cinque URL nell&#39;annullamento validità **[!UICONTROL CDN - Conferma]** interfaccia utente:

   ![Annullamento validità CDN - Conferma](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Se necessario, selezionare **X** a destra di un URL per eliminarlo dal processo di invalidazione.

1. Nell&#39;angolo superiore destro della pagina, seleziona **[!UICONTROL Invia]** per avviare il processo di annullamento della validità CDN.

## Risolvere i problemi relativi agli errori di annullamento della validità CDN

In tutti i casi, l’intero batch viene elaborato per l’annullamento della validità o l’intero batch non riesce.

| Errore | Spiegazione |
| --- | --- |
| *Impossibile recuperare gli URL per le risorse selezionate.* | Si verifica se si verifica uno dei seguenti scenari:<br>- Impossibile trovare una configurazione Dynamic Media.<br>- Eccezione durante il recupero di un utente del servizio tramite il quale viene letta la configurazione di Dynamic Media.<br>- Il server di pubblicazione o la directory principale della società utilizzata per formare gli URL non è presente nella configurazione di Dynamic Media. |
| *Alcuni URL non sono definiti correttamente. Correggi e invia di nuovo.* | Si verifica se l&#39;API di annullamento della validità della cache CDN di IPS restituisce un errore che indica che l&#39;URL fa riferimento a un&#39;altra società. Oppure, se l&#39;URL non è valido in base alla convalida eseguita dall&#39;API IPS `cdnCacheInvalidation`. |
| *Impossibile annullare la validità della cache CDN.* | Si verifica se la richiesta di annullamento della validità della cache CDN non riesce per altri motivi. |
| *Nessun URL immesso per essere invalidato.* | Si verifica se non sono presenti URL nella pagina **[!UICONTROL Annullamento validità CDN - Conferma]** e si seleziona **[!UICONTROL Invia]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
