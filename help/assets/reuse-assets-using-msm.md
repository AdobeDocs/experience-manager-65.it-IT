---
title: Riutilizzare le risorse con MSM
description: Utilizza le risorse in più pagine/cartelle derivate da e collegate alle risorse principali. Le risorse rimangono sincronizzate con una copia principale e, con pochi clic, ricevono gli aggiornamenti dalle risorse principali.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin, Architect
feature: Asset Management,Multi Site Manager
exl-id: 4d0367c4-88aa-4aef-b23d-828609b0df09
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3284'
ht-degree: 9%

---

# Riutilizzare le risorse tramite MSM per [!DNL Assets] {#reuse-assets-using-msm-for-assets}

| Versione | Collegamento articolo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Fai clic qui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/reuse-assets-using-msm.html?lang=en) |
| AEM 6.5 | Questo articolo |

Funzionalità Multi Site Manager (MSM) in [!DNL Adobe Experience Manager] consente agli utenti di riutilizzare i contenuti creati una volta e riutilizzati in più posizioni web. Lo stesso è disponibile per le risorse digitali di MSM per [!DNL Assets] funzionalità. Utilizzo di MSM per [!DNL Assets], è possibile:

* Crea una volta le risorse, quindi copiale per riutilizzarle in altre aree del sito.
* Mantieni più copie sincronizzate e aggiorna la copia principale originale una sola volta per inviare le modifiche alle copie secondarie.
* Apporta modifiche locali sospendendo temporaneamente o definitivamente il collegamento tra le risorse principali e secondarie.

## Prerequisiti {#prereq}

Per utilizzare MSM per [!DNL Assets], installare almeno [!DNL Experience Manager] 6.5 Service Pack 1 Per ulteriori informazioni, consulta [le note sulla versione del service pack più recente](/help/release-notes/release-notes.md).

## Comprendere i vantaggi e i concetti {#concepts}

### Come funziona e i vantaggi {#how-it-works-and-the-benefits}

Per comprendere gli scenari di utilizzo per il riutilizzo dello stesso contenuto (testo e risorse) in più posizioni web, consulta [possibili scenari MSM](/help/sites-administering/msm.md). [!DNL Experience Manager] mantiene un collegamento tra la risorsa originale e le relative copie collegate, denominate Live Copy (LC). Il collegamento mantenuto consente di inviare le modifiche centralizzate a molte Live Copy. In questo modo è possibile eseguire aggiornamenti più rapidi eliminando le limitazioni della gestione delle copie duplicate. La propagazione delle modifiche è senza errori e centralizzata. Questa funzionalità consente di eseguire aggiornamenti limitati alle Live Copy selezionate. Gli utenti possono scollegare il collegamento, ovvero interrompere l’ereditarietà, e apportare modifiche locali che non vengono sovrascritte la prossima volta che la copia primaria viene aggiornata e le modifiche vengono implementate. Lo scollegamento può essere eseguito per alcuni campi di metadati selezionati o per un’intera risorsa. Offre flessibilità per l’aggiornamento locale delle risorse originariamente ereditate da una copia principale.

MSM mantiene una relazione live tra la risorsa sorgente e le relative Live Copy in modo che:

* Le modifiche alle risorse sorgente vengono applicate (implementate) anche alle Live Copy, ovvero le Live Copy vengono sincronizzate con la sorgente.
* Puoi aggiornare le Live Copy sospendendo la relazione live o rimuovendo l’ereditarietà per alcuni campi limitati. Le modifiche all’origine non vengono più applicate alla Live Copy.

### Glossario di MSM per [!DNL Assets] termini {#glossary}

**Origine:** Le risorse o cartelle originali. Copia primaria da cui derivano le Live Copy.

**Live Copy:** Copia delle risorse/cartelle di origine sincronizzate con la relativa origine. Le Live Copy possono essere una fonte di ulteriori Live Copy. Scopri come creare LC.

**Ereditarietà:** Un collegamento/riferimento tra una risorsa/cartella Live Copy e la relativa origine che il sistema utilizza per ricordare dove inviare gli aggiornamenti. L’ereditarietà esiste a livello granulare per i campi di metadati. È possibile rimuovere l’ereditarietà per i campi di metadati selettivi mantenendo la relazione live tra l’origine e la relativa Live Copy.

