---
title: Aggiunta di informazioni dai dati utente ai metadati di invio del modulo
seo-title: Aggiunta di informazioni dai dati utente ai metadati di invio del modulo
description: 'Scoprite come aggiungere informazioni ai metadati di un modulo inviato con i dati forniti dall''utente. '
seo-description: 'Scoprite come aggiungere informazioni ai metadati di un modulo inviato con i dati forniti dall''utente. '
uuid: c3eea3c0-31f8-4bf8-b5cf-34f907bdbdba
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2c971da0-5bd5-40d1-820d-4efc2a44b49d
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---


# Aggiunta di informazioni dai dati utente ai metadati di invio del modulo{#adding-information-from-user-data-to-form-submission-metadata}

È possibile utilizzare i valori immessi in un elemento del modulo per calcolare i campi di metadati di una bozza o di un invio di un modulo. I metadati consentono di filtrare i contenuti in base ai dati utente. Ad esempio, un utente immette John Doe nel campo del nome del modulo. Potete utilizzare queste informazioni per calcolare i metadati in grado di classificare l&#39;invio in base al JD iniziale.

Per calcolare i campi di metadati con i valori immessi dall’utente, aggiungere elementi del modulo nei metadati. Quando un utente immette un valore in tale elemento, uno script utilizza il valore per calcolare le informazioni. Queste informazioni vengono aggiunte nei metadati. Quando aggiungete un elemento come campo di metadati, dovete fornire una chiave. La chiave viene aggiunta come un campo nei metadati e le informazioni calcolate vengono registrate rispetto ad essa.

Ad esempio, un&#39;impresa di assicurazione sanitaria pubblica un modulo. In questo modulo, un campo acquisisce l&#39;età degli utenti finali. Dopo l&#39;invio del modulo da parte di un certo numero di utenti, il cliente desidera controllare tutti gli invii effettuati in una determinata fascia di età. Anziché esaminare tutti i dati che si complicano con l&#39;aumento del numero di moduli, metadati aggiuntivi sono utili per il cliente. L&#39;autore del modulo può configurare le proprietà/i dati compilati dall&#39;utente finale affinché la ricerca sia più semplice. Per metadati aggiuntivi si intendono le informazioni compilate dall’utente memorizzate al livello principale del nodo di metadati, durante la configurazione dell’autore.

Considerare un altro esempio di modulo che acquisisce ID e-mail e numero di telefono. Quando un utente visita il modulo in modo anonimo e lo abbandona, l&#39;autore può configurare il modulo per il salvataggio automatico dell&#39;ID e-mail e del numero di telefono. Questo modulo viene salvato automaticamente e il numero di telefono e l&#39;ID e-mail vengono memorizzati nel nodo di metadati della bozza. Un esempio di utilizzo di questa configurazione è il dashboard di gestione dei lead.

## Aggiunta di elementi del modulo ai metadati {#adding-form-elements-to-metadata}

Per aggiungere un elemento nei metadati, effettuate le seguenti operazioni:

1. Aprire il modulo adattivo in modalità di modifica.\
   Per aprire il modulo in modalità di modifica, nel modulo di gestione selezionare il modulo e toccare **Apri**.
1. In modalità di modifica, selezionate un componente, toccate ![livello campo](assets/field-level.png) > **Contenitore modulo adattivo**, quindi toccate ![cmppr](assets/cmppr.png).
1. Nella barra laterale, fate clic su **Metadati**.
1. Nella sezione Metadati, fate clic su **Aggiungi**.
1. Utilizzare il campo Valore della scheda Metadati per aggiungere script. Gli script aggiunti raccolgono i dati dagli elementi del modulo e calcolano i valori che vengono inviati ai metadati.

   Ad esempio, **true** viene registrato nei metadati se la pagina immessa è maggiore di 21 e **false** viene registrato se è inferiore a 21. Nella scheda Metadati, inserite il seguente script:

   `(agebox.value >= 21) ? true : false`

   ![Script metadati](assets/add-element-metadata.png)

   Script immesso nella scheda Metadati

1. Fai clic su **OK**.

Dopo che un utente ha immesso i dati nell&#39;elemento selezionato come campo di metadati, le informazioni calcolate vengono registrate nei metadati. Potete visualizzare i metadati nella directory archivio configurata per la memorizzazione dei metadati.

## Visualizzazione dei metadati di invio del modulo aggiornati: {#seeing-updated-form-nbsp-submission-metadata}

Per l’esempio precedente, i metadati sono memorizzati nell’archivio CRX. I metadati sono come:

![Metadati](assets/metadata_entry_new.png)

Se aggiungete un elemento casella di controllo nei metadati, i valori selezionati vengono memorizzati come una stringa separata da virgole. Ad esempio, è possibile aggiungere un componente casella di controllo nel modulo e specificarne il nome come `checkbox1`. Nelle proprietà del componente della casella di controllo vengono aggiunti gli elementi Patente di guida, Numero previdenza sociale e Passaporto per i valori 0, 1 e 2.

![Memorizzazione di più valori da una casella di controllo](assets/checkbox-metadata.png)

È possibile selezionare un contenitore di moduli adattivi e nelle proprietà del modulo aggiungere una chiave di metadati `cb1` che memorizza `checkbox1.value` e pubblicare il modulo. Quando un cliente compila il modulo, il cliente seleziona le opzioni Passport e Social Security Number nel campo della casella di controllo. I valori 1 e 2 sono memorizzati come 1, 2 nel campo cb1 dei metadati di invio.

![Voce di metadati per più valori selezionati in un campo casella di controllo](assets/metadata-entry.png)

>[!NOTE]
>
>L&#39;esempio precedente è solo a scopo di apprendimento. Accertatevi di cercare i metadati nella posizione corretta, come configurato nell’implementazione AEM Forms .

