---
title: "Integrazione di System.Web.Routing | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 31fe2a4f-5c47-4e5d-8ee1-84c524609d41
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Integrazione di System.Web.Routing
Quando si ospita un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] in Internet Information Service \(IIS\), si inserisce un file con estensione svc nella directory virtuale.Questo file con estensione svc specifica la factory di host del servizio da utilizzare e la classe che implementa il servizio.Quando si inviano richieste al servizio, si specifica il file con estensione svc nell'URI, ad esempio: http:\/\/contoso.com\/EmployeeServce.svc.Per i programmatori che scrivono servizi REST, questo tipo di URI non è ottimale.Gli URI per i servizi REST indicano una risorsa specifica e in genere non presentano estensioni.La funzionalità di integrazione <xref:System.Web.Routing> consente di ospitare un servizio REST di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che risponde a URI sprovvisti di estensione.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] routing, vedere la pagina relativa al [routing ASP.NET](http://go.microsoft.com/fwlink/?LinkId=184660) e l'esempio [AspNetRouteIntegration](../../../../docs/framework/wcf/samples/aspnetrouteintegration.md).  
  
## Utilizzo dell'integrazione System.Web.Routing  
 Per utilizzare la funzionalità di integrazione <xref:System.Web.Routing>, viene utilizzata la classe <xref:System.ServiceModel.Activation.ServiceRoute> per creare una o più route e aggiungerle a <xref:System.Web.Routing.RouteTable> in un file Global.asax.Queste route specificano i relativi URI a cui risponde il servizio.Nell'esempio seguente viene illustrato come effettuare questa operazione.  
  
```  
<%@ Application Language="C#" %>  
<%@ Import Namespace="System.Web.Routing" %>  
<%@ Import Namespace="System.ServiceModel.Activation" %>  
<%@ Import Namespace="System.ServiceModel.Web " %>  
  
<script RunAt="server">  
    void Application_Start(object sender, EventArgs e)  
    {  
        RegisterRoutes(RouteTable.Routes);  
    }  
  
    private void RegisterRoutes(RouteCollection routes)  
    {  
        routes.Add(new ServiceRoute("Customers", new WebServiceHostFactory(), typeof(Service)));   
   }  
</script>  
  
```  
  
 Tutte le richieste vengono indirizzato con un URI relativo che inizia con Customers al servizio `Service`.  
  
 Nel file Web.config è necessario aggiungere il modulo `System.Web.Routing.UrlRoutingModule`, impostare l'attributo `runAllManagedModulesForAllRequests` su `true` e aggiungere il gestore `UrlRoutingHandler` all'elemento `<system.webServer>`, come indicato nell'esempio seguente.  
  
```xml  
<system.webServer>  
      <modules runAllManagedModulesForAllRequests="true">  
        <add name="UrlRoutingModule" type="System.Web.Routing.UrlRoutingModule, System.Web, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a" />  
      </modules>  
      <handlers>  
        <add name="UrlRoutingHandler" preCondition="integratedMode" verb="*" path="UrlRouting.axd"/>  
      </handlers>  
    </system.webServer>  
```  
  
 Vengono caricati un modulo e il gestore necessario per il routing.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Routing](../../../../docs/framework/wcf/feature-details/routing.md).È inoltre necessario impostare l'attributo `aspNetCompatibilityEnabled` su `true` nell'elemento `<serviceHostingEnvironment>`, come indicato nel codice seguente.  
  
```  
<system.serviceModel>  
    <serviceHostingEnvironment aspNetCompatibilityEnabled="true"/>  
        <!-- ... -->  
    </system.serviceModel>  
```  
  
 La classe che implementa il servizio deve abilitare i requisiti di compatibilità ASP.NET, come indicato nell'esempio seguente.  
  
```  
[ServiceContract]  
[AspNetCompatibilityRequirements(RequirementsMode=AspNetCompatibilityRequirementsMode.Allowed)]  
    public class Service  
    {  
        // ...  
    }  
```  
  
## Vedere anche  
 [Modello di programmazione HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)   
 [Routing di ASP.NET](http://go.microsoft.com/fwlink/?LinkId=184660)