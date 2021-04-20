---
title: Creazione di progetti di traduzione per frammenti di contenuto
seo-title: Creazione di progetti di traduzione per frammenti di contenuto
description: Scopri come tradurre i frammenti di contenuto.
seo-description: Scopri come tradurre i frammenti di contenuto.
uuid: 23176e70-4003-453c-af25-6499a5ed3f6d
contentOwner: heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: d2decc31-a04b-4a8e-bb19-65f21cf7107e
feature: Content Fragments
role: Business Practitioner, Administrator
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 2%

---


# Creazione di progetti di traduzione per frammenti di contenuto {#creating-translation-projects-for-content-fragments}

Oltre alle risorse, Adobe Experience Manager (AEM) Assets supporta i flussi di lavoro di copia per lingua per [frammenti di contenuto](/help/assets/content-fragments/content-fragments.md) (comprese le varianti). Non è necessaria alcuna ottimizzazione aggiuntiva per eseguire flussi di lavoro di copia della lingua sui frammenti di contenuto. In ogni flusso di lavoro, l’intero frammento di contenuto viene inviato per la traduzione.

I tipi di flussi di lavoro che puoi eseguire sui frammenti di contenuto sono esattamente simili ai tipi di flusso di lavoro che esegui per le risorse. Inoltre, le opzioni disponibili all’interno di ciascun tipo di flusso di lavoro corrispondono alle opzioni disponibili nei corrispondenti tipi di flussi di lavoro per le risorse.

Puoi eseguire i seguenti tipi di flussi di lavoro di copia per lingua sui frammenti di contenuto:

**Creare e tradurre**

In questo flusso di lavoro, i frammenti di contenuto da tradurre vengono copiati nella directory principale della lingua in cui si desidera tradurre. Inoltre, a seconda delle opzioni selezionate, nella console Progetti viene creato un progetto di traduzione per i frammenti di contenuto. A seconda delle impostazioni, il progetto di traduzione può essere avviato manualmente o può essere eseguito automaticamente non appena viene creato il progetto di traduzione.

**Aggiorna copie per lingua**

Quando il frammento di contenuto sorgente viene aggiornato o modificato, il frammento di contenuto specifico per le impostazioni internazionali o la lingua corrispondente deve essere riconvertito. Il flusso di lavoro per le copie in lingua aggiornata traduce un gruppo aggiuntivo di frammenti di contenuto e lo include in una copia in lingua per una specifica impostazione internazionale. In questo caso, i frammenti di contenuto tradotti vengono aggiunti alla cartella di destinazione che contiene già frammenti di contenuto tradotti in precedenza.

## Creare e tradurre un flusso di lavoro {#create-and-translate-workflow}

Il flusso di lavoro Crea e traduci include le seguenti opzioni. Le fasi procedurali associate a ciascuna opzione sono simili a quelle associate all’opzione corrispondente per le attività.

