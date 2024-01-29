---
title: Hotfix per AEM Forms
description: Informazioni su come scaricare e installare un hotfix per AEM Forms.
exl-id: 37287332-3c8d-4ddc-a77e-3c5ee332898b
source-git-commit: 4685a4babbec07dc09fe19c9264b4141b9989fbb
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 1%

---

# Hotfix per Adobe Experience Manager Forms{#aem-form-hotfix}

In questo articolo sono elencate le correzioni critiche implementate per risolvere problemi noti, migliorare la stabilità del sistema e migliorare le prestazioni complessive di AEM Forms.

>[!NOTE]
>
> Gli hotfix sono progettati per essere cumulativi e comprendono tutte le correzioni precedenti. Quando applichi l’aggiornamento rapido più recente a una versione, questo non solo risolve il problema più recente, ma incorpora anche tutte le correzioni di bug e i miglioramenti precedenti.

## Hotfix per Adaptive Forms {#hotfix-for-adaptive-forms}

<table>
  <tbody>
  <tr>
    <td><strong>Data</strong></td>
    <td><strong>Collegamento per il download degli hotfix (collegamento per la distribuzione di software AEM)</strong></td>
    <td><strong>Problemi risolti</strong></td>
  </tr>
  <tr>
    <td>martedì 29 gennaio 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fforms-foundation-qs-content-4.0.170-FORMS-12692-B0001.zip">Hotfix per AEM Service Pack 6.5.19.0 per Windows sul server JEE</a> </li>
     </ul>
     </td>
    <td>
    <ul>
    <li>In AEM Forms sul server JEE, il Forms HTML5 che utilizza il percorso di contesto non riesce a eseguire il rendering. (FORMS-12485)</li>
    </ul>
    </td>    
  </tr>
  <tr>
    <td>martedì 29 gennaio 2024</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-win-pkg-6.0.1016-004.zip">Hotfix per AEM Service Pack 6.5.18.0 per Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-linux-pkg-6.0.1016-004.zip">Hotfix per AEM Service Pack 6.5.18.0 per Linux</a></li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Ffd%2Fadobe-aemfd-osx-pkg-6.0.1016-004.zip">Hotfix per AEM Service Pack 6.5.18.0 per Apple macOS</a></li>
     </ul>
     </td>
    <td>
    <ul>
    <li> Il componente Firma a mano scarabocchio incluso non viene riprodotto correttamente per un’anteprima in un modulo adattivo. (FORMS-12073)</li>
    </ul>
    </td>    
   </tr>
   <tr>
    <td>martedì 20 novembre 2023</td>
     <td>
     <ul>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-linux-pkg-6.0.1016-002.zip">Hotfix per AEM Service Pack 6.5.18.0 per Linux</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-win-pkg-6.0.1016-002.zip">Hotfix per AEM Service Pack 6.5.18.0 per Microsoft Windows</a> </li>
     <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/adobe-aemfd-osx-pkg-6.0.1016-002.zip">Hotfix per AEM Service Pack 6.5.18.0 per Apple macOS</a></li>
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

## Scaricare e installare un Hotfix {#download-install-hotfix}

Per scaricare e installare l’Hotfix, effettua le seguenti operazioni:

1. Scarica [Hotfix](#hotfix-for-adaptive-forms) dal collegamento Software Distribution.
1. Estrai il file di archivio Hotfix per ottenere un pacchetto Experience Manager (.zip) e i file bundle (.jar).
1. Carica e installa il pacchetto (.zip) tramite [Gestione pacchetti](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=es#accessing).
1. Apri i bundle di Gestione configurazione `https://server:host/system/console/bundles`, carica e installa il bundle (.jar). L&#39;aggiornamento rapido è installato.
