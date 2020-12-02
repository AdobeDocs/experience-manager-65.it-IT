---
title: Salvataggio di un modulo HTML5 come bozza
seo-title: Salvataggio di un modulo HTML5 come bozza
description: Salvare un modulo HTML5 come bozza e riprendere a compilare il modulo in una fase successiva.
seo-description: Salvare un modulo HTML5 come bozza e riprendere a compilare il modulo in una fase successiva.
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 4%

---


# Salvataggio di un modulo HTML5 come bozza {#saving-an-html-form-as-a-draft}

È possibile salvare un modulo HTML5 come bozza e riprendere a compilare il modulo in un secondo momento. Forms Portal consente a qualsiasi utente di salvare e ripristinare un modulo HTML5. Per abilitare la funzionalità Salva come bozza, aggiungi le seguenti configurazioni al nodo del profilo:

## Profilo personalizzato per consentire la funzione Salva come bozza {#custom-profile-to-allow-save-as-draft-feature}

In questo caso,  AEM Forms fornisce un profilo **Salva come bozza**. È possibile eseguire il rendering di un modulo con il profilo Salva come bozza per abilitare la funzionalità bozza per un modulo HTML5. È possibile specificare il profilo di rendering HTML per un modulo in [Forms Manager](/help/forms/using/introduction-managing-forms.md).

Per abilitare la funzionalità Salva come bozza per il profilo [personalizzato esistente](/help/forms/using/custom-profile.md), aggiungi le seguenti proprietà al nodo del profilo personalizzato:

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
   <td><p>Abilita la funzione Salva come bozza</p> <p>per questo profilo.</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>Stringa</td>
   <td>vero</td>
   <td><p>Consente il caricamento di allegati</p> <p>con questo profilo.</p> </td>
  </tr>
 </tbody>
</table>

## Archivio e elenco delle bozze {#drafts-storage-and-listing}

Dopo aver attivato la funzionalità Salva come bozza per un modulo; quando il modulo viene salvato, viene elencato nel componente [Bozze e invio](/help/forms/using/draft-submission-component.md). È possibile recuperare e iniziare a compilare il modulo salvato dal componente Bozza e Invia.

Per abilitare l&#39;elenco dei moduli per il componente Bozza e Invia, aggiungere la seguente proprietà al nodo del profilo:

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
   <td>Per abilitare le bozze e i moduli per essere elencati nel componente Bozze e invii di Forms Portal dopo l'invio<br /></td>
  </tr>
 </tbody>
</table>

Per impostazione predefinita,  AEM Forms memorizza i dati utente associati alla bozza e all&#39;invio di un modulo nel nodo /content/forms/fp nell&#39;istanza Pubblica. È possibile aggiungere il provider di archiviazione personalizzato. Per informazioni dettagliate, vedere [Memorizzazione personalizzata per il componente Bozze e invii](/help/forms/using/adding-custom-storage-provider-forms.md).