* Crea solo struttura: Per le fasi della procedura, consulta [Creare una struttura solo per le risorse](translation-projects.md#create-structure-only).
* Crea un nuovo progetto di traduzione: Per le fasi della procedura, consulta [Creare un nuovo progetto di traduzione per le risorse](translation-projects.md#create-a-new-translation-project).
* Aggiungi al progetto di traduzione esistente: Per le fasi della procedura, consulta [Aggiungi al progetto di traduzione esistente per le risorse](translation-projects.md#add-to-existing-translation-project).

## Aggiorna il flusso di lavoro delle copie in lingua {#update-language-copies-workflow}

Il flusso di lavoro per la copia in lingua di aggiornamento include le seguenti opzioni. Le fasi procedurali associate a ciascuna opzione sono simili a quelle associate all’opzione corrispondente per le attività.

* Crea un nuovo progetto di traduzione: Per le fasi della procedura, consulta [Creare un nuovo progetto di traduzione per le risorse](translation-projects.md#create-a-new-translation-project) (aggiornamento del flusso di lavoro).
* Aggiungi al progetto di traduzione esistente: Per le fasi della procedura, consulta [Aggiungi al progetto di traduzione esistente per le risorse](translation-projects.md#add-to-existing-translation-project) (aggiornamento del flusso di lavoro).

È inoltre possibile creare copie in lingua temporanea per i frammenti in modo analogo a come si creano copie temporanee per le risorse. Per informazioni dettagliate, consulta [Creazione di copie in lingua temporanea per le risorse](translation-projects.md#creating-temporary-language-copies).

## Traduzione di frammenti multimediali diversi {#translating-mixed-media-fragments}

AEM consente di tradurre frammenti di contenuto che includono vari tipi di risorse e raccolte multimediali. Se traduci un frammento di contenuto che include risorse in linea, le copie tradotte di tali risorse vengono memorizzate nella directory principale della lingua di destinazione.

Se il frammento di contenuto include una raccolta, le risorse all’interno della raccolta vengono tradotte insieme al frammento di contenuto. Le copie tradotte delle risorse vengono memorizzate nella directory principale della lingua di destinazione appropriata in una posizione che corrisponde alla posizione fisica delle risorse di origine nella directory principale della lingua di origine.

Per tradurre frammenti di contenuto che includono file multimediali diversi, modifica innanzitutto il framework di traduzione predefinito per abilitare la traduzione di risorse in linea e raccolte associate a frammenti di contenuto.

1. Tocca o fai clic sul logo AEM e passa a **[!UICONTROL Strumenti > Implementazione > Cloud Services]**.
1. Individua **[!UICONTROL Integrazione di traduzione]** in **[!UICONTROL Adobe Marketing Cloud]** e tocca o fai clic su **[!UICONTROL Mostra configurazioni]**.

   ![chlimage_1-444](assets/chlimage_1-444.png)

1. Dall&#39;elenco delle configurazioni disponibili, tocca o fai clic su **[!UICONTROL Configurazione predefinita (configurazione integrazione traduzione)]** per aprire la pagina **[!UICONTROL Configurazione predefinita]**.

   ![chlimage_1-445](assets/chlimage_1-445.png)

1. Fai clic su **[!UICONTROL Modifica]** nella barra degli strumenti per visualizzare la finestra di dialogo **[!UICONTROL Configurazione di traduzione]**.

   ![chlimage_1-446](assets/chlimage_1-446.png)

1. Passa alla scheda **[!UICONTROL Risorse]** e scegli **[!UICONTROL Risorse multimediali in linea e raccolte associate]** dall’elenco **[!UICONTROL Traduci risorse frammento di contenuto]**. Tocca o fai clic su **[!UICONTROL OK]** per salvare le modifiche.

   ![chlimage_1-447](assets/chlimage_1-447.png)

1. Apri un frammento di contenuto dall’interno della cartella principale inglese.

   ![chlimage_1-448](assets/chlimage_1-448.png)

1. Tocca o fai clic sull’icona **[!UICONTROL Inserisci risorsa]** .

   ![chlimage_1-449](assets/chlimage_1-449.png)

1. Inserisci una risorsa nel frammento di contenuto.

   ![inserire una risorsa nel frammento di contenuto](assets/column-view.png)

1. Tocca o fai clic sull’icona **[!UICONTROL Associa contenuto]** .

   ![chlimage_1-451](assets/chlimage_1-451.png)

1. Tocca o fai clic su **[!UICONTROL Associa contenuto]**.

   ![chlimage_1-452](assets/chlimage_1-452.png)

1. Seleziona una raccolta e includerla nel frammento di contenuto. Tocca o fai clic su **[!UICONTROL Salva]**.

   ![chlimage_1-453](assets/chlimage_1-453.png)

1. Seleziona il frammento di contenuto e tocca o fai clic sull&#39;icona **[!UICONTROL GlobalNav]** .
1. Seleziona **[!UICONTROL Riferimenti]** dal menu per visualizzare il riquadro **[!UICONTROL Riferimenti]** .

   ![chlimage_1-454](assets/chlimage_1-454.png)

1. Tocca o fai clic su **[!UICONTROL Copie per lingua]** in **[!UICONTROL Copie]** per visualizzare le copie per lingua.

   ![chlimage_1-455](assets/chlimage_1-455.png)

1. Tocca o fai clic su **[!UICONTROL Crea e traduci]** nella parte inferiore del pannello per visualizzare la finestra di dialogo **[!UICONTROL Crea e traduci]** .

   ![chlimage_1-456](assets/chlimage_1-456.png)

1. Seleziona la lingua di destinazione dall&#39;elenco **[!UICONTROL Lingue di destinazione]**.

   ![chlimage_1-457](assets/chlimage_1-457.png)

1. Seleziona il tipo di progetto di traduzione dall&#39;elenco **[!UICONTROL Progetto]**.

   ![chlimage_1-458](assets/chlimage_1-458.png)

1. Specifica il titolo del progetto nella casella **[!UICONTROL Titolo progetto]** , quindi tocca o fai clic su **Crea**.

   ![chlimage_1-459](assets/chlimage_1-459.png)

1. Passa alla console **[!UICONTROL Progetti]** e apri la cartella del progetto di traduzione creato.

   ![chlimage_1-460](assets/chlimage_1-460.png)

1. Tocca o fai clic sulla sezione del progetto per aprire la pagina dei dettagli del progetto.

   ![chlimage_1-461](assets/chlimage_1-461.png)

1. Dalla sezione Processo di traduzione , verifica il numero di risorse da tradurre.
1. Dalla sezione **[!UICONTROL Processo di traduzione]** , avvia il lavoro di traduzione.

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