**Rollout:** Azione che invia le modifiche apportate all’origine a valle alle relative Live Copy. È possibile aggiornare una o più Live Copy in una sola volta utilizzando l’azione di rollout. Consulta Rollout.

**Configurazione rollout:** Regole che determinano quali proprietà vengono sincronizzate, come e quando. Queste configurazioni vengono applicate durante la creazione di Live Copy; possono essere modificate in un secondo momento; e un figlio può ereditare la configurazione di rollout dalla risorsa principale. Per MSM per [!DNL Assets], utilizza solo la configurazione di rollout standard. Le altre configurazioni di rollout non sono disponibili per MSM per [!DNL Assets].

**Sincronizza:** Un’altra azione, oltre al rollout, che porta parità tra l’origine e la relativa Live Copy inviando gli aggiornamenti dall’origine alle Live Copy. Viene avviata una sincronizzazione per una particolare Live Copy e l’azione richiama le modifiche dall’origine. Utilizzando questa azione, è possibile aggiornare solo una delle Live Copy. Consulta azione di sincronizzazione.

**Sospendi:** Rimuovi temporaneamente la relazione live tra una Live Copy e la relativa risorsa/cartella di origine. È possibile riprendere la relazione. Consulta Azione di sospensione.

**Riprendi:** Riprendi la relazione live in modo che una Live Copy inizi nuovamente a ricevere gli aggiornamenti dall’origine. Consulta Riprendere l’azione.

**Reimposta:** L’azione Reimposta rende nuovamente la Live Copy una replica dell’origine sovrascrivendo eventuali modifiche locali. Rimuove inoltre le cancellazioni di ereditarietà e ripristina l’ereditarietà su tutti i campi di metadati. Per apportare modifiche locali in futuro, è necessario annullare nuovamente l’ereditarietà di campi specifici. Vedere modifiche locali di LC.

**Scollega:** Rimuovi irrevocabilmente la relazione live di una risorsa/cartella Live Copy. Dopo l’azione di scollegamento, le Live Copy non possono mai ricevere aggiornamenti dall’origine e cessano di essere Live Copy. Consulta rimuovere la relazione.

## Creare una Live Copy di una risorsa {#createlc}

Per creare una Live Copy da una o più risorse o cartelle di origine, effettua una delle seguenti operazioni:

* Metodo 1: seleziona le risorse di origine e fai clic su **[!UICONTROL Crea]** > **[!UICONTROL Live Copy]** dalla barra degli strumenti nella parte superiore.
* Metodo 2: In [!DNL Experience Manager] interfaccia utente, fai clic su **[!UICONTROL Crea]** > **[!UICONTROL Live Copy]** dall’angolo superiore destro dell’interfaccia.

Puoi creare live copy di una risorsa o cartella una alla volta. Puoi creare Live Copy derivate da una risorsa o da una cartella che è essa stessa una Live Copy. I frammenti di contenuto (CF) non sono supportati per il caso d’uso. Quando si tenta di creare le proprie Live Copy, le CF vengono copiate così come sono senza alcuna relazione. I CF copiati sono uno snapshot nel tempo e non si aggiornano quando i CF originali vengono aggiornati.

Per creare Live Copy utilizzando il primo metodo, effettua le seguenti operazioni:

1. Seleziona le risorse o le cartelle di origine. Dalla barra degli strumenti, fai clic su **[!UICONTROL Crea]** > **[!UICONTROL Live Copy]**.

   ![Crea Live Copy da [!DNL Experience Manager] Interfaccia](assets/create_lc1.png)

   *Figura: Creare una Live Copy da [!DNL Experience Manager] di rete.*

1. Seleziona una cartella di destinazione. Fai clic su **[!UICONTROL Avanti]**.
1. Immetti titolo e nome. Le risorse non hanno elementi figlio. Quando crei una Live Copy delle cartelle, puoi scegliere di includerne o escluderne altre secondarie.
1. Seleziona una configurazione di rollout. Fai clic su **[!UICONTROL Crea]**.

