---
title: Configurazione del connettore per IBM&reg; Content Manager
description: Configura il connettore per IBM&reg; Content Manager per abilitare la comunicazione tra i moduli AEM e IBM&reg; Content Manager.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 50f0c963-8007-4e2a-aa73-d99b97d9a1aa
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---

# Configurazione del connettore per IBM® Content Manager{#configuring-connector-for-ibm-content-manager}

Il connettore per IBM® Content Manager consente la comunicazione tra i moduli AEM e IBM® Content Manager. Per ulteriori informazioni di base, vedere &quot;Connettori per ECM&quot; in [Riferimento servizi](https://www.adobe.com/go/learn_aemforms_services_63).

## Configurare la connessione IBM® Content Manager {#configure-the-ibm-content-manager-connection}

1. Nella console di amministrazione, fai clic su Servizi > Connettore per IBM® Content Manager.
1. Nella casella Nome archivio dati immettere il nome dell&#39;archivio dati di IBM® Content Manager a cui si desidera connettersi. Se il database è locale, immettere il nome del database. Se il database è remoto, immettere il nome dell&#39;alias.
1. Nella casella Nome utente, inserisci l’ID utente di un utente che si connette all’archivio dati di IBM® Content Manager.
1. Nella casella Password immettere la password dell&#39;utente.
1. (Facoltativo) Nella casella Stringa di connessione alias immettere argomenti di connessione aggiuntivi. Di solito, questa casella dovrebbe essere vuota. Per ulteriori informazioni, consulta la documentazione di IBM®.
1. Fai clic su Salva.

## Convalida delle impostazioni del servizio {#validation-of-service-settings}

Se immetti un alias dataStore, un nome utente o una password non corretti, si ottengono i seguenti risultati, a seconda che il connettore dell’archivio dei contenuti per il servizio IBM® Content Manager sia in esecuzione:

* Se il servizio viene arrestato, quando si salvano le informazioni di configurazione del servizio non viene visualizzato alcun errore. Tuttavia, al successivo avvio del servizio, viene generata un&#39;eccezione e il servizio non viene avviato.
* Se il servizio viene avviato, quando si salvano le informazioni di configurazione del servizio, il servizio tenta di convalidare immediatamente le informazioni sulle credenziali. In questo caso, si verifica un errore e le informazioni di configurazione non vengono salvate.
