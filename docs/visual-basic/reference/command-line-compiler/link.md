---
title: /Link (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- l compiler option [Visual Basic]
- EmbedInteropTypes
- embed interop types [COM Interop]
- -link compiler option [Visual Basic]
- /link compiler option [Visual Basic]
- link compiler option [Visual Basic]
- -l compiler option [Visual Basic]
- /l compiler option [Visual Basic]
ms.assetid: 1885f24a-86f5-486c-a064-9fb7e455ccec
caps.latest.revision: 27
author: stevehoag
ms.author: shoag
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e98c855f0a0185e9d1b6682df9fc734e9f1f07bc
ms.lasthandoff: 03/13/2017

---
# <a name="link-visual-basic"></a>/link (Visual Basic)
Indica al compilatore di rendere disponibile per il progetto in corso di compilazione informazioni sui tipi COM nei file specificati.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/link:fileList  
' -or-  
/l:fileList  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|---|---|  
|`fileList`|Obbligatorio. Elenco delimitato da virgole di nomi di file di assembly. Se il nome del file contiene uno spazio, racchiudere il nome tra virgolette.|  
  
## <a name="remarks"></a>Note  
 Il `/link` consente di distribuire un'applicazione che incorpora informazioni sul tipo. L'applicazione può quindi utilizzare tipi che implementano le informazioni sul tipo incorporato senza richiedere un riferimento all'assembly di runtime in un assembly di runtime. Se vengono pubblicate diverse versioni dell'assembly di runtime, l'applicazione che contiene le informazioni sul tipo incorporato può funzionare con le diverse versioni senza dover ricompilare. Per un esempio, vedere [procedura dettagliata: incorporamento di tipi da assembly gestiti](http://msdn.microsoft.com/library/b28ec92c-1867-4847-95c0-61adfe095e21).  
  
 Utilizzo di `/link` opzione è particolarmente utile quando si lavora con interoperabilità COM. È possibile incorporare tipi COM in modo che l'applicazione non richiede un assembly di interoperabilità primario (PIA) nel computer di destinazione. Il `/link` opzione indica al compilatore di incorporare le informazioni sul tipo COM dall'assembly di interoperabilità cui viene fatto riferimento nel codice compilato risulta. Il tipo COM è identificato dal valore CLSID (GUID). Di conseguenza, l'applicazione può eseguire in un computer di destinazione che ha installato gli stessi tipi COM con gli stessi valori CLSID. Le applicazioni che consentono di automatizzare Microsoft Office sono un buon esempio. Poiché le applicazioni come Office mantengono in genere lo stesso valore CLSID tra le diverse versioni, l'applicazione può utilizzare i tipi COM di cui viene fatto riferimenti come long come .NET Framework 4 o versione successiva è installato nel computer di destinazione e l'applicazione utilizza metodi, proprietà o eventi che rientrano nei tipi di riferimento COM.  
  
 Il `/link` opzione incorpora solo interfacce, strutture e delegati. Incorporamento di classi COM non è supportata.  
  
> [!NOTE]
>  Quando si crea un'istanza di un tipo COM incorporato nel codice, è necessario creare l'istanza utilizzando l'interfaccia appropriata. Il tentativo di creare un'istanza di un tipo COM incorporato utilizzando la coclasse provoca un errore.  
  
 Per impostare il `/link` opzione [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)], aggiungere un riferimento all'assembly e impostare il `Embed Interop Types` proprietà **true**. Il valore predefinito per il `Embed Interop Types` è **false**.  
  
 Se si collega a un assembly COM (Assembly a) che a sua volta fa riferimento a un altro assembly COM (Assembly B), è necessario anche collegare all'Assembly B se viene soddisfatta una delle operazioni seguenti:  
  
-   Un tipo da Assembly A eredita da un tipo o implementa un'interfaccia dell'Assembly B.  
  