Per creare Live Copy utilizzando il secondo metodo, segui questi passaggi:

1. In entrata [!DNL Experience Manager] dall&#39;angolo superiore destro, fare clic su **[!UICONTROL Crea]** > **[!UICONTROL Live Copy]**.

   ![Crea Live Copy da [!DNL Experience Manager] Interfaccia](assets/create_lc2.png)

   *Figura: Creare una Live Copy da [!DNL Experience Manager] di rete.*

1. Seleziona la risorsa o la cartella di origine. Fai clic su **[!UICONTROL Avanti]**.
1. Seleziona la cartella di destinazione. Fai clic su **[!UICONTROL Avanti]**.
1. Immetti titolo e nome. Le risorse non hanno elementi figlio. Quando crei una Live Copy delle cartelle, puoi scegliere di includerne o escluderne altre secondarie.
1. Seleziona una configurazione di rollout. Fai clic su **[!UICONTROL Crea]**.

>[!NOTE]
>
>Quando un’origine o una Live Copy viene spostata, le relazioni vengono mantenute. Quando una Live Copy viene eliminata, le relazioni vengono rimosse.

## Visualizzare varie proprietà e stati di sorgente e Live Copy {#properties}

Puoi visualizzare le informazioni e gli stati relativi a MSM di Live Copy, ad esempio relazione, sincronizzazione, rollout e altro ancora, dalle varie aree della [!DNL Experience Manager] dell&#39;utente.

I due metodi seguenti funzionano per le risorse e le cartelle:

* Seleziona la risorsa Live Copy e trova le informazioni nella relativa pagina Proprietà.
* Seleziona la cartella di origine e trova le informazioni dettagliate di ciascuna Live Copy dalla sezione [!UICONTROL Console Live Copy].

>[!TIP]
>
>Per verificare lo stato di alcune Live Copy separate, utilizza il primo metodo per controllare **[!UICONTROL Proprietà]** pagina. Per verificare lo stato di molte Live Copy, utilizza il secondo metodo per controllare **[!UICONTROL Stato di relazione]** pagina.

### Informazioni e stato di una Live Copy {#statuslcasset}

Per verificare le informazioni e gli stati di una risorsa Live Copy o di una cartella, segui la procedura riportata di seguito.

1. Seleziona una risorsa Live Copy o una cartella. Clic **[!UICONTROL Proprietà]** dalla barra degli strumenti. In alternativa, utilizza la scelta rapida da tastiera `p`.
1. Clic **[!UICONTROL Live Copy]**. Puoi controllare il percorso dell’origine, lo stato della sospensione, lo stato della sincronizzazione, la data dell’ultimo rollout e l’utente che ha eseguito l’ultimo rollout.

   ![Le informazioni e gli stati della Live Copy vengono visualizzati in una console in Proprietà](assets/lcfolder_info_properties.png)

   *Figura: Informazioni e stati della Live Copy.*

1. Puoi abilitare o disabilitare se le risorse figlie prendono in prestito la configurazione Live Copy.

1. Puoi scegliere l’opzione per la Live Copy per ereditare la configurazione di rollout dall’elemento padre o modificare la configurazione.

### Informazioni e stati di tutte le Live Copy di una cartella {#status-lc-folder}

[!DNL Experience Manager] fornisce una console per controllare le statistiche di tutte le live copy di una cartella sorgente. Questa console visualizza lo stato di tutte le risorse figlie.

1. Selezionare una cartella di origine. Clic **[!UICONTROL Proprietà]** dalla barra degli strumenti. In alternativa, utilizza la scelta rapida da tastiera `p`.
1. Fai clic su **[!UICONTROL Origine Live Copy]**. Per aprire la console, fai clic su **[!UICONTROL Panoramica Live Copy]**. Questo dashboard offre uno stato di primo livello per tutte le risorse figlie.

   ![Visualizzare gli stati delle Live Copy nella console Live Copy dell’origine](assets/livecopy-statuses.png)

   *Figura: Visualizzare gli stati delle Live Copy in [!UICONTROL Console Live Copy] di origine.*

