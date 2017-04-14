---
title: "Rappresentazione di client | Microsoft Docs"
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
  - "Rappresentazione dell'esempio di Client [Windows Communication Foundation]"
  - "rappresentazione, Esempio di Windows Communication Foundation"
  - "comportamenti dei servizi, esempio di rappresentazione"
ms.assetid: 8bd974e1-90db-4152-95a3-1d4b1a7734f8
caps.latest.revision: 25
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 25
---
# Rappresentazione di client
L'esempio Rappresentazione di client mostra come rappresentare l'applicazione del chiamante al servizio così che il servizio possa accedere a risorse di sistema per conto del chiamante.  
  
 L'esempio è basato sull'esempio [Servizio indipendente](../../../../docs/framework/wcf/samples/self-host.md).I file del servizio e di configurazione client sono gli stessi dell'esempio [Servizio indipendente](../../../../docs/framework/wcf/samples/self-host.md).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 Il codice del servizio è stato modificato in modo tale che il metodo `Add` nel servizio rappresenta il chiamante utilizzando <xref:System.ServiceModel.OperationBehaviorAttribute> come mostra il codice di esempio seguente.  
  
```  
[OperationBehavior(Impersonation = ImpersonationOption.Required)]  
public double Add(double n1, double n2)  
{  
    double result = n1 + n2;  
    Console.WriteLine("Received Add({0},{1})", n1, n2);  
    Console.WriteLine("Return: {0}", result);  
    DisplayIdentityInformation();  
    return result;  
}  
  
```  
  
 Di conseguenza, il contesto di sicurezza del thread in esecuzione passa a rappresentare il chiamante prima di immettere il metodo `Add` ed essere ripristinato sul metodo esistente.  
  
 Il metodo `DisplayIdentityInformation` illustrato nel codice di esempio seguente è una funzione di utilità che visualizza l'identità del chiamante.  
  
```  
static void DisplayIdentityInformation()  
{  
    Console.WriteLine("\t\tThread Identity            :{0}",  
         WindowsIdentity.GetCurrent().Name);  
    Console.WriteLine("\t\tThread Identity level  :{0}",   
         WindowsIdentity.GetCurrent().ImpersonationLevel);  
    Console.WriteLine("\t\thToken                     :{0}",  
         WindowsIdentity.GetCurrent().Token.ToString());  
    return;  
}  
  
```  
  
 Il metodo `Subtract` nel servizio rappresenta il chiamante utilizzando chiamate imperative come mostra il codice di esempio seguente.  
  
```  
public double Subtract(double n1, double n2)  
{  
    double result = n1 - n2;  
    Console.WriteLine("Received Subtract({0},{1})", n1, n2);  
    Console.WriteLine("Return: {0}", result);  
Console.WriteLine("Before impersonating");  
DisplayIdentityInformation();  
  
    if (ServiceSecurityContext.Current.WindowsIdentity.ImpersonationLevel == TokenImpersonationLevel.Impersonation ||  
        ServiceSecurityContext.Current.WindowsIdentity.ImpersonationLevel == TokenImpersonationLevel.Delegation)  
    {  
        // Impersonate.  
        using (ServiceSecurityContext.Current.WindowsIdentity.Impersonate())  
        {  
            // Make a system call in the caller's context and ACLs   
            // on the system resource are enforced in the caller's context.   
            Console.WriteLine("Impersonating the caller imperatively");  
            DisplayIdentityInformation();  
        }  
    }  
    else  
    {  
        Console.WriteLine("ImpersonationLevel is not high enough to perform this operation.");  
    }  
  
Console.WriteLine("After reverting");  
DisplayIdentityInformation();  
    return result;  
}  
```  
  
 Notare che in questo caso che il chiamante non è rappresentato per la chiamata intera ma è rappresentato solo per una parte della chiamata.In generale, la rappresentazione di ambiti più piccoli, è preferibile alla rappresentazione dell'intera operazione.  
  
 Gli altri metodi non rappresentano il chiamante.  
  
 Il codice client è stato modificato per impostare il livello di rappresentazione su <xref:System.Security.Principal.TokenImpersonationLevel>.Il client specifica il livello di rappresentazione che il servizio deve utilizzare, utilizzando l'enumerazione <xref:System.Security.Principal.TokenImpersonationLevel>.L'enumerazione supporta i seguenti i seguenti valori: <xref:System.Security.Principal.TokenImpersonationLevel>, <xref:System.Security.Principal.TokenImpersonationLevel>, <xref:System.Security.Principal.TokenImpersonationLevel>, <xref:System.Security.Principal.TokenImpersonationLevel> e <xref:System.Security.Principal.TokenImpersonationLevel>.Per eseguire una verifica di accesso quando si accede a una risorsa di sistema sul computer locale protetto utilizzando Windows ACL, il livello di rappresentazione deve essere impostato su <xref:System.Security.Principal.TokenImpersonationLevel>, come mostra il codice di esempio seguente.  
  
```  
// Create a client with given client endpoint configuration  
CalculatorClient client = new CalculatorClient();  
  
client.ClientCredentials.Windows.AllowedImpersonationLevel = TokenImpersonationLevel.Impersonation;  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nelle finestre della console client e del servizio.Premere INVIO in tutte le finestre della console per arrestare il servizio e il client.  
  
> [!NOTE]
>  Il servizio deve essere eseguito a partire da un account amministrativo o l'account sotto cui viene eseguito deve avere diritti per iscrivere l'URI http:\/\/localhost:8000\/ServiceModelSamples con il livello HTTP.Tali diritti possono essere concessi configurando una [Prenotazione dello spazio dei nomi](http://go.microsoft.com/fwlink/?LinkId=95012) utilizzando lo strumento [Httpcfg.exe](http://go.microsoft.com/fwlink/?LinkId=95010).  
  
> [!NOTE]
>  In computer che eseguono [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)], la rappresentazione è supportata solo se l'applicazione Host.exe ha il privilegio di rappresentazione.Per impostazione predefinita, solo gli amministratori dispongono di questa autorizzazione. Per aggiungere questo privilegio a un account eseguito dal servizio, andare in **Strumenti di amministrazione**, aprire **Criteri di sicurezza locali**, aprire **Criteri locali**, fare clic su **Assegnazione diritti utente** e selezionare **Rappresenta un client dopo l'autenticazione** e fare doppio clic su **Proprietà** per aggiungere un utente o un gruppo.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di aver eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio su una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
4.  Per dimostrare che il servizio rappresenta il chiamante, eseguire il client sotto un account diverso rispetto a quello sotto cui il servizio è in esecuzione.A tale scopo, al prompt dei comandi, digitare:  
  
    ```  
    runas /user:<machine-name>\<user-name> client.exe  
    ```  
  
     Viene richiesta una password.Immettere la password per l'account precedentemente specificata.  
  
5.  Quando si esegue il client, notare l'identità prima e dopo aver eseguito credenziali diverse.  
  
## Vedere anche