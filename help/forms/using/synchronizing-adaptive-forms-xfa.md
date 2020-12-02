---
title: Sincronizzazione di Forms adattivo con i modelli di modulo XFA
seo-title: Sincronizzazione di Forms adattivo con i modelli di modulo XFA
description: Sincronizzazione di moduli adattivi con file XFA/XDP.
seo-description: Sincronizzazione di moduli adattivi con file XFA/XDP.
uuid: 92818132-1ae0-4576-84f2-ece485a34457
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: dac4539b-804d-4420-9170-68000ebb2638
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 0%

---


# Sincronizzazione di Forms adattivo con modelli di modulo XFA{#synchronizing-adaptive-forms-with-xfa-form-templates}

## Introduzione {#introduction}

È possibile creare un modulo adattivo basato su un modello di modulo XFA ( `*.XDP` file). Questo riutilizzo consente di mantenere l&#39;investimento nei moduli XFA esistenti. Per informazioni sull&#39;utilizzo di un modello di modulo XFA per la creazione di un modulo adattivo, vedere [Creare un modulo adattivo basato su un modello](../../forms/using/creating-adaptive-form.md#p-create-an-adaptive-form-based-on-an-xfa-form-template-p).

È possibile riutilizzare i campi del file XDP nel modulo adattivo. Questi campi sono denominati campi associati. Le proprietà dei campi associati (come script, etichette e formato di visualizzazione) vengono copiate dal file XDP. È inoltre possibile scegliere di ignorare il valore di alcune di queste proprietà.

 AEM Forms consente di mantenere sincronizzati i campi dei moduli adattivi con eventuali modifiche apportate successivamente ai campi corrispondenti nel file XDP. Questo articolo spiega come abilitare la sincronizzazione.

![È possibile trascinare i campi da un modulo XFA a un modulo adattivo](assets/drag-drop-xfa.gif.gif)

Nell’ambiente di authoring  AEM Forms, è possibile trascinare i campi da un modulo XFA (a sinistra) a un modulo adattivo (a destra)

## Prerequisiti {#prerequisites}

Per utilizzare le informazioni contenute in questo articolo, si consiglia di acquisire familiarità con le aree seguenti:

* [Creazione di un modulo adattivo](../../forms/using/creating-adaptive-form.md)

* XFA (XML Forms Architecture)

Per utilizzare le risorse, come illustrato nell&#39;articolo, scaricate il pacchetto di esempio come descritto nella sezione successiva, [Pacchetto di esempio](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-sample-package-p).

## Pacchetto di esempio {#sample-package}

L&#39;articolo utilizza un esempio per dimostrare come sincronizzare il modulo adattivo con un modello di modulo XFA aggiornato. Le risorse utilizzate nell&#39;esempio sono disponibili in un pacchetto, che può essere scaricato dalla sezione [Download](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-downloads-p) di questo articolo.

Dopo aver caricato il pacchetto, potete visualizzare queste risorse nell’interfaccia  di AEM Forms.

Installate il pacchetto utilizzando il gestore pacchetti: `https://<server>:<port>/crx/packmgr/index.jsp`

Il pacchetto contiene le risorse seguenti:

1. `sample-form.xdp`: Modello di modulo XFA utilizzato come esempio

1. `sample-xfa-af`: Il modulo adattivo basato sul file sample-form.xdp. Questo modulo adattivo, tuttavia, non include campi. Nel passaggio successivo, verrà aggiunto del contenuto a questo modulo adattivo.

### Aggiunta di contenuto al modulo adattivo {#add-content-to-adaptive-form-br}

1. Andate a https://&lt;server>:&lt;porta>/aem/forms.html. Se richiesto, immettete le credenziali.
1. Aprite sample-af-xfa per la modifica in modalità di creazione.
1. Dal browser Contenuto nella barra laterale, scegliete la scheda Oggetti modello dati. Trascinare NumericField1 e TextField1 nel modulo adattivo.
1. Modificare il titolo del campo NumericField1 da **Campo numerico** a **Campo numerico AF.**

>[!NOTE]
>
>Nei passaggi precedenti, veniva sovrascritta una proprietà di un campo nel file XDP. Questa proprietà, pertanto, non verrà sincronizzata se la proprietà corrispondente nel file XDP viene modificata in un secondo momento.

## Rilevamento delle modifiche nel file XDP {#detecting-changes-in-xdp-file}

Ogni volta che si verificano modifiche in un file XDP o in un frammento, l&#39;interfaccia  di AEM Forms contrassegna tutti i moduli adattivi basati sul file XDP o sul frammento.

Dopo aver aggiornato un file XDP, è necessario caricarlo nuovamente nell&#39;interfaccia  AEM Forms per contrassegnare le modifiche.

Ad esempio, è possibile aggiornare il file `sample-form.xdp` utilizzando i seguenti passaggi:

1. Passa a `https://<server>:<port>/projects.html.` Se richiesto, immetti le tue credenziali.
1. Fate clic sulla scheda Forms a sinistra.
1. Scaricate il file `sample-form.xdp` nel computer locale. Il file XDP viene scaricato come file `.zip`, che può essere estratto utilizzando qualsiasi utilità di decompressione file.

