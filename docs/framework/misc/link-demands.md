---
title: "Link Demands | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "security [.NET Framework], demands"
  - "demanded permissions"
  - "permissions [.NET Framework], demands"
  - "granting permissions, demands"
  - "code access security, demands"
  - "user demands for permission"
  - "caller security checks"
  - "link demands"
ms.assetid: a33fd5f9-2de9-4653-a4f0-d9df25082c4d
caps.latest.revision: 18
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 16
---
# Link Demands
Una richiesta di collegamento determina l'esecuzione di un controllo di sicurezza in fase di compilazione JIT, durante il quale viene esaminato solo l'assembly chiamante immediato del codice.  Il collegamento si verifica quando il codice è associato a un riferimento a un tipo, quale un riferimento a un puntatore a funzione o una chiamata al metodo.  Se l'assembly chiamante non dispone delle autorizzazioni sufficienti per collegarsi al codice, il collegamento non viene autorizzato e in fase di caricamento ed esecuzione del codice viene generata un'eccezione di runtime.  Le richieste di collegamento possono essere sottoposte a override nelle classi che ereditano dal codice.  
  
 Mediante questo tipo di richiesta non viene eseguita un'analisi completa dello stack e permane il rischio che il codice sia soggetto ad attacchi subdoli.  Se, ad esempio, un metodo nell'assembly A è protetto da una richiesta di collegamento, un chiamante diretto nell'assembly B viene valutato in base alle autorizzazioni dell'assembly B.  La richiesta di collegamento non valuta tuttavia un metodo nell'assembly C, se il metodo nell'assembly A viene chiamato indirettamente usando il metodo nell'assembly B.  La richiesta di collegamento specifica solo le autorizzazioni di cui devono disporre i chiamanti diretti nell'assembly chiamante immediato per effettuare collegamenti al codice.  Non vengono specificate le autorizzazioni necessarie a tutti i chiamanti per l'esecuzione del codice.  
  
 I modificatori di percorso chiamate nello stack <xref:System.Security.CodeAccessPermission.Assert%2A>, <xref:System.Security.CodeAccessPermission.Deny%2A> e <xref:System.Security.CodeAccessPermission.PermitOnly%2A> non influiscono sulla valutazione delle richieste di collegamento.  poiché queste non eseguono una verifica del percorso chiamate nello stack.  
  
 Se si accede a un metodo protetto da una richiesta di collegamento tramite [Reflection](../../../docs/framework/reflection-and-codedom/reflection.md), viene controllato il chiamante immediato del relativo codice tramite reflection.  Tale comportamento si verifica sia per l'individuazione che per la chiamata di metodi realizzate mediante reflection.  Si supponga, ad esempio, che nel codice si usi la reflection per restituire un oggetto <xref:System.Reflection.MethodInfo> che rappresenta un metodo protetto da una richiesta di collegamento. L'oggetto **MethodInfo** viene quindi passato ad altro codice, che lo userà per richiamare il metodo originale.  In questo caso il controllo della richiesta di collegamento viene eseguito due volte: una sul codice che restituisce l'oggetto **MethodInfo** e l'altra sul codice che lo richiama.  
  
> [!NOTE]
>  Una richiesta di collegamento effettuata su un costruttore di classe statico non consente di proteggere il costruttore, poiché i costruttori statici vengono chiamati dal sistema, all'esterno del percorso di esecuzione del codice dell'applicazione.  Quando una richiesta di collegamento viene applicata a un'intera classe, tale richiesta non consente quindi di proteggere l'accesso a un costruttore statico, anche se consente di proteggere il resto della classe.  
  
 Il frammento di codice seguente specifica in modo dichiarativo che a ogni codice collegato al metodo `ReadData` deve essere assegnata l'autorizzazione `CustomPermission`.  Questa autorizzazione è un'autorizzazione personalizzata ipotetica e non esiste in .NET Framework.  La richiesta viene specificata passando un flag **SecurityAction.LinkDemand** a `CustomPermissionAttribute`.  
  
```vb  
<CustomPermissionAttribute(SecurityAction.LinkDemand)> _  
Public Shared Function ReadData() As String  
    ' Access a custom resource.  
End Function    
```  
  
```csharp  
[CustomPermissionAttribute(SecurityAction.LinkDemand)]  
public static string ReadData()  
{  
    // Access a custom resource.  
}  
```  
  
## Vedere anche  
 [Attributi](../../../docs/standard/attributes/index.md)   
 [Code Access Security](../../../docs/framework/misc/code-access-security.md)