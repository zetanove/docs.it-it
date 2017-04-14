---
title: "UriTemplate e UriTemplateTable | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5cbbe03f-4a9e-4d44-9e02-c5773239cf52
caps.latest.revision: 24
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 24
---
# UriTemplate e UriTemplateTable
Gli sviluppatori Web devono poter essere in grado di descrivere la forma e il layout degli URI a cui rispondono i loro servizi.In [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] sono state aggiunte due nuove classi per consentire agli sviluppatori di controllare gli URI.<xref:System.UriTemplate> e <xref:System.UriTemplateTable> rappresentano in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] gli elementi fondamentali del motore di invio basato su URI.Queste classi possono inoltre essere utilizzate autonomamente, in modo da consentire agli sviluppatori di sfruttare i modelli e il meccanismo di mapping degli URI senza dover implementare un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Modelli  
 I modelli consentono di descrivere set di URI relativi.Nella tabella seguente il set di modelli URI illustra come definire un sistema per il recupero di vari tipi di informazioni meteorologiche.  
  
|Dati|Modello|  
|----------|-------------|  
|Previsioni nazionali|previsioni\/nazionali|  
|Previsioni regionali|previsioni\/{regione}|  
|Previsioni urbane|previsioni\/{regione}\/{città}|  
|Previsioni di attività|previsioni\/{regione}\/{città}\/{attività}|  
  
 Questa tabella descrive un insieme di URI simili fra loro dal punto di vista strutturale.Ogni voce è un modello URI.I segmenti nelle parentesi graffe descrivono variabili,mentre quelli non all'interno di parentesi graffe descrivono stringhe letterali.Le classi modello di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consentono di sviluppare un elemento di codice che accetta un URI in ingresso, ad esempio "\/previsioni\/Campania\/Napoli\/ciclo", e quindi lo fa corrispondere al modello che lo descrive, ovvero "\/previsioni\/{regione}\/{città}\/{attività}".  
  
## UriTemplate  
 L'elemento <xref:System.UriTemplate> è una classe che incapsula un modello URI.Il costruttore accetta un parametro di stringa che definisce il modello.Questa stringa contiene il modello nel formato descritto nella sezione seguente.La classe <xref:System.UriTemplate> fornisce metodi che consentono di mettere in corrispondenza un URI in ingresso con un modello, generare un URI a partire da un modello, recuperare una raccolta di nomi variabili utilizzati nel modello, determinare se due modelli sono equivalenti e restituire la stringa del modello.  
  
 Il metodo <xref:System.UriTemplate.Match%28System.Uri%2CSystem.Uri%29> accetta un indirizzo di base e un URI candidato e tenta di creare una corrispondenza tra l'URI e il modello.Se il tentativo ha esito positivo, viene restituita un'istanza della classe <xref:System.UriTemplateMatch>.L'oggetto <xref:System.UriTemplateMatch> contiene un URI di base, l'URI candidato, una raccolta nome\/valore dei parametri di query, una matrice di segmenti di percorso relativo, una raccolta nome\/valore di variabili di cui era stata creata una corrispondenza, l'istanza <xref:System.UriTemplate> utilizzata per creare la corrispondenza, una stringa contenente eventuali porzioni prive di corrispondenza dell'URI candidato \(utilizzate se il modello contiene un carattere jolly\) e un oggetto associato al modello.  
  
