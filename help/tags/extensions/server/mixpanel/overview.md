---
keywords: Ereignisweiterleitungs-Erweiterung;Mixpanel;Ereignisweiterleitungserweiterung "mixpanel"
title: Ereignisweiterleitungserweiterung für die Mixpanel Track Events API
description: Diese Ereignisweiterleitungs-Erweiterung von Adobe Experience Platform sendet Edge Network-Ereignisse an Mixpanel.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 2%

---

# [!DNL Mixpanel Track Events] API-Ereignisweiterleitungserweiterung

[[!DNL Mixpanel]](https://www.mixpanel.com) ist ein Tool zur Produktanalyse, mit dem Sie Daten darüber erfassen können, wie Benutzer mit einem digitalen Produkt interagieren. Sie können Produktdaten mit einfachen, interaktiven Berichten analysieren, mit denen Sie die Daten mit nur wenigen Klicks abfragen und visualisieren können. [!DNL Mixpanel] wurde entwickelt, um Teams effizienter zu gestalten, indem es allen ermöglicht, Benutzerdaten in Echtzeit zu analysieren, um Trends zu identifizieren, das Benutzerverhalten zu verstehen und Entscheidungen über Ihr Produkt zu treffen.

[!DNL Mixpanel] verwendet ein ereignisbasiertes, benutzerzentriertes Modell, das jede Interaktion mit einem einzelnen Benutzer verbindet. Das Datenmodell [!DNL Mixpanel] basiert auf den Konzepten von Benutzern, Ereignissen und Eigenschaften.

>[!NOTE]
>
>In der Dokumentation zu [Identitätsverwaltung](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) finden Sie Informationen dazu, wie [!DNL Mixpanel] Ereignisse zu Identitäts-Clustern zusammenführt. [!DNL Mixpanel] Es wird außerdem empfohlen, das Dokument zu [eindeutigen IDs](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) zu lesen, um zu verstehen, wie sie zur Identifizierung von Benutzern in Ereignisdaten verwendet werden.

## Anwendungsfälle

Diese Erweiterung sollte verwendet werden, wenn Sie Daten aus dem Edge Network in [!DNL Mixpanel] verwenden möchten, um seine Produktanalysefunktionen zu nutzen.

Angenommen, ein Einzelhandelsunternehmen verfügt über eine mehrkanalige Präsenz (Website und Mobilgeräte). Die Organisation erfasst Transaktions- oder Konversationseingaben als Ereignisdaten von ihren Plattformen und lädt sie mithilfe der Ereignisweiterleitungs-Erweiterung in [!DNL Mixpanel].

Die Analyseteams können dann die [!DNL Mixpanel's]-Funktionen nutzen, um die Datensätze zu verarbeiten und geschäftliche Einblicke zu gewinnen, die zum Generieren von Diagrammen, Dashboards oder anderen Visualisierungen verwendet werden können, um geschäftliche Stakeholder zu informieren.

Weitere Informationen zu [!DNL Mixpanel]-spezifischen Anwendungsfällen finden Sie in der folgenden Dokumentation:

* [Neu zu [!DNL Mixpanel]](https://docs.mixpanel.com/docs)
* [Was ist [!DNL Mixpanel]?](https://developer.mixpanel.com/docs)
* [12 must-try [!DNL Mixpanel] features](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## Voraussetzungen für [!DNL Mixpanel] {#prerequisites-mixpanel}

Sie müssen über ein gültiges [!DNL Mixpanel] -Konto verfügen, um diese Erweiterung verwenden zu können. Rufen Sie die [[!DNL Mixpanel] Registrierungsseite](https://mixpanel.com/register/) auf, um sich zu registrieren und ein Konto zu erstellen, falls noch keines vorhanden ist.

Stellen Sie sicher, dass die Einstellung [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) für Ihr Projekt aktiviert ist. Navigieren Sie zu **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** und schalten Sie die Einstellung um.

### Identitäts-Cluster in [!DNL Mixpanel] verstehen

In [!DNL Mixpanel] enthält ein Identitäts-Cluster eine Sammlung von `distinct_id` -Werten, die eine Verbindung zu einem einzelnen Benutzer herstellen. [!DNL Mixpanel] verarbeitet den Cluster von Identitäten für jeden Benutzer und löst einen einzelnen kanonischen `distinct_id` aus jedem Cluster auf, der für die Berichterstellung verwendet werden soll. Sie können auch Ihre eigene Kennung (die so genannte lokale Kennung `distinct_id`) für anonyme Ereignisse einfügen, die vor einem Benutzeridentifikationsereignis auftreten.

[!DNL Mixpanel] löst Identitäts-Cluster durch zwei Methoden auf:

* **Identifizieren** : [!DNL Mixpanel] verbindet Ihre ausgewählte Kennung mit einem anonymen `distinct_id`. Wenn auf Ihrer Website das SDK [!DNL Mixpanel] aktiviert ist, verwendet Platform die `distinct_id`, die dem Benutzer zugewiesen ist, der derzeit angemeldet ist.
* **Alias**: [!DNL Mixpanel] kombiniert zwei nicht anonyme `distinct id`s, wenn zusätzliche Zusammenführungskriterien erfüllt sind.

>[!NOTE]
>
>Weitere Informationen zu diesen Methoden finden Sie im Dokument [!DNL Mixpanel] für die [Identitätsverwaltung](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) .
>
>Vergewissern Sie sich, dass Sie die Funktion [[!DNL Mixpanel] Identitätszusammenführung](#prerequisites-mixpanel) aktiviert haben, um sicherzustellen, dass Identitäts-Cluster ordnungsgemäß aufgelöst werden.

### Erforderliche Konfigurationsdetails sammeln {#configuration-details}

Um Experience Platform mit [!DNL Mixpanel] zu verbinden, müssen Sie über die folgenden Eingaben verfügen:

| Schlüsseltyp | Beschreibung | Beispiel |
| --- | --- | --- |
| Projekt-Token | Das Projekt-Token, das Ihrem [!DNL Mixpanel] -Konto zugeordnet ist. Eine Anleitung dazu finden Sie in der Dokumentation zu [!DNL Mixpanel] unter [Suchen Ihres Projekt-Tokens](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) . | `25470xxxxxxxxxxxxxxxxxxx1289` |

## Installieren und Konfigurieren der [!DNL Mixpanel] -Erweiterung {#install}

Um die Erweiterung zu installieren, erstellen Sie [eine Ereignisweiterleitungs-Eigenschaft](../../../ui/event-forwarding/overview.md#properties) oder wählen Sie eine vorhandene Eigenschaft aus, die Sie stattdessen bearbeiten möchten.

Wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation aus. Wählen Sie auf der Registerkarte **[!UICONTROL Katalog]** die Option **[!UICONTROL Installieren]** auf der Karte für die Erweiterung [!DNL Mixpanel] aus.

![Installieren der [!DNL Mixpanel]-Erweiterung.](../../../images/extensions/server/mixpanel/install-extension.png)

## Erstellen einer [!DNL Send Event] -Regel

Beginnen Sie mit der Erstellung einer neuen Regel in Ihrer Ereignisweiterleitungseigenschaft. Fügen Sie unter **[!UICONTROL Aktionen]** eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL Mixpanel]** fest. Legen Sie als Nächstes den Aktionstyp auf **[!UICONTROL Ereignis verfolgen]** fest, um Edge Network-Ereignisse an [!DNL Mixpanel] zu senden.

| Eingabe | Beschreibung | Erforderlich |
| --- | --- | --- |
| [!UICONTROL Projekt-Token] | Dieses Feld sollte dem Projekt-Token zugeordnet werden, das Ihrem [!DNL Mixpanel] -Konto zugeordnet ist. | Ja |
| [!UICONTROL Ereignistyp] | Der Ereignisname. | Ja |
| [!UICONTROL Ereigniszeit] | Die Ereigniszeit. | |
| [!UICONTROL Diverse ID des Mixpanel] | Die eindeutige Kennung des Benutzers, der das Ereignis ausgeführt hat. | |
| [!UICONTROL ID einfügen] | Eine eindeutige Kennung für das Ereignis, die zur Deduplizierung verwendet wird. | |
| [!UICONTROL Ereigniseigenschaften] | Ein JSON-Objekt mit benutzerdefinierten Eigenschaften des Ereignisses. Wählen Sie aus der Bereitstellung von rohen JSON-Dateien oder der Verwendung eines vereinfachten Satzes von Schlüsselwerteingaben. | |

>[!NOTE]
>
>Weitere Informationen zu den Standardfeldern für ein [!DNL Mixpanel] -Ereignis finden Sie in der [offiziellen Dokumentation](https://developer.mixpanel.com/reference/import-events#event).

![Fügen Sie eine Aktionskonfiguration für die Ereignisweiterleitungsregel hinzu.](../../../images/extensions/server/mixpanel/track-event-action.png)

Sobald die Aktion [!UICONTROL Ereignis verfolgen] zur Regel hinzugefügt wurde, können Sie die Bedingungen der Regel so konfigurieren, dass sie nur für bestimmte Ereignisse ausgelöst wird. Alternativ können Sie den Abschnitt &quot;Bedingungen&quot;leer lassen, damit die Regel für alle Ereignisse ausgelöst wird.

>[!IMPORTANT]
>
>Wenn Ihre Website das SDK [!DNL Mixpanel] verwendet, können Sie mit dem nächsten Schritt [Überprüfen Ihrer Daten in  [!DNL Mixpanel]](#validate) fortfahren. Wenn Sie das SDK [!DNL Mixpanel] nicht verwenden, müssen Sie [eine separate Identitäts-Tracking-Regel erstellen](#create-an-identity-tracking-rule), um sicherzustellen, dass die entsprechenden Ereignisse und `distinct_id` -Werte an [!DNL Mixpanel] gesendet werden, wenn ein Benutzeridentifikationsereignis auftritt.

## Daten mit [!DNL Mixpanel] validieren {#validate}

Wenn Ihre Implementierung erfolgreich ist und Ereignisse erfasst werden, werden Ereignisse in der [[!DNL Mixpanel] Konsole](https://help.mixpanel.com/hc/en-us/articles/4402837164948) angezeigt.

Überprüfen Sie, ob die Post-Login-Ereignisse mit E-Mail-Werten und den bei Verwendung von **[!UICONTROL Ereignis senden]** erstellten Ereignissen zusammengeführt wurden. [!DNL Mixpanel] Bei ordnungsgemäßer Implementierung verknüpft [!DNL Mixpanel] sie mit einem einzelnen [Benutzerprofil](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Konversionsereignisse mithilfe der Ereignisweiterleitung an [!DNL Mixpanel] gesendet werden. Diese Ereignisweiterleitungs-Erweiterung nutzt das [!DNL Mixpanel]-SDK und die JavaScript-API. Weitere Informationen zu diesen Technologien finden Sie in der offiziellen Dokumentation:

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] JavaScript-API](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Weiterführende Informationen zu Ereignisweiterleitungsfunktionen in Experience Platform finden Sie in der [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
