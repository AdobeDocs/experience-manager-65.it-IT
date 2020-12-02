---
title: Configurazione degli endpoint remoti
seo-title: Configurazione degli endpoint remoti
description: Scopri come configurare gli endpoint remoti.
seo-description: Scopri come configurare gli endpoint remoti.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# Configurazione degli endpoint {#configuring-remoting-endpoints}

Un endpoint remoto consente a un&#39;applicazione creata con Flex di richiamare il servizio utilizzando (obsoleto per AEM moduli) AEM moduli Remoting. Per ogni servizio attivato viene automaticamente creato un endpoint remoto. Una destinazione Flex con lo stesso nome dell&#39;endpoint viene creata e i client Flex possono creare oggetti remoti che puntano a questa destinazione per richiamare le operazioni sul servizio appropriato.

## Impostazioni endpoint remoto {#remoting-endpoint-settings}

**Metodo di autenticazione client Flex:** determina il tipo di risposta che il server invia al client quando il servizio richiamato è abilitato per la protezione, l&#39;operazione richiamata non supporta chiamate anonime e il client trasmette credenziali nulle o non valide.
