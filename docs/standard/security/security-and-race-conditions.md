---
title: "Security and Race Conditions | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "security [.NET Framework], race conditions"
  - "race conditions"
  - "secure coding, race conditions"
  - "code security, race conditions"
ms.assetid: ea3edb80-b2e8-4e85-bfed-311b20cb59b6
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# Security and Race Conditions
Un'altra area di interesse è quella relativa alla possibilità che problemi della sicurezza possano essere sfruttati da race condition.  Questa condizione si manifesta in diversi modi;  negli argomenti che seguono sono illustrati alcuni aspetti problematici che è necessario evitare in fase di sviluppo.  
  
## Race condition nel metodo Dispose  
 Se il metodo **Dispose** di una classe \(per ulteriori informazioni, vedere [Garbage Collection](../../../docs/standard/garbage-collection/index.md)\) non è sincronizzato, è possibile eseguire più volte il codice di pulitura in **Dispose**, come illustrato nell'esempio seguente.  
  
```vb  
Sub Dispose()  
    If Not (myObj Is Nothing) Then  
       Cleanup(myObj)  
       myObj = Nothing  
    End If  
End Sub  
  
```  
  
```csharp  
void Dispose()   
{  
    if( myObj != null )   
    {  
        Cleanup(myObj);  
        myObj = null;  
    }  
}  
```  
  
 Poiché questa implementazione del metodo **Dispose** non è sincronizzata, il codice `Cleanup` potrebbe essere chiamato da un primo thread, seguito da un secondo thread prima che il valore di `_myObj` sia impostato su **Null**.  Il problema di sicurezza dipende dalle operazioni effettuate durante l'esecuzione del codice `Cleanup`.  Un problema di maggiore importanza legato all'utilizzo di implementazioni di **Dispose** non sincronizzate coinvolge l'utilizzo di handle di risorse quali i file.  L'eliminazione di elementi non corretti può provocare l'utilizzo dell'handle errato e comportare problemi di vulnerabilità della sicurezza.  
  
## Race condition nei costruttori  
 In alcune applicazioni, altri thread possono accedere ai membri delle classi prima che sia completata l'esecuzione dei costruttori di classe.  Se si verifica questa condizione, esaminare tutti i costruttori di classe per accertarsi che non vi siano problemi di sicurezza o sincronizzare i thread, se necessario.  
  
## Race condition per oggetti memorizzati nella cache  
 Il codice che consente la memorizzazione nella cache delle informazioni di sicurezza o nel quale viene utilizzata l'operazione [Assert](../../../docs/framework/misc/using-the-assert-method.md) per la sicurezza dall'accesso di codice può essere vulnerabile a race condition se altre parti della classe non sono sincronizzate in modo corretto, come mostrato nell'esempio riportato di seguito.  
  
```vb  
Sub SomeSecureFunction()  
    If SomeDemandPasses() Then  
        fCallersOk = True  
        DoOtherWork()  
        fCallersOk = False()  
    End If  
End Sub  
  
Sub DoOtherWork()  
    If fCallersOK Then  
        DoSomethingTrusted()  
    Else  
        DemandSomething()  
        DoSomethingTrusted()  
    End If  
End Sub  
  
```  
  
```csharp  
void SomeSecureFunction()   
{  
    if(SomeDemandPasses())   
    {  
        fCallersOk = true;  
        DoOtherWork();  
        fCallersOk = false();  
    }  
}  
void DoOtherWork()   
{  
    if( fCallersOK )   
    {  
        DoSomethingTrusted();  
    }  
    else   
    {  
        DemandSomething();  
        DoSomethingTrusted();  
    }  
}  
```  
  
 Se sono presenti altri percorsi di `DoOtherWork` che è possibile chiamare da un altro thread con lo stesso oggetto, la pretesa può essere aggirata da un chiamante non attendibile.  
  
 Se nella cache sono memorizzate informazioni di sicurezza, esaminare il codice per ricercare eventuali problemi di sicurezza.  
  
## Race condition nei finalizzatori  
 Le race condition possono verificarsi anche in un oggetto che fa riferimento a una risorsa statica o non gestita che viene resa disponibile nel finalizzatore.  Se più oggetti condividono una risorsa modificata in un finalizzatore di classe, è necessario sincronizzare l'accesso a tale risorsa per tutti gli oggetti.  
  
## Vedere anche  
 [Secure Coding Guidelines](../../../docs/standard/security/secure-coding-guidelines.md)