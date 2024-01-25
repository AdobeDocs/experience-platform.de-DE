---
title: Adobe Analytics Source Connector für Report Suite-Daten
description: Dieses Dokument bietet einen Überblick über Analytics und beschreibt die Anwendungsfälle für Analytics-Daten.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: b82bbdf7957e5a8d331d61f02293efdaf878971c
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 10%

---

# Adobe Analytics-Quell-Connector für Report Suite-Daten

Mit Adobe Experience Platform können Sie Adobe Analytics-Daten über den Analytics-Quell-Connector erfassen. Die [!DNL Analytics] Quell-Connector streamt Daten, die von [!DNL Analytics] in Platform in Echtzeit konvertieren, SCDS-formatiert konvertieren [!DNL Analytics] Daten in [!DNL Experience Data Model] (XDM)-Felder zur Verwendung durch Platform.

Dieses Dokument bietet einen Überblick über [!DNL Analytics] und beschreibt die Anwendungsfälle für [!DNL Analytics] Daten.

## Adobe Analytics und Analytics-Daten

[!DNL Analytics] ist eine leistungsstarke Engine, die Ihnen hilft, mehr über Ihre Kunden zu erfahren, wie sie mit Ihren Web-Eigenschaften interagieren, zu sehen, wo Ihre Ausgaben für digitales Marketing effektiv sind, und zu identifizieren, welche Verbesserungsmöglichkeiten es gibt. [!DNL Analytics] verarbeitet jährlich Billionen von Web-Transaktionen und die [!DNL Analytics] Mit dem Quell-Connector können Sie diese umfangreichen Verhaltensdaten einfach aufrufen und die [!DNL Real-Time Customer Profile] innerhalb von Minuten.

![Eine Grafik, die die Journey von Daten aus verschiedenen Adobe-Applikationen, einschließlich Adobe Analytics, veranschaulicht.](./images/analytics-data-experience-platform.png)

Auf hoher Ebene [!DNL Analytics] erfasst Daten aus verschiedenen digitalen Kanälen und Rechenzentren auf der ganzen Welt. Nachdem die Daten erfasst wurden, werden VISTA-Regeln (Visitor Identification, Segmentation and Transformation Architecture) und Verarbeitungsregeln angewendet, um die eingehenden Daten zu formen. Nachdem die Rohdaten diese einfache Verarbeitung durchlaufen haben, werden sie von [!DNL Real-Time Customer Profile]. In einem Prozess, der parallel zu den oben genannten erfolgt, werden dieselben verarbeiteten Daten in Mikro-Batches gepackt und in Platform-Datensätzen erfasst, die von [!DNL Query Service]und anderen Anwendungen zur Datenerkennung.

Siehe [Übersicht über Verarbeitungsregeln](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=de) für weitere Informationen zu Verarbeitungsregeln.

## Experience-Datenmodell (XDM)

XDM ist eine öffentlich dokumentierte Spezifikation, die gemeinsame Strukturen und Definitionen für eine Anwendung bereitstellt, die zur Kommunikation mit Diensten auf dem Experience Platform verwendet werden kann.

Durch Einhaltung von XDM-Standards können Daten einheitlich integriert werden, was die Bereitstellung von Daten und das Sammeln von Informationen erleichtert.

Weiterführende Informationen zu XDM finden Sie in der [XDM-Systemübersicht](../../../xdm/home.md).

## Wie werden Felder von Adobe Analytics XDM zugeordnet?

>[!IMPORTANT]
>
>Datenvorbereitung-Transformationen können zum Datenfluss insgesamt Latenzzeiten hinzufügen. Die zusätzliche Latenz variiert je nach Komplexität der Umwandlungslogik.

Wenn eine Quellverbindung für [!DNL Analytics] Daten über die Platform-Benutzeroberfläche in Experience Platform eingehen, werden Datenfelder automatisch zugeordnet und in [!DNL Real-Time Customer Profile] innerhalb von Minuten. Anweisungen zum Erstellen einer Quellverbindung mit [!DNL Analytics] Informationen zur Platform-Benutzeroberfläche finden Sie unter [Analytics-Quell-Connector-Tutorial](../../tutorials/ui/create/adobe-applications/analytics.md).

Detaillierte Informationen zum Feld-Mapping, das zwischen [!DNL Analytics] und Experience Platform, siehe [Adobe Analytics-Feldzuordnung](./mapping/analytics.md) Handbuch.

## Wie hoch ist die erwartete Latenz für Analytics-Daten in Platform?

Die erwartete Latenz für Analytics-Daten in Platform ist in der folgenden Tabelle dargestellt. Die Latenz variiert je nach Kundenkonfiguration, Datenvolumen und Verbraucheranwendungen. Wenn die Analytics-Implementierung beispielsweise mit `A4T` konfiguriert ist, erhöht sich die Latenz zur Pipeline um 5 bis 10 Minuten.

| Analytics-Daten | Erwartete Latenz |
| -------------- | ---------------- |
| Neue Daten in [!DNL Real-Time Customer Profile] (A4T **not** enabled) | &lt; 2 Minuten |
| Neue Daten in [!DNL Real-Time Customer Profile] (A4T **is** enabled) | bis zu 30 Minuten |
| Neue Daten an Data Lake | &lt; 2,25 Stunden |
| Aufstockung von weniger als 10 Milliarden Ereignissen | &lt; 4 Wochen |

