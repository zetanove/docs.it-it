---
title: "Specifying Fully Qualified Type Names | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "names [.NET Framework], fully qualified type names"
  - "reflection, fully qualified type names"
  - "names [.NET Framework], assemblies"
  - "tokens"
  - "BNF"
  - "assemblies [.NET Framework], names"
  - "Backus-Naur form"
  - "languages, BNF grammar"
  - "fully qualified type names"
  - "type names"
  - "special characters"
  - "IDENTIFIER"
ms.assetid: d90b1e39-9115-4f2a-81c0-05e7e74e5580
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# Specifying Fully Qualified Type Names
Per ottenere un input valido per diverse operazioni di reflection, è necessario specificare i nomi dei tipi.  Un nome di tipo completo è costituito dalla specifica di un nome di assembly, dalla specifica di uno spazio dei nomi e da un nome di tipo.  Le specifiche dei nomi di tipi vengono utilizzate da metodi come <xref:System.Type.GetType%2A?displayProperty=fullName>, <xref:System.Reflection.Module.GetType%2A?displayProperty=fullName>, <xref:System.Reflection.Emit.ModuleBuilder.GetType%2A?displayProperty=fullName> e <xref:System.Reflection.Assembly.GetType%2A?displayProperty=fullName>.  
  
## Grammatica Backus\-Naur Form per nomi di tipi  
 La Backus\-Naur Form \(BNF\) definisce la sintassi di linguaggi formali.  Nella tabella che segue sono elencate le regole lessicali BNF che consentono di riconoscere un input valido.  I terminal \(elementi non ulteriormente riducibili\) sono riportati in maiuscolo.  I non terminal \(elementi ulteriormente riducibili\) sono riportati come combinazione di lettere maiuscole e minuscole o in stringhe racchiuse tra virgolette. In quest'ultimo caso le virgolette \("\) non fanno parte della sintassi.  Il carattere barra verticale \(&#124;\) denota regole che presentano sottoregole.  
  
|Grammatica BNF per i nomi di tipo completi|  
|------------------------------------------------|  
|TypeSpec                          :\=   ReferenceTypeSpec<br /><br /> &#124;     SimpleTypeSpec|  
|ReferenceTypeSpec            :\=   SimpleTypeSpec '&'|  
|SimpleTypeSpec                :\=   PointerTypeSpec<br /><br /> &#124;     ArrayTypeSpec<br /><br /> &#124;     TypeName|  
|PointerTypeSpec                :\=   SimpleTypeSpec '\*'|  
|ArrayTypeSpec                  :\=   SimpleTypeSpec '\[ReflectionDimension\]'<br /><br /> &#124;     SimpleTypeSpec '\[ReflectionEmitDimension\]'|  
|ReflectionDimension           :\=   '\*'<br /><br /> &#124;     ReflectionDimension ',' ReflectionDimension<br /><br /> &#124;     NOTOKEN|  
|ReflectionEmitDimension    :\=   '\*'<br /><br /> &#124;     Number '..' Numero<br /><br /> &#124;     Number '…'<br /><br /> &#124;     ReflectionDimension ',' ReflectionDimension<br /><br /> &#124;     NOTOKEN|  
|Number                            :\=   \[0\-9\]\+|  
|TypeName                         :\=   NamespaceTypeName<br /><br /> &#124;     NamespaceTypeName ',' AssemblyNameSpec|  
|NamespaceTypeName        :\=   NestedTypeName<br /><br /> &#124;     NamespaceSpec '.' NestedTypeName|  
|NestedTypeName               :\=   IDENTIFIER<br /><br /> &#124;     NestedTypeName '\+' IDENTIFIER|  
|NamespaceSpec                 :\=   IDENTIFIER<br /><br /> &#124;     NamespaceSpec '.' IDENTIFIER|  
|AssemblyNameSpec           :\=   IDENTIFIER<br /><br /> &#124;     IDENTIFIER ',' AssemblyProperties|  
|AssemblyProperties            :\=   AssemblyProperty<br /><br /> &#124;     AssemblyProperties ',' AssemblyProperty|  
|AssemblyProperty              :\=   AssemblyPropertyName '\=' AssemblyPropertyValue|  
  
## Specifica di caratteri speciali  
 In TypeName IDENTIFIER rappresenta qualsiasi nome valido stabilito in base alle regole di un linguaggio.  
  
 Utilizzare la barra rovesciata \(\\\) come carattere di escape per separare i seguenti token, quando vengono utilizzati in IDENTIFIER.  
  
