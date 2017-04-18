---
title: Istruzione Imports (tipo e Namespace .NET) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Imports
- imports
dev_langs:
- VB
helpviewer_keywords:
- declared element names [Visual Basic], qualification
- imports [Visual Basic]
- Imports statement [Visual Basic]
- aliases [Visual Basic], Imports statement
- container elements [Visual Basic]
- namespaces [Visual Basic], importing
- Imports statement [Visual Basic], syntax
- import aliases [Visual Basic]
- aliases [Visual Basic], import
- declared elements [Visual Basic], container elements
ms.assetid: 7062f8aa-d890-4232-9eed-92836e13fb6e
caps.latest.revision: 40
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
ms.openlocfilehash: 393f3e9a264817d8658585267c954d973290530a
ms.lasthandoff: 03/13/2017

---
# <a name="imports-statement-net-namespace-and-type"></a>Istruzione Imports (tipo e spazio dei nomi .NET)
Consente di digitare i nomi di riferimento senza qualifica dello spazio dei nomi.  
  
## <a name="syntax"></a>Sintassi  
  
```  
Imports [ aliasname = ] namespace  
-or-  
Imports [ aliasname = ] namespace.element  
```  
  
## <a name="parts"></a>Parti  
  
|Termine|Definizione|  
|---|---|  
|`aliasname`|Facoltativo. Un *alias di importazione* o il nome mediante il quale il codice può fare riferimento a `namespace` anziché la stringa del nome completo. Vedere [dichiarati i nomi degli elementi](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).|  
|`namespace`|Obbligatorio. Il nome completo dello spazio dei nomi importati. Può essere una stringa di spazi dei nomi annidata a qualsiasi livello.|  
|`element`|Facoltativo. Il nome di un elemento di programmazione dichiarato nello spazio dei nomi. Può essere qualsiasi elemento del contenitore.|  
  
## <a name="remarks"></a>Note  
 Il `Imports` istruzione consente i tipi che sono contenuti in un determinato spazio dei nomi a cui fare riferimento direttamente.  
  
 È possibile fornire un nome singolo spazio dei nomi o una stringa di spazi dei nomi annidati. Ogni spazio dei nomi annidato è separato dallo spazio dei nomi successivo di livello superiore da un punto (`.`), come illustrato nell'esempio seguente.  
  
 `Imports System.Collections.Generic`  
  
 Ogni file di origine può contenere un numero qualsiasi di `Imports` istruzioni. Queste devono seguire le dichiarazioni di opzione, ad esempio il `Option Strict` istruzione che deve precedere le dichiarazioni di elemento di programmazione, ad esempio `Module` o `Class` istruzioni.  
  
 È possibile utilizzare `Imports` solo a livello di file. Ciò significa che il contesto della dichiarazione per l'importazione deve essere un file di origine e non può essere un spazio dei nomi, classe, struttura, modulo, interfaccia, procedura o blocco.  
  
 Si noti che il `Imports` istruzione non rende disponibili elementi di altri progetti e assembly al progetto. L'importazione non sostituisce l'impostazione di un riferimento. Rimuove solo la necessità di qualificare i nomi che sono già disponibili per il progetto. Per ulteriori informazioni, vedere "Importazione di elementi contenitore" in [riferimenti a elementi dichiarati](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
> [!NOTE]
>  È possibile definire implicita `Imports` istruzioni utilizzando il [pagina riferimenti, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic). Per ulteriori informazioni, vedere [procedura: aggiungere o rimuovere spazi dei nomi importati (Visual Basic)](http://msdn.microsoft.com/library/44cebec3-0ea0-47c2-8406-4edeab6a997e).  
  
## <a name="import-aliases"></a>Alias di importazione  
 Un *alias di importazione* definisce l'alias per un tipo o dello spazio dei nomi. Gli alias di importazione sono utili quando è necessario utilizzare gli elementi con lo stesso nome dichiarato in uno o più spazi dei nomi. Per ulteriori informazioni e un esempio, vedere "Qualificare un nome di un elemento" in [riferimenti a elementi dichiarati](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
 Non è necessario dichiarare un membro al livello di modulo con lo stesso nome `aliasname`. Se non lo, il compilatore Visual Basic utilizza `aliasname` solo per il membro dichiarato e non oltre lo riconosce come un alias di importazione.  
  
 Sebbene la sintassi utilizzata per dichiarare un alias di importazione è uguale a quella utilizzata per l'importazione di un prefisso dello spazio dei nomi XML, i risultati sono diversi. Un alias di importazione è utilizzabile come un'espressione nel codice, mentre un prefisso dello spazio dei nomi XML può essere utilizzato solo in valori letterali XML o proprietà axis XML come prefisso per un nome di attributo o elemento qualificato.  
  
### <a name="element-names"></a>Nomi di elementi  
 Se si fornisce `element`, deve rappresentare un *elemento contenitore*, vale a dire un elemento di programmazione che può contenere altri elementi. Gli elementi contenitore comprendono classi, strutture, moduli, interfacce ed enumerazioni.  
  
 L'ambito degli elementi resi disponibili da un `Imports` istruzione dipende dal fatto che vengano specificati `element`. Se si specifica solo `namespace`, tutto in modo univoco denominato membri dello spazio dei nomi e i membri degli elementi contenitore all'interno di tale spazio dei nomi, sono disponibili senza qualifica. Se si specificano entrambe `namespace` e `element`, solo i membri di tale elemento sono disponibili senza qualifica.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente restituisce tutte le cartelle nella directory c:\. utilizzando la <xref:System.IO.DirectoryInfo>classe.</xref:System.IO.DirectoryInfo>  
  
 Il codice non ha alcun `Imports` istruzioni all'inizio del file. Pertanto, il `DirectoryInfo`, <xref:System.Text.StringBuilder>, e <xref:Microsoft.VisualBasic.ControlChars.CrLf>i riferimenti sono completi degli spazi dei nomi.</xref:Microsoft.VisualBasic.ControlChars.CrLf> </xref:System.Text.StringBuilder>  
  
 [!code-vb[VbVbalrStatements&#152;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_1.vb)]  
  
## <a name="example"></a>Esempio  
 L'esempio seguente include `Imports` istruzioni per gli spazi dei nomi cui viene fatto riferimento. Di conseguenza, i tipi non devono essere completo con gli spazi dei nomi.  
  
 [!code-vb[VbVbalrStatements&#153;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_2.vb)]  
  
 [!code-vb[&#154; VbVbalrStatements](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_3.vb)]  
  
## <a name="example"></a>Esempio  
 L'esempio seguente include `Imports` istruzioni che creare alias per gli spazi dei nomi cui viene fatto riferimento. I tipi sono qualificati con gli alias.  
  
 [!code-vb[&#155; VbVbalrStatements](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_4.vb)]  
  
 [!code-vb[VbVbalrStatements&#156;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_5.vb)]  
  
## <a name="example"></a>Esempio  
 L'esempio seguente include `Imports` istruzioni che creano gli alias dei tipi di riferimento. Gli alias vengono utilizzati per specificare i tipi.  
  
 [!code-vb[VbVbalrStatements&#157;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_6.vb)]  
  
 [!code-vb[VbVbalrStatements&#158;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_7.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione Namespace](../../../visual-basic/language-reference/statements/namespace-statement.md)   
 [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [I riferimenti e istruzione Imports](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)   
 [Istruzione Imports (XML Namespace)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)   
 [Riferimenti a elementi dichiarati](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
