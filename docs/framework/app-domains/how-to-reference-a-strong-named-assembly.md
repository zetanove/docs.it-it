---
title: "Procedura: aggiungere un riferimento a un assembly con nome sicuro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "assembly [.NET Framework], con nome sicuro"
  - "associazione di assembly, con nome sicuro"
  - "riferimento ad assembly in fase di compilazione"
  - "assembly con nome sicuro, riferimenti in fase di compilazione"
ms.assetid: 4c6a406a-b5eb-44fa-b4ed-4e95bb95a813
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Procedura: aggiungere un riferimento a un assembly con nome sicuro
Il processo per la creazione di riferimenti a tipi o risorse di un assembly con nome sicuro è solitamente trasparente all'utente.  È possibile creare tali riferimenti in fase di compilazione \(associazione anticipata\) o in fase di esecuzione.  
  
 Un riferimento in fase di compilazione viene creato quando si indica al compilatore che l'assembly contiene riferimenti espliciti a un altro assembly.  Quando si utilizzano i riferimenti in fase di compilazione, il compilatore riceve automaticamente la chiave pubblica dell'assembly con nome sicuro a cui si fa riferimento e tale chiave viene posizionata nel riferimento di assembly dell'assembly in fase di compilazione.  
  
> [!NOTE]
>  Un assembly con nome sicuro può utilizzare solo tipi di altri assembly con nome sicuro.  In caso contrario, la sicurezza dell'assembly con nome sicuro risulterebbe compromessa.  
  
### Per creare un riferimento in fase di compilazione a un assembly con nome sicuro  
  
1.  Al prompt dei comandi digitare il seguente comando:  
  
     \<*compiler command*\> **\/reference:**\<*assembly name*\>  
  
     In questo comando, *compiler command* corrisponde al comando del compilatore per il linguaggio utilizzato e *assembly name* rappresenta il nome dell'assembly con nome sicuro a cui si fa riferimento.  È possibile utilizzare anche altre opzioni del compilatore, ad esempio l'opzione **\/t:library** per la creazione di un assembly di librerie.  
  
 L'esempio seguente consente di creare un assembly denominato `myAssembly.dll` che fa riferimento a un assembly con nome sicuro denominato `myLibAssembly.dll` da un modulo di codice denominato `myAssembly.cs`.  
  
```  
csc /t:library myAssembly.cs /reference:myLibAssembly.dll  
```  
  
### Per creare un riferimento in fase di esecuzione a un assembly con nome sicuro  
  
1.  Quando si crea un riferimento in fase di esecuzione a un assembly con nome sicuro, ad esempio quando si utilizza il metodo <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> o <xref:System.Reflection.Assembly.GetType%2A?displayProperty=fullName>, è necessario utilizzare il nome visualizzato dell'assembly con nome sicuro a cui si fa riferimento.  La sintassi di un nome visualizzato è la seguente:  
  
     \<*assembly name*\>**,** \<*version number*\>**,** \<*culture*\>**,** \<*public key token*\>  
  
     Di seguito è riportato un esempio.  
  
    ```  
    myDll, Version=1.1.0.0, Culture=en, PublicKeyToken=03689116d3a4ae33   
    ```  
  
     In questo esempio `PublicKeyToken` corrisponde al token di chiave pubblica in formato esadecimale.  Se non è presente alcun valore relativo alle impostazioni cultura, utilizzare `Culture=neutral`.  
  
 Nell'esempio di codice seguente viene illustrato come utilizzare queste informazioni con il metodo <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName>.  
  
 [!code-cpp[Assembly.Load1#3](../../../samples/snippets/cpp/VS_Snippets_CLR/Assembly.Load1/CPP/load2.cpp#3)]
 [!code-csharp[Assembly.Load1#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Assembly.Load1/CS/load2.cs#3)]
 [!code-vb[Assembly.Load1#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Assembly.Load1/VB/load2.vb#3)]  
  
 È possibile stampare il formato esadecimale della chiave pubblica e del token di chiave pubblica per un assembly specifico utilizzando il comando di [Sn.exe \(Nome sicuro\)](../../../docs/framework/tools/sn-exe-strong-name-tool.md) seguente:  
  
 **sn \-Tp \<** *assembly* **\>**  
  
 Se si dispone di un file di chiave pubblica, è possibile utilizzare il seguente comando \(si noti la differenza tra maiuscole e minuscole nell'opzione della riga di comando\):  
  
 **sn \-tp \<** *assembly* **\>**  
  
## Vedere anche  
 [Creazione e utilizzo degli assembly con nome sicuro](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)