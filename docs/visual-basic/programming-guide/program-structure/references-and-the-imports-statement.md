---
title: I riferimenti e istruzione Imports (Visual Basic) | Documenti di Microsoft
ms.custom: 
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
- assemblies [Visual Basic], namespaces
- references, assembly
- namespaces, assemblies
- referencing assemblies
- Imports statement, referencing assemblies
- assemblies [Visual Basic], references
ms.assetid: 38149bd4-0a6f-4b31-b5f8-94a8c33f1600
caps.latest.revision: 12
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: 283a27e7703b31a9aeed8f7e4104e89b7ff78525
ms.lasthandoff: 03/13/2017

---
# <a name="references-and-the-imports-statement-visual-basic"></a>Riferimenti e istruzione Imports (Visual Basic)
È possibile rendere gli oggetti esterni disponibili al progetto scegliendo il **Aggiungi riferimento** comando il **progetto** menu. Fa riferimento [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] può fare riferimento agli assembly, che sono come le librerie dei tipi ma contengono ulteriori informazioni.  
  
## <a name="the-imports-statement"></a>Istruzione Imports  
 Gli assembly includono uno o più spazi dei nomi. Quando si aggiunge un riferimento a un assembly, è inoltre possibile aggiungere un `Imports` istruzione a un modulo che controlla la visibilità degli spazi dei nomi dell'assembly all'interno del modulo. Il `Imports` istruzione fornisce un contesto di ambito che consente di utilizzare solo la parte dello spazio dei nomi necessari per fornire un riferimento univoco.  
  
 Il `Imports` istruzione presenta la seguente sintassi:  
  
 `Imports` [`|``Aliasname` =] `Namespace`  
  
 `Aliasname`fa riferimento a un nome breve, che è possibile utilizzare all'interno di codice per fare riferimento a uno spazio dei nomi importato. `Namespace`è uno spazio dei nomi disponibile tramite un riferimento di progetto, tramite una definizione all'interno del progetto o tramite una precedente `Imports` istruzione.  
  
 Un modulo può contenere un numero qualsiasi di `Imports` istruzioni. Essi devono apparire dopo qualsiasi `Option` istruzioni, se presente, ma prima di qualsiasi altro codice.  
  
> [!NOTE]
>  Non confondere i riferimenti di progetto con il `Imports` istruzione o `Declare` istruzione. Riferimenti al progetto rendono disponibili per gli oggetti esterni, ad esempio oggetti negli assembly, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] progetti. Il `Imports` istruzione viene utilizzata per semplificare l'accesso ai riferimenti del progetto, ma non fornisce l'accesso a tali oggetti. Il `Declare` istruzione viene utilizzata per dichiarare un riferimento a una routine esterna in una libreria di collegamento dinamico (DLL).  
  
## <a name="using-aliases-with-the-imports-statement"></a>Utilizzo degli alias con l'istruzione Imports  
 Il `Imports` istruzione semplifica l'accesso ai metodi delle classi, eliminando la necessità di digitare in modo esplicito il nome completo dei riferimenti. Gli alias consentono di assegnare un nome più descrittivo a una sola parte di uno spazio dei nomi. Ad esempio, il ritorno a capo/avanzamento riga sequenza che provoca un singolo testo da visualizzare su più righe fa parte del <xref:Microsoft.VisualBasic.ControlChars>modulo il <xref:Microsoft.VisualBasic?displayProperty=fullName>dello spazio dei nomi.</xref:Microsoft.VisualBasic?displayProperty=fullName> </xref:Microsoft.VisualBasic.ControlChars> Per utilizzare questa costante in un programma senza un alias, è necessario digitare il codice seguente:  
  
 [!code-vb[VbVbalrApplication n.&3;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/references-and-the-imports-statement_1.vb)]  
  
 `Imports`le istruzioni devono essere sempre le prime righe immediatamente successive alle `Option` istruzioni in un modulo. Nel frammento di codice seguente viene illustrato come importare e assegnare un alias per il <xref:Microsoft.VisualBasic.ControlChars?displayProperty=fullName>modulo:</xref:Microsoft.VisualBasic.ControlChars?displayProperty=fullName>  
  
 [!code-vb[VbVbalrApplication n.&4;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/references-and-the-imports-statement_2.vb)]  
  
 I riferimenti futuri a questo spazio dei nomi possono essere notevolmente più brevi:  
  
 [!code-vb[VbVbalrApplication n.&5;](../../../visual-basic/programming-guide/program-structure/codesnippet/VisualBasic/references-and-the-imports-statement_3.vb)]  
  
 Se un `Imports` istruzione non include un nome di alias, gli elementi definiti nello spazio dei nomi importato possono essere utilizzati nel modulo senza qualifica. Se viene specificato il nome di alias, deve essere utilizzato come qualificatore per i nomi contenuti nello spazio dei nomi.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.ControlChars></xref:Microsoft.VisualBasic.ControlChars>   
 <xref:Microsoft.VisualBasic></xref:Microsoft.VisualBasic>   
 [NIB Procedura: Aggiungere o rimuovere riferimenti usando la finestra di dialogo Aggiungi riferimento](http://msdn.microsoft.com/en-us/3bd75d61-f00c-47c0-86a2-dd1f20e231c9)   
 [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [Gli assembly e Global Assembly Cache](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [Procedura: creare e utilizzare assembly dalla riga di comando](http://msdn.microsoft.com/library/70f65026-3687-4e9c-ab79-c18b97dd8be4)   
 [Istruzione Imports (tipo e spazio dei nomi .NET)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)
