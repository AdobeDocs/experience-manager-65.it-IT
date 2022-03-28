---
title: Annullare la validità della cache della rete di distribuzione dei contenuti tramite Dynamic Media
description: L’annullamento della validità della rete CDN (Content Delivery Network) memorizzata nella cache consente di aggiornare rapidamente le risorse consegnate da Dynamic Media, anziché attendere la scadenza della cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
feature: CDN Cache
exl-id: 23d3c274-0736-49f7-8d44-a56a55cfd06d
source-git-commit: b61157b0e9afa49ef72150ae0c1703a959d154be
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 1%

---


# Invalidare la cache CDN tramite Dynamic Media {#invalidating-cdn-cache-for-dm-assets}

Le risorse Dynamic Media sono memorizzate nella cache della rete CDN (Content Delivery Network) per velocizzarne la distribuzione ai clienti. Tuttavia, quando apporti aggiornamenti a tali risorse, vuoi che tali modifiche abbiano effetto immediatamente sul tuo sito web. L’eliminazione o l’annullamento della validità della cache CDN consente di aggiornare rapidamente le risorse consegnate da Dynamic Media. Invece di attendere la scadenza della cache utilizzando un valore TTL (Time To Live) (l’impostazione predefinita è dieci ore), puoi inviare una richiesta dall’interno di Dynamic Media affinché la cache scada in pochi minuti.



>[!IMPORTANT]
>
>I passaggi seguenti si applicano solo alla modalità Dynamic Media - Scene7 in Adobe Experience Manager 6.5, Service Pack 6 (Experience Manager 6.5.6) o versione successiva. Questa funzione di annullamento della validità della rete CDN richiede anche l’utilizzo della rete CDN preconfigurata inclusa in Adobe Experience Manager - Dynamic Media. Qualsiasi altra CDN personalizzata non è supportata con questa funzione.<br>Se utilizzi Dynamic Media in Experience Manager 6.5, Service Pack 5 (Experience Manager 6.5.5) o versioni precedenti, segui i passaggi descritti in [Annullare la validità della cache CDN tramite Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md).

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Caching overview in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Per annullare la validità del contenuto CDN memorizzato nella cache per le risorse Dynamic Media:**

*Parte 1 di 2: Creazione di un modello di annullamento della validità CDN*

