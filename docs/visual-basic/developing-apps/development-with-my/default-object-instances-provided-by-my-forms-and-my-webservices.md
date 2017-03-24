---
title: "Default Object Instances Provided by My.Forms and My.WebServices (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.WebServices object, developing applications"
  - "My.Forms object, developing applications"
  - "rapid application development (RAD), My.Forms"
  - "rapid application development (RAD), My.WebServices"
ms.assetid: de930027-9108-4f0c-b97c-5e7db4d6ef79
caps.latest.revision: 5
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 5
---
# Default Object Instances Provided by My.Forms and My.WebServices (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Gli oggetti [My.Forms](../../../visual-basic/language-reference/objects/my-forms-object.md) e [My.WebServices](../../../visual-basic/language-reference/objects/my-webservices-object.md) forniscono l'accesso a form, origini dati e servizi Web XML utilizzati dalla propria applicazione  grazie alle raccolte di *istanze predefinite* di ciascuno di questi oggetti.  
  
## Istanze predefinite  
 Un'istanza predefinita è un'istanza della classe fornita dal runtime e che non deve essere dichiarata e con istanze mediante le istruzioni `Dim` e `New`.  Nell'esempio di codice riportato di seguito viene illustrato come sia possibile disporre di un'istanza dichiarata e con istanze di una classe <xref:System.Windows.Forms.Form> denominata `Form1` e come si sia in grado di ottenere un'istanza predefinita di questa classe <xref:System.Windows.Forms.Form> mediante `My.Forms`.  
  
 [!code-vb[VbVbcnMy#5](../../../visual-basic/developing-apps/development-with-my/codesnippet/VisualBasic/default-object-instances-provided-by-my-forms-and-my-webservices_1.vb)]  
  
 [!code-vb[VbVbcnMy#6](../../../visual-basic/developing-apps/development-with-my/codesnippet/VisualBasic/default-object-instances-provided-by-my-forms-and-my-webservices_2.vb)]  
  
 Mediante l'oggetto `My.Forms` viene restituita una raccolta di istanze predefinite per ogni classe `Form` presente nel progetto.  Analogamente, l'oggetto `My.WebServices` fornisce un'istanza predefinita della classe proxy per ogni servizio Web a cui è stato creato un riferimento nell'applicazione.  
  
## Vedere anche  
 [My.Forms Object](../../../visual-basic/language-reference/objects/my-forms-object.md)   
 [My.WebServices Object](../../../visual-basic/language-reference/objects/my-webservices-object.md)   
 [How My Depends on Project Type](../../../visual-basic/developing-apps/development-with-my/how-my-depends-on-project-type.md)