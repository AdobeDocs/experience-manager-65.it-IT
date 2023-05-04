---
title: Riutilizzare le risorse con MSM
description: Utilizzare risorse su più pagine/cartelle derivate e collegate a risorse principali. Le risorse rimangono sincronizzate con una copia primaria e, con alcuni clic, ricevono gli aggiornamenti dalle risorse principali.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin, Architect
feature: Asset Management,Multi Site Manager
exl-id: 4d0367c4-88aa-4aef-b23d-828609b0df09
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '3389'
ht-degree: 10%

---

# Riutilizzare le risorse con MSM per [!DNL Assets] {#reuse-assets-using-msm-for-assets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/reuse-assets-using-msm.html?lang=en) |
| AEM 6.5 | Questo articolo |

Funzionalità Multi Site Manager (MSM) in [!DNL Adobe Experience Manager] consente agli utenti di riutilizzare contenuti creati una volta e riutilizzati in più posizioni web. Lo stesso è disponibile per le risorse digitali come MSM per [!DNL Assets] funzionalità. Utilizzo di MSM per [!DNL Assets], puoi:

* Crea le risorse una volta e quindi fai copie di queste risorse da riutilizzare in altre aree del sito.
* Mantieni più copie in sincronizzazione e aggiorna la copia principale originale una volta per inviare le modifiche alle copie figlio.
* Apporta modifiche locali sospendendo temporaneamente o permanentemente il collegamento tra le risorse principali e secondarie.

## Prerequisiti {#prereq}

