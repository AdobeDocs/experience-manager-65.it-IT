---
title: Tipi di certificato utilizzati dalle estensioni Acrobat Reader DC
seo-title: Tipi di certificato utilizzati dalle estensioni Acrobat Reader DC
description: Informazioni sui tipi di certificato utilizzati dalle estensioni Acrobat Reader DC.
seo-description: Informazioni sui tipi di certificato utilizzati dalle estensioni Acrobat Reader DC.
uuid: 93c02abc-2d5a-44ed-b93c-981afbd0553d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 331b9317-87b5-4a96-a1bc-429675ff90c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 3%

---


# Tipi di certificato utilizzati dalle estensioni Acrobat Reader DC {#certificate-types-used-by-acrobat-reader-dc-extensions}

Il Visualizzatore certificati fornisce le seguenti informazioni sul certificato:

* Nome &quot;descrittivo&quot; del certificato
* Profili certificato
* Periodo di validità
* Diritti di utilizzo delle estensioni Acrobat Reader DC

## Nome &quot;descrittivo&quot; certificato {#certificate-friendly-name}

Il nome &quot;descrittivo&quot; di un certificato di estensione Acrobat Reader DC è una stringa che descrive le proprietà del certificato, come nell&#39;esempio seguente:

SONO 2D Barcode Full Production V6.1 P8 0002054

La stringa contiene gli elementi seguenti:

**Tipo di certificato:** Descrive i moduli AEM attivati dal certificato e il livello di attivazione, ad esempio ARE 2D Barcode Full. Per un elenco dei tipi di certificato disponibili, consultate la colonna Tipo nella tabella nella sezione Profili certificato.

**Tipo di distribuzione:** indica l&#39;uso previsto del certificato, ad esempio Produzione. Il valore può essere Valutazione o Produzione. Per un elenco dei tipi di distribuzione associati a ciascun tipo di certificato, vedete la colonna Tipo di distribuzione nella tabella nella sezione Profili certificato.

**Versione dei diritti di utilizzo:** Descrive la versione dell&#39;algoritmo dei diritti di utilizzo per il quale può essere utilizzato il certificato, ad esempio V6.1. Questa versione non indica la versione di  estensioni Acrobat o Acrobat Reader DC.

**Codice profilo:** il codice del profilo è una breve descrizione delle proprietà complete del certificato, ad esempio P8. Per un elenco dei codici di profilo associati a ciascun tipo di file, vedi la colonna Codice di profilo nella tabella nella sezione Profili di certificato.

**Numero di serie:** A ogni certificato rilasciato dal Adobe viene assegnato un numero di serie, ad esempio 0002054.  Adobe Enterprise Support o un rappresentante commerciale  Adobe Enterprise può utilizzare questo numero di serie per tracciare il certificato in un ordine di prodotto specifico o in una relazione OEM.

## Profili certificato {#certificate-profiles}

Nella tabella seguente sono elencati i profili di certificato che si possono incontrare durante l&#39;analisi dei certificati delle estensioni Acrobat Reader DC.

<table>
 <thead>
  <tr>
   <th><p>Codice profilo</p></th>
   <th><p>Tipo</p></th>
   <th><p>Periodo di validità</p></th>
   <th><p>Tipo di distribuzione</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>P1</p></td>
   <td><p>Produzione SAP</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione</p></td>
  </tr>
  <tr>
   <td><p>P2</p></td>
   <td><p>SAP Internal Test</p></td>
   <td><p>2 anni</p></td>
   <td><p>Valutazione e test</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Estensioni Acrobat Reader DC, Produzione</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Estensioni Acrobat Reader DC, Utilizzo interno  Adobe</p></td>
   <td><p>2 anni</p></td>
   <td><p>Produzione</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Estensioni Acrobat Reader DC, Integrazione dei partner</p></td>
   <td><p>2 anni</p></td>
   <td><p>Valutazione e test</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Estensioni Acrobat Reader DC, Valutazione</p></td>
   <td><p>60 giorni</p></td>
   <td><p>Valutazione</p></td>
  </tr>
  <tr>
   <td><p>P8</p></td>
   <td><p>Forms, Produzione</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione</p></td>
  </tr>
  <tr>
   <td><p>P9</p></td>
   <td><p> Adobe Acrobat 7.x, produzione</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>Forms; possono essere utilizzati dagli OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione e valutazione</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>Forms; possono essere utilizzati dagli OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione e valutazione</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>Solo firma; possono essere utilizzati dagli OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione e valutazione</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>Solo commenti offline; possono essere utilizzati dagli OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione e valutazione</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>Solo commenti; possono essere utilizzati dagli OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione e valutazione</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>autorizzazioni complete; possono essere utilizzati dagli OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione e valutazione</p></td>
  </tr>
 </tbody>
