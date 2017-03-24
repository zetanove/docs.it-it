---
title: /doc | Documenti di Microsoft
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
- doc compiler option [Visual Basic]
- -doc compiler option [Visual Basic]
- /doc compiler option [Visual Basic]
ms.assetid: 5fc32ec9-a149-4648-994c-a8d0cccd0a65
caps.latest.revision: 18
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
ms.openlocfilehash: 1054eb256eb7670ee0454b02fc094e0306c1218d
ms.lasthandoff: 03/13/2017

---
# <a name="doc"></a>/doc
Elabora commenti sulla documentazione in un file XML.  
  
## <a name="syntax"></a>Sintassi  
  
```  
/doc[+ | -]  
' -or-  
/doc:file  
```  
  
## <a name="arguments"></a>Argomenti  
  
|Termine|Definizione|  
|---|---|  
|`+` &#124; `-`|Facoltativo. Specificando +, o semplicemente `/doc`, indica al compilatore di generare informazioni relative alla documentazione e inserirle in un file XML. Specifica di `-` è l'equivalente della specifica di non `/doc`, non causando alcuna informazione di documentazione da creare.|  
|`file`|Richiesto se è usato `/doc:`. Specifica il file XML di output, che viene popolato con i commenti dai file di codice sorgente della compilazione. Se il nome del file contiene uno spazio, racchiudere il nome tra virgolette ("").|  
  
## <a name="remarks"></a>Note  
 Il `/doc` opzione consente di controllare se il compilatore genera un file XML contenente i commenti della documentazione. Se si utilizza il `/doc:``file` sintassi, il `file` parametro specifica il nome del file XML. Se si utilizza `/doc` o `/doc+`, il compilatore utilizza il nome del file XML del file eseguibile o della libreria che il compilatore sta creando. Se si utilizza `/doc-` o non si specifica il `/doc` opzione, il compilatore non crea un file XML.  
  
 Nei file di codice sorgente, i commenti della documentazione possono precedere le definizioni seguenti:  
  
-   Definite dall'utente tipi, ad esempio un [classe](../../../visual-basic/language-reference/statements/class-statement.md) o [interfaccia](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
-   I membri, ad esempio un campo, [evento](../../../visual-basic/language-reference/statements/event-statement.md), [proprietà](../../../visual-basic/language-reference/statements/property-statement.md), [funzione](../../../visual-basic/language-reference/statements/function-statement.md), o [subroutine](../../../visual-basic/language-reference/statements/sub-statement.md).  
  
 Utilizzare il file XML generato con il [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] [IntelliSense](https://docs.microsoft.com/visualstudio/ide/using-intellisense) funzionalità, si supponga che il nome del file del file XML sia lo stesso dell'assembly a cui si desidera supportare. Assicurarsi che il file XML sia nella stessa directory dell'assembly in modo che quando viene fatto riferimento all'assembly nel [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] progetto, il file XML è disponibile anche. File di documentazione XML non sono necessari per IntelliSense funzioni per il codice all'interno di un progetto o all'interno dei progetti a cui fa riferimento un progetto.  
  
 A meno che non esegue la compilazione con `/target:module`, il file XML contiene i tag `<assembly></assembly>`. Questi tag specificano il nome del file contenente il manifesto dell'assembly per il file di output della compilazione.  
  
 Vedere [tag di commento XML](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md) per informazioni sulla generazione di documentazione dai commenti nel codice.  
  
|Per impostare l'opzione /doc in Visual Studio ambiente di sviluppo integrato|  
|---|  
|1.  Selezionare un progetto in **Esplora soluzioni**. Nel **progetto** menu, fare clic su **proprietà**. Per altre informazioni, vedere [Introduzione a Creazione progetti](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Fare clic sulla scheda **Compila**.<br />3.  Impostare il valore di **file di documentazione XML genera** casella.|  
  
## <a name="example"></a>Esempio  
 Vedere [documentare il codice con XML](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md) per un esempio.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilatore della riga di comando di Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Documentazione del codice tramite XML](../../../visual-basic/programming-guide/program-structure/documenting-your-code-with-xml.md)
