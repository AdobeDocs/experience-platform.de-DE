---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Experience-Datenmodell; Experience-Datenmodell; Datenmodell; Datenmodell; Schemaregistrierung; Schemaregistrierung; Kompatibilität; Kompatibilitätsmodus; Kompatibilitätsmodus; Feldtyp; Feldtypen;
solution: Experience Platform
title: Handbuch zur Schema Registry-API
description: Dieses Dokument enthält zusätzliche Informationen zum Arbeiten mit der Schema Registry-API.
topic-legacy: developer guide
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 36%

---

# Handbuch zur Schema Registry-API

Dieses Dokument enthält zusätzliche Informationen zur Arbeit mit dem [!DNL Schema Registry] API.

## Verwenden von Abfrageparametern {#query}

Die [!DNL Schema Registry] unterstützt die Verwendung von Abfrageparametern zur Seite und Filterung von Ergebnissen bei der Auflistung von Ressourcen.

>[!NOTE]
>
>Wenn mehrere Abfrageparameter kombiniert werden, müssen diese durch Und-Zeichen (`&`) getrennt werden.

### Paging {#paging}

Zu den häufigsten Abfrageparametern für das Paging gehören:

| Parameter | Beschreibung |
| --- | --- |
| `orderby` | Sortieren Sie die Ergebnisse nach einer bestimmten Eigenschaft. Beispiel: `orderby=title` sortiert die Ergebnisse in aufsteigender Reihenfolge (A-Z) nach Titel. Hinzufügen einer `-` vor dem Parameterwert (`orderby=-title`) sortiert Elemente nach Titel in absteigender Reihenfolge (Z-A). |
| `limit` | Bei Verwendung in Verbindung mit einer `orderby` Parameter, `limit` begrenzt die maximale Anzahl von Elementen, die für eine bestimmte Anfrage zurückgegeben werden sollen. Dieser Parameter kann nicht ohne `orderby` Parameter vorhanden.<br><br>Die `limit` -Parameter gibt eine positive Ganzzahl an (zwischen `0` und `500`) als *Hint* , um die maximale Anzahl der zurückzugebenden Elemente anzugeben. Beispiel: `limit=5` gibt nur fünf Ressourcen in der Liste zurück. Dieser Wert wird jedoch nicht genau berücksichtigt. Die tatsächliche Antwortgröße kann kleiner oder größer sein, da die zuverlässige Funktion der `start` -Parameter, wenn einer angegeben wird. |
| `start` | Bei Verwendung in Verbindung mit einer `orderby` Parameter, `start` gibt an, wo die untergeordnete Liste von Elementen beginnen soll. Dieser Parameter kann nicht ohne `orderby` Parameter vorhanden. Dieser Wert kann aus dem `_page.next` -Attribut einer Listenantwort verwenden, um auf die nächste Ergebnisseite zuzugreifen. Wenn die Variable `_page.next` null ist, ist keine zusätzliche Seite verfügbar.<br><br>Normalerweise wird dieser Parameter weggelassen, um die erste Ergebnisseite zu erhalten. Danach `start` auf den Maximalwert der primären Sortiereigenschaft der `orderby` -Feld, das auf der vorherigen Seite empfangen wurde. Die API-Antwort gibt dann Einträge zurück, die mit jenen beginnen, die über eine primäre Sortiereigenschaft von verfügen `orderby` strikt größer als (für aufsteigende Werte) oder strikt kleiner als (für absteigende Werte) der angegebene Wert.<br><br>Wenn beispielsweise die Variable `orderby` -Parameter auf `orderby=name,firstname`, die `start` -Parameter enthält einen Wert für `name` -Eigenschaft. Wenn Sie in diesem Fall die nächsten 20 Einträge einer Ressource direkt nach dem Namen &quot;Miller&quot;anzeigen möchten, verwenden Sie: `?orderby=name,firstname&start=Miller&limit=20`. |

{style=&quot;table-layout:auto&quot;}

### Filtern {#filtering}

Sie können die Ergebnisse mithilfe der `property` -Parameter, der verwendet wird, um einen bestimmten Operator auf eine bestimmte JSON-Eigenschaft in den abgerufenen Ressourcen anzuwenden. Zu den unterstützten Operatoren gehören:

