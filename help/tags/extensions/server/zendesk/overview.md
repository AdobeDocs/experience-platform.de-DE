---
title: Erweiterung der Zendesk-Ereignisweiterleitung
description: Erweiterung der Zendesk-Ereignisweiterleitung für Adobe Experience Platform.
exl-id: 22e94699-5b84-4a73-b007-557221d3e223
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 98%

---

# Übersicht über die [!DNL Zendesk]-Ereignis-API-Erweiterung-

[Zendesk](https://www.zendesk.de) ist eine Kunden-Service-Lösung und ein Vertriebswerkzeug. Die Zendesk-Erweiterung [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) nutzt die [[!DNL Zendesk Events API]](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/), um Ereignisse aus dem Adobe Experience Platform Edge Network zur weiteren Verarbeitung an Zendesk zu senden. Sie können die Erweiterung verwenden, um Interaktionen mit Kundenprofilen zu sammeln und für nachgelagerte Analysen und Maßnahmen zu nutzen.

In diesem Dokument wird beschrieben, wie Sie die Erweiterung in der Benutzeroberfläche installieren und konfigurieren.

## Voraussetzungen

Sie müssen über ein Zendesk-Konto verfügen, um diese Erweiterung verwenden zu können. Sie können sich für ein Zendesk-Konto auf der [Zendesk-Website](https://www.zendesk.de/register/) registrieren.

Sie müssen ebenfalls die folgenden Details für Ihre Zendesk-Konfiguration erheben:

| Schlüsseltyp | Beschreibung | Beispiel |
| --- | --- | --- |
| Subdomain | Während des Registrierungsprozesses wird eine einzigartige **Subdomain** für das Konto erstellt. Weitere Informationen finden Sie in der [Zendesk-Dokumentation](https://developer.zendesk.com/documentation/ticketing/working-with-oauth/creating-and-using-oauth-tokens-with-the-api/). | `xxxxx.zendesk.com` (wobei `xxxxx` der Wert ist, der bei der Erstellung des Kontos angegeben wurde) |
| API-Token | Zendesk verwendet Inhaber-Token als Authentifizierungsmechanismus für die Kommunikation mit der Zendesk-API. Generieren Sie nach der Anmeldung am Zendesk-Portal ein API-Token. Weitere Informationen finden Sie in der [Zendesk-Dokumentation](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token). | `cwWyOtHAv12w4dhpiulfe9BdZFTz3OKaTSzn2QvV` |

{style=&quot;table-layout:auto&quot;}

Abschließend müssen Sie ein Geheimnis für die Ereignisweiterleitung für das API-Token erstellen. Setzen Sie den Geheimnistyp auf **[!UICONTROL Token]** und setzen Sie den Wert auf das API-Token, das Sie aus Ihrer Zendesk-Konfiguration erhalten haben. Weitere Informationen zum Konfigurieren von Geheimnissen finden Sie in der Dokumentation zu [Geheimnissen in der Ereignisweiterleitung](../../../ui/event-forwarding/secrets.md).

## Installieren der Erweiterung {#install}

Um die Zendesk-Erweiterung in der Benutzeroberfläche zu installieren, navigieren Sie zu **Ereignisweiterleitung** und wählen eine Eigenschaft aus, zu der Sie die Erweiterung hinzufügen möchten, oder erstellen Sie stattdessen eine neue Eigenschaft.

Sobald Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, navigieren Sie zu **Erweiterungen** > **Katalog**. Suchen Sie nach „[!DNL Zendesk]“, und wählen Sie dann **[!DNL Install]** auf der Zendesk-Erweiterung.

![Die Schaltfläche „Installieren“ für die Zendesk-Erweiterung wird in der Benutzeroberfläche ausgewählt](../../../images/extensions/server/zendesk/install.png)

## Konfigurieren Sie die Erweiterung {#configure}

>[!IMPORTANT]
>
>Je nach Ihren Implementierungsanforderungen müssen Sie möglicherweise ein Schema, Datenelemente und einen Datensatz erstellen, bevor Sie die Erweiterung konfigurieren. Bitte überprüfen Sie alle Konfigurationsschritte, bevor Sie beginnen, um festzustellen, welche Entitäten Sie für Ihren Anwendungsfall einrichten müssen.

Wählen Sie **Erweiterungen** in der linken Navigation aus. Wählen Sie unter **Installiert** die Schaltfläche **Konfigurieren** für die Zendesk-Erweiterung aus.

![Die Schaltfläche „Konfigurieren“ für die Zendesk-Erweiterung wird in der Benutzeroberfläche ausgewählt](../../../images/extensions/server/zendesk/configure.png)

Geben Sie unter **[!UICONTROL Zendesk Domain]** den Wert für Ihre Zendesk-Subdomain ein. Wählen Sie unter **[!UICONTROL Zendesk-Token]** das zuvor erstellte Geheimnis aus, das das API-Token enthält.

![In der Benutzeroberfläche ausgefüllte Konfigurationsoptionen](../../../images/extensions/server/zendesk/input.png)

## Konfigurieren einer Ereignisweiterleitungsregel

Beginnen Sie mit der Erstellung einer neuen [Regel](../../../ui/managing-resources/rules.md) für die Ereignisweiterleitung und konfigurieren Sie die Bedingungen nach Bedarf. Wählen Sie bei der Auswahl der Aktionen für die Regel die [!UICONTROL Zendesk] Erweiterung und wählen Sie dann die [!UICONTROL Ereignis erstellen] Aktionstyp.

![Regel festlegen](../../../images/extensions/server/zendesk/rule.png)

Beim Einrichten der Aktionskonfiguration werden Sie aufgefordert, den verschiedenen Eigenschaften, die an Zendesk gesendet werden, Datenelemente zuzuweisen.

![Aktionskonfiguration festlegen](../../../images/extensions/server/zendesk/action-configurations.png)

Diese Datenelemente sollten wie unten beschrieben zugeordnet werden.

### `event` keys

`event` ist ein JSON-Objekt, das das vom Benutzer ausgelöste Ereignis darstellt. Einzelheiten zu den vom `event`-Objekt erfassten Eigenschaften finden Sie im Zendesk-Dokument über die [Anatomie eines Ereignisses](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/).

Die folgenden Schlüssel können innerhalb des `event`-Objekts beim Mapping auf Datenelemente referenziert werden:

| `event`-Key | Typ | Platform-Pfad | Beschreibung | Obligatorisch | Beschränkungen |
| --- | --- | --- | --- | --- | --- |
| `source` | Zeichenfolge | `arc.event.xdm._extconndev.event_source` | Das Programm, das das Ereignis gesendet hat. | Ja | Verwenden Sie nicht `Zendesk` als Wert, da dies ein geschützter Quellenname für Zendesk-Standardereignisse ist. Der Versuch, ihn zu verwenden, führt zu einem Fehler.<br>Die Länge des Wertes darf 40 Zeichen nicht überschreiten. |
| `type` | Zeichenfolge | `arc.event.xdm._extconndev.event_type` | Ein Name für den Ereignistyp. Sie können dieses Feld verwenden, um verschiedene Arten von Ereignissen für eine bestimmte Quelle zu kennzeichnen. Sie können beispielsweise einen Satz von Ereignissen für die Benutzeranmeldung und einen anderen für Warenkörbe erstellen. | Ja | Die Länge des Wertes darf 40 Zeichen nicht überschreiten. |
| `description` | Zeichenfolge | `arc.event.xdm._extconndev.description` | Eine Beschreibung für das Ereignis. | Nein | (Nicht angegeben) |
| `created_at` | Zeichenfolge | `arc.event.xdm.timestamp` | Ein ISO-8601-Zeitstempel, der den Zeitpunkt angibt, zu dem das Ereignis erstellt wurde. | Nein | (Nicht angegeben) |
| `properties` | Objekt | `arc.event.xdm._extconndev.EventProperties` | Ein benutzerdefiniertes JSON-Objekt mit Details über das Ereignis. | Ja | (Nicht angegeben) |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>In der [[!DNL Zendesk Events API] Dokumentation](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) finden Sie weitere Hinweise zu den Ereigniseigenschaften.

### `profile` keys

`profile` ist ein JSON-Objekt, das den Benutzer darstellt, der das Ereignis ausgelöst hat. Einzelheiten zu den Eigenschaften, die das `profile`-Objekt erfasst, finden Sie im Zendesk-Dokument [Anatomie eines Profils](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/).

Die folgenden Schlüssel können innerhalb des `profile`-Objekts beim Mapping auf Datenelemente referenziert werden:

| `profile`-Key | Typ | Platform-Pfad | Beschreibung | Obligatorisch | Beschränkungen |
| --- | --- | --- | --- | --- | --- |
| `source` | Zeichenfolge | `arc.event.xdm._extconndev.profile_source` | Das mit dem Profil verknüpfte Produkt oder der Service, beispielsweise `Support`, `CompanyName` oder `Chat`. | Ja | (Nicht angegeben) |
| `type` | Zeichenfolge | `arc.event.xdm._extconndev.profile_type` | Ein Name für den Profiltyp. Sie können dieses Feld verwenden, um verschiedene Arten von Profilen für eine bestimmte Quelle zu erstellen. Sie können beispielsweise einen Satz von Unternehmensprofilen für Kunden und einen anderen für Mitarbeiter erstellen. | Ja | Die Länge des Profiltyps darf 40 Zeichen nicht überschreiten. |
| `name` | Zeichenfolge | `arc.event.xdm._extconndev.name` | Der Name der Person aus dem Profil | Nein | (Nicht angegeben) |
| `user_id` | Zeichenfolge | `arc.event.xdm._extconndev.user_id` | Die Benutzer-ID der Person in Zendesk. | Nein | (Nicht angegeben) |
| `identifiers` | Array | `arc.event.xdm._extconndev.identifiers` | Ein Array, das mindestens einen Bezeichner enthält. Jeder Bezeichner besteht aus einem Typ und einem Wert. | Ja | Weitere Informationen über das Array `identifiers` finden Sie in der [Zendesk-Dokumentation](https://developer.zendesk.com/api-reference/custom-data/profiles_api/profiles_api/#identifiers-array). Alle Felder und Werte müssen einzigartig sein. |
| `attributes` | Objekt | `arc.event.xdm._extconndev.attrbutes` | Ein Objekt, das benutzerdefinierte Eigenschaften über die Person enthält. | Nein | Weitere Informationen zu Profilattributen finden Sie in der [Zendesk-Dokumentation](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/#attributes). |

{style=&quot;table-layout:auto&quot;}

## Validieren von Daten in Zendesk {#validate}

Wenn die Ereigniserfassung und Adobe Experience Platform-Integration erfolgreich sind, sollten die Ereignisse in der Zendesk-Konsole wie unten dargestellt angezeigt werden. Dies zeigt eine erfolgreiche Integration an.

Profile:

![Seite „Zendesk-Profile“](../../../images/extensions/server/zendesk/zendesk-profiles.png)

Ereignisse:

![Seite „Zendesk-Ereignisse“](../../../images/extensions/server/zendesk/zendesk-events.png)

## Obergrenzen für Anfragen {#limits}

Je nach Kontotyp kann die Zendesk [!DNL Events API] die folgende Anzahl von Anfragen pro Minute verarbeiten:

| [!DNL Account Type] | Anfragen pro Minute |
| --- | --- |
| [!DNL Team] | 250 |
| [!DNL Growth] | 250 |
| [!DNL Professional] | 500 |
| [!DNL Enterprise] | 750 |
| [!DNL Enterprise Plus] | 1000 |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu diesen Obergrenzen finden Sie in der [Zendesk-Dokumentation](https://developer.zendesk.com/api-reference/ticketing/account-configuration/usage_limits/#:~:text=API%20requests%20made%20by%20Zendesk%20apps%20are%20subject,sources%20for%20the%20account%2C%20including%20internal%20product%20requests.).

## Fehler und Fehlerbehebung {#errors-and-troubleshooting}

Bei der Verwendung oder Konfiguration der Erweiterung können die folgenden Fehler von der Zendesk-Ereignis-API zurückgegeben werden:

| Fehler-Code | Beschreibung | Auflösung | Beispiel |
|---|---|---|---|
| 400 | **Ungültige Profillänge**: Dieser Fehler tritt auf, wenn die Länge eines Profilattributs mehr als 40 Zeichen umfasst. | Begrenzen Sie die Länge der Profilattributdaten auf maximal 40 Zeichen. | `{"error": [{"code":"InvalidProfileTypeLength","title": "Profile type length > 40 chars"}]}` |
| 401 | **Route nicht gefunden**: Dieser Fehler tritt auf, wenn eine ungültige Domain angegeben wurde. | Vergewissern Sie sich, dass eine gültige Domain in folgendem Format angegeben wird: `{subdomain}.zendesk.com` | `{"error": [{"description": "No route found for host {subdomain}.zendesk.com","title": "RouteNotFound"}]}` |
| 401 | **Ungültige oder fehlende Authentifizierung**: Dieser Fehler tritt auf, wenn das Zugriffs-Token ungültig ist, fehlt oder abgelaufen ist. | Stellen Sie sicher, dass das Zugriffs-Token gültig und nicht abgelaufen ist. | `{"error": [{"code":"MissingOrInvalidAuthentication","title": "Invalid or Missing Authentication"}]}` |
| 403 | **Unzureichende Berechtigungen**: Dieser Fehler tritt auf, wenn keine ausreichenden Berechtigungen für den Zugriff auf die Ressource bereitgestellt wurden. | Überprüfen Sie, ob die erforderlichen Berechtigungen bereitgestellt wurden. | `{"error": [{"code":"PermissionDenied","title": "Insufficient permisssions to perform operation"}]}` |
| 429 | **Zu viele Anfragen**: Dieser Fehler tritt auf, wenn das Datensatzlimit für das Endpunktobjekt überschritten wurde. | Einzelheiten zu den Beschränkungen für einzelnen Anfragen finden Sie im obigen Abschnitt über [Anfragebeschränkungen](#limits). | `{"error": [{"code":"TooManyRequests","title": "Too Many Requests"}]}` |

{style=&quot;table-layout:auto&quot;}

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie die Zendesk-Erweiterung für die Ereignisweiterleitung in der Benutzeroberfläche installiert und konfiguriert wird. Weitere Informationen zur Erfassung von Ereignisdaten in Zendesk finden Sie in der offiziellen Dokumentation:

* [Erste Schritte mit Ereignissen](https://developer.zendesk.com/documentation/custom-data/events/getting-started-with-events/)
* [Zendesk-Ereignis-API](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/)
* [Über die Ereignis-API](https://developer.zendesk.com/documentation/custom-data/events/about-the-events-api/)
* [Anatomie eines Ereignisses](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/)
* [Zendesk-Profile-API](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/#profile-object)
* [Über die Profile-API](https://developer.zendesk.com/documentation/custom-data/profiles/about-the-profiles-api/)
* [Anatomie eines Profils](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/)
