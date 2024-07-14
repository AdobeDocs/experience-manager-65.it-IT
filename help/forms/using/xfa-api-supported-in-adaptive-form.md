---
title: Supporto XFA nei moduli adattivi basati su XDP
description: Elenca eventi, proprietà, script e convalida XFA supportati nei moduli adattivi.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 255be73f-3169-457c-aaa7-a2fb59f1f2cd
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 5%

---

# Supporto XFA nei moduli adattivi basati su XDP{#xfa-support-in-xdp-based-adaptive-forms}

## Introduzione {#introduction}

<span class="preview"> Adobe consiglia di utilizzare l&#39;acquisizione dati moderna ed estensibile [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=it) per [la creazione di un nuovo Forms adattivo](/help/forms/using/create-an-adaptive-form-core-components.md) o [l&#39;aggiunta di Forms adattivo alle pagine AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Questi componenti rappresentano un progresso significativo nella creazione di Forms adattivi, garantendo esperienze utente straordinarie. Questo articolo descrive un approccio precedente all’authoring di Forms adattivi utilizzando i componenti di base. </span>

I moduli adattivi supportano vari eventi, proprietà, script e convalide XFA definiti in un file XDP, tra cui:

* Esecuzione degli script definiti sugli eventi nel file XDP.
* Acquisizione dei valori predefiniti e delle proprietà comportamentali per i campi del file XDP.
* Esecuzione degli script di convalida definiti nel file XDP.

Quando un modulo adattivo viene creato in base a un file XDP, le proprietà, gli eventi e le convalide vengono compilati automaticamente nell’interfaccia utente per l’authoring dei moduli. Tuttavia, gli autori di moduli possono ignorare alcuni di questi elementi per creare un’esperienza alternativa.

Questo articolo elenca gli eventi, le proprietà e le convalide XFA supportati e rispettati nei moduli adattivi e spiega come sostituirli nei moduli adattivi.

## Elementi XFA supportati e loro mappatura nei moduli adattivi {#supported-xfa-elements-and-their-mapping-in-adaptive-forms-br}

### Campi {#fields}

Quando un modulo adattivo viene creato utilizzando un file XDP, puoi trascinare un campo XFA sul modulo adattivo. Nella tabella seguente è riportato il mapping dei campi XFA ai campi di un modulo adattivo.

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
   <td><p>Casella di riepilogo </p> </td>
   <td><p>Elenco a discesa</p> </td>
  </tr>
  <tr>
   <td><p>Campo data/ora </p> </td>
   <td><p>Selettore data</p> </td>
  </tr>
  <tr>
   <td><p>Disegno a mano</p> </td>
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
   <td><p>Set di sottomoduli </p> </td>
   <td><p>Pannello</p> </td>
  </tr>
 </tbody>
</table>

### Proprietà {#properties}

La tabella seguente acquisisce il comportamento nei moduli adattivi dei vari script XFA definiti nei file XDP.

<table>
 <tbody>
  <tr>
   <td><p><strong>Proprietà del componente XFA</strong></p> </td>
   <td><p><strong>Comportamento corrispondente nei moduli adattivi</strong></p> </td>
  </tr>
  <tr>
   <td><p>somExpression </p> </td>
   <td><p>Mappato alla proprietà Bind reference (bindRef) in un modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>presenza </p> </td>
   <td><p>Mappato alla proprietà visibile nel modulo adattivo. È possibile sostituirlo utilizzando l'espressione Visibilità.</p> </td>
  </tr>
  <tr>
   <td><p>accesso </p> </td>
   <td><p>Mappato alla proprietà abilitata in un modulo adattivo. È possibile sostituirlo utilizzando l'espressione di Access.</p> </td>
  </tr>
  <tr>
   <td><p>Accessibilità: ruolo </p> </td>
   <td><p>Mappato alla proprietà del ruolo nel modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>Accessibilità: talkPriority </p> </td>
   <td><p>Mappato alla proprietà talkPriority nel modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>Accessibilità: talkText</p> </td>
   <td><p>Mappato al testo personalizzato per l’accessibilità nel modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>Accessibilità: toolTip </p> </td>
   <td><p>Mappato alla proprietà di descrizione breve nel modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>didascalia<em> (tutti i tipi di campo)</em></p> </td>
   <td><p>Mappato alla proprietà Title nel modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>displayFormat<em> (tutti i tipi di campo)</em></p> </td>
   <td><p>Mappato al Pattern di visualizzazione in formato adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>rawValue<em> (tutti i tipi di campo)</em></p> </td>
   <td><p>Mappato alla proprietà value in adaptive Form.</p> </td>
  </tr>
  <tr>
   <td><p>elementi<em> (casella di riepilogo, casella di controllo)</em></p> </td>
   <td><p>Mappata alla proprietà options nel modulo adattivo. È possibile sostituirlo utilizzando l'espressione Opzioni.</p> </td>
  </tr>
  <tr>
   <td><p>maxChar<em> (campo di testo)</em></p> </td>
   <td><p>Mappato alla proprietà Numero massimo di caratteri consentiti nel modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>multiline<em> (campo di testo)</em></p> </td>
   <td><p>Mappato alla proprietà Allow multiple lines (Consenti più righe) nel modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>fracDigit<em> (campo numerico, campo decimale)</em></p> </td>
   <td><p>Mappato alla proprietà Frac digits nel modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>leadDigit<em> (campo numerico, campo decimale)</em></p> </td>
   <td><p>Mappato alla proprietà Cifre lead nel modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>multiSelect<em> (casella di riepilogo)</em></p> </td>
   <td><p>Mappato su Consente la selezione di più proprietà in un modulo adattivo.</p> </td>
  </tr>
 </tbody>
