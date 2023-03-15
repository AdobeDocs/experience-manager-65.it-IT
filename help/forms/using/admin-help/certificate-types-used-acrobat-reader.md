---
title: Tipi di certificato utilizzati dalle estensioni Acrobat Reader DC
seo-title: Certificate types used by Acrobat Reader DC extensions
description: Scopri i tipi di certificato utilizzati dalle estensioni Acrobat Reader DC.
seo-description: Learn about the certificate types used by Acrobat Reader DC extensions.
uuid: 93c02abc-2d5a-44ed-b93c-981afbd0553d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 331b9317-87b5-4a96-a1bc-429675ff90c5
exl-id: 800bffd5-0cdc-4251-bba4-e350f226f019
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 4%

---

# Tipi di certificato utilizzati dalle estensioni Acrobat Reader DC {#certificate-types-used-by-acrobat-reader-dc-extensions}

Il Visualizzatore certificati fornisce le seguenti informazioni sul certificato:

* Nome &quot;descrittivo&quot; del certificato
* Profili del certificato
* Periodo di validità
* Diritti di utilizzo delle estensioni Acrobat Reader DC

## Nome &quot;descrittivo&quot; del certificato {#certificate-friendly-name}

Il nome &quot;descrittivo&quot; di un certificato di estensione Acrobat Reader DC è una stringa che descrive le proprietà del certificato, come nell&#39;esempio seguente:

CODICI A Barre 2D Full Production V6.1 P8 0002054

La stringa contiene i seguenti elementi:

**Tipo di certificato:** Descrive i moduli AEM attivati dal certificato e il livello di attivazione, ad esempio ARE 2D Barcode Full. Per un elenco dei tipi di certificato disponibili, consulta la colonna Tipo nella tabella nella sezione Profili certificato .

**Tipo di distribuzione:** Indica l’uso previsto del certificato, ad esempio Produzione. Il valore può essere Valutazione o Produzione. Per un elenco dei tipi di distribuzione associati a ciascun tipo di certificato, consulta la colonna Tipo di distribuzione nella tabella nella sezione Profili certificato .

**Versione dei diritti di utilizzo:** Descrive la versione dell&#39;algoritmo dei diritti di utilizzo per cui è possibile utilizzare il certificato, ad esempio V6.1. Questa versione non indica la versione di Acrobat o delle estensioni Acrobat Reader DC.

**Codice profilo:** Il codice del profilo è una descrizione abbreviata delle proprietà complete del certificato, ad esempio P8. Per un elenco dei codici di profilo associati a ciascun tipo di file, consulta la colonna Codice profilo nella tabella nella sezione Profili certificato .

**Numero di serie:** A ciascun certificato rilasciato dall’Adobe viene assegnato un numero di serie, ad esempio 0002054. Adobe Enterprise Support o un rappresentante di account Adobe Enterprise può utilizzare questo numero di serie per tracciare il certificato in un ordine di prodotto specifico o in una relazione OEM.

## Profili del certificato {#certificate-profiles}

Nella tabella seguente sono elencati i profili di certificato che si possono incontrare durante l’analisi dei certificati delle estensioni Acrobat Reader DC.

<table>
 <thead>
  <tr>
   <th><p>Codice del profilo</p></th>
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
   <td><p>Test interno SAP</p></td>
   <td><p>2 anni</p></td>
   <td><p>Valutazione e prova</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Estensioni Acrobat Reader DC, Produzione</p></td>
   <td><p>Max</p></td>
   <td><p>Produzione</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Estensioni Acrobat Reader DC, uso Adobe interno</p></td>
   <td><p>2 anni</p></td>
   <td><p>Produzione</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Estensioni Acrobat Reader DC, integrazione dei partner</p></td>
   <td><p>2 anni</p></td>
   <td><p>Valutazione e prova</p></td>
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
   <td><p>Adobe Acrobat 7.x, produzione</p></td>
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

