---
title: Zendesk-Ereignisweiterleitungserweiterung
description: Zendesk-Ereignisweiterleitungserweiterung für Adobe Experience Platform.
source-git-commit: ae585660bbf057f25e6f0dfc2520e6bb0af9d8d0
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 7%

---

# [!DNL Zendesk] Übersicht über die Ereignis-API-Erweiterung

[Zendesk](https://www.zendesk.com) ist eine Kundenservice-Lösung und ein Vertriebstool. Die Zendesk [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) -Erweiterung nutzt die [[!DNL Zendesk Events API]](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) , um Ereignisse vom Adobe Experience Platform Edge Network zur weiteren Verarbeitung an Zendesk zu senden. Sie können die Erweiterung verwenden, um Kundenprofilinteraktionen zur Verwendung in der nachgelagerten Analyse und Aktion zu erfassen.

In diesem Dokument wird beschrieben, wie Sie die Erweiterung in der Benutzeroberfläche installieren und konfigurieren.

## Voraussetzungen

Sie müssen über ein Zendesk-Konto verfügen, um diese Erweiterung verwenden zu können. Sie können sich für ein Zendesk-Konto im [Zendesk-Website](https://www.zendesk.com/register/).

Sie müssen außerdem die folgenden Details für Ihre Zendesk-Konfiguration sammeln:

| Schlüsseltyp | Beschreibung | Beispiel |
| --- | --- | --- |
| Subdomain | Während des Registrierungsprozesses wird eine eindeutige **Subdomain** wird speziell für das Konto erstellt. Siehe Abschnitt [Zendesk-Dokumentation](https://developer.zendesk.com/documentation/ticketing/working-with-oauth/creating-and-using-oauth-tokens-with-the-api/) für weitere Informationen. | `xxxxx.zendesk.com` , `xxxxx` ist der Wert, der bei der Kontoerstellung angegeben wurde) |
| API-Token | Zendesk verwendet Trägertoken als Authentifizierungsmechanismus für die Kommunikation mit der Zendesk-API. Nachdem Sie sich beim Zendesk-Portal angemeldet haben, generieren Sie ein API-Token. Siehe Abschnitt [Zendesk-Dokumentation](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token) für weitere Informationen. | `cwWyOtHAv12w4dhpiulfe9BdZFTz3OKaTSzn2QvV` |

{style=&quot;table-layout:auto&quot;}

Schließlich müssen Sie ein Ereignis-Weiterleitungsgeheimnis für das API-Token erstellen. Setzen Sie den geheimen Typ auf **[!UICONTROL Token]** und setzen Sie den Wert auf das API-Token, das Sie aus Ihrer Zendesk-Konfiguration erfasst haben. Weitere Informationen finden Sie in der Dokumentation unter [Geheimnisse in der Ereignisweiterleitung](../../../ui/event-forwarding/secrets.md) für weitere Informationen zum Konfigurieren von Geheimnissen.

## Installieren der Erweiterung {#install}

Navigieren Sie zur Installation der Zendesk-Erweiterung in der Benutzeroberfläche zu **Ereignisweiterleitung** und wählen Sie eine Eigenschaft aus, der die Erweiterung hinzugefügt werden soll, oder erstellen Sie stattdessen eine neue Eigenschaft.

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, navigieren Sie zu **Erweiterungen** > **Katalog**. Suchen Sie nach &quot;[!DNL Zendesk]&quot;, und wählen Sie dann **[!DNL Install]** auf der Zendesk-Erweiterung.

![Schaltfläche &quot;Installieren&quot;für die Zendesk-Erweiterung, die in der Benutzeroberfläche ausgewählt wird](../../../images/extensions/zendesk/install.png)

## Konfigurieren Sie die Erweiterung {#configure}

>[!IMPORTANT]
>
>Je nach Ihren Implementierungsanforderungen müssen Sie möglicherweise ein Schema, Datenelemente und einen Datensatz erstellen, bevor Sie die Erweiterung konfigurieren. Lesen Sie vor dem Start alle Konfigurationsschritte durch, um festzustellen, welche Entitäten Sie für Ihren Anwendungsfall einrichten müssen.

Auswählen **Erweiterungen** in der linken Navigation. under **Installiert** auswählen **Konfigurieren** in der Zendesk-Erweiterung.

![Schaltfläche &quot;Konfigurieren&quot;für die in der Benutzeroberfläche ausgewählte Zendesk-Erweiterung](../../../images/extensions/zendesk/configure.png)

under **[!UICONTROL Zendesk Domain]** Geben Sie den Wert für Ihre Zendesk-Subdomäne ein. under **[!UICONTROL Zendesk Token]**, wählen Sie das zuvor erstellte Geheimnis aus, das das API-Token enthält.

![In der Benutzeroberfläche ausgefüllte Konfigurationsoptionen](../../../images/extensions/zendesk/input.png)

## Konfigurieren einer Ereignisweiterleitungsregel

Erstellen einer neuen Ereignisweiterleitungsregel [Regel](../../../ui/managing-resources/rules.md) und konfigurieren Sie die Bedingungen nach Bedarf. Wählen Sie bei der Auswahl der Aktionen für die Regel die [!UICONTROL Splunk] Erweiterung und wählen Sie dann die [!UICONTROL Ereignis erstellen] Aktionstyp.

![Regel definieren](../../../images/extensions/zendesk/rule.png)

Beim Einrichten der Aktionskonfiguration werden Sie aufgefordert, den verschiedenen Eigenschaften, die an Zendesk gesendet werden, Datenelemente zuzuweisen.

![Aktionskonfiguration definieren](../../../images/extensions/zendesk/action-configurations.png)

Diese Datenelemente sollten wie unten beschrieben zugeordnet werden.

### `event` keys

`event` ist ein JSON-Objekt, das das vom Benutzer ausgelöste Ereignis darstellt. Weitere Informationen finden Sie im Dokument Zendesk . [Anatomie eines Ereignisses](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/) für Details zu den Eigenschaften, die von der `event` -Objekt.

Die folgenden Schlüssel können innerhalb der `event` -Objekt bei der Zuordnung zu Datenelementen:

| `event` Schlüssel | Typ | Plattformpfad | Beschreibung | Obligatorisch | Beschränkungen |
| --- | --- | --- | --- | --- | --- |
| `source` | Zeichenfolge | `arc.event.xdm._extconndev.event_source` | Die Anwendung, die das Ereignis gesendet hat. | Ja | Nicht anwenden `Zendesk` als Wert, da es ein geschützter Quellname für Zendesk-Standardereignisse ist. Versuche, sie zu verwenden, führen zu einem Fehler.<br>Die Länge des Wertes darf 40 Zeichen nicht überschreiten. |
| `type` | Zeichenfolge | `arc.event.xdm._extconndev.event_type` | Ein Name für den Ereignistyp. Sie können dieses Feld verwenden, um verschiedene Arten von Ereignissen für eine bestimmte Quelle zu kennzeichnen. Sie können beispielsweise einen Satz von Ereignissen für die Benutzeranmeldung und einen anderen für Warenkörbe erstellen. | Ja | Die Länge des Wertes darf 40 Zeichen nicht überschreiten. |
| `description` | Zeichenfolge | `arc.event.xdm._extconndev.description` | Eine Beschreibung für das Ereignis. | Nein | (Nicht angegeben) |
| `created_at` | Zeichenfolge | `arc.event.xdm.timestamp` | Ein Zeitstempel nach ISO-8601, der den Zeitpunkt der Erstellung des Ereignisses angibt. | Nein | (Nicht angegeben) |
| `properties` | Objekt | `arc.event.xdm._extconndev.EventProperties` | Ein benutzerdefiniertes JSON-Objekt mit Details zum Ereignis. | Ja | (Nicht angegeben) |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Siehe Abschnitt [[!DNL Zendesk Events API] Dokumentation](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) für zusätzliche Anleitungen zu Ereigniseigenschaften.

### `profile` keys

`profile` ist ein JSON-Objekt, das den Benutzer darstellt, der das Ereignis ausgelöst hat. Weitere Informationen finden Sie im Dokument Zendesk . [Anatomie eines Profils](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/) für Details zu den Eigenschaften, die von der `profile` -Objekt.

Die folgenden Schlüssel können innerhalb der `profile` -Objekt bei der Zuordnung zu Datenelementen:

| `profile` Schlüssel | Typ | Plattformpfad | Beschreibung | Obligatorisch | Beschränkungen |
| --- | --- | --- | --- | --- | --- |
| `source` | Zeichenfolge | `arc.event.xdm._extconndev.profile_source` | Das mit dem Profil verknüpfte Produkt oder Service, z. B. `Support`, `CompanyName`oder `Chat`. | Ja | (Nicht angegeben) |
| `type` | Zeichenfolge | `arc.event.xdm._extconndev.profile_type` | Ein Name für den Profiltyp. Sie können dieses Feld verwenden, um verschiedene Arten von Profilen für eine bestimmte Quelle zu erstellen. Sie können beispielsweise eine Gruppe von Unternehmensprofilen für Kunden und eine andere für Mitarbeiter erstellen. | Ja | Die Länge des Profiltyps darf 40 Zeichen nicht überschreiten. |
| `name` | Zeichenfolge | `arc.event.xdm._extconndev.name` | Der Name der Person aus dem Profil | Nein | (Nicht angegeben) |
| `user_id` | Zeichenfolge | `arc.event.xdm._extconndev.user_id` | Die Benutzer-ID der Person in Zendesk. | Nein | (Nicht angegeben) |
| `identifiers` | Array | `arc.event.xdm._extconndev.identifiers` | Ein Array, das mindestens eine Kennung enthält. Jeder Bezeichner besteht aus einem Typ und einem Wert. | Ja | Siehe Abschnitt [Zendesk-Dokumentation](https://developer.zendesk.com/api-reference/custom-data/profiles_api/profiles_api/#identifiers-array) Weitere Informationen über `identifiers` Array. Alle Felder und Werte müssen eindeutig sein. |
| `attributes` | Objekt | `arc.event.xdm._extconndev.attrbutes` | Ein Objekt, das benutzerdefinierte Eigenschaften für die Person enthält. | Nein | Siehe Abschnitt [Zendesk-Dokumentation](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/#attributes) für weitere Informationen zu Profilattributen. |

{style=&quot;table-layout:auto&quot;}

## Daten in Zendesk überprüfen {#validate}

Wenn die Ereigniserfassung und Adobe Experience Platform-Integration erfolgreich sind, sollten die Ereignisse in der Zendesk-Konsole wie unten dargestellt angezeigt werden. Dies weist auf eine erfolgreiche Integration hin.

Profile:

![Seite &quot;Zendesk-Profile&quot;](../../../images/extensions/zendesk/zendesk-profiles.png)

Ereignisse:

![Seite &quot;Zendesk-Ereignisse&quot;](../../../images/extensions/zendesk/zendesk-events.png)

## Anforderungsbeschränkungen {#limits}

Basierend auf dem Kontotyp, dem Zendesk [!DNL Events API] kann die folgende Anzahl von Anforderungen pro Minute verarbeiten:

| [!DNL Account Type] | Anforderungen pro Minute |
| --- | --- |
| [!DNL Team] | 250 |
| [!DNL Growth] | 250 |
| [!DNL Professional] | 500 |
| [!DNL Enterprise] | 750 |
| [!DNL Enterprise Plus] | 1000 |

{style=&quot;table-layout:auto&quot;}

Siehe Abschnitt [Zendesk-Dokumentation](https://developer.zendesk.com/api-reference/ticketing/account-configuration/usage_limits/#:~:text=API%20requests%20made%20by%20Zendesk%20apps%20are%20subject,sources%20for%20the%20account%2C%20including%20internal%20product%20requests.) für weitere Informationen zu diesen Beschränkungen.

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

Beim Verwenden oder Konfigurieren der Erweiterung werden die folgenden Fehler möglicherweise von der Zendesk Events API zurückgegeben:

| Fehler-Code | Beschreibung | Auflösung | Beispiel |
|---|---|---|---|
| 400 | **Ungültige Profillänge:** Dieser Fehler tritt auf, wenn die Länge eines Profilattributs mehr als 40 Zeichen umfasst. | Begrenzen Sie die Länge der Profilattributdaten auf maximal 40 Zeichen. | `{"error": [{"code":"InvalidProfileTypeLength","title": "Profile type length > 40 chars"}]}` |
| 401 | **Route nicht gefunden:** Dieser Fehler tritt auf, wenn eine ungültige Domäne angegeben wurde. | Stellen Sie sicher, dass eine gültige Domäne im folgenden Format bereitgestellt wird: `{subdomain}.zendesk.com` | `{"error": [{"description": "No route found for host {subdomain}.zendesk.com","title": "RouteNotFound"}]}` |
| 401 | **Ungültige oder fehlende Authentifizierung:** Dieser Fehler tritt auf, wenn der Zugriff auf das Token ungültig, fehlt oder abgelaufen ist. | Vergewissern Sie sich, dass das Zugriffstoken gültig ist und nicht abgelaufen ist. | `{"error": [{"code":"MissingOrInvalidAuthentication","title": "Invalid or Missing Authentication"}]}` |
| 403 | **Unzureichende Berechtigungen:** Dieser Fehler tritt auf, wenn keine ausreichenden Berechtigungen für den Zugriff auf die Ressource bereitgestellt wurden. | Überprüfen Sie, ob die erforderlichen Berechtigungen erteilt wurden. | `{"error": [{"code":"PermissionDenied","title": "Insufficient permisssions to perform operation"}]}` |
| 429 | **Zu viele Anforderungen:** Dieser Fehler tritt auf, wenn die Datensatzbegrenzung für das Endpunktobjekt überschritten wurde. | Siehe Abschnitt oben unter [Anforderungsbeschränkungen](#limits) für Einzelheiten zu den Schwellenwerten pro Begrenzung. | `{"error": [{"code":"TooManyRequests","title": "Too Many Requests"}]}` |

{style=&quot;table-layout:auto&quot;}

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Sie die Zendesk-Ereignisweiterleitungs-Erweiterung in der Benutzeroberfläche installieren und konfigurieren. Weitere Informationen zur Erfassung von Ereignisdaten in Zendesk finden Sie in der offiziellen Dokumentation:

* [Erste Schritte mit Ereignissen](https://developer.zendesk.com/documentation/custom-data/events/getting-started-with-events/)
* [Zendesk Events API](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/)
* [Über die Events-API](https://developer.zendesk.com/documentation/custom-data/events/about-the-events-api/)
* [Anatomie eines Ereignisses](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/)
* [Zendesk Profiles API](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/#profile-object)
* [Über die Profiles API](https://developer.zendesk.com/documentation/custom-data/profiles/about-the-profiles-api/)
* [Anatomie eines Profils](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/)
