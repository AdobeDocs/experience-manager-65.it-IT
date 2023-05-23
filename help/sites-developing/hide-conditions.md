---
title: Utilizzo di Nascondi condizioni
seo-title: Using Hide Conditions
description: È possibile utilizzare le condizioni Nascondi per determinare se una risorsa componente è sottoposta o meno a rendering.
seo-description: Hide conditions can be used to determine if a component resource is rendered or not.
uuid: 93b4f450-1d94-4222-9199-27b5f295f8e6
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 104d1c64-b9b3-40f5-8f9b-fe92d9daaa1f
exl-id: 65f5d5e1-ac11-4a3c-8a51-ce06a741c264
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 2%

---

# Utilizzo di Nascondi condizioni {#using-hide-conditions}

È possibile utilizzare le condizioni Nascondi per determinare se una risorsa componente è sottoposta o meno a rendering. Un esempio potrebbe essere quando un autore di modelli configura il Componente core [componente elenco](https://helpx.adobe.com/experience-manager/core-components/using/list.html) nel [editor modelli](/help/sites-authoring/templates.md) e decide di disabilitare le opzioni per creare l’elenco in base alle pagine figlie. La disattivazione di questa opzione nella finestra di dialogo per progettazione imposta una proprietà in modo che, quando viene eseguito il rendering del componente Elenco, venga valutata la condizione Nascondi e non venga visualizzata l’opzione per visualizzare le pagine figlie.

## Panoramica {#overview}

Le finestre di dialogo possono diventare molto complesse con numerose opzioni per l’utente, che può utilizzare solo una frazione delle opzioni a sua disposizione. Questo può portare a esperienze di interfaccia utente schiaccianti per gli utenti.

Utilizzando le condizioni di nascondi, gli amministratori, gli sviluppatori e gli utenti con privilegi avanzati possono nascondere le risorse in base a un set di regole. Questa funzione consente loro di decidere quali risorse visualizzare quando un autore modifica il contenuto.

>[!NOTE]
>
>Se si nasconde una risorsa basata su un’espressione, le autorizzazioni ACL non vengono sostituite. Il contenuto rimane modificabile ma non viene visualizzato.

## Dettagli sull’implementazione e sull’utilizzo {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` è responsabile del filtraggio delle risorse in base all’esistenza e al valore del `granite:hide` , situata nel campo da filtrare. L&#39;implementazione di `/libs/cq/gui/components/authoring/dialog/dialog.jsp` include un&#39;istanza di `FilteringResourceWrapper.`

L’implementazione utilizza il Granite [API Risolutore ELR](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) e aggiunge `cqDesign` tramite ExpressionCustomizer.

Di seguito sono riportati alcuni esempi di condizioni di nascondi in un nodo di progettazione che si trova in `etc/design` o come informativa sui contenuti.

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

Quando definisci l’espressione Nascondi, tieni presente quanto segue:

* Per essere valido, è necessario esprimere l’ambito in cui si trova la proprietà (ad esempio `cqDesign.myProperty`).
* I valori sono di sola lettura.
* Le funzioni (se richieste) devono essere limitate a un determinato set fornito dal servizio.

## Esempio {#example}

Esempi di malattie delle pelli si possono trovare in tutta l’AEM e nella [Componenti core](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=it) in particolare. Ad esempio, considera [componente core elenco](https://helpx.adobe.com/experience-manager/core-components/using/list.html).

[Utilizzo dell’editor modelli](/help/sites-authoring/templates.md), l’autore del modello può definire nella finestra di dialogo per progettazione le opzioni del componente Elenco disponibili per l’autore della pagina. Opzioni quali se consentire all’elenco di essere statico, un elenco di pagine figlie, un elenco di pagine con tag e così via. può essere abilitato o disabilitato.

Se un autore di modelli sceglie di disabilitare l’opzione pagine figlie, viene impostata una proprietà di progettazione e viene valutata una condizione di nascondi in base a essa, impedendo all’autore della pagina di eseguire il rendering dell’opzione.

1. Per impostazione predefinita, l’autore della pagina può utilizzare il componente core Elenco per creare un elenco utilizzando pagine figlie scegliendo l’opzione **Pagine figlie**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Nella finestra di dialogo per progettazione del componente core Elenco, l’autore del modello può scegliere l’opzione **Disabilita elementi figlio** per impedire che l’opzione per generare un elenco basato su pagine figlie venga mostrata all’autore della pagina.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Un nodo di criterio viene creato in `/conf/we-retail/settings/wcm/policies/weretail/components/content/list` con una proprietà `disableChildren` imposta su `true`.
1. La condizione Nascondi è definita come il valore di un `granite:hide` proprietà nel nodo della proprietà della finestra di dialogo `/conf/we-retail/settings/wcm/policies/weretail/components/content/list`

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. Il valore di `disableChildren` viene estratto dalla configurazione di progettazione e dall’espressione `${cqDesign.disableChildren}` valuta per `false`, il che significa che l’opzione non verrà renderizzata come parte del componente.

   È possibile visualizzare l’espressione hide come valore della proprietà `granite:hide` proprietà [in GitHub qui](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/blob/master/content/src/content/jcr_root/apps/core/wcm/components/list/v1/list/_cq_dialog/.content.xml#L40).

1. Opzione **Pagine figlie** non viene più eseguito per l’autore della pagina quando si utilizza il componente Elenco.

   ![chlimage_1-221](assets/chlimage_1-221.png)
