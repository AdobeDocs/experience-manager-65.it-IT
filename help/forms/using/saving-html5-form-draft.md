---
title: Salvataggio di un modulo HTML5 come bozza
description: Salvare un modulo HTML5 come bozza e riprendere la compilazione in una fase successiva.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: Mobile Forms
exl-id: a9879445-d626-4279-8a95-a9009294b483
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 5%

---

# Salvataggio di un modulo HTML5 come bozza {#saving-an-html-form-as-a-draft}

È possibile salvare un modulo HTML5 come bozza e riprendere la compilazione in una fase successiva. Forms Portal consente a qualsiasi utente di salvare e ripristinare un modulo di HTML5. Per abilitare la funzionalità Salva come bozza, aggiungi le seguenti configurazioni al nodo del profilo:

## Profilo personalizzato per consentire la funzione Salva come bozza {#custom-profile-to-allow-save-as-draft-feature}

Con AEM Forms puoi offrire **Salva come bozza** profilo. È possibile eseguire il rendering di un modulo con il profilo Salva come bozza per abilitare la funzionalità di bozza per un modulo HTML5. È possibile specificare il profilo di rendering HTML per un modulo in [Forms Manager](/help/forms/using/introduction-managing-forms.md).

Per abilitare la funzionalità Salva come bozza per il file esistente [profilo personalizzato](/help/forms/using/custom-profile.md), aggiungi le seguenti proprietà al nodo del profilo personalizzato:

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

Dopo aver abilitato la funzionalità Salva come bozza per un modulo, quando il modulo viene salvato viene elencato in [Componente Bozze e invio](/help/forms/using/draft-submission-component.md). Potete recuperare e iniziare a riempire il modulo salvato con i componenti Bozza e Invio.

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
   <td>Per abilitare le bozze e i moduli da elencare in<br /> Componente Bozze e invii di Forms Portal dopo l’invio</td>
  </tr>
 </tbody>
</table>

Per impostazione predefinita, AEM Forms memorizza i dati utente associati alla bozza e all’invio di un modulo nel nodo /content/forms/fp dell’istanza Publish. È possibile aggiungere il provider di archiviazione personalizzato. Per ulteriori informazioni, vedere [Archiviazione personalizzata per il componente Bozze e invii](/help/forms/using/adding-custom-storage-provider-forms.md).
