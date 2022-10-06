---
title: Salvataggio di un modulo HTML5 come bozza
seo-title: Saving an HTML5 form as a draft
description: Salvare un modulo HTML5 come bozza e riprendere a compilarlo in un secondo momento.
seo-description: Save an HTML5 form as a draft and resume filling the form at a later stage.
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: Mobile Forms
exl-id: a9879445-d626-4279-8a95-a9009294b483
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 5%

---

# Salvataggio di un modulo HTML5 come bozza {#saving-an-html-form-as-a-draft}

È possibile salvare un modulo HTML5 come bozza e riprendere a compilarlo in un secondo momento. Forms Portal consente a qualsiasi utente di salvare e ripristinare un modulo HTML5. Per abilitare la funzionalità Salva come bozza, aggiungi le seguenti configurazioni al nodo del profilo:

## Profilo personalizzato per consentire la funzione Salva come bozza {#custom-profile-to-allow-save-as-draft-feature}

Con AEM Forms è disponibile un **Salva come bozza** profilo. È possibile eseguire il rendering di un modulo con il profilo Salva come bozza per abilitare la funzionalità di bozza per un modulo HTML5. È possibile specificare il profilo di rendering di HTML per un modulo in [Forms Manager](/help/forms/using/introduction-managing-forms.md).

Per abilitare la funzionalità Salva come bozza [profilo personalizzato](/help/forms/using/custom-profile.md), aggiungi le seguenti proprietà al nodo di profilo personalizzato:

<table>
 <tbody>
  <tr>
   <td><strong>Nome proprietà</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Valore</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>mfAllowFPDraft</td>
   <td>Stringa</td>
   <td>vero</td>
   <td><p>Abilita il salvataggio come feature di bozza</p> <p>per questo profilo.</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>Stringa</td>
   <td>vero</td>
   <td><p>Consente il caricamento degli allegati</p> <p>con questo profilo.</p> </td>
  </tr>
 </tbody>
</table>

## Archiviazione e inserimento di bozze {#drafts-storage-and-listing}

Dopo aver abilitato la funzionalità Salva come bozza per un modulo; quando il modulo viene salvato, viene elencato nella [Bozze e componente Invio](/help/forms/using/draft-submission-component.md). È possibile recuperare e iniziare a compilare il modulo salvato dal componente Bozza e Invia.

Per abilitare l’elenco dei moduli per il componente Bozza e Invia, aggiungi la seguente proprietà al nodo del profilo:

<table>
 <tbody>
  <tr>
   <td><strong>Nome proprietà</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Valore</strong></td>
   <td><strong>Descrizione</strong></td>
  </tr>
  <tr>
   <td>fp.enablePortalSubmit</td>
   <td>Stringa</td>
   <td>vero</td>
   <td>Per abilitare le bozze e i moduli ad essere elencati in<br /> Componente Bozze e invii del portale Forms dopo l’invio</td>
  </tr>
 </tbody>
</table>

Per impostazione predefinita, AEM Forms memorizza i dati utente associati alla bozza e all’invio di un modulo nel nodo /content/forms/fp sull’istanza Pubblica. Puoi aggiungere il provider di archiviazione personalizzato. Per ulteriori informazioni, consulta [Archiviazione personalizzata per il componente Bozze e invii](/help/forms/using/adding-custom-storage-provider-forms.md).
