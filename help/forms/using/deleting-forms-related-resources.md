---
title: Eliminare moduli e risorse correlati
description: Come eliminare un modulo o una risorsa in AEM Forms e l’impatto sulle risorse di riferimento e di riferimento e sui moduli XFA.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
exl-id: b31f9f56-dd33-4478-ad34-01ac7d5a1b40
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 2%
---
# Eliminare moduli e risorse correlati {#deleting-forms-and-related-resources}

Puoi eliminare i moduli e le risorse per rimuovere tali risorse dall’archivio. L’operazione di eliminazione funziona su tutti i tipi di risorse e le cartelle.

Se elimini una risorsa dall’istanza Autore, viene eliminata anche dall’istanza Pubblica. Il server AEM Forms è costituito dalle istanze Author e Publish. L’istanza di authoring è per la creazione e la gestione delle risorse e delle risorse dei moduli. L’istanza Publish contiene le risorse dei moduli pubblicati e le risorse correlate disponibili per gli utenti finali.

## Come eliminare un modulo {#how-to-delete-a-form}

1. Accedere all&#39;interfaccia utente di AEM Forms accedendo a `https://[hostname]:'port'/aem/forms.html.`
1. Passare al modulo che si desidera eliminare e selezionarlo. Fai clic su Elimina ![aem6forms_delete2](assets/aem6forms_delete2.png) nella barra degli strumenti e conferma l’operazione di eliminazione.

   >[!NOTE]
   >
   >È possibile eliminare un solo modulo alla volta. Eliminare più moduli singolarmente o eliminare la cartella principale.

1. Prima di eliminare una risorsa, AEM Forms verifica la presenza di riferimenti e richiede una conferma esplicita. Fai clic su Forza eliminazione se desideri eliminare la risorsa indipendentemente dallo stato della relazione.

   >[!NOTE]
   >
   >L’eliminazione di una risorsa a cui fanno riferimento altre risorse può causare problemi funzionali.

   >[!NOTE]
   >
   >Se la risorsa selezionata è una cartella e contiene tale risorsa nella gerarchia, elimina le altre risorse singolarmente o l’intera cartella.

## Impatto dell’eliminazione di un modulo XFA di riferimento {#impact-of-deleting-a-referenced-xfa-form}

In AEM Forms, è possibile fare riferimento a un modello di modulo XFA da un modulo adattivo o da un altro modello di modulo XFA. Inoltre, un modello può fare riferimento a una risorsa o a un altro modello XFA.

Non è consigliabile eliminare un modulo XFA a cui fa riferimento un modulo adattivo, in quanto potrebbe danneggiare il modulo adattivo. Quando un modulo adattivo fa riferimento a un modulo XFA, i relativi campi sono associati. Dopo l’eliminazione di XFA, il modulo adattivo non è in grado di sincronizzare i propri campi con i campi XFA e visualizza un messaggio di errore per tali campi. Per ulteriori informazioni sull&#39;impatto dell&#39;eliminazione XFA a cui si fa riferimento e sulle AF dirty, consulta [Aggiornamento dei moduli XFA di riferimento](/help/forms/using/get-xdp-pdf-documents-aem.md#p-updating-referenced-xfa-forms-p).

Per eliminare un modulo XFA di questo tipo, aggiorna il modulo adattivo e rimuovi le associazioni con i campi XFA.
