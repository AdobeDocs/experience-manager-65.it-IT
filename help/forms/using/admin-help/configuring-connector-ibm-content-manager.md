---
title: Configurazione del connettore per IBM Content Manager
seo-title: Configuring Connector for IBM Content Manager
description: Configura il connettore per IBM Content Manager per abilitare la comunicazione tra AEM moduli e IBM Content Manager.
seo-description: Configure the Connector for IBM Content Manager to enable communication between AEM forms and IBM Content Manager.
uuid: 3d55169d-93e3-4d4e-b18b-2a3394e1de3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3094b178-3b1a-46b3-8fbd-c20388afa3a7
exl-id: 50f0c963-8007-4e2a-aa73-d99b97d9a1aa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Configurazione del connettore per IBM Content Manager{#configuring-connector-for-ibm-content-manager}

Il connettore per IBM Content Manager consente la comunicazione tra AEM moduli e IBM Content Manager. Per ulteriori informazioni di base, consulta &quot;Connettori per ECM&quot; in [Riferimento servizi](https://www.adobe.com/go/learn_aemforms_services_63).

## Configurare la connessione IBM Content Manager {#configure-the-ibm-content-manager-connection}

1. Nella console di amministrazione, fai clic su Servizi > Connettore per IBM Content Manager.
1. Nella casella Nome archivio dati immettere il nome dell&#39;archivio dati di IBM Content Manager a cui si desidera connettersi. Se il database è locale, immettere il nome del database. Se il database è remoto, immettere il nome alias corrispondente.
1. Nella casella Nome utente, immetti l’ID utente di un utente che si connette all’archivio dati di IBM Content Manager.
1. Nella casella Password , immetti la password dell’utente.
1. (Facoltativo) Nella casella Stringa di connessione alias, immettere ulteriori argomenti di connessione. Nella maggior parte dei casi, questa casella deve essere vuota. Per ulteriori informazioni, consulta la documentazione di IBM .
1. Fai clic su Salva.

## Convalida delle impostazioni del servizio {#validation-of-service-settings}

Se immetti un alias, un nome utente o una password dell&#39;archivio dati non corretti, otterrai i seguenti risultati, a seconda che il connettore dell&#39;archivio contenuti per il servizio IBM Content Manager sia attualmente in esecuzione:

* Se il servizio viene arrestato, quando si salvano le informazioni di configurazione del servizio non viene visualizzato alcun errore. Tuttavia, al successivo avvio del servizio, verrà generata un’eccezione e il servizio non verrà avviato.
* Se il servizio viene avviato, quando si salvano le informazioni di configurazione del servizio, il servizio tenta di convalidare immediatamente le informazioni delle credenziali. In questo caso, si verifica un errore e le informazioni di configurazione non vengono salvate.
