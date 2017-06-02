---
title: "Impersonating and Reverting | Microsoft Docs"
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
  - "WindowsIdentity objects, impersonating"
  - "security [.NET Framework], impersonating Windows accounts"
  - "impersonating Windows accounts"
ms.assetid: b93d402c-6c28-4f50-b2bc-d9607dc3e470
caps.latest.revision: 13
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 11
---
# Impersonating and Reverting
Talvolta può essere necessario ottenere un token di account Windows NT per rappresentare un account Windows. Può essere necessario, ad esempio, che l'applicazione basata su ASP.NET agisca per conto di più utenti in momenti diversi. L'applicazione potrebbe accettare un token che rappresenta un amministratore da Internet Information Services \(IIS\), rappresentare tale utente, eseguire un'operazione e ripristinare l'identità precedente. In seguito potrebbe accettare un token da IIS che rappresenta un utente con meno diritti, eseguire un'operazione e di nuovo il ripristino.  
  
 Nelle situazioni in cui l'applicazione deve rappresentare un account Windows che non è stato associato al thread corrente da IIS, è necessario recuperare il token di tale account e usarlo per attivare l'account. A tale scopo, è possibile eseguire queste attività:  
  
1.  Recuperare un token di un account per un particolare utente effettuando una chiamata al metodo **LogonUser** non gestito. Questo metodo non si trova nella libreria di classi base di .NET Framework, ma nel file **advapi32.dll** non gestito. L'accesso ai metodi nel codice non gestito è un'operazione avanzata che non rientra nell'ambito di questo argomento. Per altre informazioni, vedere [Interoperabilità con codice non gestito](../../../docs/framework/interop/index.md). Per altre informazioni sul metodo **LogonUser** e su **advapi32.dll**, vedere la documentazione di Platform SDK.  
  
2.  Creare una nuova istanza della classe **WindowsIdentity**, passando il token. Il codice seguente illustra questa chiamata, dove `hToken` rappresenta un token di Windows.  
  
    ```csharp  
    WindowsIdentity ImpersonatedIdentity = new WindowsIdentity(hToken);  
  
    ```  
  
    ```vb  
    Dim ImpersonatedIdentity As New WindowsIdentity(hToken)  
    ```  
  
3.  Iniziare la rappresentazione creando una nuova istanza della classe <xref:System.Security.Principal.WindowsImpersonationContext> e inizializzandola con il metodo <xref:System.Security.Principal.WindowsIdentity.Impersonate%2A?displayProperty=fullName> della classe inizializzata, come mostrato nel codice seguente.  
  
    ```csharp  
    WindowsImpersonationContext MyImpersonation = ImpersonatedIdentity.Impersonate();  
  
    ```  
  
    ```vb  
    WindowsImpersonationContext MyImpersonation = ImpersonatedIdentity.Impersonate()  
    ```  
  
4.  Quando la rappresentazione non è più necessaria, chiamare il metodo <xref:System.Security.Principal.WindowsImpersonationContext.Undo%2A?displayProperty=fullName> per ripristinare la rappresentazione, come mostrato nel codice seguente.  
  
    ```csharp  
    MyImpersonation.Undo();  
  
    ```  
  
    ```vb  
    MyImpersonation.Undo()  
    ```  
  
 Se il codice attendibile ha già associato un oggetto <xref:System.Security.Principal.WindowsPrincipal> al thread, è possibile chiamare il metodo **Impersonate** dell'istanza, che non accetta un token di account. Si noti che questo è utile solo quando l'oggetto **WindowsPrincipal** nel thread rappresenta un utente diverso da quello per cui il processo è attualmente in esecuzione. Questa situazione può verificarsi, ad esempio, quando si usa ASP.NET con l'autenticazione di Windows attivata e la rappresentazione disattivata. In questo caso, il processo viene eseguito con un account configurato in Internet Information Services \(IIS\), mentre l'entità corrente rappresenta l'utente di Windows che sta accedendo alla pagina.  
  
 Si noti che né **Impersonate** né **Undo** modificano l'oggetto **Principal** \(<xref:System.Security.Principal.IPrincipal>\) associato al contesto chiamata corrente. La rappresentazione e il ripristino modificano invece il token associato al processo del sistema operativo corrente.  
  
## Vedere anche  
 <xref:System.Security.Principal.WindowsIdentity>   
 <xref:System.Security.Principal.WindowsImpersonationContext>   
 [Principal and Identity Objects](../../../docs/standard/security/principal-and-identity-objects.md)   
 [Interoperating with Unmanaged Code](../../../docs/framework/interop/index.md)