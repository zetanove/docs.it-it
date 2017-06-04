---
title: "Applicazione di attributi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "assembly [.NET Framework], attributi"
  - "attributi [.NET Framework], applicazione"
ms.assetid: dd7604eb-9fa3-4b60-b2dd-b47739fa3148
caps.latest.revision: 19
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 19
---
# Applicazione di attributi
Per applicare un attributo a un elemento del codice utilizzare la seguente procedura.  
  
1.  Definire un nuovo attributo o utilizzare un attributo esistente importandone lo spazio dei nomi da .NET Framework.  
  
2.  Applicare l'attributo all'elemento di codice posizionandolo immediatamente prima dell'elemento.  
  
     Ogni linguaggio ha una propria sintassi di attributo.  In C\+\+ e C\# l'attributo è racchiuso tra parentesi quadre e separato dall'elemento da uno spazio, che può includere un'interruzione di riga.  In Visual Basic l'attributo è racchiuso tra parentesi angolari e deve essere presente sulla stessa riga logica. È possibile utilizzare il carattere di continuazione di riga se si desidera inserire un'interruzione di riga.  In J\# l'attributo viene collegato utilizzando una sintassi di commento speciale.  
  
3.  Specificare i parametri posizionali e i parametri denominati per l'attributo.  
  
     I parametri posizionali sono obbligatori e devono precedere eventuali parametri denominati. Corrispondono ai parametri di uno dei costruttori dell'attributo.  I parametri denominati sono facoltativi e corrispondono a proprietà di lettura\/scrittura dell'attributo.  In C\+\+, C\# e J\# specificare `name`\=`value` per ogni parametro facoltativo, dove `name` è il nome della proprietà.  In Visual Basic specificare `name`:\=`value`.  
  
 L'attributo viene emesso nei metadati quando si compila il codice ed è disponibile per Common Language Runtime e qualsiasi strumento o applicazione tramite i servizi di reflection in fase di esecuzione.  
  
 Per convenzione tutti i nomi di attributo terminano con Attribute.  In diversi linguaggi destinati alla fase di esecuzione, quali Visual Basic e C\#, non è tuttavia necessario specificare il nome completo degli attributi.  Se si desidera inizializzare, ad esempio, <xref:System.ObsoleteAttribute?displayProperty=fullName> sarà sufficiente farvi riferimento come **Obsolete**.  
  
## Applicazione di un attributo a un metodo  
 Nell'esempio di codice riportato di seguito si illustra come dichiarare l'attributo **System.ObsoleteAttribute**, che contrassegna il codice come obsoleto.  La stringa `"Will be removed in next version"` viene passata all'attributo.  Questo attributo fa sì che, quando viene chiamato il codice descritto dall'attributo stesso, venga generato un avviso del compilatore che visualizza la stringa passata.  
  
 [!code-cpp[Conceptual.Attributes.Usage#3](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source1.cpp#3)]
 [!code-csharp[Conceptual.Attributes.Usage#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source1.cs#3)]
 [!code-vb[Conceptual.Attributes.Usage#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source1.vb#3)]  
  
## Applicazione di attributi a livello di assembly  
 Se si desidera applicare un attributo a livello di assembly utilizzare la parola chiave **assembly** \(`Assembly` in Visual Basic\).  Nel codice riportato di seguito si illustra l'attributo **AssemblyTitleAttribute** applicato a livello di assembly.  
  
 [!code-cpp[Conceptual.Attributes.Usage#2](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source1.cpp#2)]
 [!code-csharp[Conceptual.Attributes.Usage#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source1.cs#2)]
 [!code-vb[Conceptual.Attributes.Usage#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source1.vb#2)]  
  
 All'applicazione di questo attributo la stringa `"My Assembly"` viene inserita nel manifesto dell'assembly nella porzione del file costituita da metadati.  È possibile visualizzare l'attributo sia mediante lo strumento [MSIL Disassembler \(Ildasm.exe\)](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) sia creando un programma personalizzato che recuperi l'attributo.  
  
## Vedere anche  
 [Attributi](../../../docs/standard/attributes/index.md)   
 [Recupero di informazioni memorizzate negli attributi](../../../docs/standard/attributes/retrieving-information-stored-in-attributes.md)   
 [Concepts](../Topic/Attributed%20Programming%20Concepts.md)   
 [Attributi](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)