1. Per visualizzare informazioni dettagliate su ciascuna risorsa della cartella Live Copy, seleziona la risorsa in questione, quindi dalla barra degli strumenti fai clic su **[!UICONTROL Stato di relazione]**.

   ![Informazioni dettagliate e stato di una risorsa figlia Live Copy in una cartella](assets/livecopy_relationship_status.png)

   Informazioni dettagliate e stato di una risorsa figlia Live Copy in una cartella

>[!TIP]
>
>Puoi visualizzare rapidamente gli stati delle Live Copy di altre cartelle senza dover sfogliare troppo. Cambia la cartella dalla parte superiore centrale del **[!UICONTROL Panoramica Live Copy]** di rete.

### Azioni rapide dalla barra Riferimenti per l’origine {#refrailsource}

Per una risorsa o una cartella di origine, puoi visualizzare le seguenti informazioni ed eseguire le azioni seguenti direttamente dalla barra Riferimenti:

* Visualizza i percorsi delle Live Copy.
* Aprire o visualizzare una Live Copy specifica in [!DNL Experience Manager] dell&#39;utente.
* Sincronizza gli aggiornamenti a una Live Copy specifica.
* Sospendi la relazione o modifica la configurazione di rollout per una Live Copy specifica.
* Accedi alla console Panoramica Live Copy.

Seleziona la risorsa o la cartella di origine, apri la barra a sinistra e fai clic su **[!UICONTROL Riferimenti]**. In alternativa, seleziona una risorsa o una cartella e utilizza la scelta rapida da tastiera `Alt + 4`.

![Azioni e informazioni disponibili nella barra laterale Riferimenti per l’origine selezionata](assets/referencerail_source.png)

*Figura: Azioni e informazioni disponibili nella barra Riferimenti per la sorgente selezionata.*

Per una Live Copy specifica, fai clic su **[!UICONTROL Modifica Live Copy]** per sospendere la relazione o modificare la configurazione di rollout.

![Per una Live Copy specifica, l’opzione per sospendere la relazione o modificare la configurazione di rollout è accessibile dalla barra Riferimenti quando la risorsa sorgente è selezionata](assets/referencerail_editlc_options.png)

*Figura: Sospendere la relazione o modificare la configurazione di rollout di una Live Copy specifica.*

### Azioni rapide dalla barra Riferimenti per Live Copy {#ref-rail-lc}

Per una risorsa o una cartella Live Copy, puoi visualizzare le seguenti informazioni ed eseguire le azioni seguenti direttamente dalla barra Riferimenti:

* Visualizzare il percorso della relativa origine.
* Aprire o visualizzare una Live Copy specifica in [!DNL Experience Manager] dell&#39;utente.
* Eseguire il rollout degli aggiornamenti.

Seleziona una risorsa o una cartella Live Copy, apri la barra a sinistra e fai clic su **[!UICONTROL Riferimenti]**. In alternativa, seleziona una risorsa o una cartella e utilizza la scelta rapida da tastiera `Alt + 4`.

![Azioni disponibili nella barra laterale Riferimenti per la Live Copy selezionata](assets/referencerail_livecopy.png)

*Figura: Azioni disponibili nella barra laterale Riferimenti per la Live Copy selezionata.*

## Propagare le modifiche dall’origine alle Live Copy {#rolloutsync}

