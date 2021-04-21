---
keywords: Experience Platform;Home;beliebte Themen;API;XDM;XDM;Erlebnisdatenmodell;Erlebnisdatenmodell;Datenmodell;Datenmodell;Datenmodell;Schema-Registrierung;Schema-Registrierung;Kompatibilität;Kompatibilitätsmodus;Kompatibilitätsmodus;Feldtyp;Feldtypen;Feldtypen;
solution: Experience Platform
title: Handbuch zur API für die Registrierung von Schemas
description: Dieses Dokument enthält zusätzliche Informationen zum Arbeiten mit der Schema Registry-API.
topic-legacy: developer guide
exl-id: 2ddc7fe8-dd0b-4cf9-8561-e89fcdadbfce
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 49%

---

# Handbuch zur API zur Schema-Registrierung

Dieses Dokument enthält zusätzliche Informationen zum Arbeiten mit der [!DNL Schema Registry]-API.

## Verwenden von Abfrageparametern {#query}

Die Variable [!DNL Schema Registry] unterstützt die Verwendung von Abfrage-Parametern zum Anzeigen von Seiten- und Filterergebnissen bei der Auflistung von Ressourcen.

>[!NOTE]
>
>Wenn mehrere Abfrageparameter kombiniert werden, müssen diese durch Und-Zeichen (`&`) getrennt werden.

### Paging {#paging}

Zu den häufigsten Abfrageparametern für das Paging gehören:

| Parameter | Beschreibung |
| --- | --- |
| `start` | Geben Sie an, wo die aufgelisteten Ergebnisse beginnen sollen. Dieser Wert kann aus dem `_page.next`-Attribut einer Liste-Antwort abgerufen und für den Zugriff auf die nächste Ergebnisseite verwendet werden. Wenn der Wert `_page.next` null ist, ist keine zusätzliche Seite verfügbar. |
| `limit` | Schränken Sie die Anzahl der zurückgegebenen Ressourcen ein. Beispiel: `limit=5` gibt eine Liste von fünf Ressourcen zurück. |
| `orderby` | Sortieren Sie die Ergebnisse nach einer bestimmten Eigenschaft. Beispiel: `orderby=title` sortiert die Ergebnisse in aufsteigender Reihenfolge (A-Z) nach Titel. Durch Hinzufügen eines `-` vor dem Parameterwert (`orderby=-title`) werden Elemente in absteigender Reihenfolge (Z-A) nach Titel sortiert. |

### Filtern {#filtering}

Sie können die Ergebnisse mit dem Parameter `property` filtern, mit dem ein bestimmter Operator auf eine bestimmte JSON-Eigenschaft in den abgerufenen Ressourcen angewendet wird. Zu den unterstützten Operatoren gehören:

| Operator | Beschreibung | Beispiel |
| --- | --- | --- |
| `==` | Filter, ob die Eigenschaft dem bereitgestellten Wert entspricht. | `property=title==test` |
| `!=` | Filter, ob die Eigenschaft nicht mit dem bereitgestellten Wert übereinstimmt. | `property=title!=test` |
| `<` | Filter, ob die Eigenschaft kleiner als der angegebene Wert ist. | `property=version<5` |
| `>` | Filter, ob die Eigenschaft größer als der angegebene Wert ist. | `property=version>5` |
| `<=` | Filter, ob die Eigenschaft kleiner als oder gleich dem bereitgestellten Wert ist. | `property=version<=5` |
| `>=` | Filter, ob die Eigenschaft größer oder gleich dem bereitgestellten Wert ist. | `property=version>=5` |
| `~` | Filter, ob die Eigenschaft mit einem bereitgestellten regulären Ausdruck übereinstimmt. | `property=title~test$` |
| (Keine) | Wenn nur der Eigenschaftsname angegeben wird, werden nur Einträge zurückgegeben, bei denen die Eigenschaft vorhanden ist. | `property=title` |

>[!TIP]
>
>Sie können den Parameter `property` verwenden, um Mixins nach ihrer kompatiblen Klasse zu filtern. Beispiel: `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` gibt nur Mixins zurück, die mit der [!DNL XDM Individual Profile]-Klasse kompatibel sind.

## Kompatibilitätsmodus

