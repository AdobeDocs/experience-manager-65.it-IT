---
title: Mappatura personalizzata dei gruppi di utenti in AEM 6.5
seo-title: Mappatura personalizzata dei gruppi di utenti in AEM 6.5
description: Scopri come funziona la mappatura personalizzata per i gruppi di utenti in AEM.
seo-description: Scopri come funziona la mappatura personalizzata per i gruppi di utenti in AEM.
uuid: 7520351a-ab71-4661-b214-a0ef012c0c93
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 13085dd3-d283-4354-874b-cd837a9db9f9
docset: aem65
translation-type: tm+mt
source-git-commit: c2937a1989c6cfe33cc3f56f89c307cb5fb8d272
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 1%

---


# Mappatura personalizzata dei gruppi di utenti in AEM 6.5 {#custom-user-group-mapping-in-aem}

## Confronto del contenuto JCR relativo al CUG {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>Versioni AEM precedenti</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Commenti</strong></td>
  </tr>
  <tr>
   <td><p>Proprietà: cq:cugEnabled</p> <p>Dichiarazione del tipo di nodo: N/D, proprietà residua</p> </td>
   <td><p>Autorizzazione:</p> <p>Nodo: rep:cugPolicy di tipo nodo rep:CugPolicy</p> <p>Dichiarazione del tipo di nodo: rep:CugMixin</p> <p> </p> <p> </p> <p> </p> Autenticazione:</p> <p>Tipo di mixin: granite:AuthenticationRequired</p> </td>
   <td><p>Per limitare l'accesso in lettura, al nodo di destinazione viene applicato un criterio CUG dedicato.</p> <p>NOTA: I criteri possono essere applicati solo ai percorsi supportati configurati.</p> <p>i nodi con nome rep:cugPolicy e tipo rep:CugPolicy sono protetti e non possono essere scritti utilizzando chiamate API JCR regolari; utilizzate invece la gestione del controllo di accesso JCR.</p> <p>Consulta <a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">questa pagina</a> per ulteriori informazioni.</p> <p>Per applicare i requisiti di autenticazione su un nodo è sufficiente aggiungere il tipo di mixin granite:AuthenticationRequired.</p> <p>NOTA: Rispettato solo sotto i percorsi supportati configurati.</p> </td>
  </tr>
  <tr>
   <td><p>Proprietà: cq:cugPrincipals</p> <p>Dichiarazione del tipo di nodo: NA, proprietà residua</p> </td>
   <td><p>Proprietà: rep:principalNames</p> <p>Dichiarazione del tipo di nodo: rep:CugPolicy</p> </td>
   <td><p>La proprietà contenente i nomi delle entità autorizzate a leggere il contenuto al di sotto del CUG limitato è protetta e non può essere scritta utilizzando chiamate API JCR regolari; utilizzate invece la gestione del controllo di accesso JCR.</p> <p>Per <a href="https://svn.apache.org/repos/asf/jackrabbit/trunk/jackrabbitapi/src/main/java/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.java">ulteriori dettagli sull’implementazione, consultate questa pagina</a> .</p> </td>
  </tr>
  <tr>
   <td><p>Proprietà: cq:cugLoginPage</p> <p>Dichiarazione del tipo di nodo: NA, proprietà residua</p> </td>
   <td><p>Proprietà: granite:loginPath (facoltativo)</p> <p>Dichiarazione del tipo di nodo: granite:AuthenticationRequired</p> </td>
   <td><p>Un nodo JCR con il tipo di mixin granite:AuthenticationRequired definito, può eventualmente definire un percorso di login alternativo.</p> <p>NOTA: Rispettato solo sotto i percorsi supportati configurati.</p> </td>
  </tr>
  <tr>
   <td><p>Proprietà: cq:cugRealm</p> <p>Dichiarazione del tipo di nodo: NA, proprietà residua</p> </td>
   <td>NA</td>
   <td>Non più supportato con la nuova implementazione.</td>
  </tr>
 </tbody>
</table>

## Confronto dei servizi OSGi {#comparison-of-osgi-services}

**Versioni AEM precedenti**

Etichetta: Supporto per  gruppo di utenti chiuso Granite del Adobe (CUG)

