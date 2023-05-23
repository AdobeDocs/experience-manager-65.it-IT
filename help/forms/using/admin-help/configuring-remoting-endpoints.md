---
title: Configurazione degli endpoint di comunicazione remota
seo-title: Configuring Remoting endpoints
description: Scopri come configurare gli endpoint remoti.
seo-description: Learn how to configure remoting endpoints.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Configurazione degli endpoint di comunicazione remota {#configuring-remoting-endpoints}

Un endpoint remoto consente a un’applicazione creata con Flex di richiamare il servizio utilizzando i moduli AEM Remoting (obsoleti per i moduli AEM). Per ogni servizio attivato viene creato automaticamente un endpoint di comunicazione remota. Viene creata una destinazione Flex con lo stesso nome dell&#39;endpoint e i client Flex possono creare oggetti remoti che puntano a questa destinazione per richiamare operazioni sul servizio pertinente.

## Impostazioni endpoint remoto {#remoting-endpoint-settings}

**Metodo di autenticazione client Flex:** Determina il tipo di risposta che il server invia al client quando il servizio richiamato è abilitato per la sicurezza, l&#39;operazione richiamata non supporta chiamate anonime e il client trasmette credenziali non valide o non valide.
