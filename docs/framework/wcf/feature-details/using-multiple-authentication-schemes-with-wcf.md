---
title: "Uso di vari schemi di autenticazione con WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f32a56a0-e2b2-46bf-a302-29e1275917f9
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Uso di vari schemi di autenticazione con WCF
Con WCF è ora possibile specificare più schemi di autenticazione in un singolo endpoint.  Inoltre, i servizi ospitati dal Web possono ereditare le relative impostazioni di autenticazione direttamente da IIS.  Nei servizi self\-hosted è possibile specificare gli schemi di autenticazione da usare.  Per altre informazioni sulla configurazione delle impostazioni di autenticazione in IIS, vedere [Autenticazione IIS](http://go.microsoft.com/fwlink/?LinkId=232458)  
  
## Servizi ospitati da IIS  
 Per i servizi ospitati da IIS, impostare gli schemi di autenticazione che si desidera usare in IIS.  Quindi, Nella configurazione di binding del file web.config del servizio in uso specificare il tipo clientCredential come "InheritedFromHost", come illustrato nel seguente frammento XML:  
  
```xml  
<bindings>  
      <basicHttpBinding>  
        <binding name="secureBinding">  
          <security mode="Transport">  
            <transport clientCredentialType="InheritedFromHost" />  
          </security>  
        </binding>  
      </basicHttpBinding>  
    </bindings>  
```  
  
 È possibile specificare l'uso di un solo subset di schemi di autenticazione con il servizio tramite l'oggetto ServiceAuthenticationBehavior o l'elemento \<serviceAuthenticationManager\>.  Quando si configura questo tipo di codice, usare l'oggetto ServiceAuthenticationBehavior come illustrato nel seguente frammento di codice.  
  
```csharp  
// ...  
ServiceAuthenticationBehavior sab = null;  
sab = serviceHost.Description.Behaviors.Find<ServiceAuthenticationBehavior>();  
  
if (sab == null)  
{  
    sab = new ServiceAuthenticationBehavior();  
    sab.AuthenticationSchemes = AuthenticationSchemes.Basic | AuthenticationSchemes.Negotiate | AuthenticationSchemes.Digest;  
    serviceHost.Description.Behaviors.Add(sab);  
}  
else  
{  
     sab.AuthenticationSchemes = AuthenticationSchemes.Basic | AuthenticationSchemes.Negotiate | AuthenticationSchemes.Digest;  
}  
// ...  
  
```  
  
 Quando si applica questa configurazione in un file di configurazione, usare l'elemento \<serviceAuthenticationManager\> come illustrato nel frammento di XML seguente.  
  
```xml  
<behaviors>  
      <serviceBehaviors>  
        <behavior name="limitedAuthBehavior">  
          <serviceAuthenticationManager authenticationSchemes="Negotiate, Digest, Basic"/>  
          <!-- ... -->  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
```  
  
 In questo modo verrà considerato un solo subset degli schemi di autenticazione qui elencati per l'applicazione nell'endpoint del servizio, in base a quanto selezionato in IIS.  Pertanto, uno sviluppatore può escludere, ad esempio, l'autenticazione di base dall'elenco omettendola dall'elenco serviceAuthenticationManager e, anche se abilitata in IIS, non verrà applicata nell'endpoint del servizio.  
  
## Servizi self\-hosted  
 I servizi self\-hosted vengono configurati in modo leggermente diverso dal momento che non esiste alcuna applicazione IIS da cui ereditare le impostazioni.  In questo caso si usa l'elemento \<serviceAuthenticationManager\> o ServiceAuthenticationBehavior per specificare le impostazioni di autenticazione che verranno ereditate.  Nel codice l'aspetto è simile al seguente:  
  
```csharp  
// ...  
ServiceAuthenticationBehavior sab = null;  
sab = serviceHost.Description.Behaviors.Find<ServiceAuthenticationBehavior>();  
  
if (sab == null)  
{  
    sab = new ServiceAuthenticationBehavior();  
    sab.AuthenticationSchemes = AuthenticationSchemes.Basic | AuthenticationSchemes.Negotiate | AuthenticationSchemes.Digest;  
    serviceHost.Description.Behaviors.Add(sab);  
}  
else  
{  
     sab.AuthenticationSchemes = AuthenticationSchemes.Basic | AuthenticationSchemes.Negotiate | AuthenticationSchemes.Digest;  
}  
// ...  
  
```  
  
 Nella configurazione l'aspetto è simile al seguente:  
  
```xml  
<behaviors>  
      <serviceBehaviors>  
        <behavior name="limitedAuthBehavior">  
          <serviceAuthenticationManager authenticationSchemes="Negotiate, Digest, Basic"/>  
          <!-- ... -->  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
```  
  
 Quindi è possibile specificare InheritFromHost nelle impostazioni di binding come illustrato nel seguente frammento XML.  
  
```xml  
<bindings>  
      <basicHttpBinding>  
        <binding name="secureBinding">  
          <security mode="Transport">  
            <transport clientCredentialType="InheritedFromHost" />  
          </security>  
        </binding>  
      </basicHttpBinding>  
    </bindings>  
```  
  
 In alternativa, è possibile specificare gli schemi di autenticazione in un binding personalizzato, impostando gli schemi di autenticazione sull'elemento di binding del trasporto HTTP, come illustrato nel seguente frammento di configurazione.  
  
```xml  
<binding name="multipleBinding">  
      <textMessageEncoding/>  
      <httpTransport authenticationScheme="Negotiate, Ntlm, Digest, Basic" />  
    </binding>  
  
```  
  
## Vedere anche  
 [Associazioni e protezione](../../../../docs/framework/wcf/feature-details/bindings-and-security.md)   
 [Endpoint: indirizzi, associazioni e contratti](../../../../docs/framework/wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)   
 [Configurazione di associazioni fornite dal sistema](../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Funzionalità di sicurezza con associazioni personalizzate](../../../../docs/framework/wcf/feature-details/security-capabilities-with-custom-bindings.md)   
 [Associazioni](../../../../docs/framework/wcf/feature-details/bindings.md)   
 [Associazioni](../../../../docs/framework/wcf/feature-details/bindings.md)   
 [Associazioni personalizzate](../../../../docs/framework/wcf/extending/custom-bindings.md)