---
title: "Elemento &lt;httpListener&gt; (impostazioni di rete) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 62f121fd-3f2e-4033-bb39-48ae996bfbd9
caps.latest.revision: 7
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 7
---
# Elemento &lt;httpListener&gt; (impostazioni di rete)
Personalizza i parametri utilizzati dalla classe <xref:System.Net.HttpListener>.  
  
## Sintassi  
  
```  
  
      <httpListener  
  unescapeRequestUrl ="true|false"  
/>  
```  
  
## Tipo  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attribute|Descrizione|  
|---------------|-----------------|  
|unescapeRequestUrl|Valore booleano che indica se un'istanza <xref:System.Net.HttpListener> utilizza l'URI senza codice di escape non elaborato anziché l'URI convertito.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[impostazioni](../../../../../docs/framework/configure-apps/file-schema/network/settings-element-network-settings.md)|Configura opzioni di rete di base per lo spazio dei nomi <xref:System.Net>.|  
  
## Note  
 L'attributo [indica se T:System.Net.HttpListener](assetId:///indica se T:System.Net.HttpListener?qualifyHint=False&autoUpgrade=True) utilizza l'URI senza codice di escape non elaborato anziché l'URI convertito laddove vengono convertiti i valori con codifica in percentuale e vengono eseguiti altri passaggi della normalizzazione.  
  
 Quando un'istanza <xref:System.Net.HttpListener> riceve una richiesta tramite il servizio `http.sys`, crea un'istanza della stringa URI fornita da `http.sys` e l'espone come proprietà <xref:System.Net.HttpListenerRequest.Url%2A?displayProperty=fullName>.  
  
 Il servizio `http.sys` espone due stringhe URI di richiesta:  
  
-   URI non elaborato  
  
-   URI convertito  
  
 L'URI non elaborato è rappresentato dall'oggetto <xref:System.Uri?displayProperty=fullName> fornito nella riga di richiesta di una richiesta HTTP:  
  
 `GET /path/`  
  
 `Host: www.contoso.com`  
  
 L'URI non elaborato fornito da `http.sys` per la richiesta sopra indicata è "\/path\/."  Questo rappresenta la stringa che segue il verbo HTTP come è inviato sulla rete.  
  
 Il servizio `http.sys` crea un URI convertito partendo dalle informazioni disponibili nella richiesta tramite l'URI presente nella riga della richiesta HTTP e nell'intestazione Host allo scopo di determinare il server di origine a cui la richiesta deve essere inoltrata.  Questa operazione viene eseguita confrontando le informazioni dalla richiesta con un set di prefissi URI registrati.  La documentazione SDK del server HTTP si riferisce a questo URI convertito come la struttura HTTP\_COOKED\_URL.  
  
 Per essere in grado di confrontare la richiesta con i prefissi URI registrati, è necessario effettuare alcune normalizzazioni della richiesta.  Nell'esempio precedente l'URI convertito sarebbe:  
  
 `http://www.contoso.com/path/`  
  
 Il servizio `http.sys` combina il valore della proprietà <xref:System.Uri.Host%2A?displayProperty=fullName> e la stringa della riga della richiesta in moda da creare un URI convertito.  Inoltre, `http.sys` e la classe <xref:System.Uri?displayProperty=fullName> esegue anche quanto di seguito descritto:  
  
-   Non effettua l'escape di tutte le percentuali dei valori codificati.  
  
-   Converte caratteri non ASCII con codifica in percentuale in una rappresentazione UTF\-16 del carattere.  Notare che sono supportati i caratteri UTF\-8, ANSI\/DBCS e Unicode \(codifica Unicode tramite il formato %uXXXX\).  
  
-   Esegue gli altri passaggi della normalizzazione, come la compressione del percorso.  
  
 Poiché la richiesta non contiene alcuna informazione sulla codifica utilizzata per i valori con codifica in percentuale, potrebbe non essere possibile determinare la codifica corretta unicamente tramite l'analisi dei valori con codifica in percentuale.  
  
 Pertanto `http.sys` fornisce due chiavi del Registro di sistema per la modifica del processo:  
  
|Chiave del Registro di sistema|Valore predefinito|Descrizione|  
|------------------------------------|------------------------|-----------------|  
|EnableNonUTF8|1|Se è zero, `http.sys` accetta solo URL con codifica UTF\-8.<br /><br /> Se diverso da zero, `http.sys` accetta anche URL con codifica ANSI o DBCS nelle richieste.|  
|FavorUTF8|1|Se diverso da zero, `http.sys` tenta sempre di decodificare prima un URL come UTF\-8; se quella conversione non riesce e se EnableNonUTF8 è diverso da zero, Http.sys tenta quindi di decodificarlo come ANSI o DBCS.<br /><br /> Se è zero \(e EnableNonUTF8 è diverso da zero\), `http.sys` tenta di decodificarlo come ANSI o DBCS; se non vi riesce, prova a convertirlo in UTF\-8.|  
  
 Quando <xref:System.Net.HttpListener> riceve una richiesta, utilizza l'URI convertito da `http.sys` come input alla proprietà <xref:System.Net.HttpListenerRequest.Url%2A>.  
  
 Occorre inoltre supportare caratteri oltre ai caratteri e numeri in URI.  Un esempio è dato dal seguente URI, utilizzato per recuperare informazioni sul cliente in base al numero cliente "1\/3812":  
  
 `http://www.contoso.com/Customer('1%2F3812')/`  
  
 Notare la barra con codifica in percentuale nell'Uri \(%2F\).  Questo è necessario poiché in questo caso il carattere della barra rappresenta dati e non un delimitatore del percorso.  
  
 Il passaggio della stringa al costruttore Uri produrrà il seguente URI:  
  
 `http://www.contoso.com/Customer('1/3812')/`  
  
 La suddivisione del percorso nei relativi segmenti darebbe origine agli elementi seguenti:  
  
 `Customer('1`  
  
 `3812')`  
  
 Questo non è l'intento del mittente della richiesta.  
  
 Se l'attributo **unescapeRequestUrl** è impostato su **false**, quando <xref:System.Net.HttpListener> riceve una richiesta, utilizza l'URI non elaborato anziché l'URI convertito da?qualifyHint=False&autoUpgrade=True`http.sys come input per la proprietà` <xref:System.Net.HttpListenerRequest.Url%2A>.  
  
 Il valore predefinito per l'attributo **unescapeRequestUrl** è **true**.  
  
 La proprietà <xref:System.Net.Configuration.HttpListenerElement.UnescapeRequestUrl%2A> può essere utilizzata per ottenere il valore corrente dell'attributo **unescapeRequestUrl** dai file di configurazione applicabili.  
  
## Esempio  
 Nell'esempio di codice seguente viene mostrato come configurare la classe <xref:System.Net.HttpListener> quando riceve una richiesta per utilizzare l'URI non elaborato anziché l'URI convertito da `http.sys` come input alla proprietà <xref:System.Net.HttpListenerRequest.Url%2A>.  
  
```  
<configuration>  
  <system.net>  
    <settings>  
      <httpListener  
        unescapeRequestUrl="false"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## Informazioni sull'elemento  
  
|||  
|-|-|  
|Spazio dei nomi|System.Net|  
|Nome di schema||  
|File di convalida||  
|Può essere vuoto||  
  
## Vedere anche  
 <xref:System.Net.Configuration.HttpListenerElement>   
 <xref:System.Net.HttpListener>   
 <xref:System.Net.HttpListenerRequest.Url%2A>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)