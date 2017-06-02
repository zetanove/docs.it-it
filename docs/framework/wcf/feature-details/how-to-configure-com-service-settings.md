---
title: "Procedura: configurare le impostazioni del servizio COM+ | Microsoft Docs"
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
  - "COM+ [WCF], configurazione delle impostazioni del servizio."
ms.assetid: f42a55a8-3af8-4394-9fdd-bf12a93780eb
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Procedura: configurare le impostazioni del servizio COM+
Quando l'interfaccia di un'applicazione viene aggiunta o rimossa usando lo strumento di configurazione del servizio COM\+, la configurazione del servizio Web viene aggiornata nel file di configurazione dell'applicazione.  Nella modalità hosting del servizio COM\+ il file Application.config si trova nella directory radice dell'applicazione \(l'impostazione predefinita è %PROGRAMFILES%\\ComPlus Applications\\{appid}\).  In entrambe le modalità di hosting Web il file Web.config è posizionato nella directory vroot specificata.  
  
> [!NOTE]
>  Per evitare la manomissione dei messaggi tra un client e un server è necessario firmare i messaggi.  Inoltre, per evitare la diffusione di informazioni dai messaggi scambiati tra un client e un server è necessario usare la crittografia a livello di messaggio o di trasporto.  Come per i servizi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], è necessario usare la limitazione delle richieste per limitare il numero di chiamate, connessioni, istanze e operazioni in sospeso simultanee.  Ciò consente di evitare un utilizzo eccessivo di risorse.  Il comportamento della limitazione delle richieste viene specificato tramite impostazioni del file di configurazione del servizio.  
  
## Esempio  
 Si consideri un componente che implementa l'interfaccia seguente:  
  
```  
[Guid("C551FBA9-E3AA-4272-8C2A-84BD8D290AC7")]  
public interface IFinances  
{  
    string Debit(string accountNo, double amount);  
    string Credit(string accountNo, double amount);  
}  
  
```  
  
 Se il componente viene esposto come un servizio Web, il contratto di servizio corrispondente che viene esposto, e al quale si devono conformare i client, è il seguente:  
  
```  
[ServiceContract(Session = true,  
Namespace = "http://tempuri.org/C551FBA9-E3AA-4272-8C2A-84BD8D290AC7",  
Name = "IFinances")]  
public interface IFinancesContract : IDisposable  
{  
    [OperationContract]  
    string Debit(string accountNo, double amount);  
    [OperationContract]  
    string Credit(string accountNo, double amount);  
}  
  
```  
  
> [!NOTE]
>  L'IID fa parte dello spazio dei nomi iniziale per il contratto.  
  
 Le applicazioni client che usano questo servizio dovrebbero essere conformi a questo contratto, nonché usare un'associazione che sia compatibile con quella specificata nella configurazione dell'applicazione.  
  
 Nell'esempio di codice seguente viene illustrato un file di configurazione predefinito.  Essendo un servizio Web [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], è conforme allo schema di configurazione del modello di servizio standard e può essere modificato come altri file di configurazione dei servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Modifiche tipiche includono:  
  
-   Modifica dell'indirizzo endpoint dal modulo ApplicationName\/ComponentName\/InterfaceName predefinito in un modulo maggiormente utilizzabile.  
  
-   Modifica dello spazio dei nomi del servizio dal modulo "http:\/\/tempuri.org\/InterfaceID" predefinito in un modulo più attinente.  
  
-   Modifica dell'endpoint per l'uso di un'associazione del trasporto differente.  
  
     Nel caso di un servizio COM\+ ospitato, per impostazione predefinita viene usato il trasporto tramite named pipe. È comunque possibile usare un trasporto esterno al computer come TCP.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
    <system.serviceModel>  
        <bindings>  
            <netNamedPipeBinding>  
                <binding name="comNonTransactionalBinding" />  
                <binding name="comTransactionalBinding" transactionFlow="true" />  
            </netNamedPipeBinding>  
        </bindings>  
        <comContracts>  
            <comContract contract="{C551FBA9-E3AA-4272-8C2A-84BD8D290AC7}"  
                name="IFinances" namespace="http://tempuri.org/C551FBA9-E3AA-4272-8C2A-84BD8D290AC7"  
                requiresSession="true">  
                <exposedMethods>  
                    <add exposedMethod="Debit" />  
                    <add exposedMethod="Credit" />  
                </exposedMethods>  
            </comContract>  
        </comContracts>  
        <services>  
            <service name="{DCDB24CC-0B19-4534-95CD-FBBFF4D67DD9},{C942B840-AD54-4A44-B5F7-928130980AB9}">  
                <endpoint address="IFinances" binding="netNamedPipeBinding" bindingConfiguration="comNonTransactionalBinding"  
                    contract="{C551FBA9-E3AA-4272-8C2A-84BD8D290AC7}" />  
                <host>  
                    <baseAddresses>  
                        <add baseAddress="net.pipe://localhost/ServiceModelDocSampleApp/ServiceModelDocSample.esFinance" />  
                    </baseAddresses>  
                </host>  
            </service>  
        </services>  
    </system.serviceModel>  
</configuration>  
  
```  
  
## Vedere anche  
 [Integrazione con applicazioni COM\+](../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications.md)