Dopo la modifica di un’origine, le modifiche possono essere propagate alle Live Copy utilizzando un’azione di sincronizzazione o un’azione di rollout. Per comprendere la differenza tra le due azioni, consulta [glossario](#glossary).

### Rollout, azione {#rollout}

Puoi avviare un’azione di rollout dalla risorsa sorgente e aggiornare tutte o alcune Live Copy selezionate.

1. Seleziona una risorsa Live Copy o una cartella. Clic **[!UICONTROL Proprietà]** dalla barra degli strumenti. In alternativa, utilizza la scelta rapida da tastiera `p`.
1. Fai clic su **[!UICONTROL Origine Live Copy]**. Clic **[!UICONTROL Rollout]** dalla barra degli strumenti.
1. Seleziona le Live Copy da aggiornare. Clic **[!UICONTROL Rollout]**.
1. Per eseguire il rollout degli aggiornamenti apportati alle risorse figlie, seleziona **[!UICONTROL Rollout origine e tutti gli elementi figlio]**.

   ![Eseguire il rollout delle modifiche dell’origine per alcune o tutte le Live Copy](assets/livecopy_rollout_page.png)

   *Figura: Eseguire il rollout delle modifiche dell’origine per alcune o tutte le Live Copy.*

>[!NOTE]
>
>Le modifiche apportate in una risorsa sorgente vengono implementate solo nelle Live Copy direttamente correlate. Se una Live Copy è derivata da un’altra Live Copy, le modifiche non vengono implementate nella Live Copy derivata.

In alternativa, puoi avviare un’azione di rollout dalla barra Riferimenti dopo aver selezionato una Live Copy specifica. Per ulteriori informazioni, consulta [Azioni rapide dalla barra Riferimenti per Live Copy](#ref-rail-lc). In questo metodo di rollout, vengono aggiornate solo la Live Copy selezionata e, facoltativamente, i relativi elementi secondari.

![Eseguire il rollout delle modifiche dell’origine nella Live Copy selezionata](assets/livecopy_rollout_dialog.png)

*Figura: Eseguire il rollout delle modifiche dell’origine alla Live Copy selezionata.*

### Informazioni sull’azione di sincronizzazione {#about-sync}

Un’azione di sincronizzazione richiama le modifiche da un’origine solo alla Live Copy selezionata. L’azione di sincronizzazione rispetta e mantiene le modifiche locali apportate dopo l’annullamento dell’ereditarietà. Le modifiche locali non vengono sovrascritte e l’ereditarietà annullata non viene ristabilita. È possibile avviare un&#39;azione di sincronizzazione in tre modi.

| Dove in [!DNL Experience Manager] Interfaccia | Quando e perché utilizzare | Come usare |
|---|---|---|
| [!UICONTROL Riferimenti] barra | Sincronizzazione rapida quando l&#39;origine è già selezionata. | Consulta [Azioni rapide dalla barra Riferimenti per l’origine](#refrailsource) |
| Barra degli strumenti in [!UICONTROL Proprietà] pagina | Avvia una sincronizzazione quando le proprietà Live Copy sono già aperte. | Consulta [Sincronizzare una Live Copy](#sync-lc) |
| [!UICONTROL Panoramica Live Copy] console | Sincronizzare rapidamente più risorse (non necessariamente tutte) quando viene selezionata la cartella di origine o [!UICONTROL Panoramica Live Copy] la console è già aperta. L’azione di sincronizzazione viene avviata per una risorsa alla volta, ma consente una sincronizzazione più rapida per più risorse in un’unica operazione. | Consulta [Azioni su molte risorse in una cartella Live Copy](#bulk-actions) |

### Sincronizzare una Live Copy {#sync-lc}

Per avviare un’azione di sincronizzazione, apri la pagina **[!UICONTROL Proprietà]** di una Live Copy, fai clic su **[!UICONTROL Live Copy]** e nella barra degli strumenti seleziona l’azione desiderata.

Per visualizzare gli stati e le informazioni relativi a un’azione di sincronizzazione, consulta le sezioni [Informazioni e stato di una Live Copy](#statuslcasset) e [Informazioni e stati di tutte le Live Copy di una cartella](#status-lc-folder).

![L&#39;azione Sincronizza richiama le modifiche apportate all&#39;origine](assets/livecopy_sync.png)

*Figura: Sincronizza: richiama le modifiche apportate all&#39;origine.*

>[!NOTE]
>
>Se la relazione è sospesa, l’azione di sincronizzazione non è disponibile nella barra degli strumenti. Anche se l’azione di sincronizzazione è disponibile nella barra Riferimenti, le modifiche non vengono propagate anche in caso di rollout riuscito.

## Sospendi e riprendi relazione {#suspend-resume}

Puoi sospendere temporaneamente la relazione per impedire a una Live Copy di ricevere le modifiche apportate alla risorsa o alla cartella di origine. È inoltre possibile riprendere la relazione affinché la Live Copy inizi a ricevere le modifiche dall’origine.

Per sospendere o riprendere, apri la pagina **[!UICONTROL Proprietà]** di una Live Copy, fai clic su **[!UICONTROL Live Copy]** e nella barra degli strumenti fai clic sull’azione desiderata.

In alternativa, puoi sospendere o riprendere rapidamente le relazioni tra più risorse in una cartella Live Copy della console **[!UICONTROL Panoramica Live Copy]**. Consulta la sezione [Azioni su numerose risorse presenti nelle cartelle Live Copy](#bulk-actions).

## Apportare modifiche locali a una Live Copy {#local-mods}

Una Live Copy è una replica dell’origine originale al momento della creazione. I valori dei metadati di una Live Copy vengono ereditati dal sorgente. I campi di metadati mantengono singolarmente l’ereditarietà con i rispettivi campi della risorsa sorgente.

Tuttavia, puoi apportare modifiche locali a una Live Copy per cambiare alcune proprietà selezionate. Per eseguire modifiche locali, annulla l’ereditarietà della proprietà desiderata. Quando l’ereditarietà di uno o più campi di metadati viene annullata, si mantiene la relazione live della risorsa e l’ereditarietà degli altri campi di metadati. Qualsiasi sincronizzazione o rollout non sovrascrive le modifiche locali. Per farlo, apri **[!UICONTROL Proprietà]** di una risorsa live copy, fai clic sulla **[!UICONTROL annulla ereditarietà]** accanto a un campo di metadati.

Puoi annullare tutte le modifiche locali e ripristinare lo stato della risorsa corrispondente all’origine. L’azione Reimposta esegue l’override irrevocabile e istantaneo di tutte le modifiche locali e ristabilisce l’ereditarietà di tutti i campi di metadati. Per ripristinare, da **[!UICONTROL Proprietà]** pagina di una risorsa live copy, fai clic su **[!UICONTROL Reimposta]** dalla barra degli strumenti.

![L’azione Reimposta sovrascrive le modifiche locali e porta la Live Copy in parte con la sua origine.](assets/livecopy_reset.png)

*Figura: L’azione Reimposta sovrascrive le modifiche locali e porta la Live Copy in parte con la sua origine.*

## Rimuovi relazione live {#detach}

Puoi rimuovere completamente la relazione tra un’origine e una Live Copy utilizzando l’azione Stacca. La Live Copy diventa una risorsa o una cartella autonoma dopo essere stata scollegata. Viene visualizzata come nuova risorsa in [!DNL Experience Manager] immediatamente dopo il distacco. Per scollegare una Live Copy dalla sua origine, segui la procedura riportata di seguito.

1. Seleziona una risorsa o una cartella Live Copy. Clic **[!UICONTROL Proprietà]** dalla barra degli strumenti. In alternativa, utilizza la scelta rapida da tastiera `p`.

1. Clic **[!UICONTROL Live Copy]**. Clic **[!UICONTROL Stacca]** nella barra degli strumenti. Clic **[!UICONTROL Stacca]** dalla finestra di dialogo presentata.

   ![L’azione Stacca rimuove completamente la relazione tra origine e Live Copy](assets/livecopy_detach.png)

   *Figura: L’azione Stacca rimuove completamente la relazione tra origine e Live Copy.*

   >[!CAUTION]
   >
   >La relazione viene rimossa immediatamente quando si fa clic su **[!UICONTROL Stacca]** dalla finestra di dialogo. Non è possibile annullarla facendo clic su **[!UICONTROL Annulla]** nella pagina Proprietà.

In alternativa, è possibile scollegare rapidamente più risorse in una cartella Live Copy dalla **[!UICONTROL Panoramica Live Copy]** console. Consulta la sezione [Azioni su numerose risorse presenti nelle cartelle Live Copy](#bulk-actions).

## Azioni collettive in una cartella Live Copy {#bulk-actions}

Se in una cartella Live Copy sono presenti più risorse, l’avvio di azioni su ciascuna risorsa può essere laborioso. Puoi avviare rapidamente le azioni di base su molte risorse da [!UICONTROL Console Live Copy]. I metodi di cui sopra continuano a funzionare per le singole risorse.

1. Selezionare una cartella di origine. Clic **[!UICONTROL Proprietà]** dalla barra degli strumenti. In alternativa, utilizza la scelta rapida da tastiera `p`.
1. Fai clic su **[!UICONTROL Origine Live Copy]**. Per aprire la console, fai clic su **[!UICONTROL Panoramica Live Copy]**.
1. In questo dashboard, seleziona una risorsa Live Copy da una cartella Live Copy. Nella barra degli strumenti, scegli le azioni desiderate. Le azioni disponibili sono **[!UICONTROL Sincronizza]**, **[!UICONTROL Reimposta]**, **[!UICONTROL Sospendi]**, e **[!UICONTROL Stacca]**. Puoi avviare rapidamente queste azioni su qualsiasi risorsa in un numero qualsiasi di cartelle Live Copy che si trovano in una relazione live con la cartella di origine selezionata.

   ![Aggiornare facilmente molte risorse nelle cartelle Live Copy dalla console Panoramica Live Copy](assets/livecopyconsole_update_many_assets.png)

   *Figura: Aggiornare facilmente molte risorse nelle cartelle Live Copy dalla [!UICONTROL Panoramica Live Copy] console.*

## Impatto delle attività di gestione risorse sulle Live Copy {#manage-assets}

Le Live Copy e le origini sono risorse o cartelle che possono essere gestite, in una certa misura, come risorse digitali. Alcune attività di gestione risorse in [!DNL Experience Manager] hanno un impatto specifico sulle Live Copy.

* Quando copi una Live Copy, crea una risorsa Live Copy con la stessa origine della prima Live Copy.
* Quando sposti un’origine o la relativa Live Copy, la relazione live viene mantenuta.
* L&#39;azione di modifica non funziona per le risorse Live Copy. Se l’origine di una Live Copy è una Live Copy in sé, l’azione di modifica non funziona per essa.
* L&#39;azione Check-Out non è disponibile per le risorse Live Copy.
* Per la cartella di origine, è disponibile l’opzione per creare attività di revisione.
* Quando visualizzi l’elenco delle risorse nella vista a elenco e nella vista a colonne, una risorsa o cartella Live Copy mostra una Live Copy insieme a essa. Consente di identificare facilmente le Live Copy in una cartella.

## Confronta MSM per [!DNL Assets] e [!DNL Sites] {#comparison}

In più scenari, MSM per [!DNL Assets] corrisponde al comportamento di MSM per la funzionalità Sites. Alcune differenze chiave da notare sono:

* Blueprint in MSM per [!DNL Sites] si chiama origine Live Copy in MSM per [!DNL Assets].
* In Sites puoi confrontare una blueprint e la relativa Live Copy, ma non è possibile in [!DNL Assets] per confrontare un’origine con la relativa live copy.
* Impossibile modificare una Live Copy in [!DNL Assets].
* I siti di solito hanno figli, ma [!DNL Assets] non farlo. L’opzione per includere o escludere elementi secondari non è presente durante la creazione di Live Copy di singole risorse.
* La rimozione del passaggio capitoli nella procedura guidata Crea sito non è supportata in MSM per [!DNL Assets].
* La configurazione dei blocchi MSM nelle proprietà della pagina (interfaccia utente touch) non è supportata in MSM per [!DNL Assets].
* Per MSM per [!DNL Assets], utilizza solo **[!UICONTROL Configurazione rollout standard]**. Le altre configurazioni di rollout non sono disponibili per MSM per [!DNL Assets].

## Best practice {#best-practices}

Alcune best practice per MSM sono:

* Pianifica le relazioni padre-figlio dei flussi di risorse e contenuto prima di avviare l’implementazione.

## Limitazioni e problemi noti di MSM per [!DNL Assets] {#limitations}

Segue una limitazione di MSM per [!DNL Assets].

* I frammenti di contenuto (CF) non sono supportati per il caso d’uso. Quando si tenta di creare le proprie Live Copy, le CF vengono copiate così come sono senza alcuna relazione. I CF copiati sono uno snapshot nel tempo e non si aggiornano quando i CF originali vengono aggiornati.

* MSM non funziona con il writeback dei metadati abilitato. Al writeback, l&#39;ereditarietà si interrompe.
