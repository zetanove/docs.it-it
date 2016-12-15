---
title: "/link (C# Compiler Options) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "/l compiler option [C#]"
  - "/link compiler option [C#]"
  - "-l compiler option [C#]"
  - "EmbedInteropTypes"
  - "l compiler option [C#]"
  - "embed interop types [COM Interop]"
  - "-link compiler option [C#]"
  - "link compiler option [C#]"
ms.assetid: 00da70c6-9ea1-43c2-86f2-aa7f26c03475
caps.latest.revision: 13
caps.handback.revision: 13
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# /link (C# Compiler Options)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Indica al compilatore di rendere disponibili al progetto in corso di compilazione tutte le informazioni sui tipi COM presenti nei file specificati.  
  
## Sintassi  
  
```  
/link:fileList  
// -or-  
/l:fileList  
```  
  
## Argomenti  
 `fileList`  
 Obbligatorio.  Elenco delimitato da virgole di nomi di file di assembly.  Se il nome del file contiene uno spazio, racchiuderlo tra virgolette.  
  
## Note  
 L'opzione `/link` consente di distribuire un'applicazione che ha incorporato informazioni sul tipo.  L'applicazione può quindi utilizzare i tipi in un assembly di runtime che implementa le informazioni sul tipo incorporate senza richiedere un riferimento all'assembly di runtime.  Se vengono pubblicate diverse versioni dell'assembly di runtime, l'applicazione che contiene le informazioni sul tipo incorporate può funzionare con le diverse versioni senza che sia necessaria la ricompilazione.  Per un esempio, vedere [Procedura dettagliata: Incorporamento dei tipi da assembly gestiti](../Topic/Walkthrough:%20Embedding%20Types%20from%20Managed%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md).  
  
 L'utilizzo dell'opzione `/link` è particolarmente utile quando si utilizza l'interoperabilità COM.  È possibile incorporare tipi COM in modo che l'applicazione non richieda più un assembly di interoperabilità primario \(PIA\) nel computer di destinazione.  L'opzione `/link` indica al compilatore di incorporare le informazioni sul tipo COM dall'assembly di interoperabilità a cui si fa riferimento nel codice compilato risultante.  Il tipo COM viene identificato dal valore CLSID \(GUID\).  Di conseguenza, l'applicazione può essere eseguita in un computer di destinazione in cui sono stati installati gli stessi tipi COM con gli stessi valori CLSID.  Le applicazioni che consentono di automatizzare Microsoft Office costituiscono un valido esempio.  Poiché applicazioni come Office mantengono in genere lo stesso valore CLSID in versioni diverse, l'applicazione può utilizzare i tipi COM a cui si fa riferimento purché .NET Framework 4 o versioni successive sia installato nel computer di destinazione e l'applicazione utilizzi metodi, proprietà o eventi inclusi nei tipi COM a cui si fa riferimento.  
  
 L'opzione `/link` incorpora solo interfacce, strutture e delegati.  L'incorporamento di classi COM non è supportato.  
  
> [!NOTE]
>  Quando si crea un'istanza di un tipo COM incorporato nel codice, è necessario creare l'istanza utilizzando l'interfaccia appropriata.  Il tentativo di creare un'istanza di un tipo COM incorporato utilizzando la coclasse provoca un errore.  
  
 Per impostare l'opzione `/link` in [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)], aggiungere un riferimento all'assembly e impostare la proprietà `Embed Interop Types` su **true**.  Il valore predefinito della proprietà `Embed Interop Types` è **false**.  
  
 Se si esegue il collegamento a un assembly COM \(assembly A\) che fa riferimento a un altro assembly COM \(assembly B\), è necessario eseguire il collegamento anche all'assembly B se si verifica una delle seguenti condizioni:  
  
-   Se un tipo dell'assembly A eredita da un tipo o implementa un'interfaccia dall'assembly B.  
  
-   Se viene richiamato un campo, una proprietà, un evento o un metodo che presenta un tipo restituito o un tipo di parametro proveniente dall'assembly B.  
  
 Come l'opzione del compilatore [\/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md), l'opzione del compilatore `/link` utilizza il file di risposta Csc.rsp che fa riferimento agli assembly [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] utilizzati di frequente.  Utilizzare l'opzione del compilatore [\/noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md) se non si desidera che il compilatore utilizzi il file Csc.rsp.  
  
 La forma breve di `/link` è `/l`.  
  
## Generics e tipi incorporati  
 Nelle sezioni seguenti vengono descritte le limitazioni all'utilizzo di tipi generici in applicazioni che incorporano tipi di interoperabilità.  
  
### Interfacce generiche  
 Le interfacce generiche incorporate da un assembly di interoperabilità non possono essere utilizzate,  Questa operazione viene mostrata nell'esempio seguente.  
  
 [!code-cs[VbLinkCompilerCS#1](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_1.cs)]  
  
### Tipi con parametri generici  
 I tipi che dispongono di un parametro generico il cui tipo è incorporato da un assembly di interoperabilità non possono essere utilizzati se tale tipo proviene da un assembly esterno.  La restrizione, tuttavia, non si applica alle interfacce.  Si consideri, ad esempio, l'interfaccia <xref:Microsoft.Office.Interop.Excel.Range> definita nell'assembly <xref:Microsoft.Office.Interop.Excel>.  Se una libreria incorpora tipi di interoperabilità dall'assembly <xref:Microsoft.Office.Interop.Excel> ed espone un metodo che restituisce un tipo generico che dispone di un parametro il cui tipo è l'interfaccia <xref:Microsoft.Office.Interop.Excel.Range>, tale metodo deve restituire un'interfaccia generica, come illustrato nell'esempio di codice seguente.  
  
 [!code-cs[VbLinkCompilerCS#2](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_2.cs)]  
[!code-cs[VbLinkCompilerCS#3](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_3.cs)]  
[!code-cs[VbLinkCompilerCS#4](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_4.cs)]  
  
 Nell'esempio seguente, il codice client può chiamare il metodo che restituisce l'interfaccia generica <xref:System.Collections.IList> senza errori.  
  
 [!code-cs[VbLinkCompilerCS#5](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_5.cs)]  
  
## Esempio  
 Nel codice riportato di seguito viene compilato il file di origine `OfficeApp.cs` e viene fatto riferimento agli assembly di `COMData1.dll` e `COMData2.dll` per generare `OfficeApp.exe`.  
  
```c#  
csc /link:COMData1.dll,COMData2.dll /out:OfficeApp.exe OfficeApp.cs  
```  
  
## Vedere anche  
 [C\# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)   
 [Procedura dettagliata: Incorporamento dei tipi da assembly gestiti](../Topic/Walkthrough:%20Embedding%20Types%20from%20Managed%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)   
 [\/reference \(Import Metadata\)](../../../csharp/language-reference/compiler-options/reference-compiler-option.md)   
 [\/noconfig \(Ignore csc.rsp\)](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md)   
 [Command\-line Building With csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)   
 [Cenni preliminari sull'interoperabilità](../../../csharp/programming-guide/interop/interoperability-overview.md)