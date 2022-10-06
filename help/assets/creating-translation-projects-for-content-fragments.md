---
title: Creazione di progetti di traduzione per frammenti di contenuto
seo-title: Creating Translation Projects for Content Fragments
description: Scopri come tradurre i frammenti di contenuto.
seo-description: Learn how to translate content fragments.
uuid: 23176e70-4003-453c-af25-6499a5ed3f6d
contentOwner: heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: d2decc31-a04b-4a8e-bb19-65f21cf7107e
feature: Content Fragments
role: User, Admin
exl-id: 19bb58da-8220-404e-bddb-34be94a3a7d7
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 2%

---

# Creazione di progetti di traduzione per frammenti di contenuto {#creating-translation-projects-for-content-fragments}

Oltre alle risorse, Adobe Experience Manager (AEM) Assets supporta i flussi di lavoro di copia per lingua per [frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) (comprese le variazioni). Non è necessaria alcuna ottimizzazione aggiuntiva per eseguire flussi di lavoro di copia della lingua sui frammenti di contenuto. In ogni flusso di lavoro, l’intero frammento di contenuto viene inviato per la traduzione.

I tipi di flussi di lavoro che puoi eseguire sui frammenti di contenuto sono esattamente simili ai tipi di flusso di lavoro che esegui per le risorse. Inoltre, le opzioni disponibili all’interno di ciascun tipo di flusso di lavoro corrispondono alle opzioni disponibili nei corrispondenti tipi di flussi di lavoro per le risorse.

Puoi eseguire i seguenti tipi di flussi di lavoro di copia per lingua sui frammenti di contenuto:

**Crea e traduci**

In questo flusso di lavoro, i frammenti di contenuto da tradurre vengono copiati nella directory principale della lingua in cui si desidera tradurre. Inoltre, a seconda delle opzioni selezionate, nella console Progetti viene creato un progetto di traduzione per i frammenti di contenuto. A seconda delle impostazioni, il progetto di traduzione può essere avviato manualmente o può essere eseguito automaticamente non appena viene creato il progetto di traduzione.

**Aggiorna copie per lingua**

Quando il frammento di contenuto sorgente viene aggiornato o modificato, il frammento di contenuto specifico per le impostazioni internazionali o la lingua corrispondente deve essere riconvertito. Il flusso di lavoro per le copie in lingua aggiornata traduce un gruppo aggiuntivo di frammenti di contenuto e lo include in una copia in lingua per una specifica impostazione internazionale. In questo caso, i frammenti di contenuto tradotti vengono aggiunti alla cartella di destinazione che contiene già frammenti di contenuto tradotti in precedenza.

## Creare e tradurre un flusso di lavoro {#create-and-translate-workflow}

Il flusso di lavoro Crea e traduci include le seguenti opzioni. Le fasi procedurali associate a ciascuna opzione sono simili a quelle associate all’opzione corrispondente per le attività.

