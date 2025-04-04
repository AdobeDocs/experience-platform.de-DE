---
keywords: -Erweiterung für die Ereignisweiterleitung;Mixpanel;Mixpanel-Erweiterung für die Ereignisweiterleitung
title: Mixpanel-Erweiterung zur Nachverfolgung von Ereignissen bei der API-Ereignisweiterleitung
description: Diese Adobe Experience Platform-Ereignisweiterleitungserweiterung sendet Edge Network-Ereignisse an Mixpanel.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 2%

---

# [!DNL Mixpanel Track Events] API-Ereignisweiterleitungserweiterung

[[!DNL Mixpanel]](https://www.mixpanel.com) ist ein Tool zur Produktanalyse, mit dem Sie Daten darüber erfassen können, wie Benutzende mit einem digitalen Produkt interagieren. Sie können Produktdaten mit einfachen, interaktiven Berichten analysieren, mit denen Sie die Daten mit nur wenigen Klicks abfragen und visualisieren können. [!DNL Mixpanel] ermöglicht es Teams, effizienter zu arbeiten, indem alle Benutzerdaten in Echtzeit analysieren können, um Trends zu identifizieren, das Benutzerverhalten zu verstehen und Entscheidungen über Ihr Produkt zu treffen.

[!DNL Mixpanel] verwendet ein ereignisbasiertes, benutzerzentriertes Modell, das jede Interaktion mit einem einzelnen Benutzer verbindet. Das [!DNL Mixpanel] Datenmodell basiert auf den Konzepten von Benutzern, Ereignissen und Eigenschaften.

>[!NOTE]
>
>Weitere Informationen dazu, wie Ereignisse zusammengeführt werden, um Identitäts[Cluster zu erstellen, finden Sie in der [!DNL Mixpanel]-Dokumentation ](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management)Identitätsverwaltung[!DNL Mixpanel]. Es wird außerdem empfohlen, das Dokument zu [Unique IDs](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) zu lesen, um zu verstehen, wie sie zur Identifizierung von Benutzern in Ereignisdaten verwendet werden.

## Anwendungsszenarien

Diese Erweiterung sollte verwendet werden, wenn Sie Daten aus der Edge Network verwenden möchten, [!DNL Mixpanel] die Produktanalysefunktionen von zu nutzen.

Nehmen wir zum Beispiel ein Einzelhandelsunternehmen mit einer kanalübergreifenden Präsenz (Website und Mobilgerät). Das Unternehmen erfasst Transaktions- oder Konversationseingaben als Ereignisdaten von seinen Plattformen und lädt sie mithilfe der Erweiterung für die Ereignisweiterleitung in [!DNL Mixpanel].

Die Analytics-Teams können dann [!DNL Mixpanel's] Funktionen nutzen, um die Datensätze zu verarbeiten und geschäftliche Einblicke abzuleiten, die zur Erstellung von Diagrammen, Dashboards oder anderen Visualisierungen verwendet werden können, um geschäftliche Stakeholder zu informieren.

Weiterführende Informationen zu [!DNL Mixpanel]-spezifischen Anwendungsfällen finden Sie in der folgenden Dokumentation:

* [Neu bei [!DNL Mixpanel]](https://docs.mixpanel.com/docs)
* [Was ist [!DNL Mixpanel]?](https://developer.mixpanel.com/docs)
* [12 Must-try [!DNL Mixpanel] features](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## Voraussetzungen für [!DNL Mixpanel] {#prerequisites-mixpanel}

Sie müssen über ein gültiges [!DNL Mixpanel] verfügen, um diese Erweiterung verwenden zu können. Navigieren Sie zur [[!DNL Mixpanel] Registrierungsseite](https://mixpanel.com/register/), um sich zu registrieren und ein Konto zu erstellen, falls Sie noch keines haben.

Stellen Sie sicher, dass die [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) für Ihr Projekt aktiviert ist. Navigieren Sie zu **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** und schalten Sie die Einstellung um.

### Identitäts-Cluster in [!DNL Mixpanel]

[!DNL Mixpanel] enthält ein Identitäts-Cluster eine Sammlung `distinct_id` Werte, die eine Verbindung zu einem einzelnen Benutzer herstellen. [!DNL Mixpanel] behandelt den Identitäts-Cluster für jeden Benutzer und löst einen einzelnen kanonischen `distinct_id` aus jedem Cluster auf, der im Reporting verwendet werden soll. Sie können auch eine eigene Kennung (eine so genannte lokale `distinct_id`) für anonyme Ereignisse einfügen, die vor einem Benutzeridentifizierungsereignis auftreten.

[!DNL Mixpanel] löst Identitäts-Cluster auf zwei Arten auf:

* **Identifizieren** : [!DNL Mixpanel] verbindet die von Ihnen gewählte Kennung mit einer anonymen `distinct_id`. Wenn auf Ihrer Website die [!DNL Mixpanel] SDK aktiviert ist, verwendet Experience Platform die `distinct_id`, die dem derzeit angemeldeten Benutzer zugewiesen ist.
* **Alias**: [!DNL Mixpanel] kombiniert zwei nicht anonyme `distinct id` miteinander, wenn zusätzliche Zusammenführungskriterien erfüllt sind.

>[!NOTE]
>
>Weitere Informationen zu diesen Methoden finden [ im [!DNL Mixpanel]-Dokument ](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification)Identitätsverwaltung“.
>
>Bestätigen Sie, dass Sie die Funktion [[!DNL Mixpanel] Identitätszusammenführung“ aktiviert haben](#prerequisites-mixpanel) um sicherzustellen, dass Identitäts-Cluster ordnungsgemäß aufgelöst werden.

### Sammeln erforderlicher Konfigurationsdetails {#configuration-details}

Um Experience Platform mit [!DNL Mixpanel] zu verbinden, benötigen Sie die folgenden Eingaben:

| Schlüsseltyp | Beschreibung | Beispiel |
| --- | --- | --- |
| Projekt-Token | Das Projekt-Token, das Ihrem [!DNL Mixpanel]-Konto zugeordnet ist. Eine Anleitung finden Sie in der [!DNL Mixpanel] Dokumentation unter [Suchen Ihres Projekt](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-)Tokens . | `25470xxxxxxxxxxxxxxxxxxx1289` |

## Installieren und Konfigurieren der [!DNL Mixpanel] {#install}

Um die Erweiterung zu installieren[ erstellen Sie eine Ereignisweiterleitungseigenschaft oder ](../../../ui/event-forwarding/overview.md#properties) Sie stattdessen eine vorhandene Eigenschaft aus, die bearbeitet werden soll.

Wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation aus. Wählen Sie auf der **[!UICONTROL Katalog]**-Registerkarte **[!UICONTROL Installieren]** auf der Karte für die [!DNL Mixpanel] aus.

![Installieren der [!DNL Mixpanel]-Erweiterung.](../../../images/extensions/server/mixpanel/install-extension.png)

## Erstellen einer [!DNL Send Event] Regel

Beginnen Sie mit der Erstellung einer neuen Regel in Ihrer Ereignisweiterleitungs-Eigenschaft. Fügen Sie **[!UICONTROL Aktionen]** eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL Mixpanel]** fest. Legen Sie als Nächstes den Aktionstyp auf &quot;**[!UICONTROL &quot; fest]** um Edge Network-Ereignisse an [!DNL Mixpanel] zu senden.

| Eingabe | Beschreibung | Erforderlich |
| --- | --- | --- |
| [!UICONTROL Projekt-Token] | Dieses Feld sollte dem Projekt-Token zugeordnet werden, das mit Ihrem [!DNL Mixpanel]-Konto verknüpft ist. | Ja |
| [!UICONTROL Ereignistyp] | Der Ereignisname. | Ja |
| [!UICONTROL Ereigniszeit] | Die Ereigniszeit. | |
| [!UICONTROL Mixpanel - eindeutige ID] | Die eindeutige Kennung des Benutzers, der das Ereignis ausgeführt hat. | |
| [!UICONTROL ID einfügen] | Eine eindeutige Kennung für das Ereignis, die für die Deduplizierung verwendet wird. | |
| [!UICONTROL Ereigniseigenschaften] | Ein JSON-Objekt mit benutzerdefinierten Eigenschaften des Ereignisses. Wählen Sie aus der Bereitstellung von unformatiertem JSON oder der Verwendung eines vereinfachten Satzes von Schlüssel-Wert-Eingaben. | |

>[!NOTE]
>
>Weitere Informationen zu den Standardfeldern für eine [!DNL Mixpanel] finden Sie in der [ Dokumentation](https://developer.mixpanel.com/reference/import-events#event).

![Fügen Sie eine Regelaktionskonfiguration für die Ereignisweiterleitung hinzu.](../../../images/extensions/server/mixpanel/track-event-action.png)

Nachdem die Aktion [!UICONTROL Ereignis verfolgen] zur Regel hinzugefügt wurde, können Sie die Bedingungen der Regel so konfigurieren, dass sie nur für bestimmte Ereignisse ausgelöst wird. Alternativ können Sie den Abschnitt Bedingungen leer lassen, damit die Regel für alle Ereignisse ausgelöst wird.

>[!IMPORTANT]
>
>Wenn Ihre Website die [!DNL Mixpanel] SDK verwendet, können Sie mit dem nächsten Schritt fortfahren, nämlich [Validieren Ihrer Daten in [!DNL Mixpanel]](#validate). Wenn Sie die [!DNL Mixpanel] SDK nicht verwenden, müssen Sie [eine separate Identitäts-Tracking-Regel erstellen](#create-an-identity-tracking-rule) um sicherzustellen, dass beim Eintreten eines Benutzeridentifizierungsereignisses geeignete Ereignisse und `distinct_id` an [!DNL Mixpanel] gesendet werden.

## Validieren von Daten in [!DNL Mixpanel] {#validate}

Wenn Ihre Implementierung erfolgreich ist und Ereignisse erfasst werden, werden Ereignisse in der [[!DNL Mixpanel] Konsole](https://help.mixpanel.com/hc/en-us/articles/4402837164948) angezeigt.

Überprüfen Sie, ob [!DNL Mixpanel] die Post-Login-Ereignisse, die mit E-Mail-Werten gefüllt sind, und die bei Verwendung von **[!UICONTROL Ereignis senden]** erstellten Ereignisse zusammengeführt hat. Bei korrekter Implementierung verknüpfen [!DNL Mixpanel] sie mit einem einzelnen [Benutzerprofil](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Konversionsereignisse mithilfe der Ereignisweiterleitung an [!DNL Mixpanel] senden. Diese Ereignisweiterleitungserweiterung nutzt die [!DNL Mixpanel] SDK- und JavaScript-API. Weitere Informationen zu diesen zugrunde liegenden Technologien finden Sie in der offiziellen Dokumentation:

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] JavaScript-API](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Weitere Informationen zu den Funktionen für die Ereignisweiterleitung in Experience Platform finden Sie unter [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
