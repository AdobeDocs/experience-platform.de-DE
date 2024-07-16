---
title: Adobe Analytics Source Connector für Report Suite-Daten
description: Dieses Dokument bietet einen Überblick über Analytics und beschreibt die Anwendungsfälle für Analytics-Daten.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: d56a37c5b1c5768b3f6811be9d30d45628fdabca
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 7%

---

# Adobe Analytics-Quell-Connector für Report Suite-Daten

Mit Adobe Experience Platform können Sie Adobe Analytics-Daten über den Analytics-Quell-Connector erfassen. Der [!DNL Analytics]-Quell-Connector streamt die von [!DNL Analytics] erfassten Daten in Echtzeit an Platform, wobei SCDS-formatierte [!DNL Analytics]-Daten in [!DNL Experience Data Model] (XDM)-Felder umgewandelt werden, um sie von Platform zu nutzen.

Dieses Dokument bietet einen Überblick über [!DNL Analytics] und beschreibt die Anwendungsfälle für [!DNL Analytics] -Daten.

## Adobe Analytics und Analytics-Daten

[!DNL Analytics] ist eine leistungsstarke Engine, mit der Sie mehr über Ihre Kunden erfahren, wie sie mit Ihren Web-Eigenschaften interagieren, feststellen können, wo Ihre Ausgaben für digitales Marketing effektiv sind, und Verbesserungsbereiche identifizieren können. [!DNL Analytics] verarbeitet jährlich mehrere Billionen von Web-Transaktionen und der Quell-Connector [!DNL Analytics] ermöglicht es Ihnen, diese umfangreichen Verhaltensdaten einfach zu erfassen und die [!DNL Real-Time Customer Profile] in Minutenschnelle anzureichern.

![Eine Grafik, die die Journey von Daten aus verschiedenen Adobe-Applikationen, einschließlich Adobe Analytics, veranschaulicht.](./images/analytics-data-experience-platform.png)

Auf hoher Ebene erfasst [!DNL Analytics] Daten aus verschiedenen digitalen Kanälen und Rechenzentren auf der ganzen Welt. Nachdem die Daten erfasst wurden, werden VISTA-Regeln (Visitor Identification, Segmentation and Transformation Architecture) und Verarbeitungsregeln angewendet, um die eingehenden Daten zu formen. Nachdem die Rohdaten diese einfache Verarbeitung durchlaufen haben, werden sie von [!DNL Real-Time Customer Profile] als konsumbereit betrachtet. In einem Prozess, der parallel zu dem oben genannten erfolgt, werden dieselben verarbeiteten Daten in Mikro-Batches gepackt und in Platform-Datensätzen erfasst, die von [!DNL Query Service] und anderen Anwendungen zur Datenerkennung verwendet werden.

Weitere Informationen zu Verarbeitungsregeln finden Sie in der [Übersicht über Verarbeitungsregeln](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=de) .

## Experience-Datenmodell (XDM)

XDM ist eine öffentlich dokumentierte Spezifikation, die gemeinsame Strukturen und Definitionen für eine Anwendung bereitstellt, die zur Kommunikation mit Diensten auf dem Experience Platform verwendet werden kann.

Durch Einhaltung von XDM-Standards können Daten einheitlich integriert werden, was die Bereitstellung von Daten und das Sammeln von Informationen erleichtert.

Weiterführende Informationen zu XDM finden Sie in der [XDM-Systemübersicht](../../../xdm/home.md).

## Wie werden Felder von Adobe Analytics XDM zugeordnet?

>[!IMPORTANT]
>
>Datenvorbereitung-Transformationen können zum Datenfluss insgesamt Latenzzeiten hinzufügen. Die zusätzliche Latenz variiert je nach Komplexität der Umwandlungslogik.

Wenn über die Platform-Benutzeroberfläche eine Quellverbindung zum Übertragen von [!DNL Analytics] -Daten in Experience Platform hergestellt wird, werden Datenfelder automatisch zugeordnet und innerhalb von Minuten in [!DNL Real-Time Customer Profile] aufgenommen. Anweisungen zum Erstellen einer Quellverbindung mit [!DNL Analytics] mithilfe der Platform-Benutzeroberfläche finden Sie im Tutorial [Analytics-Quell-Connector-Tutorial](../../tutorials/ui/create/adobe-applications/analytics.md).

