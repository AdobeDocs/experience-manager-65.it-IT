---
title: Supporto XFA nei moduli adattivi basati su XDP
seo-title: Supporto XFA nei moduli adattivi basati su XDP
description: Elenca eventi, proprietà, script e convalida XFA supportati nei moduli adattivi.
seo-description: Elenca eventi, proprietà, script e convalida XFA supportati nei moduli adattivi.
uuid: 75d3c292-cfed-438f-afdb-4071d95a08b7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 05303b29-9058-4723-b134-4ba605fe40c7
docset: aem65
translation-type: tm+mt
source-git-commit: 68ea2335a8466c3c23b766efb1a04b6a38d7f670
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 7%

---


# Supporto XFA nei moduli adattivi basati su XDP{#xfa-support-in-xdp-based-adaptive-forms}

## Introduzione {#introduction}

I moduli adattivi supportano vari eventi, proprietà, script e convalide XFA definiti in un file XDP, tra cui:

* Esecuzione di script definiti sugli eventi nel file XDP.
* Acquisizione di valori predefiniti e proprietà comportamentali per i campi nel file XDP.
* Esecuzione di script di convalida definiti nel file XDP.

Quando si crea un modulo adattivo basato su un file XDP, le proprietà, gli eventi e le convalide vengono compilati automaticamente nell&#39;interfaccia utente di authoring del modulo. Tuttavia, gli autori dei moduli possono ignorare alcuni di questi elementi per creare un&#39;esperienza alternativa.

Questo articolo elenca gli eventi, le proprietà e le convalide XFA supportati nei moduli adattivi e spiega come sostituirli nei moduli adattivi.

## Elementi XFA supportati e relativa mappatura nei moduli adattivi {#supported-xfa-elements-and-their-mapping-in-adaptive-forms-br}

### espandibili {#fields}

Quando si crea un modulo adattivo utilizzando un file XDP, è possibile trascinare un campo XFA nel modulo adattivo. Nella tabella seguente è riportato il modo in cui i campi XFA vengono mappati ai campi modulo adattivi.

<table>
 <tbody>
  <tr>
   <td><p><strong>Campo o contenitore XFA</strong></p> </td>
   <td><p><strong>Componente modulo adattivo corrispondente</strong></p> </td>
  </tr>
  <tr>
   <td><p>Pulsante </p> </td>
   <td><p>Pulsante</p> </td>
  </tr>
  <tr>
   <td><p>Casella di controllo </p> </td>
   <td><p>Casella di controllo</p> </td>
  </tr>
  <tr>
   <td><p>List Box </p> </td>
   <td><p>Elenco a discesa</p> </td>
  </tr>
  <tr>
   <td><p>Campo data/ora </p> </td>
   <td><p>Selettore data</p> </td>
  </tr>
  <tr>
   <td><p>Firma scarabocchio</p> </td>
   <td><p>Firma a mano</p> </td>
  </tr>
  <tr>
   <td><p>Campo numerico </p> </td>
   <td><p>Casella numerica</p> </td>
  </tr>
  <tr>
   <td><p>Campo decimale</p> </td>
   <td><p>Casella numerica</p> </td>
  </tr>
  <tr>
   <td><p>Campo testo </p> </td>
   <td><p>Casella di testo</p> </td>
  </tr>
  <tr>
   <td><p>Campo password </p> </td>
   <td><p>Casella password</p> </td>
  </tr>
  <tr>
   <td><p>Immagine</p> </td>
   <td><p>Immagine</p> </td>
  </tr>
  <tr>
   <td><p>Testo</p> </td>
   <td><p>Testo</p> </td>
  </tr>
  <tr>
   <td><p>Sottomodulo </p> </td>
   <td><p>Pannello</p> </td>
  </tr>
  <tr>
   <td><p>Area (gruppo)</p> </td>
   <td><p>Pannello</p> </td>
  </tr>
  <tr>
   <td><p>Set sottomodulo </p> </td>
   <td><p>Pannello</p> </td>
  </tr>
 </tbody>
</table>

### Proprietà {#properties}

Nella tabella seguente è illustrato il funzionamento dei vari script XFA definiti nei file XDP nei moduli adattivi.