| Operator | Beschreibung | Beispiel |
| --- | --- | --- |
| `==` | Filtert danach, ob die Eigenschaft dem bereitgestellten Wert entspricht. | `property=title==test` |
| `!=` | Filtert danach, ob die Eigenschaft nicht mit dem bereitgestellten Wert übereinstimmt. | `property=title!=test` |
| `<` | Filtert danach, ob die Eigenschaft kleiner als der angegebene Wert ist. | `property=version<5` |
| `>` | Filtert danach, ob die Eigenschaft größer als der angegebene Wert ist. | `property=version>5` |
| `<=` | Filtert danach, ob die Eigenschaft kleiner oder gleich dem angegebenen Wert ist. | `property=version<=5` |
| `>=` | Filtert danach, ob die Eigenschaft größer oder gleich dem angegebenen Wert ist. | `property=version>=5` |
| `~` | Filtert danach, ob die Eigenschaft mit einem angegebenen regulären Ausdruck übereinstimmt. | `property=title~test$` |
| (Keine) | Wenn nur der Eigenschaftsname festgelegt wird, werden nur Einträge zurückgegeben, in denen die Eigenschaft vorhanden ist. | `property=title` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>Sie können die `property` Parameter zum Filtern von Schemafeldgruppen nach ihrer kompatiblen Klasse. Beispiel: `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` gibt nur Feldergruppen zurück, die mit dem [!DNL XDM Individual Profile] -Klasse.

## Kompatibilitätsmodus {#compatibility}

[!DNL Experience Data Model]Das  (XDM) ist eine öffentlich dokumentierte Spezifikation, die von Adobe zur Verbesserung der Interoperabilität, Ausdrucksfähigkeit und Leistungsfähigkeit digitaler Erlebnisse unterstützt wird. Adobe verwaltet den Quell-Code und formale XDM-Definitionen in einem [Open-Source-Projekt auf GitHub](https://github.com/adobe/xdm/). Diese Definitionen werden in XDM Standard Notation geschrieben, wobei JSON-LD (JavaScript Object Notation for Linked Data) und JSON-Schema als Grammatik zur Definition von XDM-Schemas verwendet werden.

Wenn Sie sich die formalen XDM-Definitionen im öffentlichen Repository ansehen, können Sie erkennen, dass sich das Standard-XDM von dem unterscheidet, das Sie in Adobe Experience Platform sehen. Was Sie sehen in [!DNL Experience Platform] wird als Kompatibilitätsmodus bezeichnet und bietet eine einfache Zuordnung zwischen Standard-XDM und der Art und Weise, wie es innerhalb von verwendet wird [!DNL Platform].

### Funktionsweise des Kompatibilitätsmodus

Der Kompatibilitätsmodus ermöglicht es dem XDM JSON-LD-Modell, mit der vorhandenen Dateninfrastruktur zu arbeiten, indem Werte innerhalb des XDM-Standards verändert werden, während die Semantik gleich bleibt. Es verwendet eine verschachtelte JSON-Struktur, die Schemas in einem baumähnlichen Format anzeigt.

Der Hauptunterschied, den Sie zwischen Standard-XDM und Kompatibilitätsmodus bemerken, ist die Entfernung des Präfix „xdm:“ für Feldnamen.

Im Folgenden finden Sie einen Vergleich, der sowohl im Standard-XDM als auch im Kompatibilitätsmodus geburtstagsbezogene Felder (mit entfernten „Beschreibungsattributen“) nebeneinander anzeigt. Beachten Sie, dass die Felder für den Kompatibilitätsmodus einen Verweis auf das XDM-Feld und seinen Datentyp in den Attributen „meta:xdmField“ und „meta:xdmType“ enthalten.

<table style="table-layout:auto">
  <th>Standard-XDM</th>
  <th>Kompatibilitätsmodus</th>
  <tr>
  <td>
  <pre class=" language-json">
{ "xdm:birthDate": { "title": "Geburtsdatum", "Typ": "string", "format": "date" }, "xdm:birthDayAndMonth": { "title": "Geburtsdatum", "Typ": "string", "pattern": "[0-1][0-9]-[0-9][0-9]" }, "xdm:birthYear": { "title": "Geburtsjahr", "Typ": "integer", "minimum": 1, "Maximum": 32767 } }
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
              "maximum": 32767,
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

Am meisten [!DNL Experience Platform] Dienste, einschließlich [!DNL Catalog], [!DNL Data Lake]und [!DNL Real-Time Customer Profile] use [!DNL Compatibility Mode] anstelle von Standard-XDM. Die [!DNL Schema Registry] API verwendet auch [!DNL Compatibility Mode]und die Beispiele in diesem Dokument werden alle mit [!DNL Compatibility Mode].

Es lohnt sich zu wissen, dass eine Zuordnung zwischen Standard-XDM und der Art und Weise erfolgt, wie es in [!DNL Experience Platform], sollte jedoch Ihre Verwendung von [!DNL Platform] Dienste.

Das Open-Source-Projekt steht Ihnen zur Verfügung, aber wenn es darum geht, mit Ressourcen über die [!DNL Schema Registry]enthalten die API-Beispiele in diesem Dokument die Best Practices, die Sie kennen und befolgen sollten.
