---
title: Adobe Analytics Source Connector für Report Suite-Daten
description: Dieses Dokument bietet einen Überblick über Analytics und beschreibt die Anwendungsfälle für Analytics-Daten.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: d9dad6b5da413740559e6c8de7392bc2e169d5d9
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 6%

---

# Adobe Analytics-Quell-Connector für Report Suite-Daten

Mit Adobe Experience Platform können Sie Adobe Analytics-Daten über den Analytics-Quell-Connector aufnehmen. Der [!DNL Analytics]-Quell-Connector streamt von [!DNL Analytics] erfasste Daten in Echtzeit an Experience Platform und konvertiert SCDS-formatierte [!DNL Analytics] in [!DNL Experience Data Model] (XDM)-Felder zur Verwendung durch Experience Platform.

Dieses Dokument bietet einen Überblick über [!DNL Analytics] und beschreibt die Anwendungsfälle für [!DNL Analytics].

## Adobe Analytics und Analytics-Daten

[!DNL Analytics] ist eine leistungsstarke Engine, mit der Sie mehr über Ihre Kunden und deren Interaktion mit Ihren Web-Eigenschaften erfahren, sehen können, wo Ihre Ausgaben für digitales Marketing effektiv sind, und Bereiche für Verbesserungen ermitteln können. [!DNL Analytics] verarbeitet Billionen von Web-Transaktionen pro Jahr, und mit dem [!DNL Analytics]-Quell-Connector können Sie einfach diese umfangreichen Verhaltensdaten nutzen und die [!DNL Real-Time Customer Profile] in wenigen Minuten anreichern.

![Eine Grafik, die das Journey von Daten aus verschiedenen Adobe-Programmen, einschließlich Adobe Analytics, veranschaulicht.](./images/analytics-data-experience-platform.png)

[!DNL Analytics] sammelt Daten aus verschiedenen digitalen Kanälen und Rechenzentren weltweit. Sobald die Daten erfasst sind, werden VISTA-Regeln (Visitor Identification, Segmentation and Transformation Architecture) und Verarbeitungsregeln angewendet, um die eingehenden Daten zu formen. Nachdem die Rohdaten diese leichte Verarbeitung durchlaufen haben, werden sie als für den Verbrauch durch [!DNL Real-Time Customer Profile] bereit erachtet. In einem parallel zu den oben genannten Prozessen werden dieselben verarbeiteten Daten in Mikro-Batches aufgenommen und in Experience Platform-Datensätze aufgenommen, die von [!DNL Query Service] und anderen Datenerfassungsanwendungen verwendet werden können.

