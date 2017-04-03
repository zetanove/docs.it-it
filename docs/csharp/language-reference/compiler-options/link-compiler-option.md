---
title: -link (opzioni del compilatore C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- /l compiler option [C#]
- /link compiler option [C#]
- -l compiler option [C#]
- EmbedInteropTypes
- l compiler option [C#]
- embed interop types [COM Interop]
- -link compiler option [C#]
- link compiler option [C#]
ms.assetid: 00da70c6-9ea1-43c2-86f2-aa7f26c03475
caps.latest.revision: 13
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3096dd622a0b7c5fae13412a95322b934bd38b76
ms.lasthandoff: 03/13/2017

---
# <a name="link-c-compiler-options"></a>/link (opzioni del compilatore C#)
Indica al compilatore di rendere disponibili al progetto in fase di compilazione le informazioni sui tipi COM presenti negli assembly specificati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/link:fileList  
// -or-  
/l:fileList  
```  
  
## <a name="arguments"></a>Argomenti  
 `fileList`  
 Obbligatorio. Elenco di nomi di file di assembly delimitato da virgole. Se il nome del file contiene uno spazio, racchiudere il nome tra virgolette.  
  
## <a name="remarks"></a>Note  
 L'opzione `/link`consente di distribuire un'applicazione in cui sono incorporate informazioni sul tipo. L'applicazione può quindi usare i tipi in un assembly di runtime che implementano le informazioni sul tipo incorporate senza dovere far riferimento all'assembly di runtime. Se vengono pubblicate diverse versioni dell'assembly di runtime, l'applicazione che contiene le informazioni sul tipo incorporate può funzionare con le diverse versioni senza che sia necessaria la ricompilazione. Per un esempio, vedere [Procedura dettagliata: incorporamento dei tipi da assembly gestiti](http://msdn.microsoft.com/library/b28ec92c-1867-4847-95c0-61adfe095e21).  
  
 L'opzione `/link` è particolarmente utile quando si usa l'interoperabilità COM. È possibile incorporare tipi COM in modo che per l'applicazione non sia più necessario un assembly di interoperabilità primario nel computer di destinazione. L'opzione `/link` indica al compilatore di incorporare le informazioni sul tipo COM dall'assembly di interoperabilità a cui si fa riferimento nel codice compilato risultante. Il tipo COM viene identificato dal valore CLSID (GUID). Di conseguenza, l'applicazione può essere eseguita in un computer di destinazione in cui sono stati installati gli stessi tipi COM con gli stessi valori CLSID. Le applicazioni che consentono di automatizzare Microsoft Office costituiscono un valido esempio. Poiché applicazioni come Office mantengono in genere lo stesso valore CLSID in versioni diverse, l'applicazione può usare i tipi COM a cui si fa riferimento purché .NET Framework 4 o versioni successive sia installato nel computer di destinazione e l'applicazione usi metodi, proprietà o eventi inclusi nei tipi COM a cui si fa riferimento.  
  
 L'opzione `/link` incorpora solo interfacce, strutture e delegati. L'incorporamento di classi COM non è supportato.  
  
> [!NOTE]
>  Quando si crea un'istanza di un tipo COM incorporato nel codice, è necessario creare l'istanza usando l'interfaccia appropriata. Il tentativo di creare un'istanza di un tipo COM incorporato usando la coclasse genera un errore.  
  
 Per impostare l'opzione `/link` in [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)], aggiungere un riferimento all'assembly e impostare la proprietà `Embed Interop Types` su **true**. Il valore predefinito della proprietà `Embed Interop Types` è **false**.  
  
 Se si collega a un assembly COM (assembly A) che fa riferimento a un altro assembly COM (assembly B), è necessario eseguire il collegamento anche all'assembly B se si verifica una delle condizioni seguenti:  
  
-   Un tipo dell'assembly A eredita da un tipo o implementa un'interfaccia dall'assembly B.  
  
-   Viene richiamato un campo, una proprietà, un evento o un metodo che presenta un tipo restituito o un tipo di parametro proveniente dall'assembly B.  
  
 Come l'opzione del compilatore [/reference](../../../csharp/language-reference/compiler-options/reference-compiler-option.md), anche l'opzione `/link` usa il file di risposta csc.rsp che fa riferimento agli assembly [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] di uso più frequente. Usare l'opzione del compilatore [/noconfig](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md) se non si vuole che il compilatore usi il file csc.rsp.  
  
 La forma breve di `/link` è `/l`.  
  
## <a name="generics-and-embedded-types"></a>Generics e tipi incorporati  
 Nelle sezioni seguenti vengono descritte le limitazioni all'uso di tipi generici in applicazioni che incorporano tipi di interoperabilità.  
  
### <a name="generic-interfaces"></a>Interfacce generiche  
 Le interfacce generiche incorporate da un assembly di interoperabilità non possono essere usate, come illustrato nell'esempio riportato di seguito.  
  
 [!code-cs[VbLinkCompilerCS#1](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_1.cs)]  
  
### <a name="types-that-have-generic-parameters"></a>Tipi con parametri generici  
 I tipi che hanno un parametro generico il cui tipo è incorporato da un assembly di interoperabilità non possono essere usati se tale tipo proviene da un assembly esterno. Tale restrizione non si applica tuttavia alle interfacce. Si consideri ad esempio l'interfaccia <xref:Microsoft.Office.Interop.Excel.Range> definita nell'assembly <xref:Microsoft.Office.Interop.Excel>. Se una libreria incorpora tipi di interoperabilità dall'assembly <xref:Microsoft.Office.Interop.Excel> ed espone un metodo che restituisce un tipo generico che ha un parametro il cui tipo è l'interfaccia <xref:Microsoft.Office.Interop.Excel.Range>, tale metodo deve restituire un'interfaccia generica, come illustrato nell'esempio di codice seguente.  
  
 [!code-cs[VbLinkCompilerCS#2](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_2.cs)]  
[!code-cs[VbLinkCompilerCS#3](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_3.cs)]  
[!code-cs[VbLinkCompilerCS#4](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_4.cs)]  
  
 Nell'esempio seguente il codice client può chiamare il metodo che restituisce l'interfaccia generica <xref:System.Collections.IList> senza errori.  
  
 [!code-cs[VbLinkCompilerCS#5](../../../csharp/language-reference/compiler-options/codesnippet/CSharp/link-compiler-option_5.cs)]  
  
## <a name="example"></a>Esempio  
 Nel codice riportato di seguito viene compilato il file di origine `OfficeApp.cs` e viene fatto riferimento agli assembly di `COMData1.dll` e `COMData2.dll` per generare `OfficeApp.exe`.  
  
```csharp  
csc /link:COMData1.dll,COMData2.dll /out:OfficeApp.exe OfficeApp.cs  
```  
  
## <a name="see-also"></a>Vedere anche  
 [C# Compiler Options](../../../csharp/language-reference/compiler-options/index.md)  (Opzioni del compilatore C#)  
 [Procedura dettagliata: incorporamento dei tipi da assembly gestiti](http://msdn.microsoft.com/library/b28ec92c-1867-4847-95c0-61adfe095e21)   
 [/reference (opzioni del compilatore C#)](../../../csharp/language-reference/compiler-options/reference-compiler-option.md)   
 [/noconfig (opzioni del compilatore C#)](../../../csharp/language-reference/compiler-options/noconfig-compiler-option.md)   
 [Compilazione dalla riga di comando con csc.exe](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)   
 [Cenni preliminari sull'interoperabilità](../../../csharp/programming-guide/interop/interoperability-overview.md)
