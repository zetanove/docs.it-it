---
title: "Compilatore XSLT (xsltc.exe) | Microsoft Docs"
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
ms.assetid: 672a5ac8-8305-4d28-ba10-11089c2c0924
caps.latest.revision: 2
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 2
---
# Compilatore XSLT (xsltc.exe)
Il compilatore XSLT \(xsltc.exe\) consente di compilare fogli di stile XSLT e di generare un assembly.  Il foglio di stile compilato può quindi essere passato direttamente nel metodo <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Type%29?displayProperty=fullName>.  Non è possibile generare assembly firmati con xsltc.exe.  
  
 Lo strumento xsltc.exe è incluso in Visual Studio 2008.  Per altre informazioni, visitare l'[Area download Microsoft](http://go.microsoft.com/fwlink/?LinkId=89463).  
  
## Sintassi  
  
```  
xsltc [options] [/class:<name>] <sourceFile> [[/class:<name>] <sourceFile>...]  
```  
  
## Argomento  
  
|Argomento|Descrizione|  
|---------------|-----------------|  
|`sourceFile`|Consente di specificare il nome del foglio di stile.  Il foglio di stile deve essere un file locale o deve essere disponibile nella Intranet.|  
  
## Opzioni  
  
|Opzione|Descrizione|  
|-------------|-----------------|  
|`/c[lass]:` `name`|Consente di specificare il nome della classe del foglio di stile successivo.  Il nome della classe può essere completo.<br /><br /> Per impostazione predefinita, il nome della classe corrisponde al nome del foglio di stile.  Ad esempio, se viene compilato il foglio di stile customers.xsl, il nome predefinito della classe sarà customers.|  
|`/debug[`\+&#124;\-`]`|Consente di specificare se generare le informazioni per il debug.<br /><br /> Se si specifica `+` o `/debug`, il compilatore genererà le informazioni per il debug e le inserirà in un file del database di programma con estensione PDB.  Il nome del file PDB generato è `assemblyName`.pdb.<br /><br /> Se si specifica l'argomento `-`, che è attivo quando `/debug` non è specificato, non verranno create informazioni per il debug.  Verrà generato un assembly finale. **Note:**  La compilazione in modalità di debug può influire significativamente sulle prestazioni di XSLT.|  
|`/help`|Visualizza la sintassi e le opzioni di comando dello strumento.|  
|`/nologo`|Consente di disattivare la visualizzazione del messaggio di copyright del compilatore.|  
|`/platform:` `string`|Consente di specificare le piattaforme in cui è possibile eseguire l'assembly.  Di seguito sono illustrati i valori di piattaforma validi:<br /><br /> `x86`: consente di compilare l'assembly in modo che sia possibile eseguirlo con la versione x86 compatibile di Common Language Runtime a 32 bit.<br /><br /> `x64`: consente di compilare l'assembly in modo che sia possibile eseguirlo con Common Language Runtime a 64 bit su un computer che supporta il set di istruzioni AMD64 o EM64T.<br /><br /> [!INCLUDE[vcpritanium](../../../../includes/vcpritanium-md.md)]: consente di compilare l'assembly in modo che sia possibile eseguirlo con Common Language Runtime a 64 bit su un computer dotato di un processore [!INCLUDE[vcpritanium](../../../../includes/vcpritanium-md.md)].<br /><br /> `anycpu`: consente di compilare l'assembly in modo che sia possibile eseguirlo su qualsiasi piattaforma.  Questa è l'impostazione predefinita.|  
|`/out:` `assemblyName`|Specifica il nome dell'assembly che viene restituito come output.  Per impostazione predefinita, il nome dell'assembly corrisponde al nome del foglio di stile principale o a quello del primo foglio di stile se esistono più fogli.<br /><br /> Se il foglio di stile contiene script, questi vengono salvati in un assembly distinto.  I nomi degli assembly di script vengono generati dal nome dell'assembly principale.  Ad esempio, se è stato specificato CustOrders.dll come nome dell'assembly, al primo assembly di script verrà assegnato il nome CustOrders\_Script1.dll.|  
|`/settings:` `document+-, script+-, DTD+-,`|Consente di specificare se consentire l'uso di funzioni `document()`, script XSLT, o DTD \(Document Type Definition\) nel foglio di stile.<br /><br /> Per impostazione predefinita, il supporto per DTD, per la funzione `document()` e gli script è disabilitato.|  
|`@` `file`|Consente di specificare un file che contiene le opzioni del compilatore.|  
|`?`|Visualizza la sintassi e le opzioni di comando dello strumento.|  
  
## Note  
 Le soluzioni XSLT possono essere costituite da più moduli del foglio di stile.  Lo strumento xsltc.exe genera assembly dai fogli di stile.  Gli assembly possono quindi essere passati direttamente nel metodo <xref:System.Xml.Xsl.XslCompiledTransform.Load%28System.Type%29?displayProperty=fullName>.  Tale comportamento può contribuire a ridurre i costi correlati alle prestazioni in alcuni scenari di distribuzione di XSLT.  
  
> [!NOTE]
>  È inoltre necessario includere anche l'assembly compilato come riferimento nell'applicazione.  
  
 Lo strumento xsltc.exe non convalida i nomi di classe \(`/class:``name`\) o di assembly \(`/out:``assemblyName`\).  Se i nomi non sono validi, CLR genera errori.  
  
## Esempi  
 Il comando seguente consente di compilare il foglio di stile e di creare un assembly denominato booksort.dll.  
  
```  
xsltc booksort.xsl  
```  
  
 Il comando seguente consente di compilare il foglio di stile e di creare un assembly e un file PDB denominati rispettivamente booksort.dll e booksort.pdb.  
  
```  
xsltc booksort.xsl /debug  
```  
  
 Il comando seguente consente di compilare un foglio di stile che contiene l'elemento msxsl:script e di creare due assembly denominati calc.dll e calc\_Script1.dll.  
  
```  
xsltc /settings:script+ calc.xsl  
```  
  
 Il comando seguente consente di abilitare il supporto per gli script e per l'elaborazione DTD, nonché di creare due assembly denominati myTest.dll e myTest\_Script1.dll.  
  
```  
xsltc /settings:DTD+,script+ /out:myTest calc.xsl  
```  
  
 Il comando seguente consente di compilare due moduli di fogli di stile e di creare un unico assembly denominato booksort.dll.  
  
```  
xsltc booksort.xsl output.xsl  
```  
  
## Vedere anche  
 <xref:System.Xml.Xsl.XslCompiledTransform>   
 [Procedura: eseguire una trasformazione XSLT utilizzando un assembly](../../../../docs/standard/data/xml/how-to-perform-an-xslt-transformation-by-using-an-assembly.md)   
 [Trasformazioni XSLT](../../../../docs/standard/data/xml/xslt-transformations.md)