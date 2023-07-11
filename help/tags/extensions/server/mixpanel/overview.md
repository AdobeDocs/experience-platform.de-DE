---
keywords: Ereignisweiterleitungs-Erweiterung;Mixpanel;Ereignisweiterleitungserweiterung "mixpanel"
title: Ereignisweiterleitungserweiterung für die Mixpanel Track Events API
description: Diese Ereignisweiterleitungs-Erweiterung von Adobe Experience Platform sendet Adobe Experience Edge Network-Ereignisse an Mixpanel.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: 4f75bbfee6b550552d2c9947bac8540a982297eb
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 2%

---

# [!DNL Mixpanel Track Events] API-Ereignisweiterleitungs-Erweiterung

[[!DNL Mixpanel]](https://www.mixpanel.com) ist ein Produktanalysetool, mit dem Sie Daten darüber erfassen können, wie Benutzer mit einem digitalen Produkt interagieren. Sie können Produktdaten mit einfachen, interaktiven Berichten analysieren, mit denen Sie die Daten mit wenigen Klicks abfragen und visualisieren können. [!DNL Mixpanel] wurde entwickelt, um Teams effizienter zu machen, indem es allen ermöglicht, Benutzerdaten in Echtzeit zu analysieren, um Trends zu identifizieren, das Benutzerverhalten zu verstehen und Entscheidungen über Ihr Produkt zu treffen.

[!DNL Mixpanel] verwendet ein ereignisbasiertes, benutzerzentriertes Modell, das jede Interaktion mit einem einzelnen Benutzer verbindet. Die [!DNL Mixpanel] Das Datenmodell basiert auf den Konzepten von Benutzern, Ereignissen und Eigenschaften.

>[!NOTE]
>
>Siehe Abschnitt [!DNL Mixpanel] Dokumentation zu [Identitäts-Management](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) um zu verstehen, wie [!DNL Mixpanel] führt Ereignisse zusammen, um Identitäts-Cluster zu erstellen. Es wird außerdem empfohlen, das Dokument zu [eindeutige IDs](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) um zu verstehen, wie sie zur Identifizierung von Benutzern in Ereignisdaten verwendet werden.

## Anwendungsfälle

Diese Erweiterung sollte verwendet werden, wenn Sie Daten aus dem Edge-Netzwerk in [!DNL Mixpanel] , um die Produktanalysefunktionen zu nutzen.

Angenommen, ein Einzelhandelsunternehmen verfügt über eine mehrkanalige Präsenz (Website und Mobilgeräte). Die Organisation erfasst Transaktions- oder Konversationseingaben als Ereignisdaten von ihren Plattformen und lädt sie in [!DNL Mixpanel] die Ereignisweiterleitungs-Erweiterung verwenden.

Die Analyseteams können dann [!DNL Mixpanel's] Funktionen zur Verarbeitung der Datensätze und Ableitung von Geschäftseinblicken, die zum Generieren von Diagrammen, Dashboards oder anderen Visualisierungen verwendet werden können, um geschäftliche Stakeholder zu informieren.

Weitere Informationen zu spezifischen Anwendungsfällen für [!DNL Mixpanel], siehe folgende Dokumentation:

* [Neu in [!DNL Mixpanel]](https://docs.mixpanel.com/docs)
* [Was ist [!DNL Mixpanel]?](https://developer.mixpanel.com/docs)
* [12 &quot;must-try&quot; [!DNL Mixpanel] Funktionen](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## Voraussetzungen für [!DNL Mixpanel] {#prerequisites-mixpanel}

Sie müssen über gültige [!DNL Mixpanel] , um diese Erweiterung zu verwenden. Navigieren Sie zu [[!DNL Mixpanel] Registrierungsseite](https://mixpanel.com/register/) , um sich zu registrieren und ein Konto zu erstellen, falls Sie noch kein Konto haben.

Stellen Sie sicher, dass [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) -Einstellung für Ihr Projekt aktiviert ist. Navigieren Sie zu **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** und aktivieren Sie die Einstellung.

### Identitäts-Cluster verstehen in [!DNL Mixpanel]

In [!DNL Mixpanel], enthält ein Identitäts-Cluster eine Sammlung von `distinct_id` Werte, die eine Verbindung zu einem einzelnen Benutzer herstellen. [!DNL Mixpanel] verarbeitet den Cluster von Identitäten für jeden Benutzer, wobei ein einzelnes kanonisches `distinct_id` aus jedem Cluster, der für die Berichterstellung verwendet werden soll. Sie können auch Ihre eigene Kennung einfügen (eine lokale `distinct_id`) für anonyme Ereignisse, die vor einem Benutzeridentifikationsereignis auftreten.

[!DNL Mixpanel] löst Identitäts-Cluster mit zwei Methoden auf:

* **Identifizieren** : [!DNL Mixpanel] verbindet Ihre ausgewählte Kennung mit einem anonymen `distinct_id`. Wenn Ihre Website [!DNL Mixpanel] SDK aktiviert, verwendet Platform die `distinct_id` dem Benutzer zugewiesen, der derzeit angemeldet ist.
* **Alias**: [!DNL Mixpanel] kombiniert zwei nicht anonyme `distinct id`zusammengeführt, wenn zusätzliche Zusammenführungskriterien erfüllt sind.

>[!NOTE]
>
>Siehe Abschnitt [!DNL Mixpanel] Dokument auf [Identitäts-Management](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) für weitere Informationen zu diesen Methoden.
>
>Vergewissern Sie sich, dass Sie die [[!DNL Mixpanel] Identitätszusammenführungsfunktion](#prerequisites-mixpanel) , um sicherzustellen, dass Identitäts-Cluster angemessen aufgelöst werden.

### Erforderliche Konfigurationsdetails sammeln {#configuration-details}

So verbinden Sie Experience Platform mit [!DNL Mixpanel] Sie müssen über die folgenden Eingaben verfügen:

| Schlüsseltyp | Beschreibung | Beispiel |
| --- | --- | --- |
| Projekt-Token | Das Projekt-Token, das mit Ihrer [!DNL Mixpanel] -Konto. Siehe Abschnitt [!DNL Mixpanel] Dokumentation zu [Suchen des Projekt-Tokens](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) für Leitlinien. | `25470xxxxxxxxxxxxxxxxxxx1289` |

## Installieren und konfigurieren Sie die [!DNL Mixpanel] Erweiterung {#install}

So installieren Sie die Erweiterung: [Erstellen einer Ereignisweiterleitungs-Eigenschaft](../../../ui/event-forwarding/overview.md#properties) oder wählen Sie eine vorhandene Eigenschaft aus, die Sie stattdessen bearbeiten möchten.

Wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation aus. Im **[!UICONTROL Katalog]** Registerkarte, wählen Sie **[!UICONTROL Installieren]** auf der Karte für die [!DNL Mixpanel] -Erweiterung.

![Installieren der [!DNL Mixpanel] -Erweiterung.](../../../images/extensions/server/mixpanel/install-extension.png)

## Erstellen Sie eine [!DNL Send Event] Regel

Beginnen Sie mit der Erstellung einer neuen Regel in Ihrer Ereignisweiterleitungseigenschaft. under **[!UICONTROL Aktionen]**, fügen Sie eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL Mixpanel]**. Legen Sie als Nächstes den Aktionstyp auf **[!UICONTROL Ereignis verfolgen]** Senden von Adobe Experience Edge Network-Ereignissen an [!DNL Mixpanel].

| Eingabe | Beschreibung | Erforderlich |
| --- | --- | --- |
| [!UICONTROL Projekt-Token] | Dieses Feld sollte dem Projekt-Token zugeordnet sein, das mit Ihrem [!DNL Mixpanel] -Konto. | Ja |
| [!UICONTROL Ereignistyp] | Der Ereignisname. | Ja |
| [!UICONTROL Ereigniszeit] | Die Ereigniszeit. | |
| [!UICONTROL Mixpanel-Unique ID] | Die eindeutige Kennung des Benutzers, der das Ereignis ausgeführt hat. | |
| [!UICONTROL ID einfügen] | Eine eindeutige Kennung für das Ereignis, die zur Deduplizierung verwendet wird. | |
| [!UICONTROL Ereigniseigenschaften] | Ein JSON-Objekt, das benutzerdefinierte Eigenschaften des Ereignisses enthält. Wählen Sie aus der Bereitstellung von rohen JSON-Dateien oder der Verwendung eines vereinfachten Satzes von Schlüsselwerteingaben. | |

>[!NOTE]
>
>Weitere Informationen zu Standardfeldern für eine [!DNL Mixpanel] -Ereignis, siehe [amtliche Dokumentation](https://developer.mixpanel.com/reference/import-events#event).

![Fügen Sie eine Aktionskonfiguration für Ereignisweiterleitungsregeln hinzu.](../../../images/extensions/server/mixpanel/track-event-action.png)

Einmal [!UICONTROL Ereignis verfolgen] -Aktion zur Regel hinzugefügt wurde, können Sie die Bedingungen der Regel so konfigurieren, dass sie nur für bestimmte Ereignisse ausgelöst wird. Alternativ können Sie den Abschnitt &quot;Bedingungen&quot;leer lassen, damit die Regel für alle Ereignisse ausgelöst wird.

>[!IMPORTANT]
>
>Wenn Ihre Website die [!DNL Mixpanel] SDK: Sie können mit dem nächsten Schritt von [Validieren Ihrer Daten in [!DNL Mixpanel]](#validate). Wenn Sie die [!DNL Mixpanel] SDK: Sie müssen [eine separate Identitäts-Tracking-Regel erstellen](#create-an-identity-tracking-rule) sicherstellen, dass geeignete Ereignisse und `distinct_id` Werte werden an [!DNL Mixpanel] wenn ein Ereignis zur Identifizierung eines Benutzers eintritt.

## Validieren von Daten in [!DNL Mixpanel] {#validate}

Wenn Ihre Implementierung erfolgreich ist und Ereignisse erfasst werden, werden Ereignisse im [[!DNL Mixpanel] console](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

Überprüfen Sie, ob [!DNL Mixpanel] hat die post-Anmeldungsereignisse mit E-Mail-Werten und den Ereignissen zusammengeführt, die bei Verwendung von **[!UICONTROL Ereignis senden]**. Bei korrekter Implementierung [!DNL Mixpanel] verknüpft sie mit einer [Benutzerprofil](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Konversionsereignisse an gesendet werden [!DNL Mixpanel] über die Ereignisweiterleitung. Diese Ereignisweiterleitungs-Erweiterung nutzt die [!DNL Mixpanel] SDK und JavaScript-API. Weitere Informationen zu diesen Technologien finden Sie in der offiziellen Dokumentation:

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] JavaScript-API](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Weiterführende Informationen zu Ereignisweiterleitungsfunktionen in Experience Platform finden Sie im Abschnitt [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
