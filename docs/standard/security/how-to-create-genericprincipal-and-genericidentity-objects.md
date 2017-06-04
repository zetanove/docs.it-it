---
title: "How to: Create GenericPrincipal and GenericIdentity Objects | Microsoft Docs"
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
  - "Creating Generic Identity Objects"
  - "GenericPrincipal Objects"
  - "Creating GenericPrincipal Objects"
  - "GenericIdentity Objects"
ms.assetid: 465694cf-258b-4747-9dae-35b01a5bcdbb
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# How to: Create GenericPrincipal and GenericIdentity Objects
È possibile utilizzare la classe <xref:System.Security.Principal.GenericIdentity> unitamente alla classe <xref:System.Security.Principal.GenericPrincipal> per creare uno schema di autorizzazione che esista indipendentemente da un dominio di Windows NT o Windows 2000.  
  
### Per creare un oggetto GenericPrincipal  
  
1.  Creare una nuova istanza della classe di identità e inizializzarla con il nome che si desidera contenere.  Nel codice riportato di seguito viene creato un nuovo oggetto **GenericIdentity** e tale oggetto viene inizializzato con il nome `MyUser`.  
  
    ```vb  
    Dim MyIdentity As New GenericIdentity("MyUser")  
    ```  
  
    ```csharp  
    GenericIdentity MyIdentity = new GenericIdentity("MyUser");  
    ```  
  
2.  Creare una nuova istanza della classe **GenericPrincipal** e inizializzarla con l'oggetto **GenericIdentity** creato in precedenza e una matrice di stringhe che rappresentano i ruoli che si desidera associare all'oggetto Principal.  L'esempio di codice che segue specifica una matrice di stringhe che rappresentano un ruolo amministratore e un ruolo utente.  L'oggetto **GenericPrincipal** viene quindi inizializzato con l'oggetto **GenericIdentity** precedente e con la matrice di stringhe.  
  
    ```vb  
    Dim MyStringArray As String() = {"Manager", "Teller"}  
    DIm MyPrincipal As New GenericPrincipal(MyIdentity, MyStringArray)  
    ```  
  
    ```csharp  
    String[] MyStringArray = {"Manager", "Teller"};  
    GenericPrincipal MyPrincipal = new GenericPrincipal(MyIdentity, MyStringArray);  
    ```  
  
3.  Utilizzare il codice riportato di seguito per associare l'oggetto Principal al thread corrente.  Questo risulta particolarmente utile nelle situazioni in cui è necessario che l'oggetto Principal sia convalidato più volte, da altro codice eseguito nell'applicazione oppure da un oggetto <xref:System.Security.Permissions.PrincipalPermission>.  È comunque possibile eseguire la convalida basata sui ruoli sull'oggetto Principal senza associarlo al thread.  Per ulteriori informazioni, vedere [Sostituzione di oggetti Principal](../../../docs/standard/security/replacing-a-principal-object.md).  
  
    ```vb  
    Thread.CurrentPrincipal = MyPrincipal  
    ```  
  
    ```csharp  
    Thread.CurrentPrincipal = MyPrincipal;  
    ```  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come creare un'istanza di un oggetto **GenericPrincipal** e di un oggetto **GenericIdentity**.  Il valore di questi oggetti viene visualizzato nella console.  
  
```vb  
Imports System  
Imports System.Security.Principal  
Imports System.Threading  
  
Public Class Class1  
  
    Public Shared Sub Main()  
        ' Create generic identity.  
        Dim MyIdentity As New GenericIdentity("MyIdentity")  
  
        ' Create generic principal.  
        Dim MyStringArray As String() =  {"Manager", "Teller"}  
        Dim MyPrincipal As New GenericPrincipal(MyIdentity, MyStringArray)  
  
        ' Attach the principal to the current thread.  
        ' This is not required unless repeated validation must occur,  
        ' other code in your application must validate, or the   
        ' PrincipalPermisson object is used.   
        Thread.CurrentPrincipal = MyPrincipal  
  
        ' Print values to the console.  
        Dim Name As String = MyPrincipal.Identity.Name  
        Dim Auth As Boolean = MyPrincipal.Identity.IsAuthenticated  
        Dim IsInRole As Boolean = MyPrincipal.IsInRole("Manager")  
  
        Console.WriteLine("The Name is: {0}", Name)  
        Console.WriteLine("The IsAuthenticated is: {0}", Auth)  
        Console.WriteLine("Is this a Manager? {0}", IsInRole)  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using System.Security.Principal;  
using System.Threading;  
  
public class Class1  
{  
    public static int Main(string[] args)  
    {  
    // Create generic identity.  
    GenericIdentity MyIdentity = new GenericIdentity("MyIdentity");  
  
    // Create generic principal.  
    String[] MyStringArray = {"Manager", "Teller"};  
    GenericPrincipal MyPrincipal =   
        new GenericPrincipal(MyIdentity, MyStringArray);  
  
    // Attach the principal to the current thread.  
    // This is not required unless repeated validation must occur,  
    // other code in your application must validate, or the   
    // PrincipalPermisson object is used.   
    Thread.CurrentPrincipal = MyPrincipal;  
  
    // Print values to the console.  
    String Name =  MyPrincipal.Identity.Name;  
    bool Auth =  MyPrincipal.Identity.IsAuthenticated;   
    bool IsInRole =  MyPrincipal.IsInRole("Manager");  
  
    Console.WriteLine("The Name is: {0}", Name);  
    Console.WriteLine("The IsAuthenticated is: {0}", Auth);  
    Console.WriteLine("Is this a Manager? {0}", IsInRole);  
  
    return 0;  
    }  
}  
```  
  
 Quando il codice viene eseguito, l'applicazione restituisce un output analogo al seguente.  
  
```  
The Name is: MyIdentity  
The IsAuthenticated is: True  
Is this a Manager? True  
```  
  
## Vedere anche  
 <xref:System.Security.Principal.GenericIdentity>   
 <xref:System.Security.Principal.GenericPrincipal>   
 <xref:System.Security.Permissions.PrincipalPermission>   
 [Replacing a Principal Object](../../../docs/standard/security/replacing-a-principal-object.md)   
 [Principal and Identity Objects](../../../docs/standard/security/principal-and-identity-objects.md)