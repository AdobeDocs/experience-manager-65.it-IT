---
title: Tipi di certificati utilizzati dalle estensioni di Adobe Reader DC
description: Scopri i tipi di certificati utilizzati dalle estensioni di Adobe Reader DC
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 800bffd5-0cdc-4251-bba4-e350f226f019
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '944'
ht-degree: 100%

---

# Tipi di certificati utilizzati dalle estensioni di Adobe Reader DC {#certificate-types-used-by-acrobat-reader-dc-extensions}

Il Visualizzatore di certificati fornisce le seguenti informazioni sul certificato:

* Nome “descrittivo” del certificato
* Profili certificato
* Periodo di validità
* Diritti di utilizzo delle estensioni di Adobe Reader DC

## Nome “descrittivo” del certificato {#certificate-friendly-name}

Il nome “descrittivo” di un certificato delle estensioni di Adobe Reader DC è una stringa che descrive le proprietà del certificato, come nell’esempio seguente:

Produzione codice a barre completo ARE 2D V6.1 P8 0002054

La stringa contiene i seguenti elementi:

**Tipo di certificato:** descrive i moduli di AEM Form attivati dal certificato e il livello di attivazione, ad esempio il codice a barre ARE 2D completo. Per un elenco dei tipi di certificati disponibili, consulta la colonna Tipo nella tabella della sezione Profili certificato.

**Tipo di distribuzione:** indica l’uso previsto del certificato, ad esempio Produzione. Il valore può essere Valutazione o Produzione. Per un elenco dei tipi di distribuzione associati a ciascun tipo di certificato, consulta la colonna Tipo di distribuzione nella tabella della sezione Profili di certificato.

**Versione diritti di utilizzo:** descrive la versione dell’algoritmo dei diritti di utilizzo per cui è possibile utilizzare il certificato, ad esempio V6.1. Questa versione non indica la versione di Acrobat o le estensioni di Adobe Reader DC.

**Codice profilo:** il codice profilo è una descrizione abbreviata delle proprietà complete del certificato, ad esempio P8. Per un elenco dei codici di profilo associati a ciascun tipo di file, consultare la colonna Codice profilo nella tabella della sezione Profili certificato.

**Numero di serie:** a ogni certificato rilasciato da Adobe, ad esempio 0002054, viene assegnato un numero di serie. Supporto Enterprise di Adobe o un rappresentante dell’account Enterprise di Adobe può utilizzare questo numero di serie per tracciare il certificato in base a un ordine di prodotto specifico o a una relazione OEM.

## Profili certificato {#certificate-profiles}

Nella tabella seguente sono elencati i profili di certificato che è possibile incontrare durante l’analisi dei certificati delle estensioni di Adobe Reader DC.

<table>
 <thead>
  <tr>
   <th><p>Codice profilo</p></th>
   <th><p>Tipo</p></th>
   <th><p>Periodo di validità</p></th>
   <th><p>Tipo di implementazione</p></th>
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
   <td><p>Test interno SAP</p></td>
   <td><p>2 anni</p></td>
   <td><p>Valutazione e prova</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Estensioni Adobe Reader DC, produzione</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Estensioni di Adobe Reader DC, uso interno di Adobe</p></td>
   <td><p>2 anni</p></td>
   <td><p>Produzione</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Estensioni Acrobat Reader DC, integrazione partner</p></td>
   <td><p>2 anni</p></td>
   <td><p>Valutazione e prova</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Estensioni Adobe Reader DC, valutazione</p></td>
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
   <td><p>Adobe Acrobat 7.x, Produzione</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>Forms; può essere utilizzato dagli OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione e valutazione</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>Forms; può essere utilizzato dagli OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione e valutazione</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>Solo firma; può essere utilizzato dagli OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione e valutazione</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>Solo commenti offline; può essere utilizzato dagli OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione e valutazione</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>Solo commenti; può essere utilizzato dagli OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione e valutazione</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>Autorizzazioni complete; possono essere utilizzate dagli OEM</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione e valutazione</p></td>
  </tr>
 </tbody>
</table>

## Periodo di validità {#validity-period}