Detaillierte Informationen zur Feldzuordnung zwischen [!DNL Analytics] und Experience Platform finden Sie im Handbuch zur [Adobe Analytics-Feldzuordnung](./mapping/analytics.md).

## Wie hoch ist die erwartete Latenz für Analytics-Daten in Platform?

Die erwartete Latenz für Analytics-Daten in Platform ist in der folgenden Tabelle dargestellt. Die Latenz variiert je nach Kundenkonfiguration, Datenvolumen und Verbraucheranwendungen. Wenn die Analytics-Implementierung beispielsweise mit `A4T` konfiguriert ist, erhöht sich die Latenz zur Pipeline um 5 bis 10 Minuten.

| Analytics-Daten | Erwartete Latenz |
| -------------- | ---------------- |
| Neue Daten an [!DNL Real-Time Customer Profile] (A4T **nicht** aktiviert) | &lt; 2 Minuten |
| Neue Daten an [!DNL Real-Time Customer Profile] (A4T **ist** aktiviert) | bis zu 30 Minuten |
| Neue Daten an Data Lake | &lt; 2,25 Stunden |
| Neue Daten an Customer Journey Analytics ohne [Stitching](https://experienceleague.adobe.com/docs/analytics-platform/using/stitching/overview.html?lang=en) | &lt; 3,75 Stunden |
| Neue Daten an Customer Journey Analytics mit Stitching | &lt; 7 Stunden |
| Aufstockung von weniger als 10 Milliarden Ereignissen | &lt; 4 Wochen |

Weitere Informationen zu Customer Journey Analytics-Latenzen finden Sie unter: [Customer Journey Analytics-Schutzmechanismen](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html?lang=en).

Die Analytics-Aufstockung für Produktions-Sandboxes beträgt standardmäßig 13 Monate. Für Analytics-Daten in Nicht-Produktions-Sandboxes wird die Aufstockung auf drei Monate festgelegt. Die in der obigen Tabelle genannte Begrenzung von 10 Mrd. Ereignissen entspricht streng der erwarteten Latenz.

Wenn Sie einen Analytics-Quell-Datenfluss in einer Produktions-Sandbox erstellen, werden zwei Datenflüsse erstellt:

* Ein Datenfluss, der eine 13-monatige Aufstockung historischer Report Suite-Daten in den Data Lake ausführt. Dieser Datenfluss endet, wenn die Aufstockung abgeschlossen ist.
* Ein Datenfluss, der Live-Daten an den Data Lake und an [!DNL Real-Time Customer Profile] sendet. Dieser Datenfluss wird kontinuierlich ausgeführt.

>[!NOTE]
>
>Analytics-Aufstockungsdaten werden nicht in [!DNL Profile] erfasst und daher nicht in Lizenzprofilen berücksichtigt.

## Primäre IDs in [!DNL Analytics] -Daten

Jeder Treffer aus dem Quell-Connector [!DNL Analytics] enthält eine primäre Kennung, die davon abhängt, ob eine ECID oder eine AAID vorhanden ist. Wenn eine ECID vorhanden ist, wird die ECID als primäre Kennung bezeichnet. Wenn eine AAID vorhanden ist, wird die AAID als primäre ID bezeichnet.

Die folgende Tabelle enthält weitere Informationen zu Identitätsfeldern in Ihren [!DNL Analytics] -Daten.

| Identitätsfeld | Beschreibung |
| --- | --- |
| AAID | Die AAID ist die primäre Gerätekennung in Adobe Analytics und ist garantiert für jedes Ereignis vorhanden, das über die [!DNL Analytics] -Quelle übergeben wird. Die AAID wird manchmal als *Legacy Analytics ID* oder als Cookie-ID `s_vi` bezeichnet. Trotzdem wird eine AAID erstellt, selbst wenn das `s_vi` -Cookie nicht vorhanden ist. Die AAID wird durch die Spalten `post_visid_high` und `post_visid_low` in [[!DNL Analytics] Daten-Feeds](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html) dargestellt. Bei jedem Ereignis enthält das Feld &quot;AAID&quot;eine einzelne Identität, die einer der verschiedenen, in der Reihenfolge der Vorgänge für  [!DNL Analytics] IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html) beschriebenen Typen sein kann. [ **Hinweis**: Innerhalb einer gesamten Report Suite kann eine AAID eine Mischung aus Ereignistypen enthalten. |
| ECID | Die ECID (Experience Cloud ID) ist ein separates Gerätekennungsfeld, das in Adobe Analytics ausgefüllt wird, wenn [!DNL Analytics] mit dem Experience Cloud Identity-Dienst implementiert wird. Die ECID wird manchmal auch als MCID (Marketing Cloud-ID) bezeichnet. Wenn für ein Ereignis eine ECID vorhanden ist, kann die AAID auf der ECID basieren, je nachdem, ob die Analytics-Übergangsphase [1} konfiguriert ist. ](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) Die ECID wird in Analytics-Daten-Feeds durch den Wert `mcvisid` dargestellt. Weitere Informationen zur ECID finden Sie in der [ECID-Übersicht](../../../identity-service/features/ecid.md). Informationen zur Funktionsweise von ECID mit [!DNL Analytics] finden Sie im Dokument zu [Analytics- und Experience Cloud ID-Anfragen](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html). |
| AACUSTOMID | Die AACUSTOMID ist ein separates Identifikationsfeld, das in Adobe Analytics basierend auf der Verwendung der Variable `s.VisitorID` in der Implementierung von [!DNL Analytics] gefüllt wird. Die AACUSTOMID wird durch die Spalte `cust_visid` in [[!DNL Analytics] Daten-Feeds](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html) dargestellt. Wenn die AACUSTOMID vorhanden ist, basiert die AACUSTOMID auf der AACUSTOMID, da die AACUSTOMID alle anderen Kennungen übertrifft, die durch die [Reihenfolge der Vorgänge für  [!DNL Analytics] IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html) definiert sind. |

