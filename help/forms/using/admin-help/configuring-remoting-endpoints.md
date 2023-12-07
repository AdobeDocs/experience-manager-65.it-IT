---
title: Configurazione degli endpoint di comunicazione remota
description: Scopri come configurare gli endpoint remoti. Questo documento spiega come abilitare l’applicazione creata con Flex per richiamare il servizio utilizzando i moduli AEM per la comunicazione remota.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---

# Configurazione degli endpoint di comunicazione remota {#configuring-remoting-endpoints}

Un endpoint remoto consente a un’applicazione creata con Flex di richiamare il servizio utilizzando i moduli AEM Remoting (obsoleti per i moduli AEM). Per ogni servizio attivato viene creato automaticamente un endpoint di comunicazione remota. Viene creata una destinazione Flex con lo stesso nome dell&#39;endpoint e i client Flex possono creare oggetti remoti che puntano a questa destinazione per richiamare operazioni sul servizio pertinente.

## Impostazioni endpoint remoto {#remoting-endpoint-settings}

**Metodo di autenticazione client Flex:** Determina il tipo di risposta che il server invia al client quando il servizio richiamato è abilitato per la sicurezza, l&#39;operazione richiamata non supporta chiamate anonime e il client trasmette credenziali non valide o non valide.