<table>
 <tbody>
  <tr>
   <td><p><strong>Proprietà dei componenti XFA</strong></p> </td>
   <td><p><strong>Comportamento corrispondente nei moduli adattivi</strong></p> </td>
  </tr>
  <tr>
   <td><p>somExpression </p> </td>
   <td><p>Mappata alla proprietà Bind reference (bindRef) in forma adattiva.</p> </td>
  </tr>
  <tr>
   <td><p>presence (presenza) </p> </td>
   <td><p>Mappata alla proprietà visibile in modulo adattivo. Puoi ignorarlo utilizzando l'espressione Visibilità.</p> </td>
  </tr>
  <tr>
   <td><p>access </p> </td>
   <td><p>Mappata alla proprietà enabled in modulo adattivo. È possibile sostituirlo utilizzando l'espressione Access.</p> </td>
  </tr>
  <tr>
   <td><p>Accessibilità: role </p> </td>
   <td><p>Mappata alla proprietà role in modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>Accessibilità: speakPriority </p> </td>
   <td><p>Mappata alla proprietà speakPriority in forma adattiva.</p> </td>
  </tr>
  <tr>
   <td><p>Accessibilità: speakText</p> </td>
   <td><p>Mappata al testo Accessibilità personalizzato in modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>Accessibilità: toolTip </p> </td>
   <td><p>Mappata alla proprietà short description in forma adattiva.</p> </td>
  </tr>
  <tr>
   <td><p>caption<em> (tutti i tipi di campo)</em></p> </td>
   <td><p>Mappata alla proprietà Titolo in modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>displayFormat<em> (tutti i tipi di campo)</em></p> </td>
   <td><p>Mappata al pattern di visualizzazione in forma adattiva.</p> </td>
  </tr>
  <tr>
   <td><p>rawValue<em> (tutti i tipi di campo)</em></p> </td>
   <td><p>Mappata alla proprietà value in Modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>items<em> (casella di riepilogo, casella di controllo)</em></p> </td>
   <td><p>Mappata alla proprietà options in modulo adattivo. È possibile ignorarlo utilizzando l'espressione Opzioni.</p> </td>
  </tr>
  <tr>
   <td><p>maxChar<em> (Campo di testo)</em></p> </td>
   <td><p>Mappata alla proprietà Numero massimo di caratteri consentiti in un modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>multiline<em> (Campo di testo)</em></p> </td>
   <td><p>Mappata alla proprietà Consenti righe multiple nel modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>fracDigit<em> (Campo numerico, Campo decimale)</em></p> </td>
   <td><p>Mappata alla proprietà Frac Cifre in modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>leadDigit<em> (campo numerico, campo decimale)</em></p> </td>
   <td><p>Mappata alla proprietà Cifre lead in modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>multiSelect<em> (casella di riepilogo)</em></p> </td>
   <td><p>Mappata alla proprietà Consente più selezioni in modulo adattivo.</p> </td>
  </tr>
 </tbody>
</table>

### Script {#scripts}

Nella tabella seguente è illustrato il funzionamento dei vari script XFA definiti nel file XDP nei moduli adattivi.

<table>
 <tbody>
  <tr>
   <td><p><strong>Eventi script XFA</strong></p> </td>
   <td><p><strong>Comportamento corrispondente nei moduli adattivi</strong></p> </td>
  </tr>
  <tr>
   <td><p>initialize </p> </td>
   <td><p>Questo script viene eseguito in fase di esecuzione e non può essere ignorato in un modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>calculate</p> </td>
   <td><p>Mappata all'espressione Calculate in forma adattiva.</p> </td>
  </tr>
  <tr>
   <td><p>validate </p> </td>
   <td><p>Mappata all'espressione Validation in modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>validationState </p> </td>
   <td><p>Questo script viene eseguito in fase di esecuzione e non può essere ignorato in un modulo adattivo.<br /> </p> </td>
  </tr>
  <tr>
   <td><p>exit </p> </td>
   <td><p>Questo script viene eseguito in fase di esecuzione e non può essere ignorato in un modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>click (campi pulsante)</p> </td>
   <td><p>Mappata all'espressione Click del pulsante.</p> </td>
  </tr>
  <tr>
   <td><p>Supporto per script sul lato server</p> </td>
   <td><p>Questo script viene eseguito in fase di esecuzione e non può essere ignorato in un modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>Supporto per i servizi Web</p> </td>
   <td><p>Questo script viene eseguito in fase di esecuzione e non può essere ignorato in un modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>Modifica (campo di scripting, pulsante di scelta, casella di controllo)</p> </td>
   <td><p>Questo script viene eseguito in fase di esecuzione e non può essere ignorato in un modulo adattivo.</p> </td>
  </tr>
 </tbody>
</table>

### Convalide {#validations}

La tabella seguente illustra il modo in cui le convalide XFA vengono associate alle convalide nei moduli adattivi.

<table>
 <tbody>
  <tr>
   <td><p><strong>Convalida XFA</strong></p> </td>
   <td><p><strong>Convalida corrispondente nel modulo adattivo</strong></p> </td>
  </tr>
  <tr>
   <td><p>Pattern convalida (formatTest)</p> </td>
   <td><p>validatePictureClause</p> </td>
  </tr>
  <tr>
   <td><p>Messaggio pattern convalida (formatTestMessage)</p> </td>
   <td><p>validatePictureMessage</p> </td>
  </tr>
  <tr>
   <td><p>Obbligatorio (nullTest)</p> </td>
   <td><p>mandatory </p> </td>
  </tr>
  <tr>
   <td><p>Messaggio vuoto (nullTestMessage) </p> </td>
   <td><p>mandatoryMessage</p> </td>
  </tr>
  <tr>
   <td><p>Convalida dello script (scriptTest)</p> </td>
   <td><p>validateExp</p> </td>
  </tr>
  <tr>
   <td><p>Messaggio script convalida (scriptTestMessage)</p> </td>
   <td><p>validateMessage</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Non è possibile ignorare le proprietà obbligatorie per i pulsanti di scelta modulo adattivo e il gruppo di caselle di controllo associati ai pulsanti di controllo XFA.

