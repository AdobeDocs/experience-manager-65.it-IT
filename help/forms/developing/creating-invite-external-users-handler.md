---
title: Creazione di un gestore di utenti esterni per l’invito
description: Creazione di un gestore di utenti esterni per l’invito
translation-type: tm+mt
source-git-commit: 92e5cc0b1934dad641357a22894e70a3660b774a
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 0%

---


# Creazione di un gestore di utenti esterni per l’invito {#create-invite-external-users-handler}

Potete creare un gestore Invita utenti esterni per il servizio Rights Management. Un gestore Invita utenti esterni consente al servizio Rights Management di invitare utenti esterni a diventare utenti del Rights Management. Quando un utente diventa un utente di Rights Management, può eseguire attività quali l&#39;apertura di un documento PDF protetto tramite criterio. Dopo che il gestore Invita utenti esterni è stato distribuito in  AEM Forms, potete usare la console di amministrazione per interagire con esso.

>[!NOTE]
>
>Un gestore Invita utenti esterni è un componente AEM Forms . Prima di creare un gestore Invita utenti esterni, è consigliabile acquisire familiarità con la creazione di componenti.

**Riepilogo dei passaggi**

Per sviluppare un gestore Invita utenti esterni, è necessario eseguire le operazioni seguenti:

1. Configurare l&#39;ambiente di sviluppo.
1. Definite l’implementazione del gestore Invita utenti esterni.
1. Definire il file XML del componente.
1. Implementare il gestore Invita utenti esterni.
1. Verificate il gestore Invita utenti esterni.

## Impostazione dell&#39;ambiente di sviluppo {#setting-up-development-environment}

Per configurare l&#39;ambiente di sviluppo, è necessario creare un nuovo progetto Java, ad esempio un progetto Eclipse. La versione di Eclipse supportata è `3.2.1` o successiva.

L&#39;SPI Rights Management richiede che il `edc-server-spi.jar` file sia impostato nel percorso di classe del progetto. Se non si fa riferimento a questo file JAR, non è possibile utilizzare l&#39;SPI Rights Management nel progetto Java. Questo file JAR viene installato con l’SDK AEM Forms  nella `[install directory]\Adobe\Adobe_Experience_Manager_forms\sdk\spi` cartella.

Oltre ad aggiungere il `edc-server-spi.jar` file al percorso di classe del progetto, dovete aggiungere anche i file JAR necessari per utilizzare l&#39;API del servizio Rights Management. Questi file sono necessari per utilizzare l&#39;API del servizio di Rights Management all&#39;interno del gestore Invita utenti esterni.

## Definizione dell’implementazione del gestore di utenti esterni per l’invito {#define-invite-external-users-handler}

Per sviluppare un gestore di utenti esterni di inviti, dovete creare una classe Java che implementa l&#39; `com.adobe.edc.server.spi.ersp.InvitedUserProvider` interfaccia. Questa classe contiene un metodo denominato `invitedUser`, che il servizio di Rights Management richiama quando gli indirizzi e-mail vengono inviati tramite la pagina **Aggiungi utenti** invitati accessibile tramite la console di amministrazione.

Il `invitedUser` metodo accetta un’ `java.util.List` istanza, che contiene indirizzi e-mail con tipo stringa inviati dalla pagina **Aggiungi utenti** invitati. Il `invitedUser` metodo restituisce un array di `InvitedUserProviderResult` oggetti, che in genere è una mappatura di indirizzi e-mail agli oggetti Utente (non restituisce null).

>[!NOTE]
>
>Oltre a mostrare come creare un gestore di utenti esterni per gli inviti, in questa sezione viene utilizzata anche l&#39;API AEM Forms .

L&#39;implementazione del gestore di utenti esterni di inviti contiene un metodo definito dall&#39;utente denominato `createLocalPrincipalAccount`. Questo metodo accetta un valore di stringa che specifica un indirizzo e-mail come valore di parametro. Il `createLocalPrincipalAccount` metodo presuppone la preesistenza di un dominio locale denominato `EDC_EXTERNAL_REGISTERED`. Puoi configurare questo nome di dominio come qualsiasi cosa desideri; tuttavia, per un&#39;applicazione di produzione, potrebbe essere necessario effettuare l&#39;integrazione con un dominio aziendale.

Il `createUsers` metodo esegue un&#39;iterazione su ogni indirizzo e-mail e crea un oggetto Utente corrispondente (un utente locale nel `EDC_EXTERNAL_REGISTERED` dominio). Infine, viene chiamato il `doEmails` metodo. Questo metodo viene lasciato intenzionalmente come stub nel campione. In un&#39;implementazione di produzione, conterrebbe la logica dell&#39;applicazione per inviare messaggi e-mail di invito agli utenti appena creati. Viene lasciata nell&#39;esempio per dimostrare il flusso logico dell&#39;applicazione di un&#39;applicazione reale.

### Definizione dell’implementazione del gestore di utenti esterni per l’invito {#user-handler-implementation}

