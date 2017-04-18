---
title: Panoramica degli attributi (Visual Basic) | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 1449f69b-c063-41de-8d89-f0bbdcf96ac6
caps.latest.revision: 4
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 81f6275334a0ba1507dcff2bcd85e0b1aa276067
ms.lasthandoff: 03/13/2017

---
# <a name="attributes-overview-visual-basic"></a>Panoramica degli attributi (Visual Basic)
Gli attributi offrono un metodo efficace per l'associazione di metadati o informazioni dichiarative con il codice (assembly, tipi, metodi, proprietà e così via). Dopo aver associato un attributo a un'entità di programma, in fase di esecuzione è possibile eseguire una query su tale attributo usando una tecnica denominata *reflection*. Per altre informazioni, vedere [Reflection (Visual Basic)](../../../../visual-basic/programming-guide/concepts/reflection.md).  
  
 Di seguito sono riportate le proprietà degli attributi:  
  
-   Gli attributi aggiungono metadati al programma. I *metadati* sono informazioni relative ai tipi definiti in un programma. Tutti gli assembly .NET contengono un set specificato di metadati che descrive i tipi e membri dei tipi definiti nell'assembly. È possibile aggiungere attributi personalizzati per specificare altre informazioni eventualmente necessarie. Per altre informazioni, vedere [Creazione di attributi personalizzati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/creating-custom-attributes.md).  
  
-   È possibile applicare uno o più attributi a interi assembly, moduli o elementi di programma di minori dimensioni, ad esempio classi e proprietà.  
  
-   Gli attributi possono accettare argomenti nello stesso modo dei metodi e delle proprietà.  
  