|Token|Significato|  
|-----------|-----------------|  
|\\,|Separatore di assembly|  
|\\\+|Separatore di tipo annidato|  
|\\&|Tipo di riferimento|  
|\\\*|Tipo di puntatore|  
|\\\[|Delimitatore delle dimensioni della matrice|  
|\\\]|Delimitatore delle dimensioni della matrice|  
|\\.|Utilizzare la barra rovesciata prima di un punto solo se questo viene utilizzato in una specifica di matrice.  In NamespaceSpec non è previsto l'uso di barre rovesciate prima dei punti.|  
|\\\\|Utilizzare la barra rovesciata quando richiesta come stringa letterale.|  
  
 Tenere presente che gli spazi sono rilevanti in tutti i componenti TypeSpec ad eccezione di AssemblyNameSpec.  In AssemblyNameSpec gli spazi che precedono il separatore "," sono rilevanti, mentre quelli che lo seguono vengono ignorati.  
  
 Le classi Reflection, quali <xref:System.Type.FullName%2A?displayProperty=fullName>, restituiscono il nome alternativo in modo che possa essere utilizzato in una chiamata a <xref:System.Type.GetType%2A>, ad esempio in `MyType.GetType(myType.FullName)`.  
  
 Il nome completo di un tipo è ad esempio `Ozzy.OutBack.Kangaroo+Wallaby,MyAssembly`.  
  
 Se lo spazio dei nomi fosse `Ozzy.Out+Back`, il segno più \(\+\) dovrebbe essere preceduto da una barra rovesciata.  In caso contrario, verrebbe interpretato dal parser come operatore di annidamento.  Con Reflection la stringa viene riprodotta come `Ozzy.Out\+Back.Kangaroo+Wallaby,MyAssembly`.  
  
## Specifica dei nomi degli assembly  
 Le informazioni minime richieste per la specifica del nome di un assembly sono rappresentate dal nome testuale \(IDENTIFIER\) dell'assembly.  Dopo l'IDENTIFIER è possibile aggiungere un elenco di coppie di valori\/proprietà separate da virgole, come descritto nella tabella che segue.  Per l'assegnazione del nome dell'IDENTIFIER attenersi alle regole per l'assegnazione dei nomi di file.  IDENTIFIER non prevede distinzioni tra maiuscole e minuscole.  
  
|Nome della proprietà|Descrizione|Valori ammessi|  
|--------------------------|-----------------|--------------------|  
|**Versione**|Numero di versione dell'assembly|*Major.Minor.Build.Revision*, dove *Major*, *Minor*, *Build* e *Revision* sono valori interi compresi tra 0 e 65535.|  
|**PublicKey**|Chiave pubblica completa|Valore string della chiave pubblica completa in formato esadecimale.  Specificare un riferimento null \(**Nothing** in Visual Basic\) per indicare un assembly privato in modo esplicito.|  
|**PublicKeyToken**|Token di chiave pubblica \(hash a 8 byte della chiave pubblica completa\)|Valore string del token della chiave pubblica in formato esadecimale.  Specificare un riferimento null \(**Nothing** in Visual Basic\) per indicare un assembly privato in modo esplicito.|  
|**Impostazioni cultura**|Impostazioni cultura dell'assembly|Impostazioni cultura dell'assembly in formato RFC\-1766, o "neutral" per assembly non dipendenti dalla lingua \(non satellite\).|  
|**Personalizzato**|Oggetto binario di grandi dimensioni personalizzato \(BLOB\).  Utilizzato attualmente solo in assembly generati dal [Generatore di immagini native \(Ngen\)](../../../docs/framework/tools/ngen-exe-native-image-generator.md).|Stringa personalizzata utilizzata dallo strumento generatore di immagini native per notificare alla cache dell'assembly che l'assembly da installare è un'immagine nativa e pertanto deve essere installato nella cache delle immagini native.  Definita anche come stringa zap.|  
  
 Nell'esempio riportato di seguito viene illustrato **AssemblyName** per un assembly con nome semplice e impostazioni cultura predefinite.  
  
```csharp  
com.microsoft.crypto, Culture=""   
```  
  
 Nell'esempio riportato di seguito viene illustrato un riferimento completamente specificato per un assembly con nome sicuro e impostazioni cultura "en".  
  
