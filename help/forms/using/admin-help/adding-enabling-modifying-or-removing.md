---
title: Aggiunta, abilitazione, modifica o rimozione di endpoint
description: Scopri come aggiungere, abilitare, modificare e rimuovere endpoint.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b7461d5c-95d1-4da2-9d2a-f54c410a87f9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
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
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 100%
---
# Aggiunta, abilitazione, modifica o rimozione di endpoint {#adding-enabling-modifying-or-removing-endpoints}

>[!NOTE]
> 
> Assicurati che l’utente disponga dei privilegi di amministratore per accedere alla console dell’amministratore.

## Aggiungere un endpoint a un servizio {#add-an-endpoint-to-a-service}

Gli endpoint possono essere aggiunti solo ai servizi. Un endpoint non può esistere da solo, ma deve essere associato a un servizio.

>[!NOTE]
>
>Quando si aggiungono endpoint, è consigliabile utilizzare nomi univoci.

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione servizi.
1. Nella pagina Gestione servizio fai clic sul servizio da configurare.
1. Nell’elenco della scheda Endpoint, seleziona il tipo di endpoint da aggiungere e fai clic su Aggiungi.
1. A seconda del tipo di endpoint, configura impostazioni endpoint aggiuntive.

   [Impostazioni endpoint cartella controllata](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

   [Impostazioni endpoint e-mail](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

   [Configurazione endpoint di Gestione attività](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

   [Impostazioni endpoint di comunicazione remota](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. Fai clic su Aggiungi.

## Abilitare o disabilitare un endpoint {#enable-or-disable-an-endpoint}

Per impostazione predefinita, i nuovi endpoint vengono abilitati automaticamente. Tuttavia, se hai disabilitato un endpoint, devi attivarlo affinché sia operativo.

Se riscontri problemi con i servizi, disattiva gli endpoint associati per una migliore risoluzione del problema. È inoltre possibile disabilitare gli endpoint durante la normale manutenzione del sistema o durante l’aggiornamento di un servizio.

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione endpoint.
1. Nella pagina Gestione endpoint, seleziona la casella di controllo relativa all’endpoint da abilitare o disabilitare e fai clic su Abilita o Disabilita.

## Modificare un endpoint {#modify-an-endpoint}

>[!NOTE]
>
>Le modifiche apportate alla configurazione di un endpoint tramite la console di amministrazione non vengono riflesse nelle copie delle applicazioni in fase di progettazione. In caso di ridistribuzione di un’applicazione, tutte le modifiche apportate agli endpoint mediante la console di amministrazione andranno perse.

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione endpoint.
1. Nella pagina Gestione endpoint, fai clic sull’endpoint da modificare.
1. Nella pagina Aggiorna endpoint modifica il nome, la descrizione e le impostazioni dell’endpoint.

   >[!NOTE]
   >
   >Non includere il carattere &lt; nel nome o nella descrizione, poiché la visualizzazione di questi in Workspace risulterebbe troncata.

1. Per salvare le modifiche, fai clic su Aggiorna.

È inoltre possibile eseguire questa operazione dalla pagina Gestione servizi selezionando un servizio e facendo clic sulla scheda Endpoint.

## Rimuovere un endpoint {#remove-an-endpoint}

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione endpoint.
1. Nella pagina Gestione endpoint, seleziona la casella di controllo relativa all’endpoint da rimuovere e fai clic su Rimuovi. L’endpoint non viene più visualizzato.
