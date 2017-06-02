---
title: "Convenzioni di denominazione generali | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "nomi di conflitti [.NET Framework]"
  - "conflitti di nomi di tipi"
  - "nomi di tipi specifici di linguaggio"
  - "nomi di sulle linee guida sulla denominazione [.NET Framework]"
  - "nomi di abbreviazioni [.NET Framework]"
  - "convenzioni di denominazione abbreviazione"
  - "denominazione degli acronimi"
  - "Notazione ungherese"
  - "nomi [.NET Framework], nomi dei tipi"
  - "nomi [.NET Framework], gli acronimi"
ms.assetid: d3a77ea1-75d2-4969-a8c3-3e1e3e1aaedc
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# Convenzioni di denominazione generali
Questa sezione descrive convenzioni di denominazione generali correlate alla scelta delle parole, le linee guida sull'utilizzo di abbreviazioni e acronimi e indicazioni su come evitare di utilizzare nomi specifici della lingua.  
  
## Scelta delle parole  
 **✓ si** scegliere nomi di identificatori facilmente leggibili.  
  
 Ad esempio, una proprietà denominata `HorizontalAlignment` è più inglese\-leggibile `AlignmentHorizontal`.  
  
 **✓ si** preferire la leggibilità brevità.  
  
 Il nome della proprietà `CanScrollHorizontally` è migliore di `ScrollableX` \(un riferimento all'asse x\).  
  
 **X non** utilizzare altri caratteri non alfanumerici, trattini o caratteri di sottolineatura.  
  
 **X non** utilizzare la notazione ungherese.  
  
 **X evitare** utilizzando gli identificatori che creano conflitti con parole chiave ampiamente utilizzato linguaggi di programmazione.  
  
 In base alla regola 4 della specifica CLS \(Common Language\), tutti i linguaggi conformi devono fornire un meccanismo che consente l'accesso agli elementi denominati che utilizza una parola chiave del linguaggio come identificatore. In c\#, ad esempio, utilizza il simbolo come meccanismo di escape in questo caso @. Tuttavia, è comunque consigliabile evitare parole chiave comuni in quanto è molto più difficile di utilizzare un metodo con la sequenza di escape quello senza di esso.  
  
## Utilizzo di abbreviazioni e acronimi  
 **X non** utilizzare abbreviazioni o forme contratte nell'ambito dei nomi degli identificatori.  
  
 Ad esempio, utilizzare `GetWindow` anziché `GetWin`.  
  
 **X non** utilizzare acronimi che non sono molto diffusa e anche in tal caso, solo quando necessario.  
  
## Evitare nomi specifici del linguaggio  
 **✓ si** utilizzare nomi significativi anziché parole chiave specifiche della lingua per i nomi dei tipi.  
  
 Ad esempio, `GetLength` è un nome più significativo rispetto a `GetInt`.  
  
 **✓ si** utilizzare un nome di tipo generico di CLR, anziché un nome specifico del linguaggio, in rari casi in cui un identificatore non ha alcun significato semantico oltre il relativo tipo.  
  
 Ad esempio, un metodo di conversione in <xref:System.Int64> deve essere denominato `ToInt64`, non `ToLong` \(poiché <xref:System.Int64> è un nome CLR per il linguaggio c\#\-alias specifico `long`\). La tabella seguente vengono illustrati diversi tipi di dati di base utilizzando i nomi dei tipi CLR \(nonché i nomi dei tipi corrispondenti per c\#, Visual Basic e C\+\+\).  
  
|C\#|Visual Basic|C\+\+|CLR|  
|---------|------------------|-----------|---------|  
|**sbyte**|**SByte**|**char**|**SByte**|  
|**byte**|**Byte**|**unsigned char**|**Byte**|  
|**short**|**Breve**|**short**|**Int16**|  
|**ushort**|**UInt16**|**unsigned short**|**UInt16**|  
|**int**|**Integer**|**int**|**Int32**|  
|**uint**|**UInt32**|**unsigned int**|**UInt32**|  
|**long**|**Long**|**\_\_int64**|**Int64**|  
|**ulong**|**UInt64**|**unsigned \_\_int64**|**UInt64**|  
|**float**|**Single**|**float**|**Single**|  
|**double**|**Double**|**double**|**Double**|  
|**bool**|**Booleano**|**bool**|**Booleano**|  
|**char**|**Char**|**wchar\_t**|**Char**|  
|**string**|**String**|**String**|**String**|  
|**object**|**Oggetto**|**Oggetto**|**Oggetto**|  
  
 **✓ si**  utilizzare un nome comune, ad esempio `value` o `item`, invece di ripetere il nome del tipo in rari casi in cui un identificatore non ha alcun significato semantico e il tipo del parametro non è importante.  
  
## Denominazione di nuove versioni dell'API esistenti  
 **✓ si** utilizzare un nome simile all'API precedente durante la creazione di nuove versioni di un'API esistente.  
  
 Ciò consente di evidenziare la relazione tra le API.  
  
 **✓ si** preferisce l'aggiunta di un suffisso piuttosto che un prefisso per indicare una nuova versione di un'API esistente.  
  
 Durante l'esplorazione, documentazione, così da poter individuazione o l'utilizzo di Intellisense. La versione precedente dell'API verrà organizzata vicino le nuove API, poiché la maggior parte dei browser e Intellisense Mostra gli identificatori in ordine alfabetico.  
  
 **✓ PROVARE** utilizzando un identificatore di nuovo, ma significativo, anziché aggiungere un suffisso o prefisso.  
  
 **✓ si** utilizzare un suffisso numerico per indicare una nuova versione di un'API esistente, in particolare se il nome dell'API esistente è il solo nome significativa \(ad esempio, se è uno standard del settore\) e se si aggiungono significativo qualsiasi suffisso \(o la modifica del nome\) non è un'opzione appropriata.  
  
 **X non** utilizzare "Ex" \(o una simile\) suffisso di un identificatore per distinguerlo da una versione precedente dell'API stessa.  
  
 **✓ si** utilizza il suffisso "64" quando si introduce le versioni delle API che operano su un valore integer a 64 bit \(valore long integer\) anziché un intero a 32 bit. È necessario adottare questo approccio quando è presente l'API a 32 bit esistente. non farlo per le nuove API con solo una versione a 64 bit.  
  
 *Parti © 2005, 2009 Microsoft Corporation. Tutti i diritti sono riservati.*  
  
 *Ristampato con l'autorizzazione di Pearson formazione, Inc. da [Framework Design Guidelines: convenzioni idiomi e modelli per librerie .NET riutilizzabile, 2nd Edition](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) Krzysztof Cwalina e Brad Abrams, pubblicati il 22 ottobre 2008 da Addison\-Wesley Professional come parte della serie di sviluppo di Microsoft Windows.*  
  
## Vedere anche  
 [Linee guida](../../../docs/standard/design-guidelines/index.md)   
 [Convenzioni di denominazione](../../../docs/standard/design-guidelines/naming-guidelines.md)