---
keywords: Experience Platform; home; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Experience-Datenmodell; Experience-Datenmodell; Datenmodell; Datenmodell; Schemaregistrierung; Schema Registry; Kompatibilität; Kompatibilitätsmodus; Kompatibilitätsmodus; Feldtyp; Feldtypen
solution: Experience Platform
title: Handbuch zur Schema Registry-API
description: Dieses Dokument enthält zusätzliche Informationen zum Arbeiten mit der Schema Registry-API.
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 28891cf37dc9ffcc548f4c0565a77f62432c0b44
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 28%

---

# Handbuch zur Schema Registry-API

Dieses Dokument enthält zusätzliche Informationen zum Arbeiten mit der [!DNL Schema Registry]-API.

## Verwenden von Abfrageparametern {#query}

Der [!DNL Schema Registry] unterstützt die Verwendung von Abfrageparametern zur Seite und Filterung von Ergebnissen bei der Auflistung von Ressourcen.

>[!NOTE]
>
>Wenn mehrere Abfrageparameter kombiniert werden, müssen diese durch Und-Zeichen (`&`) getrennt werden.

### Paging {#paging}

Zu den häufigsten Abfrageparametern für das Paging gehören:

| Parameter | Beschreibung |
| --- | --- |
| `orderby` | Sortieren Sie die Ergebnisse nach einer bestimmten Eigenschaft. Beispiel: `orderby=title` sortiert die Ergebnisse in aufsteigender Reihenfolge (A-Z) nach Titel. Durch Hinzufügen von &quot;`-`&quot;vor dem Parameterwert (`orderby=-title`) werden Elemente nach Titel in absteigender Reihenfolge sortiert (Z-A). |
| `limit` | Bei Verwendung in Verbindung mit einem `orderby` -Parameter beschränkt `limit` die maximale Anzahl von Elementen, die für eine bestimmte Anfrage zurückgegeben werden sollen. Dieser Parameter kann nur verwendet werden, wenn ein `orderby` -Parameter vorhanden ist.<br><br>Der Parameter `limit` gibt eine positive Ganzzahl (zwischen `0` und `500`) als *Hinweis* an, die die maximale Anzahl der zurückzugebenden Elemente angibt. Beispielsweise gibt `limit=5` nur fünf Ressourcen in der Liste zurück. Dieser Wert wird jedoch nicht genau berücksichtigt. Die tatsächliche Antwortgröße kann kleiner oder größer sein, da eine Einschränkung darin besteht, dass der zuverlässige Vorgang des Parameters `start` bereitgestellt werden muss, sofern einer bereitgestellt wird. |
| `start` | Bei Verwendung in Verbindung mit einem `orderby` -Parameter gibt `start` an, wo die untergeordnete Liste von Elementen beginnen soll. Dieser Parameter kann nur verwendet werden, wenn ein `orderby` -Parameter vorhanden ist. Dieser Wert kann aus dem Attribut `_page.next` einer Listenantwort abgerufen und für den Zugriff auf die nächste Ergebnisseite verwendet werden. Wenn der `_page.next` -Wert null ist, ist keine zusätzliche Seite verfügbar.<br><br>Normalerweise wird dieser Parameter weggelassen, um die erste Ergebnisseite zu erhalten. Danach sollte `start` auf den Maximalwert der primären Sortiereigenschaft des auf der vorherigen Seite empfangenen `orderby` -Felds gesetzt werden. Die API-Antwort gibt dann Einträge zurück, die mit jenen beginnen, die eine primäre Sortiereigenschaft von `orderby` aufweisen, die strikt größer ist als (für aufsteigende Werte) oder strikt kleiner ist als (für absteigende Werte) der angegebene Wert.<br><br>Wenn der Parameter `orderby` beispielsweise auf `orderby=name,firstname` gesetzt ist, enthält der Parameter `start` einen Wert für die Eigenschaft `name`. Wenn Sie in diesem Fall die nächsten 20 Einträge einer Ressource anzeigen möchten, die unmittelbar auf den Namen &quot;Miller&quot;folgt, verwenden Sie: `?orderby=name,firstname&start=Miller&limit=20`. |

{style="table-layout:auto"}

### Filter {#filtering}

Sie können Ergebnisse mithilfe des Parameters `property` filtern, mit dem ein bestimmter Operator auf eine bestimmte JSON-Eigenschaft in den abgerufenen Ressourcen angewendet wird. Zu den unterstützten Operatoren gehören:

| Operator | Beschreibung | Beispiel |
| --- | --- | --- |
| `==` | Filtert danach, ob die Eigenschaft dem bereitgestellten Wert entspricht. | `property=title==test` |
| `!=` | Filtert danach, ob die Eigenschaft nicht dem bereitgestellten Wert entspricht. | `property=title!=test` |
| `<` | Filtert danach, ob die Eigenschaft kleiner als der angegebene Wert ist. | `property=version<5` |
| `>` | Filtert danach, ob die Eigenschaft größer als der angegebene Wert ist. | `property=version>5` |
| `<=` | Filtert danach, ob die Eigenschaft kleiner oder gleich dem angegebenen Wert ist. | `property=version<=5` |
| `>=` | Filtert danach, ob die Eigenschaft größer oder gleich dem angegebenen Wert ist. | `property=version>=5` |
| (Keine) | Wenn nur der Eigenschaftsname festgelegt wird, werden nur Einträge zurückgegeben, in denen die Eigenschaft vorhanden ist. | `property=title` |