* Crea solo struttura: Per le fasi della procedura, vedi [Creare una struttura solo per le risorse](translation-projects.md#create-structure-only).
* Crea un nuovo progetto di traduzione: Per le fasi della procedura, vedi [Crea un nuovo progetto di traduzione per le risorse](translation-projects.md#create-a-new-translation-project).
* Aggiungi al progetto di traduzione esistente: Per le fasi della procedura, vedi [Aggiungi al progetto di traduzione esistente per le risorse](translation-projects.md#add-to-existing-translation-project).

## Aggiorna flusso di lavoro copie per lingua {#update-language-copies-workflow}

Il flusso di lavoro per la copia in lingua di aggiornamento include le seguenti opzioni. Le fasi procedurali associate a ciascuna opzione sono simili a quelle associate all’opzione corrispondente per le attività.

* Crea un nuovo progetto di traduzione: Per le fasi della procedura, vedi [Crea un nuovo progetto di traduzione per le risorse](translation-projects.md#create-a-new-translation-project) (aggiorna flusso di lavoro).
* Aggiungi al progetto di traduzione esistente: Per le fasi della procedura, vedi [Aggiungi al progetto di traduzione esistente per le risorse](translation-projects.md#add-to-existing-translation-project) (aggiorna flusso di lavoro).

È inoltre possibile creare copie in lingua temporanea per i frammenti in modo analogo a come si creano copie temporanee per le risorse. Per maggiori dettagli, vedi [Creazione di copie in lingua temporanea per le risorse](translation-projects.md#creating-temporary-language-copies).

## Traduzione di frammenti di file multimediali diversi {#translating-mixed-media-fragments}

AEM consente di tradurre frammenti di contenuto che includono vari tipi di risorse e raccolte multimediali. Se traduci un frammento di contenuto che include risorse in linea, le copie tradotte di tali risorse vengono memorizzate nella directory principale della lingua di destinazione.

Se il frammento di contenuto include una raccolta, le risorse all’interno della raccolta vengono tradotte insieme al frammento di contenuto. Le copie tradotte delle risorse vengono memorizzate nella directory principale della lingua di destinazione appropriata in una posizione che corrisponde alla posizione fisica delle risorse di origine nella directory principale della lingua di origine.

Per tradurre frammenti di contenuto che includono file multimediali diversi, modifica innanzitutto il framework di traduzione predefinito per abilitare la traduzione di risorse in linea e raccolte associate a frammenti di contenuto.

1. Tocca o fai clic sul logo AEM e passa a **[!UICONTROL Strumenti > Implementazione > Cloud Services]**.
1. Individua **[!UICONTROL Integrazione della traduzione]** sotto **[!UICONTROL Adobe Marketing Cloud]** e tocca o fai clic su **[!UICONTROL Mostra configurazioni]**.

   ![chlimage_1-444](assets/chlimage_1-444.png)

1. Dall’elenco delle configurazioni disponibili, tocca o fai clic su **[!UICONTROL Configurazione predefinita (configurazione integrazione traduzione)]** per aprire **[!UICONTROL Configurazione predefinita]** pagina.

   ![chlimage_1-445](assets/chlimage_1-445.png)

1. Fai clic su **[!UICONTROL Modifica]** dalla barra degli strumenti per visualizzare **[!UICONTROL Configurazione della traduzione]** finestra di dialogo.

   ![chlimage_1-446](assets/chlimage_1-446.png)

1. Passa a **[!UICONTROL Risorse]** e scegli **[!UICONTROL Risorse multimediali in linea e raccolte associate]** dal **[!UICONTROL Tradurre le risorse dei frammenti di contenuto]** elenco. Tocca o fai clic **[!UICONTROL OK]** per salvare le modifiche.

   ![chlimage_1-447](assets/chlimage_1-447.png)

1. Apri un frammento di contenuto dall’interno della cartella principale inglese.

   ![chlimage_1-448](assets/chlimage_1-448.png)

1. Tocca o fai clic su **[!UICONTROL Inserisci risorsa]** icona.

   ![chlimage_1-449](assets/chlimage_1-449.png)

1. Inserisci una risorsa nel frammento di contenuto.

   ![inserire una risorsa nel frammento di contenuto](assets/column-view.png)

1. Tocca o fai clic su **[!UICONTROL Associa contenuto]** icona.

   ![chlimage_1-451](assets/chlimage_1-451.png)

1. Tocca o fai clic **[!UICONTROL Associa contenuto]**.

   ![chlimage_1-452](assets/chlimage_1-452.png)

1. Seleziona una raccolta e includerla nel frammento di contenuto. Tocca o fai clic **[!UICONTROL Salva]**.

   ![chlimage_1-453](assets/chlimage_1-453.png)

1. Seleziona il frammento di contenuto e tocca o fai clic sul pulsante **[!UICONTROL Navigazione globale]** icona.
1. Seleziona **[!UICONTROL Riferimenti]** dal menu per visualizzare il **[!UICONTROL Riferimenti]** riquadro.

   ![chlimage_1-454](assets/chlimage_1-454.png)

1. Tocca o fai clic **[!UICONTROL Copie per lingua]** sotto **[!UICONTROL Copie]** per visualizzare le copie della lingua.

   ![chlimage_1-455](assets/chlimage_1-455.png)

1. Tocca o fai clic **[!UICONTROL Crea e traduci]** nella parte inferiore del pannello per visualizzare il **[!UICONTROL Crea e traduci]** finestra di dialogo.

   ![chlimage_1-456](assets/chlimage_1-456.png)

1. Seleziona la lingua di destinazione dal **[!UICONTROL Lingue di destinazione]** elenco.

   ![chlimage_1-457](assets/chlimage_1-457.png)

1. Seleziona il tipo di progetto di traduzione dal **[!UICONTROL Progetto]** elenco.

   ![chlimage_1-458](assets/chlimage_1-458.png)

1. Specifica il titolo del progetto nella **[!UICONTROL Titolo del progetto]** quindi fai clic/tocca **Crea**.

   ![chlimage_1-459](assets/chlimage_1-459.png)

1. Passa a **[!UICONTROL Progetti]** e apri la cartella del progetto per il progetto di traduzione creato.

   ![chlimage_1-460](assets/chlimage_1-460.png)

1. Tocca o fai clic sulla sezione del progetto per aprire la pagina dei dettagli del progetto.

   ![chlimage_1-461](assets/chlimage_1-461.png)

1. Dalla sezione Processo di traduzione , verifica il numero di risorse da tradurre.
1. Da **[!UICONTROL Processo di traduzione]** riquadro, avvia il lavoro di traduzione.

   ![chlimage_1-462](assets/chlimage_1-462.png)

1. Fai clic sull’ellissi nella parte inferiore della sezione Processo di traduzione per visualizzare lo stato del lavoro di traduzione.

   ![chlimage_1-463](assets/chlimage_1-463.png)

1. Tocca o fai clic sul frammento di contenuto per controllare il percorso delle risorse associate tradotte.

   ![chlimage_1-464](assets/chlimage_1-464.png)

1. Nella console Raccolte , rivedi la copia per lingua della raccolta.

   ![chlimage_1-465](assets/chlimage_1-465.png)

   Si noti che solo il contenuto della raccolta è tradotto. La raccolta stessa non è tradotta.

1. Passa al percorso della risorsa associata tradotta. Tieni presente che la risorsa tradotta è memorizzata nella directory principale della lingua di destinazione.

   ![chlimage_1-466](assets/chlimage_1-466.png)

1. Passa alle risorse all’interno della raccolta che vengono tradotte insieme al frammento di contenuto. Tieni presente che le copie tradotte delle risorse sono memorizzate nella directory principale della lingua di destinazione appropriata.

   ![chlimage_1-467](assets/chlimage_1-467.png)

   >[!NOTE]
   >
   >Le procedure per aggiungere un frammento di contenuto a un progetto esistente o per eseguire flussi di lavoro di aggiornamento sono simili alle procedure corrispondenti per le risorse. Per un orientamento su tali procedure, fare riferimento alle procedure descritte per le attività.