1. In Experience Manager 6.5.6 o versione successiva, passa a **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Annullamento della validità CDN]**.

   ![Funzione di convalida CDN](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. Sulla **[!UICONTROL Modello di annullamento della validità CDN]** , effettua una delle seguenti opzioni in base allo scenario:

   | Scenario | Opzione |
   | --- | --- |
   | In passato ho già creato un modello di invalidazione del CDN utilizzando Dynamic Media Classic. | La **[!UICONTROL Crea modello]** il campo di testo è precompilato con i dati del modello. In tal caso, puoi modificare il modello o continuare con il passaggio successivo. |
   | Devo creare un modello. Cosa entro? | In **[!UICONTROL Crea modello]** campo di testo, immetti un URL immagine (compresi i predefiniti immagine o i modificatori) che fa riferimento a `<ID>`, invece di un ID immagine specifico come nell&#39;esempio seguente:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Se il modello contiene solo `<ID>`, quindi Dynamic Media compila `https://<publishserver_name>/is/image/<company_name>/<ID>` dove `<publishserver_name>` è il nome del server di pubblicazione definito in Impostazioni generali in Dynamic Media Classic. La `<company_name>` è il nome della radice aziendale associata a questa istanza di Experience Manager, e `<ID>` è la risorsa selezionata tramite il selettore risorse da invalidare.<br>Eventuali predefiniti/modificatori vengono pubblicati `<ID>` vengono copiati così come sono nella definizione dell’URL.<br>Solo immagini - cioè, `/is/image` - può essere formato automaticamente in base al modello.<br>Per `/is/content/`, l’aggiunta di risorse come video o PDF utilizzando il selettore risorse non genera automaticamente URL. È invece necessario specificare tali risorse nel modello di annullamento validità CDN oppure è possibile aggiungere manualmente l’URL a tali risorse in *Parte 2 di 2: Impostazione delle opzioni di annullamento della validità CDN*.<br>**Esempi:**<br> In questo primo esempio, il modello di annullamento della validità contiene `<ID>` insieme all’URL della risorsa con `/is/content`. Esempio, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. Dynamic Media forma l’URL in base a questo percorso, con `<ID>` le risorse selezionate tramite il selettore risorse che desideri invalidare.<br>In questo secondo esempio, il modello di invalidazione contiene l’URL completo della risorsa utilizzata nelle proprietà web con `/is/content` (non dipende dal selettore delle risorse). Ad esempio: `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` dove zaino è l’ID risorsa.<br>I formati di risorse supportati in Dynamic Media possono essere invalidati. Tipi di file risorsa *not* supportati per l’annullamento della validità della rete CDN includono PostScript®, Encapsulated PostScript®, Adobe Illustrator, Adobe InDesign, Microsoft® Powerpoint, Microsoft® Excel, Microsoft® Word e Rich Text Format.<br><br>・ Quando crei il modello, ma assicurati di prestare attenzione alla sintassi e agli errori di battitura; Dynamic Media non esegue alcuna convalida del modello.<br>・ Il modello di annullamento validità CDN può salvare testo fino a 2500 caratteri.<br>・ Specificare gli URL per le raccolte avanzate immagini in questo modello di annullamento validità CDN o nel **[!UICONTROL Aggiungi URL]** campo di testo in *Parte 2: Impostazione delle opzioni di annullamento validità CDN.*<br>・ Ogni voce in un modello di annullamento validità CDN deve trovarsi sulla propria riga.<br>・ Il seguente esempio di modello di annullamento validità CDN è solo a scopo dimostrativo. |

   ![Modello di annullamento validità CDN - Crea](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

   >[!NOTE]
   >
   >Il modello di annullamento validità CDN può salvare testo fino a 2500 caratteri.

1. Nell&#39;angolo in alto a destra del **[!UICONTROL Modello di annullamento della validità CDN]** pagina, seleziona **[!UICONTROL Salva]**, quindi seleziona **[!UICONTROL OK]**.<br>

   *Parte 2 di 2: Impostazione delle opzioni di annullamento della validità CDN*
   <br>

1. In Experience Manager as a Cloud Service, seleziona **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Annullamento della validità CDN]**.

   ![Funzione di convalida CDN](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. Sulla **[!UICONTROL Annullamento della validità della rete CDN - Aggiungi dettagli]** seleziona le risorse per l’annullamento della validità CDN.

   ![Annullamento della validità della rete CDN - Aggiungi dettagli](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Se si decide di lasciare le opzioni **[!UICONTROL Annullare la validità dei predefiniti immagine associati alla risorsa in CDN]** *e* **[!UICONTROL Annulla validità in base al modello]** deselezionata, l’URL di base delle risorse selezionate viene formato per l’annullamento della validità. Utilizza questa disposizione di opzione solo per le immagini.


   | Opzione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Annulla validità dei predefiniti immagine associati alla risorsa in CDN]** | (Facoltativo) Quando selezioni questa opzione, le risorse selezionate e tutti gli URL dei predefiniti per immagini associati vengono formati automaticamente per l’annullamento della validità della cache.<br>Le risorse e i relativi URL predefiniti predefiniti predefiniti associati si formano automaticamente per l’annullamento della validità. Questa opzione funziona solo per le risorse immagine. |
   | **[!UICONTROL Annullamento della validità in base al modello]** | (Facoltativo) Seleziona questa opzione per utilizzare solo il modello definito per la formazione degli URL. |
   | **[!UICONTROL Aggiungi risorse]** | Utilizza il Selettore risorse per selezionare le risorse da annullare la validità. Puoi selezionare le risorse pubblicate o non pubblicate.<br>La memorizzazione nella cache della rete CDN è basata su URL, non su risorse. Pertanto, è necessario conoscere gli URL completi presenti sul sito web. Dopo aver determinato tali URL, puoi aggiungerli al modello. Quindi, puoi selezionare e aggiungere tali risorse e annullare la validità degli URL in un unico passaggio. <br>Utilizza questa opzione con **[!UICONTROL Annullare la validità dei predefiniti immagine associati alla risorsa in CDN]** oppure **[!UICONTROL Annullamento della validità in base al modello]** o entrambi. |
   | **[!UICONTROL Aggiungi URL]** | Aggiungi o incolla manualmente percorsi URL completi alle risorse Dynamic Media la cui cache CDN desideri annullare la validità. Utilizza questa opzione se non crei un modello di annullamento validità CDN in ***Parte 1 di 2: Creazione di un modello di annullamento della validità CDN*** e dispongono solo di alcune risorse da annullare la validità.<br>**Importante:** Ogni URL aggiunto deve trovarsi sulla propria riga.<br>Puoi annullare la validità di un massimo di 1000 URL alla volta. Se il numero di URL nel **[!UICONTROL Aggiungi URL]** campo di testo maggiore di 1000. Impossibile selezionare **[!UICONTROL Successivo]**. In questi casi, devi selezionare **[!UICONTROL X]** a destra di una risorsa selezionata o di un URL aggiunto manualmente per eliminarla dall’elenco di annullamento della validità.<br>Specifica gli URL per le raccolte avanzate immagini nel modello di annullamento validità CDN o in questo **[!UICONTROL Aggiungi URL]** campo di testo. |

1. Nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Successivo]**.
1. Sulla **[!UICONTROL Annullamento della validità della rete CDN - Conferma]** nella pagina **[!UICONTROL URL]** casella di riepilogo puoi visualizzare un elenco di uno o più URL generati dal modello di invalidazione del CDN creato in precedenza e delle risorse appena aggiunte.

   Ad esempio, se utilizzi l’esempio Modello di annullamento validità CDN mostrato nei passaggi precedenti, supponi di aver aggiunto una singola risorsa denominata `spinset`. Quando visiti **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Annullamento della validità CDN]**, si traduce nei seguenti cinque URL generati nel **[!UICONTROL Annullamento della validità della rete CDN - Conferma]** interfaccia utente:

   ![Annullamento della validità della rete CDN - Conferma](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Se necessario, seleziona **X** a destra di un URL per eliminarlo dal processo di invalidazione.

1. Nell’angolo in alto a destra della pagina, seleziona **[!UICONTROL Invia]** per avviare il processo di invalidazione del CDN.

## Risolvere i problemi relativi agli errori di invalidazione CDN

In tutti i casi, l&#39;intero batch viene elaborato per l&#39;annullamento della validità oppure l&#39;intero batch non viene elaborato.

| Errore | Spiegazione |
| --- | --- |
| *Impossibile recuperare gli URL per le risorse selezionate.* | Si verifica se viene soddisfatto uno dei seguenti scenari:<br>- Impossibile trovare una configurazione Dynamic Media.<br>- C&#39;è un&#39;eccezione durante il recupero di un utente di servizio attraverso il quale viene letta la configurazione di Dynamic Media.<br>- Il server di pubblicazione o la directory principale dell&#39;azienda utilizzata per formare gli URL è mancante nella configurazione di Dynamic Media. |
| *Alcuni URL non sono definiti correttamente. Correggere e inviare nuovamente.* | Si verifica se l’API di invalidazione della cache CDN IPS restituisce un errore che indica che l’URL fa riferimento a un’azienda diversa. Oppure, se l’URL non è valido in base alla convalida eseguita dall’IPS `cdnCacheInvalidation` API. |
| *Impossibile annullare la validità della cache CDN.* | Si verifica se la richiesta di annullamento della validità della cache CDN non riesce per altri motivi. |
| *Nessun URL immesso da invalidare.* | Si verifica se non sono presenti URL nel **[!UICONTROL Annullamento della validità della rete CDN - Conferma]** e seleziona **[!UICONTROL Invia]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, select **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