{style="table-layout:auto"}

>[!TIP]
>
>Sie können den Parameter `property` verwenden, um Schemafeldgruppen nach ihrer kompatiblen Klasse zu filtern. Beispielsweise gibt `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` nur Feldergruppen zurück, die mit der Klasse [!DNL XDM Individual Profile] kompatibel sind.

## Kompatibilitätsmodus {#compatibility}

[!DNL Experience Data Model] (XDM) ist eine öffentlich dokumentierte Spezifikation, die von Adobe zur Verbesserung der Interoperabilität, Ausdrucksfähigkeit und Leistungsfähigkeit digitaler Erlebnisse unterstützt wird. Adobe verwaltet den Quell-Code und formale XDM-Definitionen in einem [Open-Source-Projekt auf GitHub](https://github.com/adobe/xdm/). Diese Definitionen werden in XDM Standard Notation geschrieben, wobei JSON-LD (JavaScript Object Notation for Linked Data) und JSON-Schema als Grammatik zur Definition von XDM-Schemata verwendet werden.

Wenn Sie sich die formalen XDM-Definitionen im öffentlichen Repository ansehen, können Sie erkennen, dass sich das Standard-XDM von dem unterscheidet, das Sie in Adobe Experience Platform sehen. Was Sie in [!DNL Experience Platform] sehen, wird als Kompatibilitätsmodus bezeichnet und bietet eine einfache Zuordnung zwischen Standard-XDM und der Art und Weise, wie es in [!DNL Platform] verwendet wird.

### Funktionsweise des Kompatibilitätsmodus

Der Kompatibilitätsmodus ermöglicht es dem XDM JSON-LD-Modell, mit der vorhandenen Dateninfrastruktur zu arbeiten, indem Werte innerhalb des XDM-Standards verändert werden, während die Semantik gleich bleibt. Es verwendet eine verschachtelte JSON-Struktur, die Schemata in einem baumähnlichen Format anzeigt.

Der Hauptunterschied, den Sie zwischen Standard-XDM und Kompatibilitätsmodus bemerken, ist die Entfernung des Präfix „xdm:“ für Feldnamen.

Im Folgenden finden Sie einen Vergleich, der sowohl im Standard-XDM als auch im Kompatibilitätsmodus geburtstagsbezogene Felder (mit entfernten „Beschreibungsattributen“) nebeneinander anzeigt. Beachten Sie, dass die Felder für den Kompatibilitätsmodus einen Verweis auf das XDM-Feld und seinen Datentyp in den Attributen „meta:xdmField“ und „meta:xdmType“ enthalten.

<table style="table-layout:auto">
  <th>Standard-XDM</th>
  <th>Kompatibilitätsmodus</th>
  <tr>
  <td>
  <pre class=" language-json">
{
  "xdm:birthDate": {
    "title": "Birth Date",
    "type": "string",
    "format": "date"
  },
  "xdm:birthDayAndMonth": {
    "title": "Birth Date",
    "type": "string",
    "pattern": "[0-1][0-9]-[0-9][0-9]"
  },
  "xdm:birthYear": {
    "title": "Birth year",
    "type": "integer",
    "minimum": 1,
    "Maximum": 32767
  }
}
  </pre>
  </td>
  <td>
  <pre class=" language-json">
{
  "birthDate": {
    "title": "Birth Date",
    "type": "string",
    "format": "date",
    "meta:xdmField": "xdm:birthDate",
    "meta:xdmType": "date"
  },
  "birthDayAndMonth": {
    "title": "Birth Date",
    "type": "string",
    "pattern": "[0-1][0-9]-[0-9][0-9]",
    "meta:xdmField": "xdm:birthDayAndMonth",
    "meta:xdmType": "string"
  },
  "birthYear": {
    "title": "Birth year",
    "type": "integer",
    "minimum": 1,
    "Maximum": 32767,
    "meta:xdmField": "xdm:birthYear",
    "meta:xdmType": "short"
  }
}
      </pre>
  </td>
  </tr>
</table>

### Warum ist der Kompatibilitätsmodus erforderlich?

Adobe Experience Platform ist für die Verwendung mit mehreren Lösungen und Diensten konzipiert, die jeweils eigene technische Herausforderungen und Einschränkungen aufweisen (z. B. wie bestimmte Technologien Sonderzeichen handhaben). Um diese Einschränkungen zu überwinden, wurde der Kompatibilitätsmodus entwickelt.

Die meisten [!DNL Experience Platform] -Dienste einschließlich [!DNL Catalog], [!DNL Data Lake] und [!DNL Real-Time Customer Profile] verwenden [!DNL Compatibility Mode] anstelle von Standard-XDM. Die [!DNL Schema Registry]-API verwendet auch [!DNL Compatibility Mode] und die Beispiele in diesem Dokument werden alle mit [!DNL Compatibility Mode] angezeigt.

Es lohnt sich zu wissen, dass eine Zuordnung zwischen dem Standard-XDM und der Art und Weise erfolgt, wie es in [!DNL Experience Platform] operationalisiert wird. Sie sollte jedoch Ihre Verwendung von [!DNL Platform]-Diensten nicht beeinträchtigen.

Das Open-Source-Projekt steht Ihnen zur Verfügung. Wenn es jedoch darum geht, mit Ressourcen über [!DNL Schema Registry] zu interagieren, bieten die API-Beispiele in diesem Dokument die Best Practices, die Sie kennen und befolgen sollten.