I certificati di valutazione vengono rilasciati a clientela e sviluppatori in modo che possano valutare e sviluppare applicazioni di esempio per i prodotti. Il periodo di validità di questi certificati è compreso tra 60 e 90 giorni. Scadono alla fine del secondo mese successivo a quello del rilascio.

I certificati di integrazione dei partner vengono rilasciati ai partner aziendali Adobe per supportare lo sviluppo, l’integrazione, la prototipazione e la dimostrazione di software. I certificati hanno una validità di due anni a decorrere dalla data di rilascio.

I certificati Adobe per uso interno vengono utilizzati in Adobe per supportare lo sviluppo, l’integrazione, la prototipazione e la dimostrazione di software. I certificati hanno una validità di due anni a decorrere dalla data di rilascio.

I certificati di produzione vengono rilasciati alla clientela che ha acquistato estensioni di Adobe Reader DC. Questi certificati sono validi per il periodo massimo consentito dall’Autorità di certificazione (CA), indicato come *Max* nella tabella Profili certificato.

## Diritti di utilizzo delle estensioni di Adobe Reader DC {#acrobat-reader-dc-extensions-usage-rights}

Durante l’esame del certificato delle estensioni di Adobe Reader DC nel Visualizzatore certificati, è possibile selezionare l’elemento dei diritti di utilizzo dalla scheda Dettagli (se configurata) per visualizzare un elenco dettagliato dei diritti di utilizzo di Adobe Reader abilitati dal certificato. I diritti di utilizzo abilitati per un particolare documento possono essere un sottoinsieme di quelli abilitati dal certificato.

Se è necessario inserire commenti online in un ambiente non collaborativo, contatta l’Assistenza Adobe per ulteriori informazioni. La proprietà Modalità corrisponde al tipo di distribuzione ed è *produzione* o *valutazione*.

I diritti di utilizzo delle estensioni di Adobe Reader DC consentiti sono costituiti da uno o più elementi specifici. Questi elementi vengono utilizzati in diverse combinazioni per ottenere varietà di funzionalità del prodotto con licenza.

<table>
 <thead>
  <tr>
   <th><p>Elemento diritti di utilizzo</p></th>
   <th><p>Funzionalità abilitata in Adobe Reader quando viene visualizzato un documento PDF con diritti abilitati</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormFillInAndSave</p></td>
   <td><p>Compila i campi del modulo e salva i file in locale.</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>Importa ed esporta i dati dei moduli come file FDF, XFDF, XML e XDP.</p></td>
  </tr>
  <tr>
   <td><p>FormAddDelete</p></td>
   <td><p>Aggiunge, modifica o elimina campi e proprietà dei campi nel modulo di PDF.</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>Invia dati, tramite e-mail od offline, a un server quando non è in esecuzione in una sessione del browser.</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>Crea pagine da pagine modello all’interno dello stesso modulo di PDF.</p></td>
  </tr>
  <tr>
   <td><p>Firma</p></td>
   <td><p>Firma e salvataggio digitale di documenti PDF e cancellazione delle firme digitali.</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>Crea e modifica annotazioni del documento, ad esempio commenti.</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>Salva le annotazioni, ad esempio i commenti, in un file di dati separato e carica i commenti da un file.</p></td>
  </tr>
  <tr>
   <td><p>BarcodePlaintext</p></td>
   <td><p>Stampa un documento con i dati del modulo con codice a barre in un modulo non crittografato che non richiede la decodifica del software del server concesso in licenza.</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>Carica e scarica annotazioni quali commenti da e verso un server di revisione e commento dei documenti online.</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>Connette ai servizi Web o ai database definiti in un modulo di PDF.</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>Modifica gli oggetti file incorporati associati al documento PDF.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>I diritti di utilizzo delle estensioni di Adobe Reader DC possono essere concessi in licenza da Adobe solo in determinate combinazioni che funzionano insieme. Non è possibile concedere in licenza queste funzionalità in modo indipendente. Per informazioni sulle combinazioni disponibili di diritti di utilizzo, contatta un rappresentante dell’account AEM Forms.
