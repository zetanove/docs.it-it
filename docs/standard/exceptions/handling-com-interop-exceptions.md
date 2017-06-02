---
title: "Gestione di eccezioni per interoperabilit&#224; COM | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "error-reference"
helpviewer_keywords: 
  - "interoperabilità COM, eccezioni"
  - "eccezioni, interoperabilità COM"
  - "eccezioni, codice non gestito"
  - "HRESULT"
  - "codice non gestito, eccezioni"
ms.assetid: e6104aa8-8e5f-4069-b864-def85579c96c
caps.latest.revision: 11
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 11
---
# Gestione di eccezioni per interoperabilit&#224; COM
Il codice gestito può essere integrato con il codice non gestito per la gestione delle eccezioni.  Se un metodo genera un'eccezione nel codice gestito, Common Language Runtime può passare un valore HRESULT a un oggetto COM.  Se un metodo non riesce nel codice non gestito, restituendo un HRESULT di errore, il runtime genera un'eccezione che può essere intercettata dal codice gestito.  
  
 Il runtime esegue automaticamente il mapping HRESULT dall'interoperabilità COM per le eccezioni più specifiche.  Ad esempio, E\_ACCESSDENIED diventa <xref:System.UnauthorizedAccessException>, E\_OUTOFMEMORY diventa <xref:System.OutOfMemoryException>, e così via.  
  
 Se il valore HRESULT è un risultato personalizzato o se è noto al runtime, il runtime passa un oggetto generico <xref:System.Runtime.InteropServices.COMException> al client.  La proprietà **ErrorCode** della classe **COMException** contiene il valore HRESULT.  
  
## Uso di IErrorInfo  
 Quando un errore viene passato da COM al codice gestito, il runtime compila l'oggetto eccezione con informazioni sull'errore.  Gli oggetti COM che supportano IErrorInfo e restituiscono valori HRESULT forniscono queste informazioni per le eccezioni del codice gestito.  Ad esempio, il runtime esegue il mapping della descrizione dell'errore COM alla proprietà <xref:System.Exception.Message%2A> dell'eccezione.  Se il valore HRESULT non fornisce alcuna informazione di errore, il runtime compila molte delle proprietà dell'eccezione con i valori predefiniti.  
  
 Se un metodo non riesce nel codice non gestito, un'eccezione può essere passata a un segmento di codice gestito.  L'argomento [HRESULT ed eccezioni](../../../docs/framework/interop/how-to-map-hresults-and-exceptions.md) contiene una tabella che illustra in che modo HRESULT esegue il mapping agli oggetti eccezione di runtime.  
  
## Vedere anche  
 [Eccezioni](../../../docs/standard/exceptions/index.md)