I certificati di valutazione vengono rilasciati a clienti e sviluppatori in modo che possano valutare e sviluppare applicazioni di esempio per i prodotti. Il periodo di validità dei certificati è compreso tra 60 e 90 giorni. Scadono alla fine del secondo mese successivo ai dati del problema.

I certificati di integrazione dei partner vengono rilasciati ai partner commerciali di Adobe per supportare lo sviluppo, l&#39;integrazione, la prototipazione e la dimostrazione del software. Tali certificati sono validi per due anni dalla data del rilascio.

Adobe I certificati per uso interno vengono utilizzati in Adobe per supportare lo sviluppo, l&#39;integrazione, la prototipazione e la dimostrazione del software. Tali certificati sono validi per due anni dalla data del rilascio.

I certificati di produzione vengono rilasciati ai clienti che hanno acquistato estensioni Acrobat Reader DC. Tali certificati sono validi per il periodo massimo consentito dall&#39;autorità di certificazione (CA), indicato come *Max* nella tabella Profili certificato.

## Diritti di utilizzo delle estensioni Acrobat Reader DC {#acrobat-reader-dc-extensions-usage-rights}

Quando si esamina il certificato delle estensioni Acrobat Reader DC nel Visualizzatore certificati, è possibile selezionare la voce dei diritti di utilizzo dalla scheda Dettagli (se configurata) per visualizzare un elenco dettagliato dei diritti di utilizzo Adobe Reader che il certificato può abilitare. I diritti di utilizzo abilitati in un particolare documento possono essere un sottoinsieme di quelli abilitati dal certificato.

Se in un ambiente non collaborativo è necessario inserire commenti online, contatta il supporto Adobe per ulteriori informazioni. La proprietà Mode corrisponde al tipo di distribuzione ed è *produzione* o *valutazione*.

I diritti di utilizzo consentiti per le estensioni Acrobat Reader DC sono costituiti da uno o più elementi specifici. Questi elementi vengono utilizzati in diverse combinazioni per ottenere varietà di funzionalità del prodotto concesso in licenza.

<table>
 <thead>
  <tr>
   <th><p>Elemento dei diritti di utilizzo</p></th>
   <th><p>Funzionalità abilitata in Adobe Reader quando si visualizza un documento PDF abilitato per i diritti</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormFillInAndSave</p></td>
   <td><p>Compila i campi del modulo e salva i file localmente.</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>Importare ed esportare i dati dei moduli come file FDF, XFDF, XML e XDP.</p></td>
  </tr>
  <tr>
   <td><p>FormAddDelete</p></td>
   <td><p>Aggiungere, modificare o eliminare campi e proprietà dei campi nel modulo PDF.</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>Invia i dati, per e-mail o offline, a un server quando non è in esecuzione in una sessione del browser.</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>Crea pagine da pagine modello all’interno dello stesso modulo PDF.</p></td>
  </tr>
  <tr>
   <td><p>Firma</p></td>
   <td><p>Firma digitale e salva i documenti PDF e cancella le firme digitali.</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>Crea e modifica annotazioni di documenti, ad esempio commenti.</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>È possibile salvare annotazioni, ad esempio commenti, in un file di dati separato e caricare commenti da un file.</p></td>
  </tr>
  <tr>
   <td><p>Codice a barreTesto</p></td>
   <td><p>Stampa un documento con dati a barre del modulo codificati in un modulo non crittografato che non richiede la decodifica del software del server concesso in licenza.</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>Carica e scarica annotazioni come commenti da e verso un server di revisione e commento dei documenti online.</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>Connettersi a servizi Web o database definiti all’interno di un modulo PDF.</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>Modificare gli oggetti file incorporati associati al documento PDF.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>I diritti di utilizzo delle estensioni Acrobat Reader DC possono essere concessi in licenza da Adobe solo in determinate combinazioni che funzionano insieme. Non è possibile concedere in licenza queste funzionalità in modo indipendente. Per informazioni sulle combinazioni disponibili di diritti di utilizzo, contattare un rappresentante commerciale AEM forms.