Die Analytics-Aufstockung für Produktions-Sandboxes beträgt standardmäßig 13 Monate. Für Analytics-Daten in Nicht-Produktions-Sandboxes wird die Aufstockung auf drei Monate festgelegt. Die in der obigen Tabelle genannte Begrenzung von 10 Mrd. Ereignissen entspricht streng der erwarteten Latenz.

Wenn Sie einen Analytics-Quell-Datenfluss in einer Produktions-Sandbox erstellen, werden zwei Datenflüsse erstellt:

* Ein Datenfluss, der eine 13-monatige Aufstockung historischer Report Suite-Daten in den Data Lake ausführt. Dieser Datenfluss endet, wenn die Aufstockung abgeschlossen ist.
* Ein Datenfluss, der Live-Daten an den Daten-See und an [!DNL Real-Time Customer Profile]. Dieser Datenfluss wird kontinuierlich ausgeführt.

>[!NOTE]
>
>Analytics-Aufstockungsdaten werden nicht in erfasst [!DNL Profile] und daher nicht in Lizenzprofilen berücksichtigt wird.

## Primäre Kennungen in [!DNL Analytics] data

Jeder Treffer von [!DNL Analytics] Quell-Connector enthält eine primäre Kennung, die davon abhängt, ob eine ECID oder eine AAID vorhanden ist. Wenn eine ECID vorhanden ist, wird die ECID als primäre Kennung bezeichnet. Wenn eine AAID vorhanden ist, wird die AAID als primäre ID bezeichnet.

Die folgende Tabelle enthält weitere Informationen zu Identitätsfeldern in Ihrer [!DNL Analytics] Daten.

| Identitätsfeld | Beschreibung |
| --- | --- |
| AAID | Die AAID ist die primäre Gerätekennung in Adobe Analytics und ist garantiert für jedes Ereignis vorhanden, das über die [!DNL Analytics] -Quelle. Die AAID wird manchmal auch als *Legacy-Analytics-ID* oder als `s_vi` Cookie-ID. Trotzdem wird eine AAID erstellt, auch wenn die Variable `s_vi` -Cookie nicht vorhanden ist. Die AAID wird durch die `post_visid_high` und `post_visid_low` Spalten in [[!DNL Analytics] Datenfeeds](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html?lang=de). Bei jedem Ereignis enthält das Feld &quot;AAID&quot;eine einzelne Identität, die einer der verschiedenen Typen sein kann, die im Abschnitt [Reihenfolge der Vorgänge [!DNL Analytics] IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **Hinweis**: Innerhalb einer gesamten Report Suite kann eine AAID eine Mischung aus Ereignistypen enthalten. |
| ECID | Die ECID (Experience Cloud ID) ist ein separates Identifizierungsfeld für Geräte, das in Adobe Analytics ausgefüllt wird, wenn [!DNL Analytics] wird mit dem Experience Cloud Identity-Dienst implementiert. Die ECID wird manchmal auch als MCID (Marketing Cloud-ID) bezeichnet. Wenn eine ECID für ein Ereignis vorhanden ist, kann die AAID auf der ECID basieren, je nachdem, ob die Analytics-Variable [Übergangsphase](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) konfiguriert ist. Die ECID wird durch die `mcvisid` in Analytics-Daten-Feeds. Weitere Informationen zur ECID finden Sie im Abschnitt [ECID-Übersicht](../../../identity-service/features/ecid.md). Weitere Informationen zur Funktionsweise von ECID finden Sie unter [!DNL Analytics], siehe das Dokument unter [Analytics- und Experience Cloud-ID-Anforderungen](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html). |
| AACUSTOMID | Die AACUSTOMID ist ein separates Identifikationsfeld, das in Adobe Analytics basierend auf der Verwendung der Variablen `s.VisitorID` in der [!DNL Analytics] Implementierung. Die AACUSTOMID wird durch die Variable `cust_visid` Spalte in [[!DNL Analytics] Datenfeeds](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html?lang=de). Wenn die AACUSTOMID vorhanden ist, basiert die AACUSTOMID auf der AACUSTOMID, da die AACUSTOMID alle anderen Kennungen, wie durch die [Reihenfolge der Vorgänge [!DNL Analytics] IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### Wie die [!DNL Analytics] Identitäten zur Quellenbehandlung

Die [!DNL Analytics] -Quelle übergibt diese Identitäten an Experience Platform im XDM-Formular als:

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Diese Felder sind nicht als Identitäten markiert. Stattdessen werden dieselben Identitäten in die `identityMap` als Schlüssel-Wert-Paare:

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

Wenn in der Identitätszuordnung ECID vorhanden ist, wird es als primäre Identität für das Ereignis markiert. In diesem Fall kann AAID aufgrund der [Übergangsphase für Identity Service](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). Andernfalls wird AAID als primäre Identität für das Ereignis markiert. AACUSTOMID wird nie als primäre ID für das Ereignis markiert. Wenn jedoch AACUSTOMID vorhanden ist, basiert AAID aufgrund der Experience Cloud-Reihenfolge der Vorgänge auf AACUSTOMID.

>[!NOTE]
>
>Mit der Datenvorbereitung können Sie sekundäre Identitäten aus Analytics herausfiltern, z. B. AAID und AACUSTOMID. Wenn diese Identitäten herausgefiltert werden, werden sie nicht in das Profil aufgenommen, wenn sie in den eingehenden Analytics-Daten verfügbar sind. Ungefilterte Daten werden weiterhin in den Daten-Pool geladen.
