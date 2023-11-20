---
title: Hotfix per AEM Form Service Pack
description: Informazioni su come scaricare e installare l'hotfix per AEM Forms Service Pack
source-git-commit: 169d407835098add0312b0d12c2c80035b525762
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---


# Hotfix per Adobe Experience Manager{#aem-form-hotfix}

L&#39;installazione della più recente [Service Pack AEM](/help/release-notes/release-notes.md) Si consiglia di includere correzioni di problemi e miglioramenti a livello di sicurezza, prestazioni, stabilità, nonché correzioni di problemi segnalati dai clienti, introdotti successivamente alla data di disponibilità generale di Adobe Experience Manager 6.5.

## Hotfix per Adaptive Forms {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Data</strong></td>
    <td><strong>Nomi hotfix</strong></td>
    <td><strong>Correzioni</strong></td>
   </tr>
   <tr>
    <td>20 novembre 2023</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Hotfix per AEM Service Pack 6.5.18.0 per Linux</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">Hotfix per AEM Service Pack 6.5.18.0 per Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">Hotfix per AEM Service Pack 6.5.18.0 per Mac OS</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li>La firma in linea non funziona più quando viene impostato un URL di reindirizzamento nel contenitore della guida di un modulo adattivo. (FORMS-10493)</li>
    <li>Non è possibile pubblicare i modelli del documento record (DoR) per Adaptive Forms localizzato. (FORMS-10535)</li>
    <li>La comunicazione interattiva con immagini in linea di grandi dimensioni non si apre correttamente in modalità di modifica. (FORMS-10578)</li>
    </ul>
    </td>    
    </tr>
    <tbody>
     </table>

## Download e installazione di Hotfix {#download-install-hotfix}

Per scaricare e installare l’Hotfix, effettua le seguenti operazioni:

1. Scarica [Hotfix](#hotfix-for-adaptive-forms) dal collegamento SD.
1. Estrai il file di archivio Hotfix per ottenere un pacchetto Experience Manager (.zip) e i file bundle (.jar).
1. Carica e installa il pacchetto (.zip) tramite Gestione pacchetti.
1. Apri i bundle di Gestione configurazione `https://server:host/system/console/bundles`, carica e installa il bundle (.jar).