Per utilizzare MSM per [!DNL Assets], installa almeno [!DNL Experience Manager] 6.5 Service Pack 1. Per ulteriori informazioni, consulta [le note sulla versione dell&#39;ultimo service pack](/help/release-notes/release-notes.md).

## Comprendere i vantaggi e i concetti {#concepts}

### Come funziona e vantaggi {#how-it-works-and-the-benefits}

Per comprendere gli scenari di utilizzo per riutilizzare lo stesso contenuto (testo e risorse) in più posizioni web, vedi [possibili scenari MSM](/help/sites-administering/msm.md). [!DNL Experience Manager] mantiene un collegamento tra la risorsa originale e le relative copie collegate, denominate Live Copy (LC). Il collegamento mantenuto consente di inviare le modifiche centralizzate a molte Live Copy. Questo consente aggiornamenti più rapidi eliminando i limiti della gestione delle copie duplicate. La propagazione dei cambiamenti è priva di errori e centralizzata. Questa funzionalità consente di aggiornare le Live Copy in modo limitato. Gli utenti possono scollegare il collegamento, ovvero interrompere l’ereditarietà, e apportare modifiche locali che non verranno sovrascritte al successivo aggiornamento della copia principale e al rollout delle modifiche. Lo scollegamento può essere eseguito per alcuni campi di metadati selezionati o per un’intera risorsa. Consente la flessibilità di aggiornare localmente le risorse che sono originariamente ereditate da una copia primaria.

MSM mantiene una relazione live tra la risorsa di origine e le relative Live Copy in modo che:

* Le modifiche alle risorse di origine vengono applicate (rollout) anche alle Live Copy, ovvero le Live Copy sono sincronizzate con l’origine.
* Puoi aggiornare le Live Copy sospendendo la relazione live o rimuovendo l’ereditarietà per alcuni campi limitati. Le modifiche all’origine non vengono più applicate alla Live Copy.

### Glossario di MSM per [!DNL Assets] termini {#glossary}

**Origine:** Le risorse o le cartelle originali. Copia principale da cui derivano le Live Copy.

**Live Copy:** La copia delle risorse/cartelle sorgente in sincronizzazione con la relativa origine. Le Live Copy possono essere una fonte di ulteriori Live Copy. Scopri come creare LC.

**Ereditarietà:** Un collegamento/riferimento tra una risorsa/cartella Live Copy e la relativa origine utilizzato dal sistema per ricordare dove inviare gli aggiornamenti. L’ereditarietà esiste a livello granulare per i campi di metadati. L’ereditarietà può essere rimossa per i campi di metadati selettivi, mantenendo al tempo stesso la relazione live tra la sorgente e la sua Live Copy.

**Rollout:** Un&#39;azione che spinge le modifiche apportate alla sorgente a valle alle sue Live Copy. È possibile aggiornare una o più Live Copy contemporaneamente utilizzando l’azione di rollout. Consulta rollout.

**Configurazione del rollout:** Regole che determinano le proprietà sincronizzate, come e quando. Queste configurazioni vengono applicate durante la creazione di Live Copy; possono essere modificati successivamente; e un figlio può ereditare la configurazione di rollout dalla risorsa principale. Per MSM per [!DNL Assets], utilizza solo la configurazione di rollout standard. Le altre configurazioni di rollout non sono disponibili per MSM per [!DNL Assets].

**Sincronizza:** Un’altra azione, oltre al rollout, che porta la parità tra l’origine e la relativa Live Copy inviando gli aggiornamenti dall’origine alle Live Copy. Viene avviata una sincronizzazione per una particolare Live Copy e l’azione richiama le modifiche dall’origine. Utilizzando questa azione, è possibile aggiornare solo una delle Live Copy. Vedi Sincronizzazione dell&#39;azione.

**Sospendi:** Rimuovi temporaneamente la relazione live tra una Live Copy e la relativa risorsa/cartella sorgente. È possibile riprendere la relazione. Vedi l&#39;azione di sospensione.

**Riprendi:** Riprende la relazione live in modo che una Live Copy riceva nuovamente gli aggiornamenti dall’origine. Vedi l&#39;azione di ripresa.

**Ripristina:** L’azione Reimposta rende la Live Copy nuovamente una replica dell’origine sovrascrivendo eventuali modifiche locali. Inoltre rimuove le cancellazioni di ereditarietà e ripristina l’ereditarietà su tutti i campi di metadati. Per apportare modifiche locali in futuro, è necessario annullare nuovamente l’ereditarietà di campi specifici. Vedi le modifiche locali a LC.

**Stacca:** Rimuovi in modo irreversibile la relazione live di una risorsa/cartella Live Copy. Dopo aver scollegato l’azione, le Live Copy non possono mai ricevere aggiornamenti dall’origine e smette più di essere una Live Copy. Vedere rimozione della relazione.

## Creare una Live Copy di una risorsa {#createlc}

Per creare una Live Copy da una o più risorse o cartelle sorgente, effettua una delle seguenti operazioni:

* Metodo 1: Seleziona le risorse sorgente e fai clic su **[!UICONTROL Crea]** > **[!UICONTROL Live Copy]** dalla barra degli strumenti nella parte superiore.
* Metodo 2: In [!DNL Experience Manager] interfaccia utente, fai clic su **[!UICONTROL Crea]** > **[!UICONTROL Live Copy]** dall’angolo superiore destro dell’interfaccia.

Puoi creare Live Copy di una risorsa o di una cartella una alla volta. Puoi creare Live Copy derivate da una risorsa o da una cartella che è una Live Copy stessa. I frammenti di contenuto (CF) non sono supportati per il caso d’uso. Quando tenti di creare le loro Live Copy, i CF vengono copiati così come sono senza alcuna relazione. I CF copiati sono un&#39;istantanea nel tempo e non si aggiornano quando i CF originali vengono aggiornati.

Per creare Live Copy utilizzando il primo metodo, effettua le seguenti operazioni:

1. Seleziona le risorse o le cartelle sorgente. Dalla barra degli strumenti, fai clic su **[!UICONTROL Crea]** > **[!UICONTROL Live Copy]**.

   ![Crea Live Copy da [!DNL Experience Manager] interfaccia](assets/create_lc1.png)

   *Figura: Crea Live Copy da [!DNL Experience Manager] interfaccia.*

1. Seleziona una cartella di destinazione. Fai clic su **[!UICONTROL Avanti]**.
1. Fornire titolo e nome. Le risorse non hanno figli. Quando crei una Live Copy di cartelle, puoi scegliere di includere o escludere elementi figlio.
1. Seleziona una configurazione di rollout. Fai clic su **[!UICONTROL Crea]**.

Per creare Live Copy utilizzando il secondo metodo, effettua le seguenti operazioni:

1. In [!DNL Experience Manager] interfaccia, dall&#39;angolo in alto a destra, fai clic su **[!UICONTROL Crea]** > **[!UICONTROL Live Copy]**.

   ![Crea Live Copy da [!DNL Experience Manager] interfaccia](assets/create_lc2.png)

   *Figura: Crea Live Copy da [!DNL Experience Manager] interfaccia.*

1. Seleziona la risorsa o la cartella di origine. Fai clic su **[!UICONTROL Avanti]**.
1. Selezionare la cartella di destinazione. Fai clic su **[!UICONTROL Avanti]**.
1. Fornire titolo e nome. Le risorse non hanno figli. Quando crei una Live Copy di cartelle, puoi scegliere di includere o escludere elementi figlio.
1. Seleziona una configurazione di rollout. Fai clic su **[!UICONTROL Crea]**.

>[!NOTE]
>
>Quando si sposta un&#39;origine o una Live Copy, le relazioni vengono mantenute. Quando una Live Copy viene eliminata, le relazioni vengono rimosse.

## Visualizza varie proprietà e stati della sorgente e della Live Copy {#properties}

Puoi visualizzare le informazioni e gli stati relativi a MSM della Live Copy, ad esempio relazione, sincronizzazione, rollout e altro dalle varie aree del [!DNL Experience Manager] interfaccia utente.

I due metodi seguenti funzionano per le risorse e le cartelle:

* Seleziona la risorsa Live Copy e trova le informazioni nella relativa pagina Proprietà .
* Seleziona la cartella di origine e trova le informazioni dettagliate di ogni Live Copy dal [!UICONTROL Console Live Copy].

>[!TIP]
>
>Per verificare lo stato di alcune Live Copy separate, utilizza il primo metodo per controllare il **[!UICONTROL Proprietà]** pagina. Per controllare lo stato di molte Live Copy, utilizza il secondo metodo per controllare il **[!UICONTROL Stato della relazione]** pagina.

### Informazioni e stato di una Live Copy {#statuslcasset}

Per controllare le informazioni e gli stati di una risorsa Live Copy o di una cartella, segui questi passaggi.

1. Seleziona una risorsa Live Copy o una cartella. Fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti. In alternativa, utilizza la scelta rapida da tastiera `p`.
1. Fai clic su **[!UICONTROL Live Copy]**. Puoi controllare il percorso dell’origine, lo stato di sospensione, lo stato di sincronizzazione, la data dell’ultimo rollout e l’utente che ha eseguito l’ultimo rollout.

   ![Le informazioni e gli stati della Live Copy vengono visualizzati in una console in Proprietà](assets/lcfolder_info_properties.png)

   *Figura: Informazioni e stati della Live Copy.*

1. Puoi abilitare o disabilitare se le risorse secondarie prendono in prestito la configurazione Live Copy.

1. Puoi scegliere l’opzione per la Live Copy per ereditare la configurazione di rollout dall’elemento padre o modificare la configurazione.

### Informazioni e stati di tutte le Live Copy di una cartella {#status-lc-folder}

[!DNL Experience Manager] fornisce una console per controllare le statue di tutte le Live Copy di una cartella sorgente. In questa console viene visualizzato lo stato di tutte le risorse secondarie.

1. Selezionare una cartella di origine. Fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti. In alternativa, utilizza la scelta rapida da tastiera `p`.
1. Fai clic su **[!UICONTROL Origine Live Copy]**. Per aprire la console, fai clic su **[!UICONTROL Panoramica Live Copy]**. Questo dashboard offre uno stato di primo livello per tutte le risorse figlie.

   ![Visualizza lo stato delle Live Copy nella console Live Copy di origine](assets/livecopy-statuses.png)

   *Figura: Visualizza lo stato delle Live Copy in [!UICONTROL Console Live Copy] di origine.*

1. Per visualizzare informazioni dettagliate su ciascuna risorsa della cartella Live Copy, seleziona la risorsa in questione, quindi dalla barra degli strumenti fai clic su **[!UICONTROL Stato di relazione]**.

   ![Informazioni dettagliate e stato di una risorsa figlia Live Copy in una cartella](assets/livecopy_relationship_status.png)

   Informazioni dettagliate e stato di una risorsa figlia Live Copy in una cartella

>[!TIP]
>
>È possibile visualizzare rapidamente gli stati delle Live Copy di altre cartelle senza dover navigare troppo. Modificare la cartella dalla parte superiore centrale del **[!UICONTROL Panoramica di Live Copy]** interfaccia.

### Azioni rapide dalla barra Riferimenti per la sorgente {#refrailsource}

Per una risorsa o una cartella di origine, puoi visualizzare le seguenti informazioni ed effettuare le seguenti azioni direttamente dalla barra Riferimenti:

* Guarda i percorsi delle Live Copy.
* Apri o rivela una Live Copy specifica in [!DNL Experience Manager] interfaccia utente.
* Sincronizza gli aggiornamenti con una Live Copy specifica.
* Sospendi la relazione o modifica la configurazione di rollout per una Live Copy specifica.
* Accedi alla console della panoramica Live Copy.

Seleziona la risorsa o la cartella di origine, apri la barra a sinistra e fai clic su **[!UICONTROL Riferimenti]**. In alternativa, seleziona una risorsa o una cartella e utilizza la scelta rapida da tastiera `Alt + 4`.

![Azioni e informazioni disponibili nella barra Riferimenti per l’origine selezionata](assets/referencerail_source.png)

*Figura: Azioni e informazioni disponibili nella barra Riferimenti per l’origine selezionata.*

Per una Live Copy specifica, fai clic su **[!UICONTROL Modifica Live Copy]** per sospendere la relazione o modificare la configurazione di rollout.

![Per una Live Copy specifica, l’opzione per sospendere la relazione o modificare la configurazione di rollout è accessibile dalla barra laterale Riferimenti quando la risorsa sorgente è selezionata](assets/referencerail_editlc_options.png)

*Figura: Sospendi la relazione o cambia la configurazione di rollout di una Live Copy specifica.*

### Azioni rapide dalla barra Riferimenti per Live Copy {#ref-rail-lc}

Per una risorsa o una cartella Live Copy, puoi vedere le seguenti informazioni ed effettuare le seguenti azioni direttamente dalla barra Riferimenti:

* Visualizzare il percorso della relativa sorgente.
* Apri o rivela una Live Copy specifica in [!DNL Experience Manager] interfaccia utente.
* Implementa gli aggiornamenti.

Seleziona una risorsa o una cartella Live Copy, apri la barra a sinistra e fai clic su **[!UICONTROL Riferimenti]**. In alternativa, seleziona una risorsa o una cartella e utilizza la scelta rapida da tastiera `Alt + 4`.

![Azioni disponibili nella barra laterale Riferimenti per la Live Copy selezionata](assets/referencerail_livecopy.png)

*Figura: Azioni disponibili nella barra Riferimenti per la Live Copy selezionata.*

## Propagare le modifiche dall&#39;origine alle Live Copy {#rolloutsync}

Dopo la modifica di un’origine, le modifiche possono essere propagate alle Live Copy utilizzando un’azione di sincronizzazione o un’azione di rollout. Per comprendere la differenza tra le due azioni, vedi [glossario](#glossary).

### Azione di rollout {#rollout}

Puoi avviare un’azione di rollout dalla risorsa sorgente e aggiornare tutte o alcune Live Copy selezionate.

1. Seleziona una risorsa Live Copy o una cartella. Fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti. In alternativa, utilizza la scelta rapida da tastiera `p`.
1. Fai clic su **[!UICONTROL Origine Live Copy]**. Fai clic su **[!UICONTROL Rollout]** dalla barra degli strumenti.
1. Seleziona le Live Copy da aggiornare. Fai clic su **[!UICONTROL Rollout]**.
1. Per eseguire il rollout degli aggiornamenti apportati alle risorse figlio, seleziona **[!UICONTROL Origine rollout e tutti i figli]**.

   ![Implementa le modifiche dell’origine su alcune o tutte le Live Copy](assets/livecopy_rollout_page.png)

   *Figura: Effettua il rollout delle modifiche dell’origine in alcune o tutte le Live Copy.*

>[!NOTE]
>
>Le modifiche apportate a una risorsa di origine vengono implementate solo nelle Live Copy direttamente correlate. Se una Live Copy viene derivata da un’altra Live Copy, le modifiche non vengono implementate nella Live Copy derivata.

In alternativa, puoi avviare un’azione di rollout dalla barra Riferimenti dopo aver selezionato una Live Copy specifica. Per ulteriori informazioni, consulta [Azioni rapide dalla barra Riferimenti per Live Copy](#ref-rail-lc). In questo metodo di rollout, vengono aggiornati solo la Live Copy selezionata ed eventualmente i relativi elementi secondari.

![Implementa le modifiche dell’origine nella Live Copy selezionata](assets/livecopy_rollout_dialog.png)

*Figura: Effettua il rollout delle modifiche dell’origine nella Live Copy selezionata.*

### Informazioni sull’azione di sincronizzazione {#about-sync}

Un’azione di sincronizzazione richiama le modifiche da un’origine solo alla Live Copy selezionata. L’azione di sincronizzazione rispetta e mantiene le modifiche locali eseguite dopo l’annullamento dell’ereditarietà. Le modifiche locali non vengono sovrascritte e l’ereditarietà annullata non viene ristabilita. Puoi avviare un’azione di sincronizzazione in tre modi.

| Dove [!DNL Experience Manager] interfaccia | Quando e perché utilizzare | Come utilizzare |
|---|---|---|
| [!UICONTROL Riferimenti] barra | Sincronizza rapidamente quando la sorgente è già selezionata. | Vedi [Azioni rapide dalla barra Riferimenti per la sorgente](#refrailsource) |
| Barra degli strumenti [!UICONTROL Proprietà] page | Avvia una sincronizzazione quando le proprietà Live Copy sono già aperte. | Vedi [Sincronizzazione di una Live Copy](#sync-lc) |
| [!UICONTROL Panoramica di Live Copy] console | Sincronizza rapidamente più risorse (non necessariamente tutte) quando viene selezionata o [!UICONTROL Panoramica di Live Copy] console già aperta. L’azione di sincronizzazione viene avviata per una risorsa alla volta, ma è un modo più veloce per eseguire la sincronizzazione per più risorse contemporaneamente. | Vedi [Azioni su più risorse in una cartella Live Copy](#bulk-actions) |

### Sincronizzazione di una Live Copy {#sync-lc}

Per avviare un’azione di sincronizzazione, apri la pagina **[!UICONTROL Proprietà]** di una Live Copy, fai clic su **[!UICONTROL Live Copy]** e nella barra degli strumenti seleziona l’azione desiderata.

Per visualizzare gli stati e le informazioni relativi a un’azione di sincronizzazione, consulta le sezioni [Informazioni e stato di una Live Copy](#statuslcasset) e [Informazioni e stati di tutte le Live Copy di una cartella](#status-lc-folder).

![L&#39;azione Sincronizza richiama le modifiche apportate all&#39;origine](assets/livecopy_sync.png)

*Figura: L&#39;azione Sincronizza richiama le modifiche apportate all&#39;origine.*

>[!NOTE]
>
>Se la relazione è sospesa, l’azione di sincronizzazione non è disponibile nella barra degli strumenti. Mentre l’azione di sincronizzazione è disponibile nella barra Riferimenti, le modifiche non vengono propagate anche in seguito a un rollout riuscito.

## Sospendi e riprendi relazione {#suspend-resume}

Puoi sospendere temporaneamente la relazione per impedire a una Live Copy di ricevere le modifiche apportate alla risorsa o alla cartella di origine. La relazione può anche essere ripresa per la Live Copy per iniziare a ricevere le modifiche dalla sorgente.

Per sospendere o riprendere, apri la pagina **[!UICONTROL Proprietà]** di una Live Copy, fai clic su **[!UICONTROL Live Copy]** e nella barra degli strumenti fai clic sull’azione desiderata.

In alternativa, puoi sospendere o riprendere rapidamente le relazioni tra più risorse in una cartella Live Copy della console **[!UICONTROL Panoramica Live Copy]**. Consulta la sezione [Azioni su numerose risorse presenti nelle cartelle Live Copy](#bulk-actions).

## Apportare modifiche locali a una Live Copy {#local-mods}

Una Live Copy è una replica dell’origine originale al momento della creazione. I valori dei metadati di una Live Copy vengono ereditati dall’origine. I campi di metadati mantengono l’ereditarietà individualmente con i rispettivi campi della risorsa sorgente.

Tuttavia, puoi apportare modifiche locali a una Live Copy per cambiare alcune proprietà selezionate. Per eseguire modifiche locali, annulla l’ereditarietà della proprietà desiderata. Quando l’ereditarietà di uno o più campi di metadati viene annullata, si mantiene la relazione live della risorsa e l’ereditarietà degli altri campi di metadati. Qualsiasi sincronizzazione o rollout non sovrascrive le modifiche locali. Per farlo, apri **[!UICONTROL Proprietà]** di una risorsa Live Copy, fai clic sul pulsante **[!UICONTROL annulla ereditarietà]** accanto a un campo di metadati.

Puoi annullare tutte le modifiche locali e ripristinare lo stato della risorsa all’origine. L’azione Reimposta sostituisce irrevocabilmente e istantaneamente tutte le modifiche locali e ristabilisce l’ereditarietà su tutti i campi di metadati. Per ripristinare, dal **[!UICONTROL Proprietà]** pagina di una risorsa Live Copy, fai clic su **[!UICONTROL Reimposta]** dalla barra degli strumenti.

![L’azione Reimposta sovrascrive le modifiche locali e porta la Live Copy in parte con la relativa origine.](assets/livecopy_reset.png)

*Figura: L’azione Reimposta sovrascrive le modifiche locali e porta la Live Copy in parte con la relativa origine.*

## Rimuovi relazione live {#detach}

È possibile rimuovere completamente la relazione tra un&#39;origine e una Live Copy utilizzando l&#39;azione Stacca. La Live Copy diventa una risorsa o una cartella autonoma dopo essere stata staccata. Viene visualizzato come nuova risorsa in [!DNL Experience Manager] immediatamente dopo lo scollegamento. Per scollegare una Live Copy dall’origine, effettua le seguenti operazioni.

1. Seleziona una risorsa o una cartella Live Copy. Fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti. In alternativa, utilizza la scelta rapida da tastiera `p`.

1. Fai clic su **[!UICONTROL Live Copy]**. Fai clic su **[!UICONTROL Stacca]** nella barra degli strumenti. Fai clic su **[!UICONTROL Stacca]** dalla finestra di dialogo presentata.

   ![L&#39;azione Scollega rimuove completamente la relazione tra l&#39;origine e la Live Copy](assets/livecopy_detach.png)

   *Figura: L&#39;azione Scollega rimuove completamente la relazione tra origine e Live Copy.*

   >[!CAUTION]
   >
   >La relazione viene rimossa immediatamente quando fai clic su **[!UICONTROL Stacca]** dalla finestra di dialogo. Non è possibile annullarlo facendo clic su **[!UICONTROL Annulla]** nella pagina Proprietà.

In alternativa, è possibile scollegare rapidamente più risorse in una cartella Live Copy da **[!UICONTROL Panoramica di Live Copy]** console. Consulta la sezione [Azioni su numerose risorse presenti nelle cartelle Live Copy](#bulk-actions).

## Azioni in blocco in una cartella Live Copy {#bulk-actions}

Se una cartella Live Copy contiene più risorse, l’avvio di azioni su ciascuna risorsa può risultare noioso. Puoi avviare rapidamente le azioni di base su più risorse da [!UICONTROL Console Live Copy]. I metodi di cui sopra continuano a funzionare per le singole risorse.

1. Selezionare una cartella di origine. Fai clic su **[!UICONTROL Proprietà]** dalla barra degli strumenti. In alternativa, utilizza la scelta rapida da tastiera `p`.
1. Fai clic su **[!UICONTROL Origine Live Copy]**. Per aprire la console, fai clic su **[!UICONTROL Panoramica Live Copy]**.
1. In questo dashboard, seleziona una risorsa Live Copy da una cartella Live Copy. Nella barra degli strumenti, scegli le azioni desiderate. Le azioni disponibili sono: **[!UICONTROL Sincronizza]**, **[!UICONTROL Reimposta]**, **[!UICONTROL Sospendi]** e **[!UICONTROL Stacca]**. Puoi avviare rapidamente queste azioni su qualsiasi risorsa presente in un numero qualsiasi di cartelle Live Copy che si trovano in una relazione diretta con la cartella sorgente selezionata.

   ![Aggiornare facilmente molte risorse nelle cartelle Live Copy dalla console Panoramica Live Copy](assets/livecopyconsole_update_many_assets.png)

   *Figura: Aggiornare facilmente molte risorse nelle cartelle Live Copy da [!UICONTROL Panoramica di Live Copy] console.*

## Estendi MSM per [!DNL Assets] {#extend-api}

[!DNL Experience Manager] consente di estendere la funzionalità utilizzando le API Java MSM. Per [!DNL Assets], l&#39;estensione funziona esattamente come con MSM per [!DNL Sites]. Per maggiori dettagli, vedi [Estensione dell&#39;MSM](/help/sites-developing/extending-msm.md) e quanto segue per informazioni su attività specifiche:

* [Panoramica delle API](/help/sites-developing/extending-msm.md#overview-of-the-java-api)
* [Creare un’azione di sincronizzazione](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action)
* [Creare una configurazione di rollout](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration)
* [Creare e utilizzare una semplice classe LiveActionFactory](/help/sites-developing/extending-msm.md#creating-and-using-a-simple-liveactionfactory-class)

>[!NOTE]
>
>* Blueprint in MSM per [!DNL Sites] è chiamata sorgente Live Copy in MSM per [!DNL Assets].
>* La rimozione del passaggio dei capitoli nella creazione guidata del sito non è supportata in MSM per [!DNL Assets].
>* La configurazione dei blocchi MSM, sulle proprietà della pagina (interfaccia touch), non è supportata in MSM per [!DNL Assets].


## Impatto delle attività di gestione delle risorse sulle Live Copy {#manage-assets}

Le Live Copy e le origini sono risorse o cartelle che possono essere gestite, in una certa misura, come risorse digitali. Alcune attività di gestione delle risorse in [!DNL Experience Manager] hanno un impatto specifico sulle Live Copy.

* Copiando una Live Copy, crea una risorsa Live Copy con la stessa origine della prima Live Copy.
* Quando si sposta un&#39;origine o la relativa Live Copy, la relazione live viene mantenuta.
* L’azione Modifica non funziona per le risorse Live Copy. Se l’origine di una Live Copy è di per sé una Live Copy, l’azione di modifica non funziona.
* L’azione di estrazione non è disponibile per le risorse Live Copy.
* Per la cartella di origine è disponibile l’opzione per creare attività di revisione.
* Quando visualizzi l’elenco delle risorse nella vista a elenco e nella vista a colonne, una risorsa o una cartella Live Copy visualizza la dicitura &quot;Live Copy&quot;. Consente di identificare facilmente le Live Copy in una cartella.

## Confronta MSM per [!DNL Assets] e [!DNL Sites] {#comparison}

In più scenari, MSM per [!DNL Assets] corrisponde al comportamento di MSM per la funzionalità Sites. Alcune differenze chiave da notare sono:

* Blueprint in MSM per [!DNL Sites] è chiamata sorgente Live Copy in MSM per [!DNL Assets].
* In Sites puoi confrontare una blueprint e la sua Live Copy, ma non è possibile in [!DNL Assets] per confrontare un’origine con la sua Live Copy.
* Non è possibile modificare una Live Copy in [!DNL Assets].
* I siti di solito hanno figli, ma [!DNL Assets] No. L’opzione per includere o escludere elementi figlio non è presente quando si creano Live Copy di singole risorse.
* La rimozione del passaggio dei capitoli nella creazione guidata del sito non è supportata in MSM per [!DNL Assets].
* La configurazione dei blocchi MSM sulle proprietà di pagina (interfaccia touch) non è supportata in MSM per [!DNL Assets].
* Per MSM per [!DNL Assets], utilizza solo **[!UICONTROL Configurazione di rollout standard]**. Le altre configurazioni di rollout non sono disponibili per MSM per [!DNL Assets].

## Best practice {#best-practices}

Alcune best practice per MSM sono:

* Pianifica le relazioni padre-figlio dei flussi di risorse e contenuti prima di avviare l’implementazione.

## Limitazioni e problemi noti di MSM per [!DNL Assets] {#limitations}

Di seguito è riportata una limitazione di MSM per [!DNL Assets].

* I frammenti di contenuto (CF) non sono supportati per il caso d’uso. Quando tenti di creare le loro Live Copy, i CF vengono copiati così come sono senza alcuna relazione. I CF copiati sono un&#39;istantanea nel tempo e non vengono aggiornati quando i CF originali vengono aggiornati.

* MSM non funziona con il write-back dei metadati abilitato. Al successivo ripristino, l&#39;ereditarietà si interrompe.
