---
title: "Attribute List (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "attribute list"
  - "attributes [Visual Basic], applying"
ms.assetid: 5880073a-68a4-4b6b-8a07-ace32959a4e2
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Attribute List (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica gli attributi da applicare a un elemento di programmazione dichiarato.  Gli attributi sono separati da una virgola.  Di seguito è riportata la sintassi per un attributo unico.  
  
## Sintassi  
  
```  
[ attributemodifier ] attributename [ ( attributearguments | attributeinitializer ) ]  
```  
  
## Parti  
 `attributemodifier`  
 Obbligatoria per gli attributi applicati all'inizio di un file di origine.  Può essere [Assembly](../../../visual-basic/language-reference/modifiers/assembly.md) o [Modulo](../../../visual-basic/language-reference/modifiers/module-keyword.md).  
  
 `attributename`  
 Obbligatorio.  Nome dell'attributo.  
  
 `attributearguments`  
 Parametro facoltativo.  Elenco degli argomenti posizionali per l'attributo.  Gli argomenti sono separati da una virgola.  
  
 `attributeinitializer`  
 Parametro facoltativo.  Elenco di inizializzatori di proprietà o variabili per l'attributo.  Gli inizializzatori sono separati da una virgola.  
  
## Note  
 È possibile applicare uno o più attributi a quasi tutti gli elementi di programmazione \(tipi, routine, proprietà e così via\).  Gli attributi vengono visualizzati nei metadati dell'assembly e consentono di apporre annotazioni al codice o di specificare le modalità di utilizzo di un elemento di programmazione specifico.  È possibile applicare attributi definiti da Visual Basic e .NET Framework oppure definire attributi personalizzati.  
  
 Per ulteriori informazioni sull'utilizzo degli attributi, vedere [Attributi](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md).  Per informazioni sui nomi degli attributi, vedere [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
## Regole  
  
-   **Posizionamento.** Gli attributi possono essere applicati alla maggior parte degli elementi di programmazione dichiarati.  Per applicare uno o più attributi, posizionare un *blocco di attributi* all'inizio della dichiarazione dell'elemento.  Ciascuna voce dell'elenco di attributi specifica un attributo che si desidera applicare, nonché il modificatore e gli argomenti utilizzati per la chiamata dell'attributo.  
  
-   **Parentesi angolari.** Quando si specifica un elenco di attributi, è necessario racchiuderlo tra parentesi acute \("`<`" e "`>`"\).  
  
-   **Parte della dichiarazione.** L'attributo deve far parte della dichiarazione dell'elemento, non deve costituire un'istruzione separata.  È possibile utilizzare la sequenza di continuazione di riga \(" `_`"\) per estendere l'istruzione di dichiarazione a righe di codice sorgente multiple.  
  
-   **Modificatori.** Per ciascun attributo che viene applicato a un elemento di programmazione all'inizio di un file di origine è necessario un modificatore di attributo \(`Assembly` o `Module`\).  L'utilizzo dei modificatori di attributo non è consentito per gli attributi applicati a elementi che non si trovano all'inizio di un file di origine.  
  
-   **Argomenti.** Tutti gli argomenti posizionali relativi a un attributo devono precedere eventuali inizializzatori di proprietà o variabili.  
  
## Esempio  
 Nell'esempio riportato di seguito l'attributo <xref:System.Runtime.InteropServices.DllImportAttribute> viene applicato a una definizione di base di una routine `Function`.  
  
 [!code-vb[VbVbalrStatements#1](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/attribute-list_1.vb)]  
  
 <xref:System.Runtime.InteropServices.DllImportAttribute> indica che la routine con attributi rappresenta un punto di ingresso di una libreria a collegamento dinamico \(DLL\) non gestita.  L'attributo fornisce il nome della DLL come argomento posizionale e altre informazioni quali gli inizializzatori delle variabili.  
  
## Vedere anche  
 [Assembly](../../../visual-basic/language-reference/modifiers/assembly.md)   
 [Module \<keyword\>](../../../visual-basic/language-reference/modifiers/module-keyword.md)   
 [Attributi](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)   
 [Procedura: Interrompere e combinare istruzioni nel codice](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)