La seguente implementazione del gestore di utenti esterni per gli inviti accetta gli indirizzi e-mail inviati dalla pagina Aggiungi utenti invitati accessibile tramite la console di amministrazione.

```as3
package com.adobe.livecycle.samples.inviteexternalusers.provider; 
 
import com.adobe.edc.server.spi.ersp.*; 
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
import com.adobe.idp.um.api.*; 
import com.adobe.idp.um.api.infomodel.*; 
import com.adobe.idp.um.api.impl.UMBaseLibrary; 
import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient; 
 
import java.util.ArrayList; 
import java.util.Iterator; 
import java.util.List; 
 
public class InviteExternalUsersSample implements InvitedUserProvider 
{ 
       private ServiceClientFactory _factory = null; 
 
       private User createLocalPrincipalAccount(String email_address) throws Exception 
       { 
    String ret = null; 
 
    //  Assume the local domain already exists! 
    String domain = "EDC_EXTERNAL_REGISTERED"; 
         
    List aliases = new ArrayList(); 
    aliases.add( email_address ); 
         
    User local_user = UMBaseLibrary.createUser( email_address, domain, email_address ); 
    local_user.setCommonName( email_address ); 
    local_user.setEmail( email_address ); 
    local_user.setEmailAliases( aliases ); 
         
    //  You may wish to disable the local user until, for example, his registration is processed by a confirmation link 
    //local_user.setDisabled( true ); 
 
    DirectoryManager directory_manager = new DirectoryManagerServiceClient( _factory ); 
    String ret_oid = directory_manager.createLocalUser( local_user, null ); 
     
    if( ret_oid == null ) 
    { 
        throw new Exception( "FAILED TO CREATE PRINCIPAL FOR EMAIL ADDRESS: " + email_address ); 
    } 
 
    return local_user; 
       } 
 
       protected User[] createUsers( List emails ) throws Exception 
       { 
    ArrayList ret_users = new ArrayList(); 
 
    _factory = ServiceClientFactory.createInstance(); 
 
    Iterator iter = emails.iterator(); 
 
    while( iter.hasNext() ) 
    { 
        String current_email = (String)iter.next(); 
 
        ret_users.add( createLocalPrincipalAccount( current_email ) ); 
    } 
 
    return (User[])ret_users.toArray( new User[0] ); 
       } 
 
       protected void doInvitations(List emails) 
       { 
    //  Here you may choose to send the users who were created an invitation email 
    //  This step is completely optional, depending on your requirements.   
       } 
 
       public InvitedUserProviderResult[] invitedUser(List emails) 
       { 
    //  This sample demonstrates the workflow for inviting a user via email 
 
    try 
    { 
 
        User[] principals = createUsers(emails); 
 
        InvitedUserProviderResult[] result = new InvitedUserProviderResult[principals.length]; 
        for( int i = 0; i < principals.length; i++ ) 
        { 
        result[i] = new InvitedUserProviderResult(); 
 
        result[i].setEmail( (String)emails.get( i ) ); 
        result[i].setUser( principals[i] ); 
        } 
 
        doInvitations(emails); 
 
        System.out.println( "SUCCESSFULLY INVITED " + result.length + " USERS" ); 
 
        return result; 
 
    } 
    catch( Exception e ) 
    { 
        System.out.println( "FAILED TO INVITE USERS FOR INVITE USERS SAMPLE" ); 
        e.printStackTrace(); 
 
        return new InvitedUserProviderResult[0]; 
    } 
       } 
}
 
```

>[!NOTE]
>
>Questa classe Java viene salvata come file JAVA denominato InviteExternalUsersSample.java.

## Definizione del file XML del componente per il gestore di autorizzazioni {#define-component-xml-authorization-handler}

È necessario definire un file XML di componente per distribuire il componente gestore di utenti esterni dell’invito. Esiste un file XML di componente per ciascun componente e fornisce i metadati relativi al componente.

Il seguente `component.xml` file viene utilizzato per il gestore di utenti esterni dell&#39;invito. Il nome del servizio è `InviteExternalUsersSample` e l&#39;operazione esposta dal servizio è denominata `invitedUser`. Il parametro input è un&#39; `java.util.List` istanza e il valore di output è un array di `com.adobe.edc.server.spi.esrp.InvitedUserProviderResult` istanze.

### Definizione del file XML del componente per il gestore di utenti esterni dell’invito {#component-xml-invite-external-users-handler}

