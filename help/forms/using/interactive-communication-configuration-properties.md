---
title: Proprietà di configurazione delle comunicazioni interattive
description: Modificare le proprietà di configurazione predefinite per le comunicazioni interattive
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
docset: aem65
feature: Interactive Communication
exl-id: 09eeade6-e16d-4159-b26a-803c7201097a
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 6%

---

# Proprietà di configurazione delle comunicazioni interattive{#interactive-communications-configuration-properties}

Le comunicazioni interattive includono proprietà configurate automaticamente dopo l&#39;installazione del pacchetto del componente aggiuntivo [AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md). Gli autori di comunicazioni interattive possono modificare queste proprietà di configurazione predefinite utilizzando la pagina **Configurazione console Web Adobe Experience Manager**.

Aprire la pagina **Configurazione console Web Adobe Experience Manager** utilizzando il seguente URL:

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

Le proprietà di configurazione includono:

* [Configurazione frammenti di documenti](#document-fragments-configuration)
* [Crea configurazione corrispondenza](#create-correspondence-configuration)
* [Configurazione di un modulo adattivo e di un canale web di comunicazione interattiva](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [Configurazione del tema per canale web di comunicazione interattiva e modulo adattivo](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## Configurazione frammenti di documenti {#document-fragments-configuration}

Selezionare **Configurazione frammenti di documento** nella pagina **Configurazione console Web Adobe Experience Manager** per visualizzare le proprietà di configurazione per i frammenti di documento.

<table>
 <tbody> 
  <tr> 
   <td>Proprietà</td> 
   <td>Descrizione</td> 
   <td>Predefiniti</td> 
   <td>Valori accettabili</td> 
  </tr> 
  <tr> 
   <td>Formati di visualizzazione dei dati</td> 
   <td>Formato di visualizzazione specifico per la lingua per campi, variabili ed elementi del modello dati del modulo disponibili durante la creazione di una comunicazione interattiva per la stampa e i canali web.</td> 
   <td> 
    <ul> 
     <li>locale = en_US, de_DE, fr_FR e ja_JP</li> 
     <li>dateFormat = gg-MM-aaaa</li> 
     <li>numberDecimalSeparator = .</li> 
     <li>numberGroupSeparator = ,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>—</p> </td> 
  </tr> 
  <tr> 
   <td>Rientro</td> 
   <td>Larghezza della singola unità di rientro applicata al testo nei frammenti di documento elenco.</td> 
   <td>12,7 mm</td> 
   <td>Numero</td> 
  </tr> 
  <tr> 
   <td>Larghezza minima numeri romani</td> 
   <td>Larghezza minima da applicare al punto elenco o al campo numerico quando si utilizzano numeri romani nei frammenti di documento elenco. </td> 
   <td>12,7 mm</td> 
   <td>Numero</td> 
  </tr> 
  <tr> 
   <td>Larghezza minima numero</td> 
   <td>Larghezza minima da applicare al punto elenco o al campo numerico quando si utilizzano elenchi numerati oltre ai numeri romani nei frammenti di documenti elenco.</td> 
   <td>8 mm</td> 
   <td>Numero</td> 
  </tr> 
 </tbody> 
</table>

## Crea configurazione corrispondenza {#create-correspondence-configuration}

Selezionare **Crea configurazione corrispondenza** nella pagina **Configurazione console Web Adobe Experience Manager** per visualizzare le proprietà di configurazione per l&#39;interfaccia utente dell&#39;agente.

<table>
 <tbody> 
  <tr> 
   <td>Proprietà</td> 
   <td>Descrizione</td> 
   <td>Predefiniti</td> 
   <td>Valori accettabili</td> 
  </tr> 
  <tr> 
   <td>Mostra contenuto risolto per la modifica</td> 
   <td>Seleziona la casella di controllo per mostrare il contenuto risolto (valori effettivi anziché segnaposto) durante la modifica del modulo di testo nell’interfaccia utente dell’agente.</td> 
   <td>Non selezionato</td> 
   <td>Non applicabile</td> 
  </tr> 
  <tr> 
   <td>Applica filigrana durante l'anteprima</td> 
   <td>Selezionare la casella di controllo per applicare la filigrana al canale di stampa della comunicazione interattiva in modalità Anteprima.</td> 
   <td>Non selezionato</td> 
   <td>Non applicabile</td> 
  </tr> 
  <tr> 
   <td>Abilitare l’incorporamento di font in PDF</td> 
   <td><p>Selezionare la casella di controllo per abilitare l'incorporamento dei caratteri nei documenti PDF. Dopo aver selezionato questa opzione, puoi incorporare nuovi font dopo aver generato o visualizzato in anteprima i documenti PDF utilizzando l’interfaccia utente di Agent. Utilizza il canale Stampa di comunicazione interattiva per generare e visualizzare in anteprima i documenti PDF.</p> <p>L'incorporamento di tipi di carattere in un documento PDF è utile se un tipo di carattere è disponibile in un computer utilizzato per generare il PDF e non è disponibile nel computer client che accede al PDF.</p> <p>Per ulteriori informazioni sull'incorporamento dei caratteri, vedere <a href="../../forms/using/customize-text-editor.md" target="_blank">Personalizzare l'editor di testo</a>.</p> </td> 
   <td>Non selezionato</td> 
   <td>Non applicabile</td> 
  </tr> 
 </tbody> 
</table>

## Configurazione di un modulo adattivo e di un canale web di comunicazione interattiva {#adaptive-form-and-interactive-communication-web-channel-configuration}

Selezionare **Configurazione modulo adattivo e canale web comunicazione interattiva** nella pagina **Configurazione console web Adobe Experience Manager** per visualizzare le proprietà di configurazione per il canale web Forms adattivo e comunicazione interattiva. La tabella seguente descrive le proprietà relative alle comunicazioni interattive:

| Proprietà | Descrizione | Predefiniti | Valori accettabili |
|---|---|---|---|
| Mostra segnaposto | Seleziona la casella di controllo per abilitare la visualizzazione dei segnaposto per i campi inclusi nei moduli adattivi e nelle comunicazioni interattive. | Selezionato | Non applicabile |
| Numero massimo di voci cache | Imposta il numero massimo di moduli adattivi e comunicazioni interattive che possono essere recuperati utilizzando la memoria cache. | 100 | Numero |
| Rendi univoco il nome del file | Seleziona la casella di controllo per assegnare nomi univoci ai file da includere come allegati in Adaptive Forms e nelle comunicazioni interattive. | Non selezionato | Non applicabile |

## Configurazione del tema per canale web di comunicazione interattiva e modulo adattivo {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

Selezionare **Configurazione tema modulo adattivo e canale web comunicazione interattiva** nella pagina **Configurazione console Web Adobe Experience Manager** per visualizzare le proprietà di configurazione per i temi del canale web Forms adattivo e comunicazione interattiva.

<table>
 <tbody> 
  <tr> 
   <td>Proprietà</td> 
   <td>Descrizione</td> 
   <td>Predefiniti</td> 
   <td>Valori accettabili</td> 
  </tr> 
  <tr> 
   <td>Nome elenco tipi di carattere</td> 
   <td>Elenco di font disponibili per la creazione di Forms adattivi e comunicazioni interattive.</td> 
   <td><p>Georgia</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>Impatto</p> <p>Palatino Linotype</p> </td> 
   <td>Tutti i font server Adobe validi</td> 
  </tr> 
 </tbody> 
</table>
