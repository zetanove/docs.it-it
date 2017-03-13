---
title: "Imports Statement (.NET Namespace and Type) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Imports"
  - "imports"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "declared element names [Visual Basic], qualification"
  - "imports [Visual Basic]"
  - "Imports statement [Visual Basic]"
  - "aliases [Visual Basic], Imports statement"
  - "container elements [Visual Basic]"
  - "namespaces [Visual Basic], importing"
  - "Imports statement [Visual Basic], syntax"
  - "import aliases [Visual Basic]"
  - "aliases [Visual Basic], import"
  - "declared elements [Visual Basic], container elements"
ms.assetid: 7062f8aa-d890-4232-9eed-92836e13fb6e
caps.latest.revision: 40
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 40
---
# Imports Statement (.NET Namespace and Type)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di fare riferimento ai nomi dei tipi senza la qualificazione dello spazio dei nomi.  
  
## Sintassi  
  
```  
Imports [ aliasname = ] namespace  
-or-  
Imports [ aliasname = ] namespace.element  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`aliasname`|Parametro facoltativo.  *Alias di importazione* o nome per mezzo del quali il codice può fare riferimento a `namespace` invece di utilizzare la stringa di qualificazione completa.  Per informazioni, vedere [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).|  
|`namespace`|Obbligatorio.  Nome completo dello spazio dei nomi da importare.  Può essere una stringa di spazi dei nomi annidata a qualsiasi livello.|  
|`element`|Parametro facoltativo.  Nome di un elemento di programmazione dichiarato nello spazio dei nomi.  Può essere un qualsiasi elemento contenitore.|  
  
## Note  
 L'istruzione `Imports`  consente di fare riferimento ai tipi contenuti in uno spazio dei nomi dato in modo diretto.  
  
 È possibile fornire un singolo nome dello spazio dei nomi o una stringa di spazi dei nomi annidati.  Ciascuno spazio dei nomi annidato è separato dallo spazio dei nomi successivo di livello più alto da un punto \(`.`\) come illustrato nell'esempio riportato di seguito.  
  
 `Imports System.Collections.Generic`  
  
 Ogni file di origine può contenere un numero indefinito di istruzioni `Imports`.  Queste devono essere specificate dopo le dichiarazioni di opzione, come l'istruzione `Option Strict`, e devono precedere qualsiasi dichiarazione di elemento di programmazione, come ad esempio le istruzioni `Module` o `Class`.  
  
 La parola chiave `Imports` può essere utilizzata solo a livello di file.  In altri termini, il contesto della dichiarazione per l'importazione deve essere un file di origine, e non uno spazio dei nomi, una classe, una struttura, un modulo, un'interfaccia, una routine o un blocco.  
  
 Tenere presente che l'istruzione `Imports` non rende disponibili per il progetto elementi di altri progetti e assembly.  In altre parole, l'importazione non è un'alternativa all'impostazione di un riferimento.  Essa elimina semplicemente la necessità di qualificare i nomi che sono già disponibili per il progetto.  Per ulteriori informazioni, vedere "Containing Elements" in [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
> [!NOTE]
>  È possibile definire istruzioni `Imports` implicite utilizzando la [Riferimenti \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic).  Per ulteriori informazioni, vedere [Procedura: aggiungere o rimuovere spazi dei nomi importati \(Visual Basic\)](../Topic/How%20to:%20Add%20or%20Remove%20Imported%20Namespaces%20\(Visual%20Basic\).md).  
  
## Alias di importazione  
 Un *alias di importazione* consente di definire l'alias per uno spazio dei nomi o un tipo.  Gli alias di importazione si rivelano utili quando è necessario utilizzare elementi omonimi dichiarati in uno o più spazi dei nomi.  Per ulteriori informazioni e un esempio, vedere "Qualificare un nome di un elemento" in [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md).  
  
 Evitare di dichiarare un membro a livello di modulo con la stesso nome di `aliasname`.  In caso contrario, il compilatore di Visual Basic utilizza il `aliasname` soltanto per il membro dichiatato e non lo riconosce più come alias di importazione.  
  
 Anche se la sintassi utilizzata per dichiarare un alias di importazione è uguale a quella utilizzata per importare un prefisso dello spazio dei nomi XML, i risultati sono diversi.  Un alias di importazione può essere utilizzato come un'espressione nel codice, mentre un prefisso dello spazio dei nomi XML può essere utilizzato solo in valori letterali XML o proprietà axis XML come prefisso di un nome di attributo o elemento qualificato.  
  
### Nomi di elemento  
 Se si fornisce un parametro `element`, esso deve rappresentare un *elemento contenitore*, ovvero un elemento di programmazione che possa contenere altri elementi.  Gli elementi contenitore comprendono classi, strutture, moduli, interfacce ed enumerazioni.  
  
 L'ambito degli elementi resi disponibili da un'istruzione `Imports` è legato al fatto che venga o non venga specificato `element`.  Se si specifica soltanto il parametro `namespace`, tutti i membri con nome univoco di quello spazio dei nomi e i membri di elementi contenitore inclusi in quello spazio dei nomi, sono disponibili senza qualificazione.  Se si specifica sia `namespace` che `element`, saranno disponibili senza qualificazione soltanto i membri di quell'elemento.  
  
## Esempio  
 Nell'esempio seguente vengono restituite tutte le cartelle nella directory C:\\ tramite la classe <xref:System.IO.DirectoryInfo>.  
  
 Nel codice non sono presenti istruzioni `Imports` all'inizio del file.  Pertanto, i riferimenti `DirectoryInfo`, <xref:System.Text.StringBuilder> e <xref:Microsoft.VisualBasic.ControlChars.CrLf> sono completi degli spazi dei nomi.  
  
 [!code-vb[VbVbalrStatements#152](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_1.vb)]  
  
## Esempio  
 Nell'esempio seguente sono incluse le istruzioni `Imports` per gli spazi dei nomi a cui si fa riferimento.  Pertanto, i tipi non devono essere completi degli spazi dei nomi.  
  
 [!code-vb[VbVbalrStatements#153](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_2.vb)]  
  
 [!code-vb[VbVbalrStatements#154](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_3.vb)]  
  
## Esempio  
 Nell'esempio seguente sono incluse le istruzioni `Imports` tramite le quali vengono creati gli alias per gli spazi dei nomi a cui si fa riferimento.  I tipi vengono qualificati con gli alias.  
  
 [!code-vb[VbVbalrStatements#155](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_4.vb)]  
  
 [!code-vb[VbVbalrStatements#156](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_5.vb)]  
  
## Esempio  
 Nell'esempio seguente sono incluse le istruzioni `Imports` tramite le quali vengono creati gli alias per i tipi a cui si fa riferimento.  Gli alias vengono utilizzati per specificare i tipi.  
  
 [!code-vb[VbVbalrStatements#157](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_6.vb)]  
  
 [!code-vb[VbVbalrStatements#158](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/imports-statement-net-namespace-and-type_7.vb)]  
  
## Vedere anche  
 [Namespace Statement](../../../visual-basic/language-reference/statements/namespace-statement.md)   
 [Spazi dei nomi in Visual Basic](../../../visual-basic/programming-guide/program-structure/namespaces.md)   
 [References and the Imports Statement](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)   
 [Imports Statement \(XML Namespace\)](../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)   
 [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)