-   Il programma può esaminare i propri metadati oppure i metadati di un altro programma tramite reflection. Per altre informazioni, vedere [Accesso agli attributi tramite reflection (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md).  
  
## <a name="using-attributes"></a>Uso degli attributi  
 È possibile usare attributi nella maggior parte delle dichiarazioni, anche se la validità di un attributo specifico può essere limitata ad alcuni tipi di dichiarazione. In Visual Basic un attributo è racchiuso tra parentesi angolari (\< >) e deve apparire immediatamente prima dell'elemento a cui viene applicato, sulla stessa riga.  
  
 Nell'esempio seguente l'attributo <xref:System.SerializableAttribute> viene usato per applicare una caratteristica specifica a una classe:  
  
```vb  
<System.Serializable()> Public Class SampleClass  
    ' Objects of this type can be serialized.  
End Class  
```  
  
 Un metodo con l'attributo <xref:System.Runtime.InteropServices.DllImportAttribute> viene dichiarato nel modo seguente:  
  
```vb  
Imports System.Runtime.InteropServices  
```  
  
```vb  
<System.Runtime.InteropServices.DllImport("user32.dll")>   
Sub SampleMethod()  
End Sub  
```  
  
 In una dichiarazione è possibile inserire più attributi:  
  
```vb  
Imports System.Runtime.InteropServices  
```  
  
```vb  
Sub MethodA(<[In](), Out()> ByVal x As Double)  
End Sub  
Sub MethodB(<Out(), [In]()> ByVal x As Double)  
End Sub  
```  
  
 Alcuni attributi possono essere specificati più volte per una stessa entità. Un esempio di attributo multiuso è <xref:System.Diagnostics.ConditionalAttribute>:  
  
```vb  
<Conditional("DEBUG"), Conditional("TEST1")>   
Sub TraceMethod()  
End Sub  
```  
  
> [!NOTE]
>  Per convenzione tutti i nomi di attributo terminano con la parola "Attribute", in modo che sia possibile distinguerli da altri elementi di .NET Framework. Tuttavia, quando gli attributi vengono usati nel codice, non è necessario specificare il suffisso Attribute. Ad esempio, `[DllImport]` è equivalente a `[DllImportAttribute]`, mentre `DllImportAttribute` è il nome effettivo dell'attributo in .NET Framework.  
  
### <a name="attribute-parameters"></a>Parametri degli attributi  
 Diversi attributi dispongono di parametri, che possono essere posizionali, senza nome o denominati. I parametri posizionali devono essere specificati in un determinato ordine e non possono essere omessi. I parametri denominati sono invece facoltativi e possono essere specificati in qualsiasi ordine. I parametri posizionali vengono specificati per primi. I tre attributi seguenti, ad esempio, sono equivalenti:  
  
```vb  
<DllImport("user32.dll")>  
<DllImport("user32.dll", SetLastError:=False, ExactSpelling:=False)>  
<DllImport("user32.dll", ExactSpelling:=False, SetLastError:=False)>  
```  
  
 Il primo parametro, ovvero il nome della DLL, è posizionale ed è sempre specificato per primo. Gli altri parametri sono denominati. In questo caso, entrambi i parametri denominati sono impostati automaticamente su false e possono quindi essere omessi. Per informazioni sui valori predefiniti dei parametri, fare riferimento alla documentazione di ciascun attributo.  
  
### <a name="attribute-targets"></a>Destinazioni degli attributi  
 La *destinazione* di un attributo è l'entità a cui tale attributo viene applicato. Un attributo, ad esempio, può essere applicato a una classe, a un metodo particolare o a un intero assembly. Per impostazione predefinita, un attributo viene applicato all'elemento che lo segue. È tuttavia possibile identificare in modo esplicito, ad esempio, se un attributo viene applicato a un metodo, al relativo parametro o al relativo valore restituito.  
  
 Per identificare in modo esplicito la destinazione di un attributo, usare la sintassi seguente:  
  
```vb  
<target : attribute-list>  
```  
  
 Nella tabella seguente sono elencati i possibili valori di `target`.  
  
|Valore di destinazione|Si applica a|  
|------------------|----------------|  
|`assembly`|Intero assembly|  
|`module`|Modulo dell'assembly corrente (diverso da un modulo di Visual Basic)|  
  
 Nell'esempio seguente viene illustrato come applicare attributi ad assembly e moduli. Per altre informazioni, vedere [Attributi comuni (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/common-attributes.md).  
  
```vb  
Imports System.Reflection  
<Assembly: AssemblyTitleAttribute("Production assembly 4"),   
Module: CLSCompliant(True)>   
```  
  
## <a name="common-uses-for-attributes"></a>Usi comuni degli attributi  
 Di seguito vengono elencati alcuni degli usi comuni degli attributi nel codice:  
  
-   Contrassegno dei metodi mediante l'attributo `WebMethod` nei servizi Web per indicare che è possibile chiamare il metodo tramite il protocollo SOAP. Per altre informazioni, vedere <xref:System.Web.Services.WebMethodAttribute>.  
  
-   Descrizione della procedura di marshalling dei parametri del metodo durante l'interazione con il codice nativo. Per altre informazioni, vedere <xref:System.Runtime.InteropServices.MarshalAsAttribute>.  
  
-   Descrizione delle proprietà COM per classi, metodi e interfacce.  
  
-   Chiamata di codice non gestito mediante la classe <xref:System.Runtime.InteropServices.DllImportAttribute>.  
  
-   Descrizione dell'assembly con indicazione di titolo, versione, descrizione o marchio.  
  
-   Descrizione dei membri della classe da serializzare per la persistenza.  
  
-   Descrizione della procedura di mapping tra membri di una classe e nodi XML per la serializzazione XML.  
  
-   Descrizione dei requisiti di sicurezza per i metodi.  
  
-   Definizione delle caratteristiche usate per garantire la sicurezza.  
  
-   Controllo delle ottimizzazioni tramite il compilatore JIT (Just-In-Time), in modo da garantire un semplice debug del codice.  
  
-   Recupero di informazioni relative al chiamante di un metodo.  
  
## <a name="related-sections"></a>Sezioni correlate  
 Per altre informazioni, vedere:  
  
-   [Creazione di attributi personalizzati (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/creating-custom-attributes.md)  
  
-   [Accesso agli attributi tramite reflection (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)  
  
-   [Procedura: Creare un'unione C/C++ tramite attributi (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/how-to-create-a-c-cpp-union-by-using-attributes.md)  
  
-   [Attributi comuni (Visual Basic)](../../../../visual-basic/programming-guide/concepts/attributes/common-attributes.md)  
  
-   [Informazioni sul chiamante (Visual Basic)](../../../../visual-basic/programming-guide/concepts/caller-information.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori Visual Basic](../../../../visual-basic/programming-guide/index.md)   
 [Reflection (Visual Basic)](../../../../visual-basic/programming-guide/concepts/reflection.md)   
 [Attributi](https://msdn.microsoft.com/library/5x6cd29c)