-   Un campo, proprietà, evento o metodo che presenta un tipo di parametro o tipo restituito dall'Assembly B viene richiamato.  
  
 Utilizzare [/libpath](../../../visual-basic/reference/command-line-compiler/libpath.md) per specificare la directory in cui si trova una o più riferimenti agli assembly.  
  
 Come il [/Reference](../../../visual-basic/reference/command-line-compiler/reference.md) l'opzione del compilatore, il `/link` l'opzione del compilatore utilizza il file di risposta Vbc. rsp, i riferimenti utilizzati [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] assembly. Utilizzare il [/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md) l'opzione del compilatore se non si desidera al compilatore di utilizzare tale file.  
  
 La versione abbreviata di `/link` è `/l`.  
  
## <a name="generics-and-embedded-types"></a>Generics e tipi incorporati  
 Nelle sezioni seguenti vengono descrivono le limitazioni all'utilizzo di tipi generici nelle applicazioni che incorporano tipi di interoperabilità.  
  
### <a name="generic-interfaces"></a>Interfacce generiche  
 Impossibile utilizzare le interfacce generiche che sono incorporate da un assembly di interoperabilità. come illustrato nell'esempio riportato di seguito.  
  
 [!code-vb[VbLinkCompiler n.&1;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_1.vb)]  
  
### <a name="types-that-have-generic-parameters"></a>Tipi che dispongono di parametri generici  
 Tipi che dispongono di un parametro generico il cui tipo è incorporato a un assembly di interoperabilità non possono essere utilizzati se tale tipo proviene da un assembly esterno. Questa restrizione non si applica alle interfacce. Si consideri ad esempio il <xref:Microsoft.Office.Interop.Excel.Range>interfaccia definita nel <xref:Microsoft.Office.Interop.Excel>assembly.</xref:Microsoft.Office.Interop.Excel> </xref:Microsoft.Office.Interop.Excel.Range> Se una libreria incorpora tipi di interoperabilità dal <xref:Microsoft.Office.Interop.Excel>assembly ed espone un metodo che restituisce un tipo generico con un parametro il cui tipo è il <xref:Microsoft.Office.Interop.Excel.Range>interfaccia, che metodo deve restituire un'interfaccia generica, come illustrato nell'esempio di codice seguente.</xref:Microsoft.Office.Interop.Excel.Range> </xref:Microsoft.Office.Interop.Excel>  
  
 [!code-vb[VbLinkCompiler n.&2;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_2.vb)]  
[!code-vb[VbLinkCompiler n.&3;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_3.vb)]  
[!code-vb[VbLinkCompiler n.&4;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_4.vb)]  
  
 Nell'esempio seguente, il codice client può chiamare il metodo che restituisce il <xref:System.Collections.IList>interfaccia generica senza errori.</xref:System.Collections.IList>  
  
 [!code-vb[VbLinkCompiler n.&5;](../../../visual-basic/reference/command-line-compiler/codesnippet/VisualBasic/link_5.vb)]  
  
## <a name="example"></a>Esempio  
 Il codice seguente consente di compilare file di origine `OfficeApp.vb` e fare riferimento agli assembly da `COMData1.dll` e `COMData2.dll` per produrre `OfficeApp.exe`.  
  
```vb  
vbc /link:COMData1.dll,COMData2.dll /out:OfficeApp.exe OfficeApp.vb  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Procedura dettagliata: Incorporamento dei tipi da assembly gestiti](http://msdn.microsoft.com/library/b28ec92c-1867-4847-95c0-61adfe095e21)   
 [/Reference (Visual Basic)](../../../visual-basic/reference/command-line-compiler/reference.md)   
 [/noconfig](../../../visual-basic/reference/command-line-compiler/noconfig.md)   
 [/LIBPATH](../../../visual-basic/reference/command-line-compiler/libpath.md)   
 [Esempi di righe di comando compilazione](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)   
 [Introduzione all'interoperabilità COM](../../../visual-basic/programming-guide/com-interop/introduction-to-com-interop.md)
