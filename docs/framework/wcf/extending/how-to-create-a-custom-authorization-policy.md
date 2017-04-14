---
title: "Procedura: creare un criterio di autorizzazione personalizzato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 05b0549b-882d-4660-b6f0-5678543e5475
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Procedura: creare un criterio di autorizzazione personalizzato
L'infrastruttura del modello di identità di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] supporta un modello di autorizzazione basato sulle attestazioni.Le attestazioni vengono estratte dai token, elaborate facoltativamente dal criterio di autorizzazione personalizzato e poi collocate nella classe <xref:System.IdentityModel.Policy.AuthorizationContext> che può quindi essere esaminata per prendere decisioni in merito alle autorizzazioni.È possibile utilizzare un criterio personalizzato per trasformare le attestazioni ottenute dai token in ingresso in attestazioni previste dall'applicazione.In questo modo, il livello dell'applicazione può essere isolato dai dettagli relativi alle differenti attestazioni fornite dai diversi tipi di token supportati da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].In questo argomento viene illustrato come implementare un criterio di autorizzazione personalizzato e come aggiungerlo alla raccolta di criteri utilizzati da un servizio.  
  
### Per implementare un criterio di autorizzazione personalizzato  
  
1.  Definire una nuova classe che deriva dall'interfaccia <xref:System.IdentityModel.Policy.IAuthorizationPolicy>.  
  
2.  Implementare la proprietà di sola lettura <xref:System.IdentityModel.Policy.IAuthorizationComponent.Id%2A> generando una stringa univoca nel costruttore per la classe e restituendo tale stringa ogni volta che viene eseguito l'accesso alla proprietà.  
  
3.  Implementare la proprietà di sola lettura <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Issuer%2A> restituendo una classe <xref:System.IdentityModel.Claims.ClaimSet> che rappresenta l'emittente del criterio.Può trattarsi di una classe `ClaimSet` che rappresenta l'applicazione o di una classe `ClaimSet` incorporata \(ad esempio, la classe `ClaimSet` restituita dalla proprietà statica <xref:System.IdentityModel.Claims.ClaimSet.System%2A>.  
  
4.  Implementare il metodo <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> come descritto nella procedura seguente.  
  
### Per implementare il metodo Evaluate  
  
1.  A questo metodo vengono passati due parametri: un'istanza della classe <xref:System.IdentityModel.Policy.EvaluationContext> e un riferimento all'oggetto.  
  
2.  Se il criterio di autorizzazione personalizzato aggiunge istanze <xref:System.IdentityModel.Claims.ClaimSet> indipendentemente dal contenuto corrente di <xref:System.IdentityModel.Policy.EvaluationContext>, aggiungere ogni `ClaimSet` chiamando il metodo <xref:System.IdentityModel.Policy.EvaluationContext.AddClaimSet%28System.IdentityModel.Policy.IAuthorizationPolicy%2CSystem.IdentityModel.Claims.ClaimSet%29> e restituire `true` dal metodo <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%2A>.La restituzione di `true` indica all'infrastruttura di autorizzazione che il criterio di autorizzazione ha eseguito la sua funzione e che non occorre chiamarlo nuovamente.  
  
3.  Se il criterio di autorizzazione personalizzato aggiunge set di attestazioni solo quando determinate attestazioni sono già presenti in `EvaluationContext`, ricercare tali attestazioni esaminando le istanze di `ClaimSet` restituite dalla proprietà <xref:System.IdentityModel.Policy.EvaluationContext.ClaimSets%2A>.Se le attestazioni sono presenti, aggiungere i nuovi set di attestazioni chiamando il metodo <xref:System.IdentityModel.Policy.EvaluationContext.AddClaimSet%28System.IdentityModel.Policy.IAuthorizationPolicy%2CSystem.IdentityModel.Claims.ClaimSet%29> e, se non devono essere aggiunti altri set di attestazioni, restituire `true` per indicare all'infrastruttura di autorizzazione che il criterio di autorizzazione ha completato la sua funzione.Se le attestazioni non sono presenti, restituire `false` per indicare che il criterio di autorizzazione deve essere chiamato nuovamente nel caso in cui altri criteri di autorizzazione aggiungano altri set di attestazioni a `EvaluationContext`.  
  
4.  Negli scenari di elaborazione più complessi, si utilizza il secondo parametro del metodo <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> per archiviare una variabile di stato che l'infrastruttura di autorizzazione passerà nuovamente durante ogni chiamata successiva al metodo <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%28System.IdentityModel.Policy.EvaluationContext%2CSystem.Object%40%29> per una particolare valutazione.  
  
### Per specificare un criterio di autorizzazione personalizzato tramite configurazione  
  
1.  Specificare il tipo del criterio di autorizzazione personalizzato nell'attributo `policyType` dell'elemento `add` dell'elemento `authorizationPolicies` dell'elemento `serviceAuthorization`.  
  
    ```  
    <configuration>  
     <system.serviceModel>  
      <behaviors>  
        <serviceAuthorization serviceAuthorizationManagerType=  
                  "Samples.MyServiceAuthorizationManager" >  
          <authorizationPolicies>         
            <add policyType="Samples.MyAuthorizationPolicy"  
          </authorizationPolicies>  
        </serviceAuthorization>  
      </behaviors>  
     </system.serviceModel>  
    </configuration>  
    ```  
  
### Per specificare un criterio di autorizzazione personalizzato tramite codice  
  
1.  Creare una classe <xref:System.Collections.Generic.List%601> dell'interfaccia <xref:System.IdentityModel.Policy.IAuthorizationPolicy>.  
  
2.  Creare un'istanza del criterio di autorizzazione personalizzato.  
  
3.  Aggiungere l'istanza del criterio di autorizzazione all'elenco.  
  
4.  Ripetere i passaggi 2 e 3 per ogni criterio di autorizzazione personalizzato.  
  
5.  Assegnare una versione in sola lettura dell'elenco alla proprietà <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior.ExternalAuthorizationPolicies%2A>.  
  
     [!code-csharp[c_CustomAuthPol#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthpol/cs/c_customauthpol.cs#8)]
     [!code-vb[c_CustomAuthPol#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthpol/vb/source.vb#8)]  
  
## Esempio  
 Nell'esempio seguente viene illustrata un'implementazione completa dell'interfaccia <xref:System.IdentityModel.Policy.IAuthorizationPolicy>.  
  
 [!code-csharp[c_CustomAuthPol#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customauthpol/cs/c_customauthpol.cs#5)]
 [!code-vb[c_CustomAuthPol#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customauthpol/vb/source.vb#5)]  
  
## Vedere anche  
 <xref:System.ServiceModel.ServiceAuthorizationManager>   
 [Procedura: confrontare le attestazioni](../../../../docs/framework/wcf/extending/how-to-compare-claims.md)   
 [Procedura: creare un gestore autorizzazioni personalizzato per un servizio](../../../../docs/framework/wcf/extending/how-to-create-a-custom-authorization-manager-for-a-service.md)   
 [Criteri di autorizzazione](../../../../docs/framework/wcf/samples/authorization-policy.md)