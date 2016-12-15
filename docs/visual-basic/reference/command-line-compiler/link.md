---
title: "/link (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "l compiler option [Visual Basic]"
  - "EmbedInteropTypes"
  - "embed interop types [COM Interop]"
  - "-link compiler option [Visual Basic]"
  - "/link compiler option [Visual Basic]"
  - "link compiler option [Visual Basic]"
  - "-l compiler option [Visual Basic]"
  - "/l compiler option [Visual Basic]"
ms.assetid: 1885f24a-86f5-486c-a064-9fb7e455ccec
caps.latest.revision: 27
caps.handback.revision: 27
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# /link (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Indica al compilatore di rendere disponibili al progetto in corso di compilazione tutte le informazioni sui tipi COM presenti nei file specificati.  
  
## Sintassi  
  
```  
/link:fileList  
' -or-  
/l:fileList  
```  
  
## Argomenti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`fileList`|Obbligatorio.  Elenco delimitato da virgole di nomi di file di assembly.  Se il nome del file contiene uno spazio, racchiuderlo tra virgolette.|  
  
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
  
 Per specificare la directory in cui si trova uno o più assembly cui si fa riferimento, utilizzare [\/libpath](../../../visual-basic/reference/command-line-compiler/libpath.md).  
  
 Come l'opzione del compilatore [\/reference](../../../visual-basic/reference/command-line-compiler/reference.md), l'opzione del compilatore `/link` utilizza il file di risposta Vbc.rsp che fa riferimento agli assembly [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] utilizzati di frequente.  Utilizzare l'opzione del compilatore [\/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md) se non si desidera che il compilatore utilizzi il file Vbc.rsp.  
  
 La forma breve di `/link` è `/l`.  
  
## Generics e tipi incorporati  
 Nelle sezioni seguenti vengono descritte le limitazioni all'utilizzo di tipi generici in applicazioni che incorporano tipi di interoperabilità.  
  
### Interfacce generiche  
 Le interfacce generiche incorporate da un assembly di interoperabilità non possono essere utilizzate,  Questa operazione viene mostrata nell'esempio seguente.  
  
 [!code-vb[VbLinkCompiler#1](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_1.vb)]  
  
### Tipi con parametri generici  
 I tipi che dispongono di un parametro generico il cui tipo è incorporato da un assembly di interoperabilità non possono essere utilizzati se tale tipo proviene da un assembly esterno.  La restrizione, tuttavia, non si applica alle interfacce.  Si consideri, ad esempio, l'interfaccia <xref:Microsoft.Office.Interop.Excel.Range> definita nell'assembly <xref:Microsoft.Office.Interop.Excel>.  Se una libreria incorpora tipi di interoperabilità dall'assembly <xref:Microsoft.Office.Interop.Excel> ed espone un metodo che restituisce un tipo generico che dispone di un parametro il cui tipo è l'interfaccia <xref:Microsoft.Office.Interop.Excel.Range>, tale metodo deve restituire un'interfaccia generica, come illustrato nell'esempio di codice seguente.  
  
 [!code-vb[VbLinkCompiler#2](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_2.vb)]  
[!code-vb[VbLinkCompiler#3](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_3.vb)]  
[!code-vb[VbLinkCompiler#4](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_4.vb)]  
  
 Nell'esempio seguente, il codice client può chiamare il metodo che restituisce l'interfaccia generica <xref:System.Collections.IList> senza errori.  
  
 [!code-vb[VbLinkCompiler#5](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_5.vb)]  
  
## Esempio  
 Nel codice riportato di seguito viene compilato il file di origine `OfficeApp.vb` e viene fatto riferimento agli assembly di `COMData1.dll` e `COMData2.dll` per generare `OfficeApp.exe`.  
  
```vb#  
vbc /link:COMData1.dll,COMData2.dll /out:OfficeApp.exe OfficeApp.vb  
```  
  
## Vedere anche  
 [Visual Basic Command\-Line Compiler](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Procedura dettagliata: Incorporamento dei tipi da assembly gestiti](../Topic/Walkthrough:%20Embedding%20Types%20from%20Managed%20Assemblies%20\(C%23%20and%20Visual%20Basic\).md)   
 [\/reference](../../../visual-basic/reference/command-line-compiler/reference.md)   
 [\/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)   
 [\/libpath](../../../visual-basic/reference/command-line-compiler/libpath.md)   
 [Esempi di righe di comando di compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Introduction to COM Interop](../../../visual-basic/programming-guide/com-interop/introduction-to-com-interop.md)