### Behandlung von Identitäten durch die Quelle [!DNL Analytics]

Die [!DNL Analytics] -Quelle übergibt diese Identitäten an Experience Platform im XDM-Formular als:

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Diese Felder sind nicht als Identitäten markiert. Stattdessen werden dieselben Identitäten (sofern im Ereignis vorhanden) als Schlüssel-Wert-Paare in die `identityMap` von XDM kopiert:

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

Wenn die Identität oder Identitäten in `identityMap` kopiert werden, wird `endUserIDs._experience.mcid.namespace.code` auch für dasselbe Ereignis festgelegt:

* Wenn AAID vorhanden ist, wird `endUserIDs._experience.aaid.namespace.code` auf &quot;AAID&quot;gesetzt.
* Wenn ECID vorhanden ist, wird `endUserIDs._experience.mcid.namespace.code` auf &quot;ECID&quot;gesetzt.
* Wenn AACUSTOMID vorhanden ist, wird `endUserIDs._experience.aacustomid.namespace.code` auf &quot;AACUSTOMID&quot;gesetzt.

Wenn in der Identitätszuordnung ECID vorhanden ist, wird es als primäre Identität für das Ereignis markiert. In diesem Fall kann die AAID aufgrund der Übergangsphase für den [Identitätsdienst](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) auf der ECID basieren. Andernfalls wird AAID als primäre Identität für das Ereignis markiert. AACUSTOMID wird nie als Primäre ID für das Ereignis markiert. Wenn jedoch AACUSTOMID vorhanden ist, basiert AAID aufgrund der Experience Cloud-Reihenfolge der Vorgänge auf AACUSTOMID.

>[!NOTE]
>
>Mit der Datenvorbereitung können Sie sekundäre Identitäten aus Analytics herausfiltern, z. B. AAID und AACUSTOMID. Wenn diese Identitäten herausgefiltert werden, werden sie nicht in das Profil aufgenommen, wenn sie in den eingehenden Analytics-Daten verfügbar sind. Ungefilterte Daten werden weiterhin in den Daten-Pool geladen.
