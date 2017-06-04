---
title: "Propriet&#224; nei controlli Windows Form che supportano le linee guida per l&#39;accesso facilitato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "accessibilità, Windows Form (proprietà controllo)"
  - "Windows Form, proprietà di accessibilità dei controlli"
ms.assetid: ad3567a6-313b-4708-9e15-f487a831f049
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Propriet&#224; nei controlli Windows Form che supportano le linee guida per l&#39;accesso facilitato
I controlli nella Casella degli strumenti standard per i Windows Form soddisfano molti dei requisiti di Accesso facilitato, tra cui l'esposizione dello stato attivo e l'esposizione degli elementi dello schermo.  
  
## Pianificazione dell'Accesso facilitato  
 È possibile utilizzare le proprietà dei controlli per soddisfare altri requisiti di Accesso facilitato, come illustrato nella tabella riportata di seguito.  È inoltre necessario utilizzare i menu per consentire l'accesso alle funzionalità del programma.  
  
|Proprietà dei controlli|Considerazioni sull'Accesso facilitato|  
|-----------------------------|--------------------------------------------|  
|AccessibleDescription|La descrizione fornita per gli strumenti per l'Accesso facilitato, quali la funzione di lettura Screen Reader \(non disponibile in italiano\).  Gli strumenti per l'Accesso facilitato sono periferiche e programmi specializzati che consentono agli utenti con particolari esigenze di utilizzare i computer in modo più efficiente.|  
|AccessibleName|Il nome riportato negli strumenti per l'Accesso facilitato.|  
|AccessibleRole|Descrive l'utilizzo dell'elemento nell'interfaccia utente.|  
|TabIndex|Crea un percorso di navigazione del form sensibile.  È importante che i controlli senza etichette intrinseche, quali le caselle di testo, siano immediatamente preceduti dalle relative etichette associate nell'ordine di tabulazione.|  
|Text|Utilizzare il carattere "&" per creare tasti di scelta.  I tasti di scelta rappresentano un metodo per consentire l'accesso da tastiera documentato alle funzionalità.|  
|Font Size|Se non è possibile modificare la dimensione dei caratteri, è necessario impostarla su 10 punti o su un valore superiore.  Una volta impostata la dimensione dei caratteri del form, tutti i controlli successivamente aggiunti al form avranno la stessa dimensione.|  
|Forecolor|Se questa proprietà viene impostata sul valore predefinito, nel form verranno utilizzate le preferenze dell'utente relative ai colori.|  
|Backcolor|Se questa proprietà viene impostata sul valore predefinito, nel form verranno utilizzate le preferenze dell'utente relative ai colori.|  
|BackgroundImage|Lasciare vuota questa proprietà per rendere il testo più leggibile.|  
  
## Vedere anche  
 [Procedura dettagliata: creazione di un'applicazione Windows ad Accesso facilitato](../../../../docs/framework/winforms/advanced/walkthrough-creating-an-accessible-windows-based-application.md)