---
title: Attributo elenco (Visual Basic) | Documenti di Microsoft
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
- attribute list
- attributes [Visual Basic], applying
ms.assetid: 5880073a-68a4-4b6b-8a07-ace32959a4e2
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
ms.openlocfilehash: e360794ad217784e2358967bfbcc03959cd043b1
ms.lasthandoff: 03/13/2017

---
# <a name="attribute-list-visual-basic"></a>Elenco degli attributi (Visual Basic)
Specifica gli attributi da applicare a un elemento di programmazione dichiarato. Gli attributi sono separati da una virgola. Di seguito è la sintassi per un attributo.  
  
## <a name="syntax"></a>Sintassi  
  
```  
[ attributemodifier ] attributename [ ( attributearguments | attributeinitializer ) ]  
```  
  
## <a name="parts"></a>Parti  
 `attributemodifier`  
 Obbligatorio per gli attributi applicati all'inizio di un file di origine. Può essere [Assembly](../../../visual-basic/language-reference/modifiers/assembly.md) o [modulo](../../../visual-basic/language-reference/modifiers/module-keyword.md).  
  
 `attributename`  
 Obbligatorio. Nome dell'attributo.  
  
 `attributearguments`  
 Facoltativo. Elenco di argomenti posizionali per questo attributo. Più argomenti sono separati da virgole.  
  
 `attributeinitializer`  
 Facoltativo. Elenco di inizializzatori di variabile o proprietà per questo attributo. Gli inizializzatori sono separati da virgole.  
  
## <a name="remarks"></a>Note  
 È possibile applicare uno o più attributi a qualsiasi elemento di programmazione (tipi, procedure, le proprietà e così via). Gli attributi vengono visualizzati nei metadati dell'assembly e consentono di annotare il codice o specificare l'utilizzo di un particolare elemento di programmazione. È possibile applicare gli attributi definiti da Visual Basic e .NET Framework, ed è possibile definire attributi personalizzati.  

 Per ulteriori informazioni sull'utilizzo degli attributi, vedere [Cenni preliminari sugli attributi](../../../visual-basic/programming-guide/concepts/attributes/index.md). Per informazioni sui nomi degli attributi, vedere [nomi di elementi dichiarati](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
## <a name="rules"></a>Regole  
  
-   **Selezione host.** È possibile applicare gli attributi più dichiarati con elementi di programmazione. Per applicare uno o più attributi, posizionare un *blocco di attributi* all'inizio della dichiarazione dell'elemento. Ogni voce nell'elenco degli attributi specifica un attributo che si desidera applicare, e il modificatore e gli argomenti utilizzati per la chiamata dell'attributo.  
  
-   **Parentesi quadre.** Se si fornisce un elenco di attributi, è necessario racchiuderlo tra parentesi angolari ("`<`"e"`>`").  
  
-   **Parte della dichiarazione.** L'attributo deve essere parte della dichiarazione di elemento, non un'istruzione separata. È possibile utilizzare la sequenza di continuazione di riga (" `_`") per estendere l'istruzione di dichiarazione a più righe di codice sorgente.  
  
-   **Modificatori.** Un modificatore di attributo (`Assembly` o `Module`) è necessaria per ogni attributo applicato a un elemento di programmazione all'inizio di un file di origine. Modificatori di attributo non sono consentiti per gli attributi applicati agli elementi che non sono all'inizio di un file di origine.  
  
-   **Argomenti.** Tutti gli argomenti posizionali per un attributo devono precedere tutti gli inizializzatori di variabile o proprietà.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene applicato il <xref:System.Runtime.InteropServices.DllImportAttribute>dell'attributo a una definizione di base di un `Function` procedura.</xref:System.Runtime.InteropServices.DllImportAttribute>  
  
 [!code-vb[VbVbalrStatements n.&1;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/attribute-list_1.vb)]  
  
 <xref:System.Runtime.InteropServices.DllImportAttribute>indica che la routine con attributi rappresenta un punto di ingresso in una libreria di collegamento dinamico (DLL) non gestita.</xref:System.Runtime.InteropServices.DllImportAttribute> L'attributo fornisce il nome della DLL come un argomento posizionale e altre informazioni quali gli inizializzatori di variabile.  
  
## <a name="see-also"></a>Vedere anche  
 [Assembly](../../../visual-basic/language-reference/modifiers/assembly.md)   
 [Modulo \<parola chiave >](../../../visual-basic/language-reference/modifiers/module-keyword.md)   
 [Cenni preliminari sugli attributi](../../../visual-basic/programming-guide/concepts/attributes/index.md)   
 [Procedura: Interrompere e combinare istruzioni nel codice](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)