Nome: com.day.cq.auth.impl.CugSupportImpl

**AEM 6.5**

* Etichetta: Configurazione CUG Apache Jackrabbit Oak

   Nome: org.apache.jackrabbit.oak.spi.security.permissions.cug.impl.CugConfiguration

   ConfigurationPolicy = REQUIRED

* Etichetta: Apache Jackrabbit Oak CUG Escludi elenco

   Nome: org.apache.jackrabbit.oak.spi.security.permissions.cug.impl.CugExcludeImpl

   ConfigurationPolicy = REQUIRED

* Nome: com.adobe.granite.auth.requirements.impl.RequirementService
* Etichetta:  Adobe requisito di autenticazione Granite e gestore del percorso di accesso

   Nome: com.adobe.granite.auth.requirements.impl.DefaultRequirementHandler

   ConfigurationPolicy = REQUIRED

**Commenti**

* Configurazione dell’autorizzazione CUG e attivazione/disattivazione della valutazione.
Servizio per configurare l&#39;elenco di esclusione delle entità che non dovrebbero essere interessate dall&#39;autorizzazione CUG.

   >[!NOTE]
   > 
   >Se `CugExcludeImpl` non è configurata, `CugConfiguration` tornerà all&#39;impostazione predefinita.

   È possibile collegare un&#39;implementazione personalizzata di CugExclude in caso di esigenze specifiche.

* Componente OSGi che implementa LoginPathProvider che espone un percorso di login corrispondente a LoginSelectorHandler. Ha un riferimento obbligatorio a un RequirementHandler utilizzato per registrare l&#39;osservatore che ascolta i requisiti di autenticazione modificati memorizzati nel contenuto tramite il tipo di mixin granite:AuthenticationRequired.
* Componente OSGi che implementa RequirementHandler che notifica a SlingAuthenticator le modifiche apportate ai requisiti di autenticazione.

   Poiché il criterio di configurazione per questo componente è REQUIRE, sarà attivato solo se è specificato un set di percorsi supportati.

   Se si abilita il servizio, verrà avviato il servizio RequirementService.

<!-- nested tables not supported - text above is the table>
<table>
 <tbody>
  <tr>
   <td><strong>Older AEM Versions</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Comments</strong></td>
  </tr>
  <tr>
   <td><p>Label: Adobe Granite Closed User Group (CUG) Support</p> <p>Name: com.day.cq.auth.impl.CugSupportImpl</p> </td>
   <td><p>Label: Apache Jackrabbit Oak CUG Configuration</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
    <td><p>Label: Apache Jackrabbit Oak CUG Exclude List</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl</p> <p>ConfigurationPolicy = REQUIRED</p> <p> </p> <p> </p> <p> </p> <p> </p> </td>
      </tr>
      <tr>
       <td>Name: com.adobe.granite.auth.requirement.impl.RequirementService</td>
      </tr>
      <tr>
       <td><p>Label: Adobe Granite Authentication Requirement and Login Path Handler</p> <p>Name: com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
      </tr>
     </tbody>
    </table> </td>
   <td>
     <tbody>
      <tr>
       <td>Configuration of the CUG authorization and enable/disable the evaluation.</td>
      </tr>
      <tr>
       <td><p>Service to configure exclusion list of principals which should not be affected by the CUG authorization.</p> <p>NOTE: If the CugExcludeImpl is not configured, the CugConfiguration will fall back to the default.</p> <p>It is possible to plug a custom CugExclude implementation in case of special needs.</p> </td>
      </tr>
      <tr>
       <td>OSGi component implementing LoginPathProvider that exposes a matching login path to the LoginSelectorHandler. It has a mandatory reference to a RequirementHandler which is used to register the observer that listens to changed auth requirements stored in the content by the means of the granite:AuthenticationRequired mixin type. </td>
      </tr>
      <tr>
       <td><p>OSGi component implementing RequirementHandler that notifies the SlingAuthenticator about changes to authrequirements.</p> <p>As configuration policy for this component is REQUIRE it will only be activated if a set of supported paths is specified.</p> <p>Enabling the service will launch the RequirementService.</p> </td>
      </tr>
     </tbody>
     </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