[!DNL Experience Data Model]Das  (XDM) ist eine öffentlich dokumentierte Spezifikation, die von Adobe zur Verbesserung der Interoperabilität, Ausdrucksfähigkeit und Leistungsfähigkeit digitaler Erlebnisse unterstützt wird. Adobe verwaltet den Quell-Code und formale XDM-Definitionen in einem [Open-Source-Projekt auf GitHub](https://github.com/adobe/xdm/). Diese Definitionen werden in XDM Standard Notation geschrieben, wobei JSON-LD (JavaScript Object Notation for Linked Data) und JSON-Schema als Grammatik zur Definition von XDM-Schemas verwendet werden.

Wenn Sie sich die formalen XDM-Definitionen im öffentlichen Repository ansehen, können Sie erkennen, dass sich das Standard-XDM von dem unterscheidet, das Sie in Adobe Experience Platform sehen. Was Sie in [!DNL Experience Platform] sehen, wird als Kompatibilitätsmodus bezeichnet und bietet eine einfache Zuordnung zwischen Standard-XDM und der Verwendung innerhalb von [!DNL Platform].

### Funktionsweise des Kompatibilitätsmodus

Der Kompatibilitätsmodus ermöglicht es dem XDM JSON-LD-Modell, mit der vorhandenen Dateninfrastruktur zu arbeiten, indem Werte innerhalb des XDM-Standards verändert werden, während die Semantik gleich bleibt. Es verwendet eine verschachtelte JSON-Struktur, die Schemas in einem baumähnlichen Format anzeigt.

Der Hauptunterschied, den Sie zwischen Standard-XDM und Kompatibilitätsmodus bemerken, ist die Entfernung des Präfix „xdm:“ für Feldnamen.

Im Folgenden finden Sie einen Vergleich, der sowohl im Standard-XDM als auch im Kompatibilitätsmodus geburtstagsbezogene Felder (mit entfernten „Beschreibungsattributen“) nebeneinander anzeigt. Beachten Sie, dass die Felder für den Kompatibilitätsmodus einen Verweis auf das XDM-Feld und seinen Datentyp in den Attributen „meta:xdmField“ und „meta:xdmType“ enthalten.

<table>
  <th>Standard-XDM</th>
  <th>Kompatibilitätsmodus</th>
  <tr>
  <td>
  <pre class="JSON language-JSON hljs">
        {
          "xdm:birthDate": {
              "title": "Birth Date",
              "type": "string",
              "format": "date",
          },
          "xdm:birthDayAndMonth": {
              "title": "Birth Date",
              "type": "string",
              "pattern": "[0-1][0-9]-[0-9][0-9]",
          },
          "xdm:birthYear": {
              "title": "Birth year",
              "type": "integer",
              "minimum": 1,
              "maximum": 32767
        }
  </pre>
  </td>
  <td>
  <pre class="JSON language-JSON hljs">
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
      </pre>
  </td>
  </tr>
</table>

### Warum ist der Kompatibilitätsmodus erforderlich?

Adobe Experience Platform ist für die Verwendung mit mehreren Lösungen und Diensten konzipiert, die jeweils eigene technische Herausforderungen und Einschränkungen aufweisen (z. B. wie bestimmte Technologien Sonderzeichen handhaben). Um diese Einschränkungen zu überwinden, wurde der Kompatibilitätsmodus entwickelt.

Die meisten [!DNL Experience Platform]-Dienste einschließlich [!DNL Catalog], [!DNL Data Lake] und [!DNL Real-time Customer Profile] verwenden [!DNL Compatibility Mode] anstelle von Standard-XDM. Die [!DNL Schema Registry]-API verwendet auch [!DNL Compatibility Mode] und die Beispiele in diesem Dokument werden alle mit [!DNL Compatibility Mode] angezeigt.

Es lohnt sich zu wissen, dass eine Zuordnung zwischen Standard-XDM und der Art und Weise, wie sie in [!DNL Experience Platform] operalisiert wird, stattfindet, sollte jedoch nicht Ihre Verwendung von [!DNL Platform]-Diensten beeinträchtigen.

Das Open-Source-Projekt steht Ihnen zur Verfügung, aber wenn es darum geht, mit Ressourcen über das [!DNL Schema Registry] zu interagieren, bieten die API-Beispiele in diesem Dokument die Best Practices, die Sie kennen und befolgen sollten.
