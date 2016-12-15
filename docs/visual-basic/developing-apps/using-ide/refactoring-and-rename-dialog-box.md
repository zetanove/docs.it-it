---
title: "Finestra di dialogo Rinomina e refactoring (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.RenameSymbol"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "simboli, ridenominazione"
  - "nomi, modifica del simbolo"
  - "Rinomina (finestra di dialogo)"
ms.assetid: 001d2d81-9bb6-4e8e-ae3a-20c0daaa3959
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Finestra di dialogo Rinomina e refactoring (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

La finestra di dialogo incorporata **Rinomina** di Visual Basic consente di ridenominare gli identificatori nel codice per simboli come campi, variabili locali, metodi, spazi nome, proprietà e tipi.  È possibile aprire la finestra di dialogo **Rinomina** facendo clic con il pulsante destro del mouse sulla dichiarazione dell'elemento.  
  
 **Nuovo nome**  
 Specifica il nuovo nome dell'elemento del codice.  
  
 **Location**  
 Consente di identificare lo spazio dei nomi da cercare quando si esegue l'operazione di ridenominazione.  
  
## Operazioni di ridenominazione  
 La finestra di dialogo **Rinomina** consente di eseguire operazioni di ridenominazione leggermente diverse, in base al tipo di elemento rinominato.  
  
|Tipo di elemento|Operazione di ridenominazione|  
|----------------------|-----------------------------------|  
|Classe|Consente di applicare il nuovo nome a tutte le dichiarazioni e a tutti gli utilizzi della classe.  Per classi parziali, l'operazione di ridenominazione viene propagata a tutte le parti.|  
|Campo|Consente di applicare il nuovo nome alla dichiarazione e agli utilizzi del campo.|  
|Variabile locale|La dichiarazione e gli utilizzi della variabile vengono modificati nel nuovo nome.|  
|Metodo|Consente di applicare il nuovo nome al metodo e a tutti i riferimenti a tale metodo.|  
|Spazio dei nomi|Consente di applicare il nuovo nome allo spazio nome, nella dichiarazione, in tutte le istruzioni `Imports` e in tutti i nomi completi.|  
|Proprietà|Consente di applicare il nuovo nome alla dichiarazione e agli utilizzi della proprietà.|  
  
## Refactoring  
 Per offrire funzionalità di refactoring complete, il team di Visual Basic ha collaborato con Developer Express Inc.  per ottenere il supporto del refactoring.  Vedere [Refactor\!](http://go.microsoft.com/fwlink/?LinkId=155788) sul sito MSDN Visual Basic Developer Center per ulteriori dettagli e istruzioni sul download di questo strumento.  Refactor\!  supporta oltre 15 singole funzionalità di refactoring.  Sono incluse operazioni quali Riordina parametri, Estrai metodo, Incapsula campo e Crea overload.  
  
## Vedere anche  
 [Using the Visual Basic Development Environment](../../../visual-basic/developing-apps/using-ide/using-the-visual-basic-development-environment.md)