```csharp  
com.microsoft.crypto, Culture=en, PublicKeyToken=a5d015c7d5a0b012,  
    Version=1.0.0.0   
```  
  
 Di seguito sono riportati esempi di **AssemblyName** parzialmente specificati che possono essere soddisfatti da un assembly con nome semplice o con nome sicuro.  
  
```csharp  
com.microsoft.crypto  
com.microsoft.crypto, Culture=""  
com.microsoft.crypto, Culture=en   
```  
  
 Di seguito sono riportati esempi di **AssemblyName** parzialmente specificati che devono essere soddisfatti da un assembly con nome semplice.  
  
```csharp  
com.microsoft.crypto, Culture="", PublicKeyToken=null   
com.microsoft.crypto, Culture=en, PublicKeyToken=null  
```  
  
 Di seguito sono riportati esempi di **AssemblyName** parzialmente specificati che devono essere soddisfatti da un assembly con nome sicuro.  
  
```csharp  
com.microsoft.crypto, Culture="", PublicKeyToken=a5d015c7d5a0b012  
com.microsoft.crypto, Culture=en, PublicKeyToken=a5d015c7d5a0b012,  
    Version=1.0.0.0  
```  
  
## Specifica dei puntatori  
 SimpleTypeSpec\* rappresenta un puntatore non gestito.  Per ottenere ad esempio un puntatore per il tipo MyType, utilizzare `Type.GetType("MyType*")`.  Per ottenere un puntatore a un puntatore per il tipo MyType, utilizzare `Type.GetType("MyType**")`.  
  
## Specifica dei riferimenti  
 SimpleTypeSpec & rappresenta un riferimento o puntatore gestito.  Per ottenere ad esempio un riferimento per il tipo MyType, utilizzare `Type.GetType("MyType &")`.  Tenere presente che, a differenza dei puntatori, i riferimenti sono limitati a un solo livello.  
  
## Specifica delle matrici  
 Nella grammatica BNF, ReflectionEmitDimension è valido solo per definizioni di tipo incomplete recuperate tramite <xref:System.Reflection.Emit.ModuleBuilder.GetType%2A?displayProperty=fullName>.  Per definizioni di tipo incomplete si intendono oggetti <xref:System.Reflection.Emit.TypeBuilder> costruiti utilizzando [Reflection.Emit](frlrfSystemReflectionEmit) ma sui quali non è stato chiamato <xref:System.Reflection.Emit.TypeBuilder.CreateType%2A?displayProperty=fullName>.  È possibile utilizzare ReflectionDimension per recuperare qualsiasi definizione di tipo completata, ovvero un tipo caricato.  
  
 Per accedere alle matrici tramite reflection, è necessario specificare il numero di dimensioni della matrice.  
  
-   `Type.GetType("MyArray[]")` ottiene una matrice unidimensionale con limite inferiore pari a 0.  
  
-   `Type.GetType("MyArray[*]")` ottiene una matrice unidimensionale con limite inferiore sconosciuto.  
  
-   `Type.GetType("MyArray[][]")` ottiene una matrice di una matrice bidimensionale.  
  
-   `Type.GetType("MyArray[*,*]")` e `Type.GetType("MyArray[,]")` ottiene una matrice rettangolare bidimensionale con limiti inferiori sconosciuti.  
  
 Dal punto di vista del runtime le due notazioni `MyArray[] != MyArray[*]` sono equivalenti ma per matrici multidimensionali.  `Type.GetType("MyArray [,]") == Type.GetType("MyArray[*,*]")` viene pertanto valutata come **true**.  
  
 Per **ModuleBuilder.GetType**, `MyArray[0..5]` indica una matrice unidimensionale con dimensione pari a 6 e limite inferiore pari a 0.  `MyArray[4…]` indica invece una matrice unidimensionale di dimensioni sconosciute e limite inferiore pari a 4.  
  
## Vedere anche  
 <xref:System.Reflection.AssemblyName>   
 <xref:System.Reflection.Emit.ModuleBuilder>   
 <xref:System.Reflection.Emit.TypeBuilder>   
 <xref:System.Type.FullName%2A?displayProperty=fullName>   
 <xref:System.Type.GetType%2A?displayProperty=fullName>   
 <xref:System.Type.AssemblyQualifiedName%2A?displayProperty=fullName>   
 [Viewing Type Information](../../../docs/framework/reflection-and-codedom/viewing-type-information.md)