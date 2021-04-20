---
title: Salvataggio di un modulo HTML5 come bozza
seo-title: Salvataggio di un modulo HTML5 come bozza
description: Salvare un modulo HTML5 come bozza e riprendere a compilarlo in un secondo momento.
seo-description: Salvare un modulo HTML5 come bozza e riprendere a compilarlo in un secondo momento.
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 5%

---


# Salvataggio di un modulo HTML5 come bozza {#saving-an-html-form-as-a-draft}

È possibile salvare un modulo HTML5 come bozza e riprendere a compilarlo in un secondo momento. Forms Portal consente a qualsiasi utente di salvare e ripristinare un modulo HTML5. Per abilitare la funzionalità Salva come bozza, aggiungi le seguenti configurazioni al nodo del profilo:

## Profilo personalizzato per consentire la funzione Salva come bozza {#custom-profile-to-allow-save-as-draft-feature}

Con AEM Forms è disponibile un profilo **Salva come bozza** . È possibile eseguire il rendering di un modulo con il profilo Salva come bozza per abilitare la funzionalità di bozza per un modulo HTML5. È possibile specificare il profilo di rendering HTML per un modulo in [Forms Manager](/help/forms/using/introduction-managing-forms.md).

Per abilitare la funzionalità Salva come bozza per il tuo profilo [personalizzato esistente](/help/forms/using/custom-profile.md), aggiungi le seguenti proprietà al nodo di profilo personalizzato:

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

Dopo aver abilitato la funzionalità Salva come bozza per un modulo; quando il modulo viene salvato, viene elencato nel componente [Bozze e invio](/help/forms/using/draft-submission-component.md). È possibile recuperare e iniziare a compilare il modulo salvato dal componente Bozza e Invia.

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
   <td>Per abilitare le bozze e i moduli per essere elencati nel componente <br /> Bozze e invii del portale Forms dopo l’invio</td>
  </tr>
 </tbody>
</table>

Per impostazione predefinita, AEM Forms memorizza i dati utente associati alla bozza e all’invio di un modulo nel nodo /content/forms/fp sull’istanza Pubblica. È possibile aggiungere il provider di archiviazione personalizzato. Per ulteriori informazioni, vedere [Archiviazione personalizzata per il componente Bozze e invii](/help/forms/using/adding-custom-storage-provider-forms.md).
