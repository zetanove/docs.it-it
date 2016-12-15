---
title: "Troubleshooting: Log Listeners (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "event logs, troubleshooting"
  - "troubleshooting Visual Basic, event logs"
  - "troubleshooting event logs"
ms.assetid: ac6eb760-3d5d-461e-aedd-40599ee22e49
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Troubleshooting: Log Listeners (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

È possibile utilizzare gli oggetti `My.Application.Log` e `My.Log` per registrare informazioni sugli eventi che si verificano nell'applicazione.  
  
 Per determinare i listener di log a cui sono inviati questi messaggi, vedere [Procedura dettagliata: individuazione della posizione di inserimento delle informazioni con My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md).  
  
 L'oggetto `Log` può utilizzare il filtraggio di log per limitare la quantità di informazioni registrate.  Se i filtri non sono configurati correttamente, i log potrebbero contenere informazioni errate.  Per ulteriori informazioni sull'utilizzo dei filtri, vedere [Walkthrough: Filtering My.Application.Log Output](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-filtering-my-application-log-output.md).  
  
 Tuttavia, se un log è configurato in modo errato, potrebbero essere necessarie maggiori informazioni sulla configurazione corrente.  È possibile ottenere tali informazioni grazie alla proprietà `TraceSource` avanzata del log.  
  
### Per determinare i listener di log per l'oggetto Log nel codice  
  
1.  Importare lo spazio dei nomi <xref:System.Diagnostics> all'inizio del file di codice.  Per ulteriori informazioni, vedere [Imports Statement \(.NET Namespace and Type\)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md).  
  
     [!code-vb[VbVbalrMyApplicationLog#13](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/troubleshooting-log-listeners_1.vb)]  
  
2.  Creare una funzione che consente di restituire una stringa costituita dalle informazioni relative a ciascuno dei listener di log.  
  
     [!code-vb[VbVbalrMyApplicationLog#14](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/troubleshooting-log-listeners_2.vb)]  
  
3.  Passare la raccolta dei listener di traccia del log alla funzione `GetListeners`, quindi visualizzare il valore restituito.  
  
     [!code-vb[VbVbalrMyApplicationLog#19](../../../../visual-basic/developing-apps/programming/log-info/codesnippet/VisualBasic/troubleshooting-log-listeners_3.vb)]  
  
     Per ulteriori informazioni, vedere <xref:Microsoft.VisualBasic.Logging.Log.TraceSource%2A>.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Logging.Log?displayProperty=fullName>   
 [Utilizzo dei log applicazione](../../../../visual-basic/developing-apps/programming/log-info/working-with-application-logs.md)   
 [Procedura dettagliata: individuazione della posizione di inserimento delle informazioni con My.Application.Log](../../../../visual-basic/developing-apps/programming/log-info/walkthrough-determining-where-my-application-log-writes-information.md)