Weiterführende Informationen [&#x200B; Verarbeitungsregeln finden Sie &#x200B;](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=de) „Übersicht zu Verarbeitungsregeln“.

## Experience-Datenmodell (XDM)

XDM ist eine öffentlich dokumentierte Spezifikation, die allgemeine Strukturen und Definitionen für eine Anwendung bereitstellt, die für die Kommunikation mit Services auf Experience Platform verwendet werden soll.

Durch Einhaltung von XDM-Standards können Daten einheitlich integriert werden, was die Bereitstellung von Daten und das Sammeln von Informationen erleichtert.

Weiterführende Informationen zu XDM finden Sie in der [XDM-Systemübersicht](../../../xdm/home.md).

## Wie werden Felder von Adobe Analytics XDM zugeordnet?

>[!IMPORTANT]
>
>Umwandlungen der Datenvorbereitung können zu einer Latenz im gesamten Datenfluss führen. Die zusätzliche Latenz hängt von der Komplexität der Umwandlungslogik ab.

Wenn eine Quellverbindung hergestellt wird, um [!DNL Analytics] Daten über die Experience Platform-Benutzeroberfläche in Experience Platform zu importieren, werden die Datenfelder automatisch zugeordnet und innerhalb von Minuten in [!DNL Real-Time Customer Profile] aufgenommen. Anweisungen zum Erstellen einer Quellverbindung mit [!DNL Analytics] mithilfe der Experience Platform-Benutzeroberfläche finden Sie im [Analytics-Quell-Connector-Tutorial](../../tutorials/ui/create/adobe-applications/analytics.md).

Ausführliche Informationen zur Feldzuordnung, die zwischen [!DNL Analytics] und Experience Platform stattfindet, finden Sie im Handbuch [Adobe Analytics-Feldzuordnung](./mapping/analytics.md).

>[!TIP]
>
>Befolgen Sie diese Best Practices, um zu vermeiden, dass Ihre Lizenzberechtigungen überschritten werden und Ihre Metriken für Speicher und Datenreichhaltigkeit insgesamt überfordert werden:
>
>* Richten Sie zu Beginn die TTL (Time-to-Live) für die Aufbewahrung von Erlebnisereignissen ein, um die Verwaltung des Datenlebenszyklus und die Speichereffizienz zu optimieren. Weitere Informationen finden Sie in der Anleitung zum [Verwalten der Datensatzaufbewahrung für Erlebnisereignisse im Data Lake mithilfe von TTL](../../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md).
>
>* Wenn Sie einen Analytics-Quell-Datenfluss erstellen, konfigurieren Sie zunächst den Connector so, dass nur Daten in den Data Lake aufgenommen werden. Nachdem Sie bestätigt haben, dass der Datenfluss funktioniert, können Sie die Profilaufnahme für den Datensatz aktivieren. Dieser Ansatz funktioniert am besten, wenn Zeilen- und Spaltenfilter das Datenvolumen effektiv reduzieren. Weitere Informationen finden Sie in der Dokumentation [Verbinden von Adobe Analytics mit Experience Platform](../../tutorials/ui/create/adobe-applications/analytics.md).

## Wie hoch ist die erwartete Latenz für Analytics-Daten in Experience Platform?

Die erwartete Latenz für Analytics-Daten in Experience Platform ist in der folgenden Tabelle aufgeführt. Die Latenz variiert je nach Kundenkonfiguration, Datenvolumen und Kundenanwendungen. Wenn die Analytics-Implementierung beispielsweise mit `A4T` konfiguriert ist, erhöht sich die Latenz zur Pipeline um 5 bis 10 Minuten.

| Analytics-Daten | Erwartete Latenz |
| -------------- | ---------------- |
| Neue zu [!DNL Real-Time Customer Profile] Daten (A4T **nicht** aktiviert) | &lt; 2 Minuten |
| Neue zu [!DNL Real-Time Customer Profile] Daten (A4T **aktiviert**) | Bis zu 30 Minuten |
| Neue Daten an Data Lake | &lt; 2,25 Stunden |
| Neue Daten in Customer Journey Analytics ohne [Zuordnung](https://experienceleague.adobe.com/docs/analytics-platform/using/stitching/overview.html?lang=en) | &lt; 3,75 Stunden |
| Neue Daten zu Customer Journey Analytics mit Zuordnung | &lt; 7 Stunden |
| Aufstockung von weniger als 10 Milliarden Ereignissen | &lt; 4 Wochen |

Weitere Informationen zu Customer Journey Analytics-Latenzen finden Sie unter [Customer Journey Analytics-Leitplanken](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html?lang=en).

Die Analytics-Aufstockung für Produktions-Sandboxes ist standardmäßig auf 13 Monate eingestellt. Für Analytics-Daten in Nicht-Produktions-Sandboxes ist die Aufstockung auf drei Monate festgelegt. Die in der obigen Tabelle angegebene Grenze von 10 Milliarden Ereignissen bezieht sich ausschließlich auf die erwartete Latenz.

Wenn Sie für Produktions-Sandboxes die zusätzliche SKU lizenziert haben, die Sie berechtigt, mehr als 13 Monate historischer Aufstockungsdaten zu importieren, wenden Sie sich an Adobe, um die erweiterte Aufstockung anzufordern.

Beim Erstellen eines Analytics-Quell-Datenflusses in einer Produktions-Sandbox werden zwei Datenflüsse erstellt:

* Ein Datenfluss, der eine 13-monatige Aufstockung historischer Report Suite-Daten in den Data Lake durchführt. Dieser Datenfluss endet, wenn die Aufstockung abgeschlossen ist.
* Ein Datenfluss, der Live-Daten an den Data Lake und an [!DNL Real-Time Customer Profile] sendet. Dieser Datenfluss läuft kontinuierlich.

>[!NOTE]
>
>Analytics-Aufstockungsdaten werden nicht in [!DNL Profile] aufgenommen und daher nicht in Lizenzprofilen berücksichtigt.

## Primäre Kennungen in [!DNL Analytics]

Jeder Treffer aus dem [!DNL Analytics]-Quell-Connector enthält eine primäre Kennung, die davon abhängt, ob eine ECID oder eine AAID vorhanden ist. Wenn eine ECID vorhanden ist, wird die ECID als primäre Kennung angegeben. Wenn eine AAID vorhanden ist, wird die AAID als primär gekennzeichnet.

Die folgende Tabelle enthält weitere Informationen zu Identitätsfeldern in Ihren [!DNL Analytics].

| Identitätsfeld | Beschreibung |
| --- | --- |
| AAID | Die AAID ist die primäre Gerätekennung in Adobe Analytics und ist garantiert bei jedem Ereignis vorhanden, das durch die [!DNL Analytics] weitergeleitet wird. Die AAID wird manchmal als *veraltete Analytics-ID* oder als `s_vi` Cookie-ID bezeichnet. Trotzdem wird eine AAID erstellt, selbst wenn das `s_vi` Cookie nicht vorhanden ist. Die AAID wird in den Daten-Feeds durch die Spalten `post_visid_high` und `post_visid_low` [[!DNL Analytics]  dargestellt](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). Das Feld AAID enthält für jedes Ereignis eine einzelne Identität, die einen von mehreren verschiedenen Typen besitzen kann, die in der [Reihenfolge der Vorgänge für_IDs [!DNL Analytics]  beschrieben &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **Hinweis**: Innerhalb einer gesamten Report Suite kann eine AAID eine Mischung von Typen über Ereignisse hinweg enthalten. |
| ECID | Die ECID (Experience Cloud-ID) ist ein separates Gerätekennungsfeld, das in Adobe Analytics ausgefüllt wird, wenn [!DNL Analytics] mithilfe des Experience Cloud Identity Services implementiert wird. Die ECID wird manchmal auch als MCID (Marketing Cloud ID) bezeichnet. Wenn eine ECID für ein Ereignis vorhanden ist, kann die AAID auf ECID basieren, je nachdem, ob die Analytics-[Übergangsphase](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) konfiguriert ist. Die ECID wird in den Analytics-Daten-Feeds durch die `mcvisid` dargestellt. Weitere Informationen zu ECID finden Sie in der [ECID-Übersicht](../../../identity-service/features/ecid.md). Informationen zur Funktionsweise von ECID mit [!DNL Analytics] finden Sie im Dokument zu [Analytics- und Experience Cloud ID-Anfragen](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html). |
| AACUSTOMID | Die AACUSTOMID ist ein separates Kennungsfeld, das in Adobe Analytics auf der Grundlage der Verwendung der `s.VisitorID` in der [!DNL Analytics]-Implementierung ausgefüllt wird. Die AACUSTOMID wird in Daten-Feeds durch die Spalte `cust_visid` [[!DNL Analytics]  dargestellt](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). Wenn die AACUSTOMID vorhanden ist, basiert die AAID auf der AACUSTOMID, da die AACUSTOMID alle anderen Kennungen überträgt, wie durch die [Reihenfolge der Vorgänge für [!DNL Analytics] IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html) definiert. |

### Behandlung von Identitäten durch die [!DNL Analytics]

Die [!DNL Analytics] übergibt diese Identitäten in XDM-Form an Experience Platform als:

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Diese Felder sind nicht als Identitäten markiert. Stattdessen werden dieselben Identitäten (falls im Ereignis vorhanden) als Schlüssel-Wert-Paare in die `identityMap` von XDM kopiert:

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

Wenn die Identität(en) in `identityMap` kopiert wird/werden, wird `endUserIDs._experience.mcid.namespace.code` auch für dasselbe Ereignis festgelegt:

* Wenn AAID vorhanden ist, wird `endUserIDs._experience.aaid.namespace.code` auf „AAID“ gesetzt.
* Wenn ECID vorhanden ist, wird `endUserIDs._experience.mcid.namespace.code` auf „ECID“ gesetzt.
* Wenn AACUSTOMID vorhanden ist, wird `endUserIDs._experience.aacustomid.namespace.code` auf „AACUSTOMID“ gesetzt.

Wenn eine ECID vorhanden ist, wird sie in der Identitätszuordnung als primäre Identität für das Ereignis markiert. In diesem Fall kann AAID aufgrund der „Nachfrist für Identity [&quot; auf ECID &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). Andernfalls wird AAID als primäre Identität für das Ereignis markiert. AACUSTOMID wird nie als Primäre ID für das Ereignis markiert. Wenn jedoch AACUSTOMID vorhanden ist, basiert AAID aufgrund der Experience Cloud-Reihenfolge der Vorgänge auf AACUSTOMID.

>[!NOTE]
>
>Sie können die Datenvorbereitung verwenden, um sekundäre Identitäten aus Analytics herauszufiltern, z. B. AAID und AACUSTOMID. Wenn sie herausgefiltert werden, werden diese Identitäten nicht in das Profil aufgenommen, wenn sie in den eingehenden Analytics-Daten verfügbar sind. Nicht gefilterte Daten werden weiterhin in den Data Lake geladen.
