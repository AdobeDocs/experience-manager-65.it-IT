---
title: Sincronizzazione di Adaptive Forms con i modelli di moduli XFA
seo-title: Synchronizing Adaptive Forms with XFA Form Templates
description: Sincronizzazione dei moduli adattivi con file XFA/XDP.
seo-description: Synchronizing Adaptive forms with XFA/XDP files.
uuid: 92818132-1ae0-4576-84f2-ece485a34457
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: dac4539b-804d-4420-9170-68000ebb2638
docset: aem65
feature: Adaptive Forms
exl-id: fed67c23-a9b7-403e-9199-dfd527d5f209
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 0%

---

# Sincronizzazione di Adaptive Forms con i modelli di moduli XFA{#synchronizing-adaptive-forms-with-xfa-form-templates}

## Introduzione {#introduction}

Puoi creare un modulo adattivo basato su un modello di modulo XFA ( `*.XDP` file). Questo riutilizzo consente di preservare l’investimento nei moduli XFA esistenti. Per informazioni su come utilizzare un modello di modulo XFA per creare un modulo adattivo, [Creare un modulo adattivo basato su un modello](../../forms/using/creating-adaptive-form.md#p-create-an-adaptive-form-based-on-an-xfa-form-template-p).

Puoi riutilizzare i campi del file XDP nel modulo adattivo. Questi campi sono denominati campi associati. Le proprietà dei campi associati (come script, etichette e formato di visualizzazione) vengono copiate dal file XDP. È inoltre possibile scegliere di ignorare il valore di alcune di queste proprietà.

AEM Forms consente di mantenere i campi dei moduli adattivi sincronizzati con eventuali modifiche apportate successivamente ai campi corrispondenti nel file XDP. Questo articolo spiega come abilitare questa sincronizzazione.

![È possibile trascinare campi da un modulo XFA a un modulo adattivo](assets/drag-drop-xfa.gif.gif)

Nell’ambiente di authoring di AEM Forms, è possibile trascinare campi da un modulo XFA (a sinistra) a un modulo adattivo (a destra)

## Prerequisiti {#prerequisites}

Per utilizzare le informazioni contenute in questo articolo, si consiglia di acquisire familiarità con le seguenti aree:

* [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md)

* XFA (XML Forms Architecture)

Per utilizzare le risorse fornisce l’esempio nell’articolo, scarica il pacchetto di esempio come spiegato nella sezione successiva, [Pacchetto di esempio](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-sample-package-p).

## Pacchetto di esempio {#sample-package}

L’articolo utilizza un esempio per dimostrare come sincronizzare il modulo adattivo con un modello di modulo XFA aggiornato. Le risorse utilizzate nell’esempio sono disponibili in un pacchetto, che può essere scaricato dal [Download](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-downloads-p) in questo articolo.

Dopo aver caricato il pacchetto, puoi visualizzare queste risorse nell’interfaccia utente di AEM Forms.

Installa il pacchetto utilizzando il gestore di pacchetti: `https://<server>:<port>/crx/packmgr/index.jsp`

Il pacchetto contiene le seguenti risorse:

1. `sample-form.xdp`: Modello di modulo XFA utilizzato come esempio

1. `sample-xfa-af`: Il modulo adattivo basato sul file sample-form.xdp. Questo modulo adattivo, tuttavia, non include alcun campo. Nel passaggio successivo, verrà aggiunto del contenuto a questo modulo adattivo.

### Aggiungere contenuto al modulo adattivo {#add-content-to-adaptive-form-br}

1. Vai su https://&lt;server>:&lt;port>/aem/forms.html. Immetti le tue credenziali se richiesto.
1. Apri sample-af-xfa per la modifica in modalità di authoring.
1. Dal browser Contenuto nella barra laterale, scegliete la scheda Oggetti modello dati . Trascinare NumericField1 e TextField1 nel Modulo adattivo.
1. Modificare il titolo del campo numerico1 da **Campo numerico** a **Campo numerico AF.**

>[!NOTE]
>
>Nei passaggi precedenti, abbiamo sovrascritto una proprietà di un campo nel file XDP. Questa proprietà, quindi, non verrà sincronizzata se la proprietà corrispondente nel file XDP viene modificata in seguito.

## Rilevamento delle modifiche nel file XDP {#detecting-changes-in-xdp-file}

Ogni volta che si verificano modifiche in un file XDP o in un frammento, l’interfaccia utente di AEM Forms contrassegna tutti i moduli adattivi basati sul file XDP o sul frammento.

Dopo aver aggiornato un file XDP, devi caricarlo di nuovo nell’interfaccia utente di AEM Forms per segnalare le modifiche.

Ad esempio, aggiorniamo il `sample-form.xdp` utilizzando i seguenti passaggi:

1. Passa a `https://<server>:<port>/projects.html.` Immetti le tue credenziali, se richiesto.
1. Fai clic sulla scheda Forms a sinistra.
1. Scarica la `sample-form.xdp` sul computer locale. Il file XDP viene scaricato come `.zip` file, che può essere estratto utilizzando qualsiasi utilità di decompressione file.

1. Apri `sample-form.xdp` e modificare il titolo del campo TextField1 da **Campo di testo** a **Campo di testo personale**.

1. Carica il `sample-form.xdp` torna all’interfaccia utente di AEM Forms.

Se un file XDP viene aggiornato, compare un’icona nell’editor quando si modificano i moduli adattivi in base al file XDP. Questa icona indica che il modulo adattivo non è sincronizzato con il file XDP. Nell’immagine seguente, vedi l’icona accanto nella barra laterale.

![Icona per visualizzare che il modulo adattivo non è sincronizzato con il file XDP](assets/sync-af-xfa.png)

## Sincronizzazione dei moduli adattivi con il file XDP più recente {#synchronizing-adaptive-forms-with-the-latest-xdp-file}

Quando un modulo adattivo non sincronizzato con il file XDP viene aperto per la creazione successiva, viene visualizzato il seguente messaggio: **Schema/modello di modulo per il modulo adattivo è stato aggiornato. `Click Here` per riavviarlo con la nuova versione.**

Facendo clic sul messaggio, i campi del modulo adattivo vengono sincronizzati con i campi corrispondenti nel file XDP.

Per l&#39;esempio utilizzato in questo articolo, apri `sample-xfa-af` in modalità authoring. Il messaggio viene visualizzato nella parte inferiore del modulo adattivo.

![Messaggio che richiede la sincronizzazione del modulo adattivo con il file XDP](assets/sync-af-xfa-1.png)

### Aggiornamento delle proprietà {#updating-the-properties}

Tutte le proprietà copiate dal file XDP al modulo adattivo vengono aggiornate, ad eccezione delle proprietà esplicitamente sostituite nel modulo adattivo (dalla finestra di dialogo Componenti) dall’autore. L’elenco delle proprietà che sono state aggiornate è disponibile nei registri del server.

Per aggiornare le proprietà nel modulo adattivo di esempio, fai clic sul collegamento (con etichetta) `"Click Here"`) nel messaggio. Il titolo di TextField1 cambia da **Campo di testo** a **Campo di testo personale**.

