---
title: Proprietà di configurazione di Interactive Communications
seo-title: Interactive Communication configuration properties
description: Modifica delle proprietà di configurazione predefinite per le comunicazioni interattive
seo-description: Edit default configuration properties for Interactive Communications
uuid: 4030078f-64a3-40bb-9892-49e22a8da561
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
discoiquuid: acb61d37-cd22-422e-bbf3-a2979b13ad41
docset: aem65
feature: Interactive Communication
exl-id: 09eeade6-e16d-4159-b26a-803c7201097a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 7%

---

# Proprietà di configurazione di Interactive Communications{#interactive-communications-configuration-properties}

Le comunicazioni interattive includono proprietà configurate automaticamente dopo l&#39;installazione del [Componente aggiuntivo AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md) pacchetto. Gli autori di comunicazioni interattive possono modificare queste proprietà di configurazione predefinite utilizzando **Configurazione della console Web di Adobe Experience Manager** pagina.

Apri **Configurazione della console Web di Adobe Experience Manager** utilizzando il seguente URL:

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

Le proprietà di configurazione includono:

* [Configurazione dei frammenti di documento](#document-fragments-configuration)
* [Creare la configurazione della corrispondenza](#create-correspondence-configuration)
* [Configurazione del canale web per moduli adattivi e comunicazioni interattive](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [Configurazione del tema del canale web di comunicazione e modulo adattivo](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## Configurazione dei frammenti di documento {#document-fragments-configuration}

Tocca **Configurazione dei frammenti di documento** sulla **Configurazione della console Web di Adobe Experience Manager** per visualizzare le proprietà di configurazione dei frammenti di documento.

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
   <td>Formato di visualizzazione specifico per le impostazioni internazionali per campi, variabili ed elementi del modello dati del modulo disponibili durante la creazione di una comunicazione interattiva per i canali Stampa e Web.</td> 
   <td> 
    <ul> 
     <li>locale = en_US, de_DE, fr_FR e ja_JP</li> 
     <li>dateFormat = dd-MM-yyyy</li> 
     <li>numberDecimalSeparator = .</li> 
     <li>numberGroupSeparator = ,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>—</p> </td> 
  </tr> 
  <tr> 
   <td>Rientro</td> 
   <td>Larghezza della singola unità di rientro applicata al testo nei frammenti di documento elenco.</td> 
   <td>12.7mm</td> 
   <td>Numero</td> 
  </tr> 
  <tr> 
   <td>Larghezza minima numeri romani</td> 
   <td>Larghezza minima da applicare al campo punto elenco o numero quando si utilizzano numeri romani nei frammenti di documento elenco. </td> 
   <td>12.7mm</td> 
   <td>Numero</td> 
  </tr> 
  <tr> 
   <td>Larghezza minima</td> 
   <td>Larghezza minima da applicare al campo punto elenco o numero quando si utilizzano elenchi numerati diversi dai numeri romani nei frammenti di documento elenco.</td> 
   <td>8.0mm</td> 
   <td>Numero</td> 
  </tr> 
 </tbody> 
</table>

## Creare la configurazione della corrispondenza {#create-correspondence-configuration}

Tocca **Creare la configurazione della corrispondenza** sulla **Configurazione della console Web di Adobe Experience Manager** per visualizzare le proprietà di configurazione per l&#39;interfaccia utente dell&#39;agente.

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
   <td>Selezionare la casella di controllo per visualizzare il contenuto risolto (valori effettivi anziché segnaposto) durante la modifica del modulo di testo nell'interfaccia utente dell'agente.</td> 
   <td>Non selezionato</td> 
   <td>Non applicabile</td> 
  </tr> 
  <tr> 
   <td>Applica filigrana durante l'anteprima</td> 
   <td>Selezionare la casella di controllo per applicare la filigrana al canale Stampa di comunicazione interattiva in modalità Anteprima.</td> 
   <td>Non selezionato</td> 
   <td>Non applicabile</td> 
  </tr> 
  <tr> 
   <td>Abilitare l’incorporazione dei font in PDF</td> 
   <td><p>Selezionare la casella di controllo per abilitare i font da incorporare nei documenti PDF. Dopo aver selezionato questa opzione, è possibile incorporare nuovi font dopo aver generato o visualizzato in anteprima i documenti PDF tramite l’interfaccia utente di Agent. Utilizzare il canale Stampa di comunicazioni interattive per generare e visualizzare in anteprima documenti PDF.</p> <p>L’incorporazione di font in un documento PDF è utile se un font è disponibile su un computer utilizzato per generare PDF e non è disponibile sul computer client che accede a PDF.</p> <p>Per ulteriori informazioni sull'incorporazione dei font, consulta <a href="../../forms/using/customize-text-editor.md" target="_blank">Personalizza editor di testo</a>.</p> </td> 
   <td>Non selezionato</td> 
   <td>Non applicabile</td> 
  </tr> 
 </tbody> 
</table>

## Configurazione del canale web per moduli adattivi e comunicazioni interattive {#adaptive-form-and-interactive-communication-web-channel-configuration}

Tocca **Configurazione del canale web per moduli adattivi e comunicazioni interattive** sulla **Configurazione della console Web di Adobe Experience Manager** pagina per visualizzare le proprietà di configurazione per il canale web Adaptive Forms e Interactive Communications. La tabella seguente descrive le proprietà relative alle comunicazioni interattive:

| Proprietà | Descrizione | Predefiniti | Valori accettabili |
|---|---|---|---|
| Mostra segnaposto | Seleziona la casella di controllo per abilitare la visualizzazione dei segnaposto per i campi inclusi nei moduli adattivi e nelle comunicazioni interattive. | Selezionato | Non applicabile |
| Numero massimo di voci della cache | Imposta il numero massimo di moduli adattivi e comunicazioni interattive recuperabili utilizzando la memoria cache. | 100 | Numero |
| Rendi univoco il nome del file | Seleziona la casella di controllo per assegnare nomi univoci ai file inclusi come allegati in Adaptive Forms e Interactive Communications. | Non selezionato | Non applicabile |

## Configurazione del tema del canale web di comunicazione e modulo adattivo {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

Tocca **Configurazione del tema del canale web di comunicazione e modulo adattivo** sulla **Configurazione della console Web di Adobe Experience Manager** pagina per visualizzare le proprietà di configurazione per i temi del canale web Adaptive Forms e Interactive Communications.

<table>
 <tbody> 
  <tr> 
   <td>Proprietà</td> 
   <td>Descrizione</td> 
   <td>Predefiniti</td> 
   <td>Valori accettabili</td> 
  </tr> 
  <tr> 
   <td>Nome elenco caratteri</td> 
   <td>Elenco dei font disponibili per la creazione di Adattivo Forms e comunicazioni interattive.</td> 
   <td><p>Georgia</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>Impatto</p> <p>Palatino Linotype</p> </td> 
   <td>Tutti i font validi del server di Adobe</td> 
  </tr> 
 </tbody> 
</table>
