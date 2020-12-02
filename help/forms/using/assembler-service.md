---
title: Utilizzo di Assembler Service
seo-title: Utilizzo di Assembler Service
description: Il servizio Assembler consente di combinare, ridisporre e integrare documenti PDF e XDP e di ottenere informazioni sui documenti PDF.
seo-description: Il servizio Assembler consente di combinare, ridisporre e integrare documenti PDF e XDP e di ottenere informazioni sui documenti PDF.
uuid: 1efce50b-2d98-408e-aa43-ac4999de41a8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 6a99042f-79c7-494b-bca0-73f2b5725b58
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c
workflow-type: tm+mt
source-wordcount: '2143'
ht-degree: 0%

---


# Utilizzo di Assembler Service{#using-assembler-service}

Il servizio Assembler consente di combinare, ridisporre e integrare documenti PDF e XDP e di ottenere informazioni sui documenti PDF. Ogni processo inviato al servizio Assembler include un documento DDX (Document Description XML), documenti di origine e risorse esterne (stringhe e grafica). Per ulteriori informazioni sul servizio assembler, vedere [Panoramica del servizio Assembler](../../forms/using/overview-aem-document-services.md#p-assembler-service-p).

È possibile utilizzare il servizio di assemblaggio per le seguenti operazioni:

## Assemblare documenti PDF {#assemble-pdf-documents}

È possibile utilizzare il servizio Assembler per assemblare due o più documenti PDF in un singolo documento PDF o in un singolo Portfolio PDF. È inoltre possibile applicare al documento PDF funzioni che facilitano la navigazione o migliorano la protezione. Di seguito sono riportati alcuni modi per assemblare documenti PDF:

### Assemblare un semplice documento PDF {#assemble-a-simple-pdf-document}

L&#39;illustrazione seguente mostra tre documenti sorgente che vengono uniti in un singolo documento risultante.

![Assemblare un documento PDF semplice da più documenti PDF](assets/as_document_assembly.png)

Assemblare un documento PDF semplice da più documenti PDF

L&#39;esempio seguente è un semplice documento DDX utilizzato per assemblare il documento. Specifica i nomi dei documenti di origine utilizzati per produrre il documento risultante, nonché il nome del documento risultante:

```xml
<PDF result="Doc4">
<PDF source="Doc1"/>
<PDF source="Doc2"/>
<PDF source="Doc3"/>
</PDF>
```

L&#39;assieme Document produce un documento risultante contenente il contenuto seguente e\
caratteristiche:

* Tutto o parte di ciascun documento di origine
* Tutti o parte dei segnalibri di ciascun documento di origine, normalizzati per il documento risultante assemblato
* Altre caratteristiche adottate dal documento di base (Doc1), compresi metadati, etichette di pagina e dimensioni di pagina
* Facoltativamente, il documento risultante include un sommario costruito dai segnalibri nei documenti di origine

### Creare un Portfolio PDF {#create-a-pdf-portfolio}

Il servizio Assembler può creare Portfoli PDF contenenti una raccolta di documenti e un&#39;interfaccia utente indipendente. L’interfaccia è denominata Layout Portfolio PDF o Navigatore Portfolio PDF. Gli Portfoli PDF ampliano la capacità dei pacchetti PDF aggiungendo un navigatore, cartelle e pagine di benvenuto. L&#39;interfaccia può migliorare l&#39;esperienza dell&#39;utente sfruttando la stringa di testo localizzata, gli schemi di colore personalizzati e le risorse grafiche. L’Portfolio PDF può anche includere cartelle per l’organizzazione dei file nel portfolio.

Quando il servizio Assembler interpreta il seguente documento DDX, assembla un Portfolio PDF che include un Portfolio PDF navigator e un pacchetto di due file. Il servizio ottiene il navigatore dalla posizione specificata dall&#39;origine myNavigator. Cambia la combinazione di colori predefinita del navigatore nella combinazione di colori rosaScheme.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="Untitled 1">
<Portfolio>
<Navigator source="myNavigator"/>
<ColorScheme scheme="pinkScheme"/>
</Portfolio>
<PackageFiles>
<PDF source="sourcePDF1"/>
<PDF source="sourcePDF2"/>
</PackageFiles>
</PDF>
</DDX>
```

### Assemblare documenti crittografati {#assemble-encrypted-documents}

Quando si assembla un documento, è anche possibile cifrare il documento PDF con una password. Dopo aver crittografato un documento PDF con una password, l&#39;utente deve specificare la password per visualizzare il documento PDF in  Adobe Reader o  Acrobat. Per cifrare un documento PDF con una password, il documento DDX deve contenere i valori degli elementi di cifratura necessari per la cifratura di un documento PDF.

Il servizio di cifratura non deve necessariamente far parte dell&#39;installazione del LiveCycle per cifrare un documento PDF con una password.

Se uno o più documenti di input sono crittografati, immettere una password per aprire il documento come parte del DDX.

### Assemblare i documenti utilizzando la numerazione Bates {#assemble-documents-using-bates-numbering}

Quando assemblate un documento, potete utilizzare la numerazione Bates per applicare un identificatore di pagina univoco a ciascuna pagina. Quando si utilizza la numerazione Bates, a ogni pagina del documento (o set di documenti) viene assegnato un numero che identifica in modo univoco la pagina. Ad esempio, i documenti di fabbricazione che contengono informazioni sulla distinta base e sono associati alla produzione di un assieme possono contenere un identificatore. Un numero Bates contiene un valore numerico incrementato sequenzialmente e un prefisso e un suffisso facoltativi. Il prefisso + il valore numerico + il suffisso è denominato pattern a intervalli.

L&#39;illustrazione seguente mostra un documento PDF contenente un identificatore univoco nell&#39;intestazione del documento.

![Un documento PDF contenente un identificatore univoco nell&#39;intestazione del documento](do-not-localize/as_batesnumber.png)

Un documento PDF contenente un identificatore univoco nell&#39;intestazione del documento

### Appiattisci e assembla documenti {#flatten-and-assemble-documents}

È possibile utilizzare il servizio Assembler per trasformare un documento PDF interattivo (ad esempio, un modulo) in un documento PDF non interattivo. Un documento PDF interattivo consente agli utenti di immettere o modificare i dati presenti nei campi del documento PDF. Il processo di trasformazione di un documento PDF interattivo in un documento PDF non interattivo è denominato &quot;appiattimento&quot;. Quando un documento PDF viene appiattito, i campi del modulo mantengono l’aspetto grafico ma non sono più interattivi. Uno dei motivi per appiattire un documento PDF è garantire che i dati non possano essere modificati. Inoltre, gli script associati ai campi non funzionano più.

Quando si crea un documento PDF che viene assemblato da documenti PDF interattivi, il servizio Assembler li appiattisce prima di assemblarli nel documento risultante.

>[!NOTE]
>
>Il servizio Assembler utilizza il servizio Output per appiattire i moduli XFA dinamici. Se il servizio Assembler elabora un DDX che lo richiede per appiattire un modulo dinamico XFA e il servizio Output non è disponibile, viene generata un&#39;eccezione. Il servizio Assembler può appiattire un modulo Acrobat  o un modulo XFA statico senza utilizzare il servizio Output.

## Assemblare documenti XDP {#assemble-xdp-documents}

È possibile utilizzare il servizio Assembler per assemblare più documenti XDP in un singolo documento XDP o in un documento PDF. Per i file XDP di origine che includono punti di inserimento, è possibile specificare i frammenti da inserire.

Di seguito sono riportati alcuni modi per assemblare i documenti XDP:

### Assemblare un semplice documento XDP {#assemble-a-simple-xdp-document}

L&#39;illustrazione seguente mostra tre documenti XDP sorgente che vengono assemblati in un singolo documento XDP risultante. Il documento XDP risultante contiene i tre documenti XDP di origine, inclusi i relativi dati associati. Il documento risultante ottiene gli attributi di base dal documento di base, che è il primo documento XDP di origine.

![Assemblare un semplice documento XDP da più documenti XDP](assets/as_assembler_xdpassembly.png)

Assemblare un semplice documento XDP da più documenti XDP

Di seguito è riportato un documento DDX che produce il risultato illustrato sopra.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="MyXDPResult">
<XDP source="sourceXDP1"/>
<XDP source="sourceXDP2"/>
<XDP source="sourceXDP3"/>
</XDP>
</DDX>
```

### Risoluzione dei riferimenti durante l&#39;assembly {#resolving-references-during-assembly}

In genere, i documenti XDP possono contenere immagini cui viene fatto riferimento tramite riferimenti assoluti o relativi. Il servizio Assembler, per impostazione predefinita, mantiene i riferimenti alle immagini nel documento XDP risultante.

È possibile specificare come il servizio Assembler gestisce le immagini a cui si fa riferimento nei documenti XDP di origine tramite riferimenti assoluti o relativi nei file XDP durante l&#39;assemblaggio. Potete scegliere di incorporare tutte le immagini nel risultato in modo che non contenga riferimenti relativi o assoluti. Per definirlo è necessario impostare il valore del tag resolveAssets, che può assumere una delle seguenti opzioni. Per impostazione predefinita, nel documento dei risultati non vengono risolti riferimenti.

<table>
 <tbody> 
  <tr> 
   <th>Valore</th> 
   <th>Descrizione</th> 
  </tr> 
  <tr> 
   <td>nessuno</td> 
   <td>Non risolve alcun riferimento.</td> 
  </tr> 
  <tr> 
   <td>all</td> 
   <td>Incorpora tutte le immagini di riferimento nel documento XDP di origine.</td> 
  </tr> 
  <tr> 
   <td>relativo</td> 
   <td>Incorpora tutte le immagini a cui viene fatto riferimento tramite riferimenti relativi nel documento XDP<br /> di origine.</td> 
  </tr> 
  <tr> 
   <td>assoluto</td> 
   <td>Incorpora tutte le immagini a cui viene fatto riferimento tramite riferimenti assoluti nel documento XDP<br /> di origine.</td> 
  </tr> 
 </tbody> 
</table>

È possibile specificare il valore dell&#39;attributo resolveAssets nel tag di origine XDP o nel tag di risultato XDP padre. Se l&#39;attributo è specificato per il tag dei risultati XDP, verrà ereditato da tutti gli elementi di origine XDP secondari del risultato XDP. Tuttavia, specificando in modo esplicito l&#39;attributo per un elemento di origine, l&#39;impostazione dell&#39;elemento result viene ignorata solo per il documento di origine.

#### Risolvere tutti i riferimenti di origine in un documento XDP {#resolve-all-source-references-in-an-xdp-document}

Per risolvere tutti i riferimenti nei documenti XDP di origine, specificate l&#39;attributo resolveAssets per\
documento risultante per tutti, come nell&#39;esempio seguente:

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
<XDP source="input3.xdp" />
</XDP>
</DDX
```

È inoltre possibile specificare l&#39;attributo per tutti i documenti XDP di origine in modo indipendente per ottenere lo stesso\
risultato.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp">
<XDP source="input1.xdp" resolveAssets="all"/>
<XDP source="input2.xdp" resolveAssets="all"/>
<XDP source="input3.xdp" resolveAssets="all"/>
</XDP>
</DDX>
```

#### Risolvere i riferimenti di origine selezionati in un documento XDP {#resolve-selected-source-references-in-an-xdp-document}

Potete specificare in modo selettivo i riferimenti di origine che desiderate risolvere specificando l&#39;attributo resolveAssets per tali riferimenti. Gli attributi per i singoli documenti sorgente sostituiscono l’impostazione del documento XDP risultante. In questo esempio vengono risolti anche i frammenti inclusi.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" >
<XDPContent source="fragment.xdp" insertionPoint="MyInsertionPoint"
fragment="myFragment"/>
</XDP>
<XDP source="input2.xdp" />
</XDP>
</DDX>
```

#### Risolvere in modo selettivo i riferimenti assoluti o relativi {#selectively-resolve-absolute-or-relative-references}

Potete risolvere in modo selettivo i riferimenti assoluti o relativi in tutti o in parte i documenti sorgente, come illustrato nell’esempio di seguito:

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="absolute">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
</XDP>
</DDX
```

### Inserimento dinamico di frammenti di modulo in un modulo XFA {#dynamically-insert-form-fragments-into-an-xfa-form}

È possibile utilizzare il servizio Assembler per creare un modulo XFA creato da un altro modulo XFA in cui vengono inseriti i frammenti. Questa funzione consente di creare più moduli utilizzando i frammenti.

Il supporto per l&#39;inserimento dinamico dei frammenti di modulo supporta il controllo a origine singola. È possibile mantenere un&#39;unica origine di componenti comunemente utilizzati. Ad esempio, è possibile creare un frammento per il banner aziendale. Se il banner cambia, è sufficiente modificare il frammento. Gli altri moduli che includono il frammento rimangono invariati.

I progettisti di moduli utilizzano Designer di LiveCycle per creare frammenti di modulo. Tali frammenti hanno un nome univoco all&#39;interno di un modulo XFA. I progettisti di moduli utilizzano inoltre Designer per creare moduli XFA con punti di inserimento denominati in modo univoco. Il programmatore scrive documenti DDX che specificano la modalità di inserimento dei frammenti nel modulo XFA.

Nell&#39;illustrazione seguente sono visualizzati due moduli XML (modelli XFA). Il modulo a sinistra contiene un punto di inserimento denominato myInsertionPoint. Il modulo a destra contiene un frammento denominato myFragment.

![Inserimento di frammenti di modulo in un modulo XFA](assets/as_assembler_fragment_assy_assembled.png)

Inserimento di frammenti di modulo in un modulo XFA

Quando il servizio Assembler interpreta il seguente documento DDX, crea un modulo XML che contiene un altro modulo XML. Il sottomodulo myFragment del documento myFragmentSource viene inserito in myInsertionPoint nel documento myFormSource.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="myFormResult">
<XDP source="myFormSource">
<XDPContent fragment="myFragment" insertionPoint="myInsertionPoint"
source="myFragmentSource"/>
</XDP>
</XDP>
</DDX
```

### Creare un pacchetto di documenti XDP come PDF {#package-an-xdp-document-as-pdf}

È possibile utilizzare il servizio Assembler per creare un pacchetto di un documento XDP come documento PDF, come illustrato in questo documento DDX.

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="Untitled 1" encryption="passEncProfile1">
<XDP>
<XDP source="sourceXDP3"/>
<XDP source="sourceXDP4"/>
</XDP>
</PDF>
</DDX>
```

## Smontare documenti PDF {#disassemble-pdf-documents}

È possibile utilizzare il servizio Assembler per smontare un documento PDF. Il servizio può estrarre pagine dal documento di origine o dividere un documento di origine basato su segnalibri. In genere, questa attività è utile se il documento PDF è stato creato originariamente da molti documenti, ad esempio una raccolta di istruzioni.

### Estrarre pagine da un documento di origine {#extract-pages-from-a-source-document}

Nell&#39;illustrazione seguente, le pagine 1-3 vengono estratte dal documento di origine e inserite in un nuovo documento risultante.

![Estrazione di pagine specifiche da un documento di origine](assets/as_intro_page_extraction.png)

Estrazione di pagine specifiche da un documento di origine

L&#39;esempio seguente è un documento DDX utilizzato per smontare il documento.

```xml
<PDF result="Doc4">
<PDF source="Doc2" pages="1-3"/>
</PDF>
```

### Dividere un documento di origine in base ai segnalibri {#divide-a-source-document-based-on-bookmarks}

Nell&#39;illustrazione seguente, DocA è diviso in più documenti risultanti. Il segnalibro di primo livello 1 in una pagina identifica l&#39;inizio di un nuovo documento risultante.

![Divisione di un documento sorgente basato su segnalibri in più documenti](assets/as_intro_pdfsfrombookmarks.png)

Divisione di un documento sorgente basato su segnalibri in più documenti

L&#39;esempio seguente è un documento DDX che utilizza segnalibri per smontare un documento di origine.

```xml
<PDFsFromBookmarks prefix="A">
<PDF source="DocA"/>
</PDFsFromBookmarks>
```

## Determinare se i documenti sono conformi allo standard PDF/A {#determine-whether-documents-are-pdf-a-compliant}

È possibile utilizzare il servizio Assembler per determinare se un documento PDF è conforme allo standard PDF/A. PDF/A è un formato di archiviazione che consente di preservare a lungo termine il contenuto del documento. I font vengono incorporati nel documento e il file non viene compresso. Di conseguenza, un documento PDF/A è generalmente più grande di un documento PDF standard. Inoltre, un documento PDF/A non contiene contenuto audio e video.

## Ottenere informazioni su un documento PDF {#obtain-information-about-a-pdf-document}

È possibile utilizzare il servizio Assembler per ottenere le seguenti informazioni su un documento PDF:

* Informazioni sul testo.

   * Parole in ogni pagina del documento
   * Posizione di ogni parola su ogni pagina del documento
   * Frasi in ciascun paragrafo di ciascuna pagina del documento

* Segnalibri, inclusi il numero di pagina, il titolo, la destinazione e l’aspetto. Puoi esportare questo\
   i dati di un documento PDF e importarli in un documento PDF.

* Allegati di file, comprese le informazioni sui file. Per gli allegati a livello di pagina, include anche\
   posizione dell&#39;annotazione dell&#39;allegato del file. È possibile esportare questi dati da un documento PDF e\
   importarlo in un documento PDF.

* Creare pacchetti di file, incluse informazioni sui file, cartelle, pacchetti, schemi e dati dei campi. È possibile esportare questi dati da un documento PDF e importarli in un documento PDF.

## Convalida documenti DDX {#validate-ddx-documents}

È possibile utilizzare il servizio Assembler per determinare se un documento DDX è valido. Ad esempio, se si effettua l&#39;aggiornamento da una versione di LiveCycle precedente, la convalida verifica la validità del documento DDX.

## Chiama altri servizi {#call-other-services}

È possibile utilizzare documenti DDX che fanno sì che il servizio Assembler chiami i seguenti servizi LiveC ycle. Il servizio Assembler può chiamare solo i servizi installati con il LiveCycle.

**Servizio** Estensioni Reader: Consente  utenti Adobe Reader di firmare digitalmente il documento PDF risultante.

**Servizio** Forms: Unisce un file XDP e un file di dati XML per produrre un documento PDF contenente il modulo interattivo compilato.

**Servizio** di output: Converte un modulo XML dinamico in un documento PDF contenente un modulo non interattivo (appiattisce il modulo). Il servizio Assembler appiattisce i moduli XML statici e  moduli Acrobat senza chiamare il servizio Output.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="outDoc">
<PDF source="doc1"/>
<PDF source="doc2"/>
<ReaderRights
credentialAlias="LCESCred"
digitalSignatures="true"/>
</PDF>
</DDX>
```

L&#39;utilizzo di DDX e del servizio Assembler per chiamare altri servizi LiveC ciclabili può semplificare il diagramma del processo. È anche possibile ridurre il lavoro di personalizzazione dei flussi di lavoro. (Consulta anche