</table>

## Periodo di validità {#validity-period}

I certificati di valutazione vengono rilasciati a clienti e sviluppatori in modo che possano valutare e sviluppare applicazioni campione per i prodotti. Il periodo di validità di questi certificati è compreso tra 60 e 90 giorni. Essi scadono alla fine del secondo mese successivo ai dati di rilascio.

I certificati di integrazione dei partner vengono rilasciati a  partner aziendali del Adobe per supportare lo sviluppo, l&#39;integrazione, la prototipazione e la dimostrazione del software. Tali certificati sono validi per due anni dalla data del rilascio.

 Adobe I certificati di utilizzo interno vengono utilizzati all&#39;interno  Adobe per supportare lo sviluppo, l&#39;integrazione, la prototipazione e la dimostrazione del software. Tali certificati sono validi per due anni dalla data del rilascio.

I certificati di produzione vengono rilasciati ai clienti che hanno acquistato le estensioni Acrobat Reader DC. Questi certificati sono validi per il periodo massimo consentito dall&#39;autorità di certificazione (CA), indicato come *Max* nella tabella Profili certificati.

## Diritti di utilizzo delle estensioni Acrobat Reader DC {#acrobat-reader-dc-extensions-usage-rights}

Quando esaminate il certificato di estensione Acrobat Reader DC nel Visualizzatore certificati, potete selezionare l&#39;elemento dei diritti di utilizzo dalla scheda Dettagli (se configurata) per visualizzare un elenco dettagliato dei diritti di utilizzo Adobe Reader  che il certificato può abilitare. I diritti di utilizzo attivati in un particolare documento possono essere un sottoinsieme di quelli abilitati dal certificato.

Se i commenti online sono richiesti in un ambiente non collaborativo, contattate  Adobe Support per ulteriori informazioni. La proprietà Mode corrisponde al tipo di distribuzione ed è *production* o *Evaluation*.

I diritti di utilizzo delle estensioni Acrobat Reader DC consentiti sono costituiti da uno o più elementi specifici. Questi elementi sono utilizzati in diverse combinazioni per ottenere varietà di funzionalità di prodotto concesso in licenza.

<table>
 <thead>
  <tr>
   <th><p>Elemento diritti di utilizzo</p></th>
   <th><p>Funzionalità abilitata in  Adobe Reader quando si visualizza un documento PDF con diritti</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormFillInAndSave</p></td>
   <td><p>Compilare i campi del modulo e salvare i file localmente.</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>Importare ed esportare i dati dei moduli come file FDF, XFDF, XML e XDP.</p></td>
  </tr>
  <tr>
   <td><p>FormAddDelete</p></td>
   <td><p>Aggiungere, modificare o eliminare campi e proprietà campo nel modulo PDF.</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>Inviare dati, per e-mail o offline, a un server quando non è in esecuzione in una sessione del browser.</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>Creare pagine da pagine modello all'interno dello stesso modulo PDF.</p></td>
  </tr>
  <tr>
   <td><p>Firma</p></td>
   <td><p>Firmare e salvare digitalmente i documenti PDF e cancellare le firme digitali.</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>Creare e modificare annotazioni del documento, ad esempio commenti.</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>Salvataggio di annotazioni, ad esempio commenti, in un file di dati separato e caricamento di commenti da un file.</p></td>
  </tr>
  <tr>
   <td><p>Codice a barreTesto</p></td>
   <td><p>Stampare un documento con dati del modulo con codice a barre in un modulo non crittografato per il quale non è richiesta la decodifica da parte del software del server concesso in licenza.</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>Caricate e scaricate annotazioni come commenti da e verso un server di revisione e commenti online.</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>Connettersi a servizi Web o database definiti all'interno di un modulo PDF.</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>Modificare gli oggetti file incorporati associati al documento PDF.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>I diritti di utilizzo delle estensioni Acrobat Reader DC possono essere concessi in licenza  Adobe solo in determinate combinazioni compatibili. Non è possibile concedere la licenza a tali funzionalità in modo indipendente. Per informazioni sulle combinazioni disponibili di diritti di utilizzo, contattate un rappresentante commerciale AEM moduli.

