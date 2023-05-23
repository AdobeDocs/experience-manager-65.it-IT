---
title: Configurazione del connettore per IBM Content Manager
seo-title: Configuring Connector for IBM Content Manager
description: Configura il connettore per IBM Content Manager per abilitare la comunicazione tra i moduli AEM e IBM Content Manager.
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

Il connettore per IBM Content Manager consente la comunicazione tra i moduli AEM e IBM Content Manager. Per ulteriori informazioni di base, vedere &quot;Connettori per ECM&quot; in [Riferimento servizi](https://www.adobe.com/go/learn_aemforms_services_63).

## Configurare la connessione ad IBM Content Manager {#configure-the-ibm-content-manager-connection}

1. Nella console di amministrazione, fai clic su Servizi > Connettore per IBM Content Manager.
1. Nella casella Nome archivio dati immettere il nome dell&#39;archivio dati di IBM Content Manager a cui si desidera connettersi. Se il database è locale, immettere il nome del database. Se il database è remoto, immettere il nome dell&#39;alias.
1. Nella casella Nome utente, inserisci l’ID utente di un utente che si connetterà all’archivio dati di IBM Content Manager.
1. Nella casella Password immettere la password dell&#39;utente.
1. (Facoltativo) Nella casella Stringa di connessione alias immettere argomenti di connessione aggiuntivi. Nella maggior parte dei casi, questa casella deve essere vuota. Per ulteriori informazioni, consulta la documentazione di IBM.
1. Fai clic su Salva.

## Convalida delle impostazioni del servizio {#validation-of-service-settings}

Se immetti un alias, un nome utente o una password di dataStore errati, a seconda che il connettore dell’archivio dei contenuti per il servizio IBM Content Manager sia attualmente in esecuzione o meno, si otterranno i seguenti risultati:

* Se il servizio viene arrestato, quando si salvano le informazioni di configurazione del servizio non viene visualizzato alcun errore. Tuttavia, al successivo avvio del servizio, verrà generata un&#39;eccezione e il servizio non verrà avviato.
* Se il servizio viene avviato, quando si salvano le informazioni di configurazione del servizio, il servizio tenta di convalidare immediatamente le informazioni sulle credenziali. In questo caso, si verifica un errore e le informazioni di configurazione non vengono salvate.
