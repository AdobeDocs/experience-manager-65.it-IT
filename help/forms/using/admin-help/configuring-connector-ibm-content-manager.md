---
title: Configurazione del connettore per IBM Content Manager
seo-title: Configurazione del connettore per IBM Content Manager
description: Configurare il connettore per IBM Content Manager per abilitare la comunicazione tra AEM moduli e IBM Content Manager.
seo-description: Configurare il connettore per IBM Content Manager per abilitare la comunicazione tra AEM moduli e IBM Content Manager.
uuid: 3d55169d-93e3-4d4e-b18b-2a3394e1de3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3094b178-3b1a-46b3-8fbd-c20388afa3a7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Configurazione del connettore per IBM Content Manager{#configuring-connector-for-ibm-content-manager}

Il connettore per IBM Content Manager consente la comunicazione tra AEM moduli e IBM Content Manager. Per ulteriori informazioni, vedere &quot;Connettori per l&#39;ECM&quot; in [Guida di riferimento dei servizi](https://www.adobe.com/go/learn_aemforms_services_63).

## Configurare la connessione IBM Content Manager {#configure-the-ibm-content-manager-connection}

1. Nella console di amministrazione, fai clic su Servizi > Connettore per IBM Content Manager.
1. Nella casella Nome archivio dati, immettete il nome dell&#39;archivio dati di IBM Content Manager a cui desiderate connettervi. Se il database è locale, immettete il nome del database. Se il database è remoto, immettete il nome alias.
1. Nella casella Nome utente, immettete l&#39;ID utente di un utente che si connetterà all&#39;archivio dati di IBM Content Manager.
1. Nella casella Password, immettete la password dell’utente.
1. (Facoltativo) Nella casella Stringa connessione alias, immettere ulteriori argomenti di connessione. Nella maggior parte dei casi, questa casella deve essere vuota. Per ulteriori informazioni, consulta la documentazione IBM.
1. Fate clic su Salva.

## Convalida delle impostazioni del servizio {#validation-of-service-settings}

Se immettete un alias dataStore, un nome utente o una password non corretti, otterrete i seguenti risultati, a seconda che il connettore Content Repository per il servizio IBM Content Manager sia attualmente in esecuzione:

* Se il servizio viene arrestato, al momento del salvataggio delle informazioni di configurazione del servizio non viene visualizzato alcun errore. Tuttavia, al successivo avvio del servizio, verrà generata un&#39;eccezione e il servizio non verrà avviato.
* Se il servizio viene avviato, quando si salvano le informazioni di configurazione del servizio, il servizio tenta di convalidare immediatamente le informazioni delle credenziali. In questo caso, si verifica un errore e le informazioni di configurazione non vengono salvate.