> [!NOTE]
>  Quando viene creata una corrispondenza tra un URI candidato e un modello, la classe <xref:System.UriTemplate> ignora lo schema e il numero di porta.  
  
 Sono disponibili due metodi che consentono di generare un URI da un modello: <xref:System.UriTemplate.BindByName%28System.Uri%2CSystem.Collections.Specialized.NameValueCollection%29> e [BindByPosition\(Uri, String\<xref:System.UriTemplate.BindByPosition%28System.Uri%2CSystem.String%5B%5D%29>.Il metodo <xref:System.UriTemplate.BindByName%28System.Uri%2CSystem.Collections.Specialized.NameValueCollection%29> accetta un indirizzo di base e una raccolta nome\/valore di parametri.Questi parametri vengono sostituiti con le variabili quando il modello viene associato.Il metodo [BindByPosition\(Uri, String\<xref:System.UriTemplate.BindByPosition%28System.Uri%2CSystem.String%5B%5D%29> accetta invece le coppie nome\/valore e le sostituisce da sinistra a destra.  
  
 Il metodo <xref:System.UriTemplate.ToString> restituisce la stringa di modello.  
  
 La proprietà <xref:System.UriTemplate.PathSegmentVariableNames%2A> contiene la raccolta dei nomi delle variabili utilizzate all'interno dei segmenti di percorso contenuti nella stringa di modello.  
  
 Il metodo <xref:System.UriTemplate.IsEquivalentTo%28System.UriTemplate%29> accetta un oggetto <xref:System.UriTemplate> come parametro e restituisce un valore booleano che specifica se i due modelli sono equivalenti.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] la sezione Equivalenza fra modelli più avanti in questo argomento.  
  
 <xref:System.UriTemplate> può essere utilizzato con qualsiasi schema URI conforme alla grammatica URI HTTP.Di seguito vengono riportati esempi di schemi URI supportati.  
  
-   http:\/\/  
  
-   https:\/\/  
  
-   net.tcp:\/\/  
  
-   net.pipe:\/\/  
  
-   sb:\/\/  
  
 Schemi come file:\/\/ e urn:\/\/ non sono conformi alla grammatica URI HTTP e causeranno risultati imprevisti se utilizzati con modelli URI.  
  
### Sintassi della stringa di modello  
 Ogni modello presenta tre parti: un percorso, una query facoltativa e un frammento facoltativo.Si consideri ad esempio il modello seguente:  
  
```  
"/weather/{state}/{city}?forecast={length)#frag1  
```  
  
 Il percorso è "\/previsioni\/{regione}\/{città}", la query è "?previsioni\={durata\)" e il frammento è "\#framm1".  
  
 Le barre iniziali e finali sono facoltative nell'espressione del percorso.Le espressioni di query e di frammento possono essere omesse del tutto.Un percorso è costituito da una serie di segmenti delimitati dal simbolo "\/" e ogni segmento può contenere un valore letterale, un nome variabile \(riportato fra parentesi graffe\) o un carattere jolly \(indicato tramite il simbolo "\*"\).Nel modello precedente il segmento "\\previsioni\\ è un valore letterale, mentre"{regione}" e "{città}" rappresentano variabili.Le variabili vengono denominate a partire dal nome contenuto fra le parentesi graffe e in un secondo momento possono essere sostituite con un valore effettivo allo scopo di creare un *URI chiuso*.Il carattere jolly è facoltativo, ma può essere utilizzato solo alla fine dell'URI per indicare una corrispondenza logica con il resto del percorso.  
  
 L'espressione di query, se presente, specifica una serie di coppie nome\/valore non ordinate delimitate dal simbolo "&".Gli elementi dell'espressione di query possono essere coppie letterali \(x\=2\) o una coppia variabile \(x\={var}\).Solo il lato destro della query può contenere un'espressione variabile.\({someName} \= {someValue} non è consentito.Non è consentito utilizzare valori non abbinati \(?x\).Non c'è differenza tra un'espressione di query vuota e un'espressione di query contenente il solo carattere "?" poiché entrambe significano "qualsiasi query".  
  
 L'espressione di frammento può essere data da un valore letterale. Non sono consentite le variabili.  
  
 Tutti i nomi variabili del modello contenuti in una stringa di modello devono essere univoci.I nomi variabili del modello non fanno distinzione tra maiuscole e minuscole.  
  
 Esempi di stringhe di modello valide:  
  
-   ""  
  
-   "\/casa"  
  
-   "\/casa\/\*"  
  
-   "{casa}\/stanza"  
  
-   "{casa}\/{stanza}\/letto\/{piumone}"  
  
-   "casa\/{stanza}"  
  
-   "casa\/{stanza}\/\*"  
  
-   "casa\/stanza?x\=2"  
  
-   "casa\/{stanza}?x\={letto}"  
  
-   "casa\/{stanza}?x\={letto}&y\=divano"  
  
-   "?x\={casa}"  
  
-   "casa?x\=3&y\={var}  
  
 Esempi di stringhe di modello non valide:  
  
-   "{casa}\/{CASA}\/x\=2": nomi variabili duplicati.  
  
-   "{casa}\/stanza\/?letto\={casa}": nomi variabili duplicati.  
  
-   "?x\=2&x\=3": le coppie nome\/valore all'interno di una stringa di query devono essere univoche, anche se sono valori letterali.  
  
-   "?x\=2&": il formato della stringa di query non è valido.  
  
-   "?2&x \={casa}": la stringa di query deve contenere coppie nome\/valore.  
  
-   "?y\=2&&X\=3": la stringa di query deve contenere coppie nome\/valore e i nomi non possono iniziare con "&".  
  
### Segmenti di percorso composti  
 I segmenti di percorso composti consentono a un singolo segmento di percorso URI di contenere più variabili, nonché variabili combinate con valori letterali.Di seguito vengono riportati esempi di segmenti di percorso composti validi.  
  
-   \/nomefile.{ext}\/  
  
-   \/{nomefile}.jpg\/  
  
-   \/{nomefile}.{ext}\/  
  
-   \/{a}.{b}someLiteral{c}\({d}\)\/  
  
 Di seguito vengono riportati esempi di segmenti di percorso non validi.  
  
-   \/{}: le variabili devono avere un nome.  
  
-   \/{casa}{stanza}: le variabili devono essere separate da un valore letterale.  
  
### Segmenti di percorso composti e corrispondenti  
 I segmenti di percorso composti consentono di definire un UriTemplate che dispone di più variabili all'interno di un solo segmento di percorso.Ad esempio, nella stringa di modello seguente: "Addresses\/{state}.{city}" due variabili \(stato e città\) sono definite all'interno dello stesso segmento.Questo modello corrisponderebbe a un URL quale "http:\/\/example.com\/Washington.Redmond" ma corrisponderà anche un URL quale "http:\/\/example.com\/Washington.Redmond.Microsoft".Nel secondo caso, la variabile dello stato conterrà "Washington" e la variabile della città conterrà "Redmond.Microsoft".In questo caso il qualsiasi testo \(eccetto '\/'\) corrisponderà alla variabile {city}.Se si desidera un modello che non corrisponderà al testo "extra", posizionare la variabile in un segmento di modello separato, ad esempio: "Addresses\/{state}\/{city}".  
  
### Segmenti con caratteri jolly con nome  
 Un segmento con carattere jolly con nome è un qualsiasi segmento variabile di percorso il cui nome di variabile inizia con il carattere jolly '\*'.La stringa di modello seguente contiene un segmento con carattere jolly con nome denominato "casa".  
  
```  
"literal/{*shoe}"  
```  
  
 I segmenti con caratteri jolly devono rispettare le regole seguenti:  
  
-   Per ogni stringa di modello può esistere al massimo un segmento con carattere jolly con nome.  
  
-   Un segmento con carattere jolly con nome deve comparire nel segmento all'estrema destra del percorso.  
  
-   Un segmento con carattere jolly con nome non può coesistere con un segmento con carattere jolly anonimo all'interno della stessa stringa di modello.  
  
-   Il nome di un segmento con carattere jolly con nome deve essere univoco.  
  
-   I segmenti con carattere jolly con nome non possono disporre di valori predefiniti.  
  
-   I segmenti con carattere jolly con nome non possono terminare con "\/".  
  
### Valori di variabili predefiniti  
 I valori di variabili predefiniti consentono di specificare valori predefiniti per variabili all'interno di un modello.È possibile specificare le variabili predefinite con parentesi graffe che dichiarano la variabile o come una raccolta passata al costruttore UriTemplate.Nel modello seguente vengono illustrati due modi per specificare <xref:System.UriTemplate> con variabili con valori predefiniti.  
  
```  
UriTemplate t = new UriTemplate("/test/{a=1}/{b=5}");  
```  
  
 Questo modello dichiara una variabile denominata `a` con valore predefinito `1` e una variabile denominata `b` con valore predefinito `5`.  
  
> [!NOTE]
>  Solo le variabili del segmento di percorso possono presentare valori predefiniti.Le variabili delle stringhe di query, dei segmenti composti e quelle con carattere jolly con nome non possono presentare valori predefiniti.  
  
 Nell'esempio di codice seguente viene illustrato come gestire i valori di variabili predefiniti quando si crea una corrispondenza con un URI candidato.  
  
```  
Uri baseAddress = new Uri("http://localhost:800   
Dictionary<string,string> defVals = new Dictionary<string,string> {{"a","1"}, {"b", "5"}};  
UriTemplate t = new UriTemplate("/test/{a}/{b}", defVals);0");  
UriTemplate t = new UriTemplate("/{state=WA}/{city=Redmond}/", true);  
Uri candidate = new Uri("http://localhost:8000/OR");  
  
UriTemplateMatch m1 = t.Match(baseAddress, candidate);  
  
// Display contents of BoundVariables  
foreach (string key in m1.BoundVariables.AllKeys)  
{  
    Console.WriteLine("\t\t{0}={1}", key, m1.BoundVariables[key]);  
}  
// The output of the above code is  
// Template: /{state=WA}/{city=Redmond}/  
// Candidate URI: http://localhost:8000/OR  
// BoundVariables:  
//      STATE=OR  
//       CITY=Redmond  
  
```  
  
> [!NOTE]
>  Contrariamente a un URI come http:\/\/localhost:8000\/, un URI come http:\/\/localhost:8000\/\/\/ non corrisponde al modello elencato nel codice riportato in precedenza.  
  
 Nell'esempio di codice seguente viene illustrato come gestire i valori di variabili predefiniti quando si crea un URI con un modello.  
  
```  
Uri baseAddress = new Uri("http://localhost:8000/");  
Dictionary<string,string> defVals = new Dictionary<string,string> {{"a","1"}, {"b", "5"}};  
UriTemplate t = new UriTemplate("/test/{a}/{b}", defVals);  
NameValueCollection vals = new NameValueCollection();  
vals.Add("a", "10");  
  
Uri boundUri = t.BindByName(baseAddress, vals);  
Console.WriteLine("BaseAddress: {0}", baseAddress);  
Console.WriteLine("Template: {0}", t.ToString());  
  
Console.WriteLine("Values: ");  
foreach (string key in vals.AllKeys)  
{  
    Console.WriteLine("\tKey = {0}, Value = {1}", key, vals[key]);  
}  
Console.WriteLine("Bound URI: {0}", boundUri);  
  
// The output of the preceding code is  
// BaseAddress: http://localhost:8000/  
// Template: /test/{a}/{b}  
// Values:  
//     Key = a, Value = 10  
// Bound URI: http://localhost:8000/test/10/5  
  
```  
  
 Quando a una variabile viene assegnato il valore predefinito `null`, è necessario tenere conto di alcuni vincoli aggiuntivi.Una variabile può presentare il valore predefinito `null` se è contenuta nel segmento più a destra della stringa del modello o se tutti i segmenti a destra del segmento presentano valori predefiniti `null`.Di seguito vengono riportate stringhe di modello valide con valori predefiniti `null`:  
  
-   ```  
    UriTemplate t = new UriTemplate("shoe/{boat=null}");  
    ```  
  
-   ```  
    UriTemplate t = new UriTemplate("{shoe=null}/{boat=null}");  
    ```  
  
-   ```  
    UriTemplate t = new UriTemplate("{shoe=1}/{boat=null}");  
    ```  
  
 Di seguito vengono riportate stringhe di modello non valide con valori predefiniti `null`:  
  
-   ```  
    UriTemplate t = new UriTemplate("{shoe=null}/boat"); // null default must be in the right most path segment  
    ```  
  
-   ```  
    UriTemplate t = new UriTemplate("{shoe=null}/{boat=x}/{bed=null}"); // shoe cannot have a null default because boat does not have a default null value  
    ```  
  
### Valori predefiniti e corrispondenza  
 Quando si crea una corrispondenza tra un URI candidato e un modello con valori predefiniti, se i valori non sono specificati nell'URI candidato i valori predefiniti verranno inseriti nella raccolta <xref:System.UriTemplateMatch.BoundVariables%2A>.  
  
### Equivalenza fra modelli  
 Due modelli sono *strutturalmente equivalenti* se contengono variabili negli stessi segmenti e tutti i valori letterali dei modelli corrispondono.Ad esempio, i modelli seguenti sono strutturalmente equivalenti:  
  
-   \/a\/{var1}\/b b\/{var2}?x\=1&y\=2  
  
-   a\/{x}\/b%20b\/{var1}?y\=2&x\=1  
  
-   a\/{y}\/B%20B\/{z}\/?y\=2&x\=1  
  
 Alcune considerazioni:  
  
-   Se un modello contiene barre iniziali, solo la prima viene ignorata.  
  
-   Quando si verifica se due stringhe di modello sono strutturalmente equivalenti, i nomi variabili, i segmenti di percorso e le stringhe di query non fanno distinzione fra maiuscole e minuscole.  
  
-   Le stringhe di query non sono ordinate.  
  
## UriTemplateTable  
 La classe <xref:System.UriTemplateTable> rappresenta una tabella associativa di oggetti <xref:System.UriTemplate> associata a un oggetto scelto dallo sviluppatore.Ogni tabella <xref:System.UriTemplateTable> deve contenere almeno un modello <xref:System.UriTemplate> prima di chiamare il metodo <xref:System.UriTemplateTable.MakeReadOnly%28System.Boolean%29>.È possibile modificare il contenuto di <xref:System.UriTemplateTable> finché non viene chiamato il metodo <xref:System.UriTemplateTable.MakeReadOnly%28System.Boolean%29>.Quando viene chiamato il metodo <xref:System.UriTemplateTable.MakeReadOnly%28System.Boolean%29> viene eseguita una convalidail cui tipo dipende dal valore del parametro `allowMultiple` da passare al metodo <xref:System.UriTemplateTable.MakeReadOnly%28System.Boolean%29>.  
  
 Quando al metodo <xref:System.UriTemplateTable.MakeReadOnly%28System.Boolean%29> viene passato il valore `false`, l'oggetto <xref:System.UriTemplateTable> verifica se la tabella contiene modelli.Se rileva modelli strutturalmente equivalenti, genera un'eccezione.Questo metodo viene utilizzato insieme al metodo <xref:System.UriTemplateTable.MatchSingle%28System.Uri%29> quando si desidera garantire che solo un modello corrisponda a un determinato URI in ingresso.  
  
 Quando viene chiamato il metodo <xref:System.UriTemplateTable.MakeReadOnly%28System.Boolean%29> passando `true`, <xref:System.UriTemplateTable> consente la presenza di più modelli strutturalmente equivalenti all'interno di <xref:System.UriTemplateTable>.  
  
 Se un set di oggetti <xref:System.UriTemplate> aggiunti a un oggetto <xref:System.UriTemplateTable> contiene stringhe di query, queste non devono essere ambigue.È tuttavia consentito utilizzare stringhe di query identiche.  
  
> [!NOTE]
>  Mentre <xref:System.UriTemplateTable> consente la presenza di indirizzi di base che utilizzano schemi diversi da HTTP, lo schema e il numero di porta vengono ignorati quando si creano corrispondenze tra URI candidati e modelli.  
  
### Ambiguità delle stringhe di query  
 I modelli che condividono un percorso equivalente contengono stringhe di query ambigue se esiste un URI che corrisponde a più di un modello.  
  
 I set seguenti di stringhe di query non sono ambigui fra loro:  
  
-   ?x\=1  
  
-   ?x\=2  
  
-   ?x\=3  
  
-   ?x\=1&y\={var}  
  
-   ?x\=2&z\={var}  
  
-   ?x\=3  
  
-   ?x\=1  
  
-   ?  
  
-   ?x\={var}  
  
-   ?  
  
-   ?m\=get&c\=rss  
  
-   ?m\=put&c\=rss  
  
-   ?m\=get&c\=atom  
  
-   ?m\=put&c\=atom  
  
 I set seguenti di modelli di stringhe di query sono ambigui fra loro:  
  
-   ?x\=1  
  
-   ?x\={var}  
  
 "x\=1": corrisponde a entrambi i modelli.  
  
-   ?x\=1  
  
-   ?y\=2  
  
 "x\=1&y\=2" corrisponde a entrambi i modelli.Ciò è dovuto al fatto che una stringa di query può contenere più variabili di stringa rispetto al modello a cui corrisponde.  
  
-   ?x\=1  
  
-   ?x\=1&y\={var}  
  
 "x\=1&y\=3" corrisponde a entrambi i modelli.  
  
-   ?x\=3&y\=4  
  
-   ?x\=3&z\=5  
  
> [!NOTE]
>  I caratteri á e Á sono considerati caratteri diversi quando sono contenuti in un percorso URI o in un valore letterale di un segmento di percorso <xref:System.UriTemplate>. I caratteri a e A sono invece considerati uguali.I caratteri á e Á sono considerati caratteri uguali quando sono contenuti in un elemento {nomeVariabile} del modello <xref:System.UriTemplate> o in una stringa di query. Anche in questo caso i caratteri a e A sono considerati uguali.  
  
## Vedere anche  
 [Panoramica sul modello di programmazione HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md)   
 [Modello a oggetti per la programmazione HTTP Web di WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-object-model.md)   
 [UriTemplate](../../../../docs/framework/wcf/samples/uritemplate-sample.md)   
 [UriTemplateTable](../../../../docs/framework/wcf/samples/uritemplate-table-sample.md)   
 [Dispatcher della tabella UriTemplate](../../../../docs/framework/wcf/samples/uritemplate-table-dispatcher-sample.md)