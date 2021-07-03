---
title: Annullare la validità della cache CDN tramite Dynamic Media
description: L’annullamento della validità della rete CDN (Content Delivery Network) memorizzata nella cache consente di aggiornare rapidamente le risorse consegnate da Dynamic Media, anziché attendere la scadenza della cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
exl-id: 23d3c274-0736-49f7-8d44-a56a55cfd06d
feature: Cache CDN
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1366'
ht-degree: 1%

---

# Annullare la validità della cache CDN tramite Dynamic Media {#invalidating-cdn-cache-for-dm-assets}

Le risorse Dynamic Media sono memorizzate nella cache della rete CDN (Content Delivery Network) per velocizzarne la distribuzione ai clienti. Tuttavia, quando apporti aggiornamenti a tali risorse, vuoi che tali modifiche abbiano effetto immediatamente sul tuo sito web. L’eliminazione o l’annullamento della validità della cache CDN consente di aggiornare rapidamente le risorse consegnate da Dynamic Media. Invece di attendere la scadenza della cache utilizzando un valore TTL (Time To Live) (l’impostazione predefinita è dieci ore), puoi inviare una richiesta dall’interno di Dynamic Media affinché la cache scada in pochi minuti.

>[!NOTE]
>
>Questa funzione richiede l’utilizzo della rete CDN preconfigurata fornita con Adobe Experience Manager Dynamic Media. Qualsiasi altra CDN personalizzata non è supportata con questa funzione.

>[!IMPORTANT]
>
>I passaggi seguenti si applicano solo alla modalità Dynamic Media - Scene7 in Adobe Experience Manager 6.5, Service Pack 6 (Experience Manager 6.5.6) o versione successiva. Questa funzione di annullamento della validità della rete CDN richiede anche l’utilizzo della rete CDN preconfigurata fornita con Experience Manager Dynamic Media; qualsiasi altro CDN personalizzato non è supportato.<br>Se utilizzi Dynamic Media in Experience Manager 6.5, Service Pack 5 (Experience Manager 6.5.5) o versioni precedenti, segui i passaggi descritti in  [Invalidazione della cache CDN tramite Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md).

