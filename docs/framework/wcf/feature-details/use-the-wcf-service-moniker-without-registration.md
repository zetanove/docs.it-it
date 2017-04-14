---
title: "Procedura: usare il moniker servizio di Windows Communication Foundation senza registrazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "COM [WCF], moniker del servizio senza registrazione"
ms.assetid: ee3cf5c0-24f0-4ae7-81da-73a60de4a1a8
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Procedura: usare il moniker servizio di Windows Communication Foundation senza registrazione
Per connettersi a un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e comunicare con esso, un'applicazione client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] deve disporre dei dettagli sull'indirizzo del servizio, la configurazione dell'associazione e il contratto di servizio.  
  
 Il moniker servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ottiene in genere il contratto necessario tramite la precedente registrazione dei tipi di attributo obbligatori, ma ci sono casi in cui ciò non è possibile.  Invece che con la registrazione, il moniker può ottenere la definizione del contratto nella forma di un documento WSDL \(Web Services Definition Language\) tramite l'uso del parametro `wsdl` o dello scambio metadati, tramite il parametro `mexAddress`.  
  
 Questo consente scenari quali la distribuzione di un foglio di calcolo Excel in cui alcuni dei valori delle celle sono calcolati tramite interazioni di servizi Web.  In questo scenario, potrebbe non essere fattibile registrare l'assembly del contratto di servizio su tutti i client che potrebbero aprire il documento.  Il parametro `wsdl` o `mexAddress` consente una soluzione autonoma.  
  
> [!NOTE]
>  È necessario usare l'autenticazione reciproca per proteggersi dalla manomissione o lo spoofing di richieste e risposte.  In particolare, è importante per i client assicurarsi che l'endpoint di scambio metadati che sta rispondendo sia la parte attendibile prevista.  
  
## Esempio  
 In questo esempio viene illustrato l'uso del moniker servizio con un contratto MEX.  Un servizio con il contratto seguente viene esposto con un wsHttpBinding.  
  
```  
using System.ServiceModel;  
  
...  
  
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Demo")]  
public interface IAffiliate  
{  
    [OperationContract]  
    bool NewAffiliate(string ID, string company, string fullname, string accountsCode);  
    [OperationContract]  
    bool RemoveAffiliate(string ID);  
    [OperationContract]  
    double RevenueCheckMonthly(ref string ID);  
    [OperationContract]  
    double RevenueCheckTotal(ref string ID);  
}  
```  
  
 Per creare un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per il servizio remoto è possibile usare la stringa del moniker di esempio seguente.  
  
```  
service4:mexAddress="http://servername/Affiliates/service.svc/mex",  
address="http://servername/Affiliates/service.svc",  
contract=IAffiliate, contractNamespace=http://Microsoft.ServiceModel.Demo,  
binding=WSHttpBinding_IAffiliate, bindingNamespace=http://tempuri.org/  
```  
  
 Durante l'esecuzione dell'applicazione client, il client esegue un `WS-MetadataExchange` con l'elemento `mexAddress` fornito.  Questa operazione potrebbe restituire dettagli sull'indirizzo, l'associazione e il contratto per diversi servizi.  I parametri `address`, `contract`, `contractNamespace`, `binding` e `bindingNamespace` vengono usati per identificare il servizio designato.  Una volta messi in corrispondenza questi parametri, il moniker crea un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] con la definizione di contratto appropriata e possono essere eseguite chiamate usando il client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], come con il contratto tipizzato.  
  
> [!NOTE]
>  Se il formato del moniker non è valido o se il servizio non è disponibile, la chiamata a `GetObject` restituirà un errore di sintassi non valida.  Se si riceve questo errore, verificare che il moniker che si sta usando sia valido e che il servizio sia disponibile.  
  
## Vedere anche  
 [Procedura: registrare e configurare un moniker servizio](../../../../docs/framework/wcf/feature-details/how-to-register-and-configure-a-service-moniker.md)