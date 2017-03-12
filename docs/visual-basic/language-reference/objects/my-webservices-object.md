---
title: "My.WebServices Object | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "My.WebServices"
  - "My.MyProject.WebServices"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "My.WebServices object"
ms.assetid: f188dc05-2c75-41b6-bb68-122d1c3110a2
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# My.WebServices Object
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Fornisce proprietà per la creazione e l'accesso a una singola istanza di ciascun servizio Web XML a cui fa riferimento il progetto corrente.  
  
## Note  
 L'oggetto `My.WebServices` fornisce un'istanza di ciascun servizio Web a cui fa riferimento il progetto corrente.  Ciascuna istanza viene istanziata su richiesta.  È possibile accedere a questi servizi Web tramite le proprietà dell'oggetto `My.WebServices`.  Il nome della proprietà è uguale al nome del servizio Web a cui accede la proprietà.  Qualsiasi classe che eredita da <xref:System.Web.Services.Protocols.SoapHttpClientProtocol> è un servizio Web.  Per informazioni sull'aggiunta dei servizi Web a un progetto, vedere [Accessing Application Web Services](../../../visual-basic/developing-apps/programming/accessing-application-web-services.md).  
  
 L'oggetto `My.WebServices` espone solo i servizi Web associati al progetto corrente  e non fornisce accesso ai servizi Web dichiarati nelle DLL di riferimento.  Per accedere a un servizio Web fornito da una DLL, è necessario utilizzare il nome completo del servizio nel formato *NomeDLL*.*NomeServizioWeb*.  Per ulteriori informazioni, vedere [Accessing Application Web Services](../../../visual-basic/developing-apps/programming/accessing-application-web-services.md).  
  
 L'oggetto e le relative proprietà non sono disponibili per le applicazioni Web.  
  
## Proprietà  
 Ciascuna proprietà dell'oggetto `My.WebServices` fornisce accesso a un'istanza di un servizio Web a cui fa riferimento il progetto corrente.  Il nome della proprietà è lo stesso di quello del servizio Web a cui accede la proprietà e il tipo di proprietà equivale a quello del tipo di servizio Web.  
  
> [!NOTE]
>  In caso di conflitto tra nomi, il nome della proprietà per accedere al servizio Web sarà *RootNamespace*\_*Namespace*\_*ServiceName*.  Ad esempio, si consideri di disporre di due servizi Web denominati `Service1`.  Se uno dei servizi è nello spazio dei nomi radice `WindowsApplication1` e nello spazio dei nomi `Namespace1`, è possibile accedere a tale servizio mediante `My.WebServices.WindowsApplication1_Namespace1_Service1`.  
  
 La prima volta che si accede a una proprietà dell'oggetto `My.WebServices` viene creata una nuova istanza del servizio Web, la quale viene archiviata  per essere restituita ogni volta che si accede di nuovo a tale proprietà.  
  
 Per rimuovere un servizio Web, assegnare il valore `Nothing` alla relativa proprietà.  Il metodo per l'impostazione della proprietà assegna `Nothing` al valore archiviato.  Se alla proprietà si assegna un valore diverso da `Nothing`, il metodo per l'impostazione genera un'eccezione <xref:System.ArgumentException>.  
  
 Per verificare se una proprietà dell'oggetto `My.WebServices` archivia un'istanza del servizio Web, utilizzare l'operatore`Is` o `IsNot`.  Questi operatori consentono di controllare se il valore della proprietà è `Nothing`.  
  
> [!NOTE]
>  Generalmente, l'operatore `Is` o `IsNot` deve leggere il valore della proprietà per eseguire il confronto.  Tuttavia, se il valore della proprietà è `Nothing`, l'operatore crea una nuova istanza del servizio Web e quindi la restituisce.  Il compilatore di Visual Basic considera le proprietà dell'oggetto `My.WebServices` in modo speciale e consente all'operatore `Is` o `IsNot` di controllare lo stato della proprietà senza modificarne il valore.  
  
## Esempio  
 Nell'esempio viene chiamato il metodo `FahrenheitToCelsius` del servizio Web XML `TemperatureConverter` e viene quindi restituito il risultato.  
  
 [!code-vb[VbVbalrMyWebService#1](../../../visual-basic/language-reference/objects/codesnippet/visualbasic/VbVbalrMyWebService/Form1.vb#1)]  
  
 Per il corretto funzionamento dell'esempio, il progetto deve fare riferimento a un servizio Web denominato `Converter` che esponga il metodo `ConvertTemperature`.  Per ulteriori informazioni, vedere [Accessing Application Web Services](../../../visual-basic/developing-apps/programming/accessing-application-web-services.md).  
  
 Questo codice non può essere utilizzato nel progetto di un'applicazione Web.  
  
## Requisiti  
  
### Disponibilità per tipo di progetto  
  
|||  
|-|-|  
|Tipo di progetto|Disponibile|  
|Applicazione Windows|**Sì**|  
|Libreria di classi|**Sì**|  
|Applicazione console|**Sì**|  
|Libreria di controlli Windows|**Sì**|  
|Libreria di controlli Web|**Sì**|  
|Servizio Windows|**Sì**|  
|Sito Web|No|  
  
## Vedere anche  
 <xref:System.Web.Services.Protocols.SoapHttpClientProtocol>   
 <xref:System.ArgumentException>   
 [Accessing Application Web Services](../../../visual-basic/developing-apps/programming/accessing-application-web-services.md)