Vedi anche [Panoramica sulla memorizzazione in cache in Dynamic Media](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Per annullare la validità del contenuto CDN memorizzato nella cache per le risorse Dynamic Media:**

*Parte 1 di 2: Creazione di un modello di annullamento della validità CDN*

1. In Experience Manager 6.5.6 o versione successiva, tocca **[!UICONTROL Strumenti > Risorse > Invalidazione CDN]**.

   ![Funzione di convalida CDN](/help/assets/assets-dm/cdn-invalidation-template2.png)

1. Nella pagina **[!UICONTROL Modello di annullamento validità CDN]** , effettua una delle seguenti opzioni in base allo scenario:

   | Scenario | Opzione |
   | --- | --- |
   | In passato ho già creato un modello di invalidazione del CDN utilizzando Dynamic Media Classic. | Il campo di testo **[!UICONTROL Crea modello]** è precompilato con i dati del modello. In tal caso, puoi modificare il modello o continuare con il passaggio successivo. |
   | Devo creare un modello. Cosa entro? | Nel campo di testo **[!UICONTROL Crea modello]**, immetti un URL immagine (compresi i predefiniti immagine o i modificatori) che fa riferimento a `<ID>`, invece di un ID immagine specifico come nell&#39;esempio seguente:<br>`https://my.publishserver.com/is/image/company_name/<ID>?$product$`<br>Se il modello contiene solo `<ID>`, Dynamic Media compila `https://<publishserver_name>/is/image/<company_name>/<ID>` dove `<publishserver_name>` è il nome del server di pubblicazione definito in Impostazioni generali in Dynamic Media Classic. Il `<company_name>` è il nome della directory principale dell’azienda associata a questa istanza di Experience Manager e `<ID>` è la risorsa selezionata tramite il selettore risorse da invalidare.<br>Eventuali predefiniti/modificatori inseriti  `<ID>` vengono copiati così come sono nella definizione dell’URL.<br>Solo le immagini, ovvero  `/is/image` , possono essere formate automaticamente in base al modello.<br>Ad esempio, l’aggiunta di risorse come video o PDF tramite il selettore risorse non genera automaticamente URL.  `/is/content/` È invece necessario specificare tali risorse nel modello di annullamento validità CDN oppure è possibile aggiungere manualmente l’URL a tali risorse in *Parte 2 di 2: Impostazione delle opzioni di annullamento validità CDN*.<br>**Esempi:**<br> in questo primo esempio, il modello di annullamento della validità contiene  `<ID>` insieme all’URL della risorsa  `/is/content`. Esempio, `http://my.publishserver.com:8080/is/content/dms7snapshot/<ID>`. In Dynamic Media l’URL viene creato in base a questo percorso, con `<ID>` come risorse selezionate tramite il selettore delle risorse che desiderate invalidare.<br>In questo secondo esempio, il modello di annullamento della validità contiene l’URL completo della risorsa utilizzata nelle proprietà web con  `/is/content` (non dipendente dal selettore delle risorse). Ad esempio, `http://my.publishserver.com:8080/is/content/dms7snapshot/backpack` dove zaino è l’ID risorsa.<br>I formati di risorse supportati in Dynamic Media possono essere invalidati. I tipi di file risorsa *non* supportati per l’annullamento della validità della rete CDN includono PostScript®, PostScript® incapsulato, Adobe Illustrator, Adobe InDesign, Microsoft Powerpoint, Microsoft Excel, Microsoft Word e formato RTF.<br>Quando crei il modello, ma assicurati di prestare attenzione alla sintassi e agli errori di battitura; Dynamic Media non esegue alcuna convalida del modello.<br>Specifica gli URL per le raccolte avanzate immagini in questo modello di annullamento validità CDN o nel campo  **[!UICONTROL Aggiungi]** URLtext nella  *parte 2: Impostazione delle opzioni di annullamento validità CDN.*<br>**Importante:**ogni voce in un modello di annullamento validità CDN deve trovarsi sulla propria riga.<br>*L’esempio di modello seguente è solo a scopo illustrativo.* |

   ![Modello di annullamento validità CDN - Crea](/help/assets/assets-dm/cdn-invalidation-template-create-2.png)

1. Nell&#39;angolo in alto a destra della pagina **[!UICONTROL Modello di annullamento validità CDN]**, tocca **[!UICONTROL Salva]**, quindi tocca **[!UICONTROL OK]**.<br>

   *Parte 2 di 2: Impostazione delle opzioni di annullamento della validità CDN*
   <br>

1. Ad Experience Manager, come Cloud Service, tocca **[!UICONTROL Strumenti]** > **[!UICONTROL Risorse]** > **[!UICONTROL Annullamento validità CDN]**.

   ![Funzione di convalida CDN](/help/assets/assets-dm/cdn-invalidation-path2.png)

1. Nella pagina **[!UICONTROL Invalidazione CDN - Aggiungi dettagli]** , seleziona le risorse per l’annullamento della validità CDN.

   ![Annullamento della validità della rete CDN - Aggiungi dettagli](/help/assets/assets-dm/cdn-invalidation-add-details-2.png)

   >[!NOTE]
   >
   >Se si decide di deselezionare le opzioni **[!UICONTROL Annulla validità predefiniti immagine associati a risorse in CDN]** *e* **[!UICONTROL Annulla validità in base a modello]**, l&#39;URL di base delle risorse selezionate viene formato per l&#39;annullamento della validità. Utilizza questa disposizione di opzione solo per le immagini.


   | Opzione | Descrizione |
   | --- | --- |
   | **[!UICONTROL Annulla validità dei predefiniti immagine associati alla risorsa in CDN]** | (Facoltativo) Quando selezioni questa opzione, le risorse selezionate e tutti gli URL dei predefiniti per immagini associati vengono formati automaticamente per l’annullamento della validità della cache.<br>Le risorse e i relativi URL predefiniti predefiniti predefiniti associati si formano automaticamente per l’annullamento della validità. Questa opzione funziona solo per le risorse immagine. |
   | **[!UICONTROL Annullamento della validità in base al modello]** | (Facoltativo) Seleziona questa opzione per utilizzare solo il modello definito per la formazione degli URL. |
   | **[!UICONTROL Aggiungi risorse]** | Utilizza il Selettore risorse per selezionare le risorse da annullare la validità. Puoi selezionare le risorse pubblicate o non pubblicate.<br>La memorizzazione nella cache della rete CDN è basata su URL, non su risorse. Pertanto, è necessario conoscere gli URL completi presenti sul sito web. Dopo aver determinato tali URL, puoi aggiungerli al modello. Quindi, puoi selezionare e aggiungere tali risorse e annullare la validità degli URL in un unico passaggio. <br>Utilizza questa opzione con  **[!UICONTROL Annulla validità predefiniti immagine associati alla risorsa in CDN]**,  **[!UICONTROL Annulla validità in base al modello]** o a entrambi. |
   | **[!UICONTROL Aggiungi URL]** | Aggiungi o incolla manualmente percorsi URL completi alle risorse Dynamic Media la cui cache CDN desideri annullare la validità. Utilizza questa opzione se non hai creato un modello di annullamento validità CDN in ***Parte 1 di 2: Creazione di un modello di annullamento validità CDN*** e di alcune risorse da annullare la validità.<br>**Importante:** ogni URL aggiunto deve trovarsi sulla propria riga.<br>Puoi annullare la validità di un massimo di 1000 URL alla volta. Se il numero di URL nel campo di testo **[!UICONTROL Aggiungi URL]** è maggiore di 1000, non è possibile toccare **[!UICONTROL Avanti]**. In questi casi, tocca **[!UICONTROL X]** a destra di una risorsa selezionata o un URL aggiunto manualmente per eliminarla dall’elenco di annullamento della validità.<br>Specifica gli URL per le raccolte avanzate immagini nel modello di annullamento validità CDN o in questo campo  **[!UICONTROL Aggiungi]** URLtext . |

1. Vicino all’angolo superiore destro della pagina, tocca **[!UICONTROL Avanti]**.
1. Nella pagina **[!UICONTROL Invalidazione CDN - Conferma]**, nella casella di riepilogo **[!UICONTROL URL]** puoi visualizzare un elenco di uno o più URL generati dal modello di invalidazione CDN creato in precedenza e delle risorse appena aggiunte.

   Ad esempio, se utilizzi l’esempio Modello di annullamento validità CDN mostrato nei passaggi precedenti, supponi di aver aggiunto una singola risorsa denominata `spinset`. Quando tocchi **[!UICONTROL Strumenti > Risorse > Annullamento della validità della rete CDN]**, nell’interfaccia utente di **[!UICONTROL Annullamento della validità della rete CDN - Conferma]** si ottengono i seguenti cinque URL generati:

   ![Annullamento della validità della rete CDN - Conferma](/help/assets/assets-dm/cdn-invalidation-confirm-2.png)

   Se necessario, tocca **X** a destra di un URL per eliminarlo dal processo di invalidazione.

1. Nell’angolo in alto a destra della pagina, tocca **[!UICONTROL Invia]** per avviare il processo di invalidazione del CDN.

## Risoluzione dei problemi degli errori di invalidazione della rete CDN

In tutti i casi, l&#39;intero batch viene elaborato per l&#39;annullamento della validità oppure l&#39;intero batch non viene elaborato.

| Errore | Spiegazione |
| --- | --- |
| *Impossibile recuperare gli URL per le risorse selezionate.* | Si verifica se viene soddisfatto uno dei seguenti scenari:<br>- Non viene trovata una configurazione Dynamic Media.<br>- C&#39;è un&#39;eccezione durante il recupero di un utente di servizio attraverso il quale viene letta la configurazione di Dynamic Media.<br>- Il server di pubblicazione o la directory principale dell&#39;azienda utilizzata per formare gli URL è mancante nella configurazione di Dynamic Media. |
| *Alcuni URL non sono definiti correttamente. Correggi e invia nuovamente.* | Si verifica se l’API di invalidazione della cache CDN IPS restituisce un errore che indica che l’URL fa riferimento a un’azienda diversa. Oppure, se l’URL non è valido in base alla convalida eseguita dall’API IPS `cdnCacheInvalidation`. |
| *Impossibile annullare la validità della cache CDN.* | Si verifica se la richiesta di annullamento della validità della cache CDN non riesce per altri motivi. |
| *Nessun URL immesso da invalidare.* | Si verifica se nella pagina **[!UICONTROL Invalidazione CDN - Conferma]** non sono presenti URL e si tocca **[!UICONTROL Invia]**. |


<!--  | I do not want to create a template. | Near the upper-right corner of the page, tap **[!UICONTROL Cancel]**, then continue with ***Part 2: Working with CDN Invalidation***. Note that while you are not required to create a template to use CDN Invalidation, Adobe recommends that you create one, especially if you have numerous assets that you need to update immediately, on a regular basis. The template is used at the time you set CDN invalidation options. | -->
