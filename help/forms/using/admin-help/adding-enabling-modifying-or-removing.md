---
title: Aggiunta, attivazione, modifica o rimozione di endpoint
seo-title: Aggiunta, attivazione, modifica o rimozione di endpoint
description: Scopri come aggiungere, abilitare, modificare e rimuovere gli endpoint.
seo-description: Scopri come aggiungere, abilitare, modificare e rimuovere gli endpoint.
uuid: c53f225b-3d55-42f6-8982-0cd7dde0c4f5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7d0d4f96-fc72-4e2b-a2cc-5741b0a30f74
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---


# Aggiunta, attivazione, modifica o rimozione di endpoint {#adding-enabling-modifying-or-removing-endpoints}

## Aggiunta di un endpoint a un servizio {#add-an-endpoint-to-a-service}

Gli endpoint possono essere aggiunti solo ai servizi. Un endpoint non può esistere da solo; deve essere associato a un servizio.

>[!NOTE]
>
>È consigliabile utilizzare nomi univoci quando si aggiungono endpoint.

1. Nella console di amministrazione, fai clic su Servizi > Applicazioni e servizi > Gestione dei servizi.
1. Nella pagina Gestione dei servizi, fate clic sul servizio da configurare.
1. Nell&#39;elenco della scheda Endpoint, selezionare il tipo di endpoint da aggiungere e fare clic su Aggiungi.
1. A seconda del tipo di endpoint, configura impostazioni endpoint aggiuntive.

   [Impostazioni endpoint cartella esaminata](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

   [Impostazioni endpoint e-mail](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

   [Configurazione degli endpoint di Task Manager](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

   [Impostazioni endpoint remoto](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. Fate clic su Aggiungi.

## Attivare o disattivare un endpoint {#enable-or-disable-an-endpoint}

Per impostazione predefinita, i nuovi endpoint vengono attivati automaticamente. Tuttavia, se hai disabilitato un endpoint, dovrai attivarlo per renderlo operativo.

In caso di problemi con i servizi, disattivate gli endpoint associati per risolvere meglio il problema. È inoltre possibile disattivare gli endpoint durante la manutenzione regolare del sistema o durante l&#39;aggiornamento di un servizio.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione endpoint.
1. Nella pagina Gestione endpoint, selezionare la casella di controllo per l&#39;endpoint da abilitare o disabilitare e fare clic su Attiva o Disattiva.

## Modificare un endpoint {#modify-an-endpoint}

>[!NOTE]
>
>Le modifiche apportate a una configurazione di endpoint tramite la console di amministrazione non vengono riportate nelle copie in fase di progettazione delle applicazioni. Se si ridistribuisce un&#39;applicazione, tutte le modifiche apportate agli endpoint utilizzando la console di amministrazione andranno perse.

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione endpoint.
1. Nella pagina Gestione endpoint fare clic sull&#39;endpoint da modificare.
1. Nella pagina Aggiorna endpoint, modificate il nome, la descrizione e le impostazioni dell&#39;endpoint.

   >[!NOTE]
   >
   >Non includere un carattere &lt; nel nome o nella descrizione perché troncherà il nome o la descrizione visualizzati in Workspace.

1. Per salvare le modifiche, fate clic su Aggiorna.

È inoltre possibile eseguire questa operazione dalla pagina Gestione dei servizi selezionando un servizio e facendo clic sulla scheda Endpoint.

## Rimuovere un endpoint {#remove-an-endpoint}

1. Nella console di amministrazione, fare clic su Servizi > Applicazioni e servizi > Gestione endpoint.
1. Nella pagina Gestione endpoint, selezionare la casella di controllo per l&#39;endpoint da rimuovere e fare clic su Rimuovi. L&#39;endpoint non viene più visualizzato.