![update-property](assets/update-property.png)

>[!NOTE]
>
>L&#39;etichetta AF Numeric Field non è stata modificata perché hai ignorato questa proprietà dalla finestra di dialogo delle proprietà del componente, come descritto in [Aggiungere contenuto ai moduli adattivi](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-add-content-to-adaptive-form-br-p).

### Aggiunta di nuovi campi dal file XDP al modulo adattivo   {#adding-new-fields-from-xdp-file-to-adaptive-form-nbsp}

Tutti i campi aggiunti successivamente al file XDP originale vengono visualizzati nella scheda Gerarchia modulo ed è possibile trascinarli nel modulo adattivo.

Non è necessario fare clic sul collegamento nel messaggio di errore per aggiornare i campi nella scheda Gerarchia modulo.

### Campi eliminati nel file XDP {#deleted-fields-in-xdp-file}

Se un campo precedentemente copiato in un modulo adattivo viene eliminato da un file XDP, viene visualizzato un messaggio di errore in modalità di authoring che indica che il campo non esiste nel file XDP. In questi casi, elimina manualmente il campo dal modulo adattivo o cancella il `bindRef` nella finestra di dialogo del componente.

I passaggi seguenti illustrano questo flusso di utilizzo per le risorse nell’esempio utilizzato in questo articolo:

1. Aggiorna `sample-form.xdp` file ed elimina NumericField1.
1. Carica il `sample-form.xdp` nell’interfaccia utente di AEM Forms
1. Apri `sample-xfa-af` modulo adattivo per l’authoring. Viene visualizzato il seguente messaggio di errore: Schema/modello di modulo per il modulo adattivo è stato aggiornato. `Click Here` per riavviarlo con la nuova versione.

1. Fai clic sul collegamento (con l’etichetta &quot; `Click Here`&quot;) nel messaggio. Viene visualizzato un messaggio di errore che segnala che il campo non esiste più nel file XDP.

![Errore visualizzato quando si elimina un elemento nel file XDP](assets/no-element-xdp.png)

Anche il campo eliminato viene contrassegnato con un’icona che indica un errore nel campo.

![Icona di errore nel campo](assets/error-field.png)

>[!NOTE]
>
>Campi del modulo adattivo con binding non corretto (non valido) `bindRef` nella finestra di dialogo di modifica) sono anche considerati campi eliminati. Se l’autore non corregge questi errori e pubblica il modulo adattivo, il campo viene trattato come un normale campo modulo adattivo non associato e viene incluso nella sezione non associato del file XML di output.

## Download {#downloads}

Pacchetto di contenuti per l&#39;esempio in questo articolo

[Ottieni file](assets/sample-xfa-af-sync-1.0.zip)
