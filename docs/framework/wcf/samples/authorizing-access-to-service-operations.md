---
title: "Autorizzazione dell&#39;accesso alle operazioni del servizio | Microsoft Docs"
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
  - "autorizzazione, Esempio di Windows Communication Foundation"
  - "Autorizzazione dell'accesso alle operazioni del servizio [Windows Communication Foundation]"
  - "comportamenti dei servizi, esempio di autorizzazione dell'accesso"
ms.assetid: ddcfdaa5-8b2e-4e13-bd85-887209dc6328
caps.latest.revision: 23
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 23
---
# Autorizzazione dell&#39;accesso alle operazioni del servizio
In questo esempio viene illustrato come usare l'elemento [\<autorizzazioneServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md) per abilitare l'uso dell'attributo <xref:System.Security.Permissions.PrincipalPermissionAttribute> per autorizzare l'accesso alle operazioni del servizio.  L'esempio è basato sull'esempio [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md).  Il servizio e il client sono stati configurati usando [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md).  L'attributo `mode` di [\<sicurezza\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md) è stato impostato su `Message` e `clientCredentialType` è stato impostato su `Windows`.  <xref:System.Security.Permissions.PrincipalPermissionAttribute> viene applicato a ogni metodo del servizio e usato per limitare l'accesso alle operazioni.  Il chiamante deve essere un amministratore Windows per accedere a tutte le operazioni.  
  
 In questo esempio, il client è un'applicazione console \(.exe\) e il servizio è ospitato da Internet Information Services \(IIS\).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 Il file di configurazione del servizio usa [\<autorizzazioneServizio\>](../../../../docs/framework/configure-apps/file-schema/wcf/serviceauthorization-element.md) per impostare l'attributo `principalPermissionMode` :  
  
```  
<behaviors>  
  <serviceBehaviors>  
    <behavior>  
      ...  
      <!-- The serviceAuthorization behavior sets the  
           principalPermissionMode to UseWindowsGroups.  
           This puts a WindowsPrincipal on the current thread when a   
           service is invoked. -->  
      <serviceAuthorization principalPermissionMode="UseWindowsGroups" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 L'impostazione della `principalPermissionMode` su `UseWindowsGroups` abilita l'uso di <xref:System.Security.Permissions.PrincipalPermissionAttribute> basato sui nomi dei gruppi di Windows.  
  
 <xref:System.Security.Permissions.PrincipalPermissionAttribute> viene applicato a ogni operazione per richiedere che il chiamante appartenga al gruppo Administrators di Windows, come illustrato nell'esempio di codice seguente.  
  
```  
[PrincipalPermission(SecurityAction.Demand,   
                             Role = "Builtin\\Administrators")]  
public double Add(double n1, double n2)  
{  
    double result = n1 + n2;  
    return result;  
}  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.  Il client comunica correttamente con ogni operazione se viene eseguito con un account che appartiene al gruppo Administrators. In caso contrario, l'accesso viene negato.  Per sperimentare un errore di autorizzazione, eseguire il client con un account che non appartiene al gruppo Administrators.  Premere INVIO nella finestra della console per arrestare il client.  
  
 Un servizio può ricevere una notifica di errori di autorizzazione implementando un <xref:System.ServiceModel.Dispatcher.IErrorHandler>.  Vedere [Estensione del controllo sulla gestione e sulla segnalazione degli errori](../../../../docs/framework/wcf/samples/extending-control-over-error-handling-and-reporting.md) per informazioni sull'implementazione di `IErrorHandler`.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
## Vedere anche