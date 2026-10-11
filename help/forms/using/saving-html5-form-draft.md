---
title: Salvare un modulo HTML5 come bozza
description: Salvare un modulo di HTML5 come bozza e riprendere la compilazione del modulo in una fase successiva.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: HTML5 Forms,Mobile Forms
exl-id: a9879445-d626-4279-8a95-a9009294b483
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 10%
---
# Salvare un modulo HTML5 come bozza {#saving-an-html-form-as-a-draft}

È possibile salvare un modulo di HTML5 come bozza e riprendere la compilazione del modulo in una fase successiva. Forms Portal consente a qualsiasi utente di salvare e ripristinare un modulo HTML5. Per abilitare la funzionalità Salva come bozza, aggiungi le seguenti configurazioni al nodo del profilo:

## Profilo personalizzato per consentire la funzione Salva come bozza {#custom-profile-to-allow-save-as-draft-feature}

AEM Forms fornisce automaticamente un profilo **Salva come bozza**. È possibile eseguire il rendering di un modulo con il profilo Salva come bozza per abilitare la funzionalità di bozza per un modulo di HTML5. È possibile specificare il profilo di rendering di HTML per un modulo in [Forms Manager](/help/forms/using/introduction-managing-forms.md).

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

Per impostazione predefinita, AEM Forms memorizza i dati utente associati alla bozza e all’invio di un modulo nel nodo /content/forms/fp dell’istanza Publish. È possibile aggiungere il provider di archiviazione personalizzato. Per informazioni dettagliate, vedere [Archiviazione personalizzata per il componente Bozze e invii](/help/forms/using/adding-custom-storage-provider-forms.md).