```as3
<component xmlns="http://adobe.com/idp/dsc/component/document"> 
<component-id>com.adobe.livecycle.samples.inviteexternalusers</component-id> 
<version>1.0</version> 
<bootstrap-class>com.adobe.livecycle.samples.inviteexternalusers.provider.BootstrapImpl</bootstrap-class> 
<descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class> 
<services> 
<service name="InviteExternalUsersSample"> 
<specifications> 
<specification spec-id="com.adobe.edc.server.spi.ersp.InvitedUserProvider"/> 
</specifications> 
<specification-version>1.0</specification-version> 
<implementation-class>com.adobe.livecycle.samples.inviteexternalusers.provider.InviteExternalUsersSample</implementation-class> 
<auto-deploy category-id="Samples" service-id="InviteExternalUsersSample" major-version="1" minor-version="0"/> 
<operations> 
<operation name="invitedUser"> 
<input-parameter name="input" type="java.util.List" required="true"/> 
<output-parameter name="result" type="com.adobe.edc.server.spi.esrp.InvitedUserProviderResult[]"/> 
</operation> 
</operations> 
</service> 
</services> 
</component> 
```

## Creazione del pacchetto del gestore di utenti esterni per l&#39;invito {#packaging-invite-external-users-handler}

Per distribuire il gestore di utenti esterni dell&#39;invito a  AEM Forms, dovete creare un pacchetto del progetto Java in un file JAR. È necessario assicurarsi che i file JAR esterni da cui dipende la logica di business del gestore di utenti esterni dell&#39;invito, come i file `edc-server-spi.jar` e `adobe-rightsmanagement-client.jar` , siano inclusi anche nel file JAR. Inoltre, il file XML del componente deve essere presente. Il `component.xml` file e i file JAR esterni devono trovarsi nella directory principale del file JAR.

>[!NOTE]
>
>Nell&#39;illustrazione seguente, viene visualizzata una `BootstrapImpl` classe. In questa sezione non viene illustrato come creare una `BootstrapImpl` classe.

L&#39;illustrazione seguente mostra il contenuto del progetto Java incluso nel pacchetto del file JAR del gestore di utenti esterni dell&#39;invito.

![Invitare gli utenti](assets/ci_ci_InviteUsers.png)

A. File JAR esterni richiesti dal componente B. File JAVA

Dovete creare un pacchetto con il gestore di utenti esterni dell&#39;invito in un file JAR. Nel diagramma precedente, notate che sono elencati i file .JAVA. Una volta creato il pacchetto in un file JAR, è necessario specificare anche i file .CLASS corrispondenti. Senza i file .CLASS, il gestore di autorizzazioni non funziona.

>[!NOTE]
>
>Dopo aver creato un pacchetto del gestore di autorizzazioni esterno in un file JAR, potete distribuire il componente  AEM Forms. È possibile distribuire un solo gestore di utenti esterni invitati alla volta.

>[!NOTE]
>
>È inoltre possibile distribuire un componente a livello di programmazione.

## Verifica del gestore di utenti esterni per l’invito {#testing-invite-external-users-handler}

Per testare il gestore di utenti esterni dell’invito, potete aggiungere utenti esterni da invitare utilizzando la console di amministrazione.

Per aggiungere utenti esterni da invitare tramite la console di amministrazione:

1. Distribuire il file JAR del gestore di utenti esterni dell&#39;invito utilizzando Workbench.
1. Riavviate il server applicazione.
1. Accedete alla console di amministrazione.
1. Fate clic su **[!UICONTROL Servizi]** > **[!UICONTROL Rights Management]** > **[!UICONTROL Configurazione]** > Registrazione **** utente invitata.
1. Attivate la registrazione degli utenti invitati selezionando la casella **[!UICONTROL Abilita registrazione]** utente invitato. In **[!UICONTROL Usa sistema]** di registrazione predefinito, fate clic su **[!UICONTROL No]**. Salvate le impostazioni.
1. Dalla home page della console di amministrazione, fate clic su **[!UICONTROL Impostazioni]** > Gestione **** utente > Gestione **** dominio.
1. Fare clic su **[!UICONTROL Nuovo dominio]** locale. Nella pagina seguente, crea un dominio con il nome e il valore dell’identificatore di `EDC_EXTERNAL_REGISTERED`. Salvare le modifiche.
1. Dalla home page della console di amministrazione, fate clic su **[!UICONTROL Servizi]** > **[!UICONTROL Rights Management]** > Utenti **[!UICONTROL invitati e locali]**. Viene visualizzata la pagina **[!UICONTROL Aggiungi utente]** invitato.
1. Inserite gli indirizzi e-mail (poiché il gestore di utenti esterni per l’invito corrente non invia effettivamente messaggi e-mail, l’indirizzo e-mail non deve essere valido). Fai clic su **[!UICONTROL OK]**. Gli utenti vengono invitati nel sistema.
1. Dalla home page della console di amministrazione, fate clic su **[!UICONTROL Impostazioni]** > Gestione **** utente > **[!UICONTROL Utenti e gruppi]**.
1. Nel campo **[!UICONTROL Trova]** , inserite l’indirizzo e-mail specificato. Fate clic su **[!UICONTROL Trova]**. L&#39;utente invitato viene visualizzato come utente nel `EDC_EXTERNAL_REGISTERED` dominio locale.

>[!NOTE]
>
>Il gestore di utenti esterni di inviti non riesce se il componente viene arrestato o disinstallato.
