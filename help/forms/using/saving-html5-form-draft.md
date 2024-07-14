---
title: Salvataggio di un modulo HTML5 come bozza
description: Salvare un modulo HTML5 come bozza e riprendere la compilazione in una fase successiva.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: HTML5 Forms,Mobile Forms
exl-id: a9879445-d626-4279-8a95-a9009294b483
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 5%

---

# Salvataggio di un modulo HTML5 come bozza {#saving-an-html-form-as-a-draft}

È possibile salvare un modulo HTML5 come bozza e riprendere la compilazione in una fase successiva. Forms Portal consente a qualsiasi utente di salvare e ripristinare un modulo di HTML5. Per abilitare la funzionalità Salva come bozza, aggiungi le seguenti configurazioni al nodo del profilo:

## Profilo personalizzato per consentire la funzione Salva come bozza {#custom-profile-to-allow-save-as-draft-feature}

AEM Forms fornisce automaticamente un profilo **Salva come bozza**. È possibile eseguire il rendering di un modulo con il profilo Salva come bozza per abilitare la funzionalità di bozza per un modulo HTML5. È possibile specificare il profilo di rendering HTML per un modulo in [Forms Manager](/help/forms/using/introduction-managing-forms.md).

Per abilitare la funzionalità Salva come bozza per il [profilo personalizzato](/help/forms/using/custom-profile.md) esistente, aggiungi le seguenti proprietà al nodo del profilo personalizzato:

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
   <td><p>Abilita salvataggio come feature di sformo</p> <p>per questo profilo.</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>Stringa</td>
   <td>vero</td>
   <td><p>Consente il caricamento di allegati</p> <p>con questo profilo.</p> </td>
  </tr>
 </tbody>
</table>

## Archiviazione ed elenco bozze {#drafts-storage-and-listing}

Dopo aver abilitato la funzionalità Salva come bozza per un modulo, il modulo salvato viene elencato nel [componente Bozze e invio](/help/forms/using/draft-submission-component.md). Potete recuperare e iniziare a riempire il modulo salvato con i componenti Bozza e Invio.

Per abilitare l’elenco dei moduli per il componente Bozza e Invio, aggiungi la seguente proprietà al nodo del profilo:

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
   <td>Per abilitare le bozze e i moduli per l'inserimento nell'elenco del componente Bozze e invii di Forms Portal dopo l'invio<br /></td>
  </tr>
 </tbody>
</table>

Per impostazione predefinita, AEM Forms memorizza i dati utente associati alla bozza e all’invio di un modulo nel nodo /content/forms/fp dell’istanza di Publish. È possibile aggiungere il provider di archiviazione personalizzato. Per informazioni dettagliate, vedere [Archiviazione personalizzata per il componente Bozze e invii](/help/forms/using/adding-custom-storage-provider-forms.md).