1. Aprire il file `sample-form.xdp` e modificare il titolo del campo TextField1 da **Campo di testo** a **Campo di testo**.

1. Caricate nuovamente il file `sample-form.xdp` nell&#39;interfaccia  di AEM Forms.

Se un file XDP viene aggiornato, viene visualizzata un&#39;icona nell&#39;editor quando si modificano i moduli adattivi in base al file XDP. Questa icona indica che il modulo adattivo non è sincronizzato con il file XDP. Nell’immagine seguente, vedete l’icona accanto alla barra laterale.

![Icona per visualizzare che il modulo adattivo non è sincronizzato con il file XDP](assets/sync-af-xfa.png)

## Sincronizzazione dei moduli adattivi con l&#39;ultimo file XDP {#synchronizing-adaptive-forms-with-the-latest-xdp-file}

Quando un modulo adattivo non sincronizzato con il file XDP viene aperto per la creazione successiva, viene visualizzato il seguente messaggio: **Schema/modello di modulo per il modulo adattivo è stato aggiornato. `Click Here` per riavviarlo con la nuova versione.**

Facendo clic sul messaggio, i campi del modulo adattivo vengono sincronizzati con i campi corrispondenti nel file XDP.

Per l&#39;esempio utilizzato in questo articolo, aprite `sample-xfa-af` in modalità di creazione. Il messaggio viene visualizzato nella parte inferiore del modulo adattivo.

![Messaggio che richiede di sincronizzare il modulo adattivo con il file XDP](assets/sync-af-xfa-1.png)

### Aggiornamento delle proprietà {#updating-the-properties}

Tutte le proprietà copiate dal file XDP al modulo adattivo vengono aggiornate, fatta eccezione per le proprietà esplicitamente sostituite nel modulo adattivo (dalla finestra di dialogo dei componenti) dall&#39;autore. L&#39;elenco delle proprietà che sono state aggiornate è disponibile nei registri del server.

Per aggiornare le proprietà nel modulo adattivo di esempio, fare clic sul collegamento (con etichetta `"Click Here"`) nel messaggio. Il titolo di TextField1 cambia da **Campo di testo** a **Campo di testo personale**.

![update-property](assets/update-property.png)

>[!NOTE]
>
>L&#39;etichetta AF Numeric Field non è stata modificata perché questa proprietà è stata ignorata dalla finestra di dialogo delle proprietà del componente, come descritto in [Aggiungi contenuto a moduli adattivi](../../forms/using/synchronizing-adaptive-forms-xfa.md#p-add-content-to-adaptive-form-br-p).

### Aggiunta di nuovi campi dal file XDP al modulo adattivo   {#adding-new-fields-from-xdp-file-to-adaptive-form-nbsp}

Tutti i campi aggiunti successivamente al file XDP originale vengono visualizzati nella scheda Gerarchia modulo ed è possibile trascinare i nuovi campi nel modulo adattivo.

Non è necessario fare clic sul collegamento nel messaggio di errore per aggiornare i campi nella scheda Gerarchia modulo.

### Campi eliminati nel file XDP {#deleted-fields-in-xdp-file}

Se un campo precedentemente copiato in un modulo adattivo viene eliminato da un file XDP, in modalità di creazione viene visualizzato un messaggio di errore che informa che il campo non esiste nel file XDP. In questi casi, eliminare manualmente il campo dal modulo adattivo o deselezionare la proprietà `bindRef` nella finestra di dialogo del componente.

I passaggi seguenti illustrano questo flusso di utilizzo per le risorse nell’esempio utilizzato in questo articolo:

1. Aggiornare il file `sample-form.xdp` ed eliminare NumericField1.
1. Caricare il file `sample-form.xdp` nell&#39;interfaccia  di AEM Forms
1. Aprire il modulo `sample-xfa-af` adattivo per la creazione. Viene visualizzato il seguente messaggio di errore: Schema/modello di modulo per il modulo adattivo è stato aggiornato. `Click Here` per riavviarlo con la nuova versione.

1. Fare clic sul collegamento (con l&#39;etichetta &quot; `Click Here`&quot;) nel messaggio. Viene visualizzato un messaggio di errore che segnala che il campo non esiste più nel file XDP.

![Errore visualizzato durante l&#39;eliminazione di un elemento nel file XDP](assets/no-element-xdp.png)

Anche il campo eliminato è contrassegnato da un’icona che indica un errore nel campo.

![Icona errore nel campo](assets/error-field.png)

>[!NOTE]
>
>Anche i campi del modulo adattivo con un binding non corretto (un valore `bindRef` non valido nella finestra di dialogo di modifica) sono considerati campi eliminati. Se l&#39;autore non corregge questi errori e pubblica il modulo adattivo, il campo viene trattato come un normale campo modulo adattivo non associato e viene incluso nella sezione non associata del file XML di output.

## Download {#downloads}

Pacchetto di contenuti per l&#39;esempio in questo articolo

[Ottieni file](assets/sample-xfa-af-sync-1.0.zip)