</table>

### Script {#scripts}

La tabella seguente acquisisce il comportamento nei moduli adattivi dei vari script XFA definiti nel file XDP.

<table>
 <tbody>
  <tr>
   <td><p><strong>Eventi script XFA</strong></p> </td>
   <td><p><strong>Comportamento corrispondente nei moduli adattivi</strong></p> </td>
  </tr>
  <tr>
   <td><p>inizializzare </p> </td>
   <td><p>Questo script viene eseguito in fase di runtime e non può essere sostituito in un modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>calcola</p> </td>
   <td><p>Mappato all’espressione Calculate nel modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>convalida </p> </td>
   <td><p>Mappato all’espressione Validation in un modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>validationState </p> </td>
   <td><p>Questo script viene eseguito in fase di esecuzione e non può essere sostituito in un modulo adattivo.<br /> </p> </td>
  </tr>
  <tr>
   <td><p>uscire </p> </td>
   <td><p>Questo script viene eseguito in fase di runtime e non può essere sostituito in un modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>clic (campi pulsante)</p> </td>
   <td><p>Mappato all'espressione Click del pulsante.</p> </td>
  </tr>
  <tr>
   <td><p>Supporto per script lato server</p> </td>
   <td><p>Questo script viene eseguito in fase di runtime e non può essere sostituito in un modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>Supporto per i servizi web</p> </td>
   <td><p>Questo script viene eseguito in fase di runtime e non può essere sostituito in un modulo adattivo.</p> </td>
  </tr>
  <tr>
   <td><p>Modifica (campo scarabocchio, pulsante di scelta, casella di controllo)</p> </td>
   <td><p>Questo script viene eseguito in fase di runtime e non può essere sostituito in un modulo adattivo.</p> </td>
  </tr>
 </tbody>
</table>

### Convalide {#validations}

La tabella seguente acquisisce il modo in cui le convalide XFA si associano alle convalide nei moduli adattivi.

<table>
 <tbody>
  <tr>
   <td><p><strong>Convalida XFA</strong></p> </td>
   <td><p><strong>Convalida corrispondente nel modulo adattivo</strong></p> </td>
  </tr>
  <tr>
   <td><p>Pattern di convalida (formatTest)</p> </td>
   <td><p>validatePictureClause</p> </td>
  </tr>
  <tr>
   <td><p>Messaggio modello di convalida (formatTestMessage)</p> </td>
   <td><p>validatePictureMessage</p> </td>
  </tr>
  <tr>
   <td><p>Obbligatorio (nullTest )</p> </td>
   <td><p>obbligatorio </p> </td>
  </tr>
  <tr>
   <td><p>Messaggio vuoto (nullTestMessage) </p> </td>
   <td><p>mandatoryMessage</p> </td>
  </tr>
  <tr>
   <td><p>Convalida script (scriptTest)</p> </td>
   <td><p>validateExp</p> </td>
  </tr>
  <tr>
   <td><p>Messaggio script di convalida (scriptTestMessage)</p> </td>
   <td><p>validateMessage</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Non è possibile ignorare la proprietà obbligatoria per i pulsanti di scelta e i gruppi di caselle di controllo dei moduli adattivi associati ai pulsanti di controllo XFA.
