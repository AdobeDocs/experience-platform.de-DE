---
title: Konfigurieren von Geheimnissen bei der Ereignisweiterleitung
description: Erfahren Sie, wie Sie Geheimnisse in der Benutzeroberfläche konfigurieren, um sich bei Endpunkten zu authentifizieren, die in den Eigenschaften der Ereignisweiterleitung verwendet werden.
exl-id: eefd87d7-457f-422a-b159-5b428da54189
source-git-commit: 592acdd45b1db5da95430b4e707cd9a2c18c1645
workflow-type: tm+mt
source-wordcount: '2426'
ht-degree: 75%

---

# Konfigurieren von Geheimnissen bei der Ereignisweiterleitung

Bei der Ereignisweiterleitung sind geheime Daten eine Ressource, die eine Authentifizierungsberechtigung für ein anderes System darstellt und den sicheren Datenaustausch ermöglicht. Geheime Daten können nur in den Eigenschaften der Ereignisweiterleitung erstellt werden.

Die folgenden geheimen Typen werden derzeit unterstützt:

| Typ von geheimen Daten | Beschreibung |
| --- | --- |
| [!UICONTROL Google OAuth 2] | Enthält mehrere Attribute, um die [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749)-Authentifizierungsspezifikation zur Verwendung in der [Google Ads-API](https://developers.google.com/google-ads/api/docs/oauth/overview) und [Pub/Sub-API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview) zu unterstützen. Das System fordert von Ihnen die erforderlichen Informationen an. Anschließend übernimmt es die Verlängerung dieser Token für Sie in einem bestimmten Intervall. |
| [!UICONTROL HTTP] | Enthält zwei Zeichenfolgen-Attribute für einen Benutzernamen und ein Kennwort. |
| [!UICONTROL [!DNL LinkedIn] OAuth 2] | Das System fordert von Ihnen die erforderlichen Informationen an. Anschließend übernimmt es die Verlängerung dieser Token für Sie in einem bestimmten Intervall. |
| [!UICONTROL OAuth 2] | Enthält mehrere Attribute zur Unterstützung des [Grant-Typs der Client-Anmeldeinformationen](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.4) für die Authentifizierungsspezifikation [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749). Das System fordert von Ihnen die erforderlichen Informationen an. Anschließend übernimmt es die Verlängerung dieser Token für Sie in einem bestimmten Intervall. |
| [!UICONTROL OAuth 2 JWT] | Enthält mehrere Attribute zur Unterstützung des JSON Web Token (JWT)-Profils für [OAuth 2.0 Authorization](https://datatracker.ietf.org/doc/html/rfc7523#section-2.1) Finanzhilfen. Das System fordert von Ihnen die erforderlichen Informationen an. Anschließend übernimmt es die Verlängerung dieser Token für Sie in einem bestimmten Intervall. |
| [!UICONTROL Token] | Eine einzelne Zeichenfolge, die den Wert eines Authentifizierungs-Tokens darstellt, der von beiden Systemen verstanden wird. |

{style="table-layout:auto"}

Dieses Handbuch bietet einen allgemeinen Überblick darüber, wie Geheimnisse für eine [!UICONTROL Edge]-Eigenschaft zur Ereignisweiterleitung in der Experience Platform- oder Datenerfassungs-Benutzeroberfläche konfiguriert werden.

>[!NOTE]
>
>Ausführliche Anleitungen zum Verwalten von geheimen Daten in der Reactor-API, einschließlich einer Beispiel-JSON zur Struktur der geheimen Daten, finden Sie im [API-Handbuch für geheime Daten](../../api/guides/secrets.md).

## Voraussetzungen

In diesem Handbuch wird davon ausgegangen, dass Sie bereits mit der Verwaltung von Ressourcen für Tags und mit der Ereignisweiterleitung in der Benutzeroberfläche vertraut sind, einschließlich der Erstellung eines Datenelements und einer Ereignisweiterleitungsregel. Wenn Sie eine Einführung benötigen, finden Sie weitere Informationen im Handbuch unter [Verwalten von Ressourcen](../managing-resources/overview.md).

Außerdem sollten Sie über ein grundlegendes Verständnis des Veröffentlichungsflusses im Hinblick auf Tags und Ereignisweiterleitung verfügen, einschließlich der Möglichkeit, Ressourcen zu einer Bibliothek hinzuzufügen und einen Build zum Testen auf Ihrer Website zu installieren. Weitere Informationen finden Sie in der [Veröffentlichungsübersicht](../publishing/overview.md).

## Erstellen geheimer Daten {#create}

>[!CONTEXTUALHELP]
>id="platform_eventforwarding_secrets_environments"
>title="Umgebungen für Geheimnisse"
>abstract="Damit geheime Daten durch die Ereignisweiterleitung verwendet werden können, müssen sie einer vorhandenen Umgebung zugewiesen werden. Wenn Sie keine Umgebungen für Ihre Ereignisweiterleitungseigenschaft erstellt haben, müssen Sie diese konfigurieren, bevor Sie fortfahren."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html?lang=de" text="Umgebungen – Übersicht"

Um ein Geheimnis zu erstellen, wählen Sie in der linken Navigationsleiste **[!UICONTROL Ereignisweiterleitung]**, um die Ereignisweiterleitungseigenschaft, der Sie das Geheimnis hinzufügen möchten, zu öffnen. Wählen Sie anschließend im linken Navigationsbereich zunächst **[!UICONTROL Geheime Daten]** und dann **[!UICONTROL Neue geheime Daten erstellen]** aus.

![Neue geheimen Daten erstellen](../../images/ui/event-forwarding/secrets/create-new-secret.png)

Im nächsten Bildschirm können Sie die Details der geheimen Daten konfigurieren. Damit geheime Daten durch die Ereignisweiterleitung verwendet werden können, müssen sie einer vorhandenen Umgebung zugewiesen werden. Wenn Sie keine Umgebungen für Ihre Ereignisweiterleitungs-Eigenschaft erstellt haben, schauen Sie sich zunächst die Anleitung zur Konfiguration im Handbuch zu [Umgebungen](../publishing/environments.md) an, bevor Sie fortfahren.

>[!NOTE]
>
>Wenn Sie die geheimen Daten dennoch erstellen und speichern möchten, bevor Sie sie einer Umgebung hinzufügen, deaktivieren Sie die Option **[!UICONTROL Geheime Daten an Umgebungen anhängen]**, bevor Sie den Rest der Informationen ausfüllen. Beachten Sie, dass Sie sie später einer Umgebung zuweisen müssen, wenn Sie die geheimen Daten verwenden möchten.
>
>![Umgebung deaktivieren](../../images/ui/event-forwarding/secrets/env-disabled.png)

Wählen Sie unter **[!UICONTROL Zielumgebung]** im Dropdown-Menü die Umgebung aus, der Sie die geheimen Daten zuweisen möchten. Geben Sie unter **[!UICONTROL Name der geheimen Daten]** einen Namen für die geheimen Daten im Kontext der Umgebung an. Dieser Name muss für alle geheimen Daten unter der Ereignisweiterleitungs-Eigenschaft eindeutig sein.

![Umgebung und Name](../../images/ui/event-forwarding/secrets/env-and-name.png)

Geheime Daten können jeweils nur einer Umgebung zugewiesen werden. Sie können jedoch bei Bedarf die gleichen Anmeldeinformationen mehreren geheimen Daten in verschiedenen Umgebungen zuweisen. Wählen Sie **[!UICONTROL Umgebung hinzufügen]** aus, um der Liste eine weitere Zeile hinzuzufügen.

![Umgebung hinzufügen](../../images/ui/event-forwarding/secrets/add-env.png)

Für jede Umgebung, die Sie hinzufügen, müssen Sie einen weiteren eindeutigen Namen für die zugehörigen geheimen Daten angeben. Wenn Sie alle verfügbaren Umgebungen ausfüllen, steht die Schaltfläche **[!UICONTROL Umgebung hinzufügen]** nicht mehr zur Verfügung.

![Umgebung hinzufügen nicht verfügbar](../../images/ui/event-forwarding/secrets/add-env-greyed.png)

Von hier aus unterscheiden sich die Schritte zum Erstellen der geheimen Daten je nach dem Typ der jeweils erstellten geheimen Daten. Einzelheiten finden Sie in den nachfolgenden Abschnitten:

* [[!UICONTROL Token]](#token)
* [[!UICONTROL HTTP]](#http)
* [[!UICONTROL OAuth 2]](#oauth2)
* [[!UICONTROL OAuth 2 JWT]](#oauth2jwt)
* [[!UICONTROL Google OAuth 2]](#google-oauth2)
* [[!UICONTROL [!DNL LinkedIn] OAuth 2]](#linkedin-oauth2)

### [!UICONTROL Token] {#token}

Um geheime Daten vom Typ „Token“ zu erstellen, wählen Sie in der Dropdown-Liste **[!UICONTROL Typ]** die Option **[!UICONTROL Token]** aus. Geben Sie im nun erscheinenden Feld **[!UICONTROL Token]** die Zeichenfolge zur Anmeldung an, die vom System erkannt wird, für das Sie sich authentifizieren. Wählen Sie **[!UICONTROL Geheime Daten erstellen]** aus, um die geheimen Daten zu speichern.

![Geheime Daten vom Typ „Token“](../../images/ui/event-forwarding/secrets/token-secret.png)

### [!UICONTROL HTTP] {#http}

Um geheime Daten vom Typ „HTTP“ zu erstellen, wählen Sie in der Dropdown-Liste **[!UICONTROL Typ]** die Option **[!UICONTROL Einfaches HTTP]** aus. Geben Sie in den unten angezeigten Feldern einen Benutzernamen und ein Kennwort zur Anmeldung ein, bevor Sie die Option **[!UICONTROL Geheime Daten erstellen]** auswählen, um die jeweiligen geheimen Daten zu speichern.

>[!NOTE]
>
>Nach dem Speichern werden die Anmeldedaten mit dem [Grundlegenden HTTP-Authentifizierungsschema](https://www.rfc-editor.org/rfc/rfc7617.html) verschlüsselt.

![Geheime Daten vom Typ „HTTP“](../../images/ui/event-forwarding/secrets/http-secret.png)

### [!UICONTROL OAuth 2] {#oauth2}

Um geheime Daten vom Typ „OAuth 2“ zu erstellen, wählen Sie aus der Dropdown-Liste **[!UICONTROL Typ]** die Option **[!UICONTROL OAuth 2]** aus. Geben Sie in den unten angezeigten Feldern Ihre [[!UICONTROL Client-ID] und Ihr [!UICONTROL Client-Geheimnis]](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/) sowie die [[!UICONTROL Token-URL]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) für Ihre OAuth-Integration ein. Das Feld [!UICONTROL Token-URL] in der Benutzeroberfläche ist eine Verkettung zwischen dem Autorisierungs-Server-Host und dem Token-Pfad.

![Geheime Daten vom Typ „OAuth 2“](../../images/ui/event-forwarding/secrets/oauth-secret-1.png)

Unter **[!UICONTROL Anmeldedaten-Optionen]** können Sie weitere Optionen für die Anmeldedaten bereitstellen, z. B. `scope` und `audience` in Form von Schlüssel-Wert-Paaren. Um weitere Schlüssel-Wert-Paare hinzuzufügen, wählen Sie **[!UICONTROL Weitere hinzufügen]** aus.

![Anmeldedaten-Optionen](../../images/ui/event-forwarding/secrets/oauth-secret-2.png)

Schließlich können Sie den Wert **[!UICONTROL Versatz aktualisieren]** für die jeweiligen geheimen Daten konfigurieren. Dies stellt die Anzahl der Sekunden vor Ablauf des Tokens dar, nach denen das System eine automatische Aktualisierung durchführt. Die entsprechende Uhrzeit in Stunden und Minuten wird rechts neben dem Feld angezeigt und bei der Eingabe automatisch aktualisiert.

![Versatz aktualisieren](../../images/ui/event-forwarding/secrets/oauth-secret-3.png)

Wenn beispielsweise der Zeitversatz zur Aktualisierung auf den Standardwert von `14400` (vier Stunden) eingestellt ist und der Wert für `expires_in` beim Zugriffs-Token `86400` (24 Stunden) ist, aktualisiert das System die geheimen Daten automatisch in 20 Stunden.

>[!IMPORTANT]
>
>Bei geheimen Daten des Typs „OAuth“ müssen zwischen Aktualisierungen mindestens vier Stunden liegen und diese Daten müssen zudem mindestens acht Stunden gültig sein. Durch diese Beschränkung haben Sie mindestens vier Stunden Zeit, um bei Problemen mit dem generierten Token einzugreifen.
>
>Wenn der Versatz beispielsweise auf `28800` (acht Stunden) eingestellt ist und der Wert `expires_in` beim Zugriffs-Token `36000` (zehn Stunden) ist, würde der Austausch scheitern, da der daraus resultierende Unterschied weniger als vier Stunden betragen würde.

Wenn Sie fertig sind, wählen Sie die Option **[!UICONTROL Geheime Daten erstellen]** aus, um die geheimen Daten zu speichern.

![OAuth 2-Versatz speichern](../../images/ui/event-forwarding/secrets/oauth-secret-4.png)

### [!UICONTROL OAuth 2 JWT] {#oauth2jwt}

Um ein OAuth 2 JWT-Geheimnis zu erstellen, wählen Sie **[!UICONTROL OAuth 2 JWT]** aus dem **[!UICONTROL Typ]** Dropdown.

![Die [!UICONTROL Geheimnis erstellen] Registerkarte mit dem OAuth 2 JWT-Geheimnis hervorgehoben im [!UICONTROL Typ] Dropdown.](../../images/ui/event-forwarding/secrets/oauth-jwt-secret.png)

>[!NOTE]
>
>Die einzige [!UICONTROL Algorithmus] wird derzeit für das Signieren des JWT unterstützt RS256.

Geben Sie in den unten angezeigten Feldern Ihre [!UICONTROL Aussteller], [!UICONTROL Betreff], [!UICONTROL Zielgruppe], [!UICONTROL Benutzerspezifische Ansprüche], [!UICONTROL TTL]und wählen Sie dann die [!UICONTROL Algorithmus] aus dem Dropdown-Menü aus. Geben Sie als Nächstes die [!UICONTROL Private Key Id]sowie [[!UICONTROL Token-URL]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) für Ihre OAuth-Integration. Die [!UICONTROL Token-URL] -Feld ist kein Pflichtfeld. Wenn ein Wert angegeben wird, wird das JWT durch ein Zugriffstoken ausgetauscht. Das Geheimnis wird entsprechend der `expires_in` -Attribut aus der Antwort und dem [!UICONTROL Versatz aktualisieren] -Wert. Wenn kein Wert angegeben wird, ist das an den Rand gepushte Geheimnis das JWT. Die JWT wird entsprechend der [!UICONTROL TTL] und [!UICONTROL Versatz aktualisieren] -Werte.

![Die [!UICONTROL Geheimnis erstellen] mit einer Auswahl von Eingabefeldern markiert.](../../images/ui/event-forwarding/secrets/oauth-jwt-information.png)

under **[!UICONTROL Berechtigungsoptionen]** können Sie weitere Berechtigungsoptionen bereitstellen, z. B. `jwt_param` in Form von Schlüssel-Wert-Paaren. Um weitere Schlüssel-Wert-Paare hinzuzufügen, wählen Sie **[!UICONTROL Weitere hinzufügen]** aus.

![Die [!UICONTROL Geheimnis erstellen] Registerkarte, die die [!UICONTROL Berechtigungsoptionen] -Felder.](../../images/ui/event-forwarding/secrets/oauth-jwt-credential-options.png)

Schließlich können Sie den Wert **[!UICONTROL Versatz aktualisieren]** für die jeweiligen geheimen Daten konfigurieren. Dies stellt die Anzahl der Sekunden vor Ablauf des Tokens dar, nach denen das System eine automatische Aktualisierung durchführt. Die entsprechende Uhrzeit in Stunden und Minuten wird rechts neben dem Feld angezeigt und bei der Eingabe automatisch aktualisiert.

![Die [!UICONTROL Geheimnis erstellen] Registerkarte, die die [!UICONTROL Versatz aktualisieren] -Feld.](../../images/ui/event-forwarding/secrets/oauth-jwt-refresh-offset.png)

Wenn beispielsweise der Aktualisierungsoffset auf den Standardwert `1800` (30 Minuten) und das Zugriffstoken verfügt über eine `expires_in` Wert von `3600` (eine Stunde), aktualisiert das System das Geheimnis automatisch in einer Stunde.

>[!IMPORTANT]
>
>Ein OAuth 2 JWT-Geheimnis benötigt zwischen Aktualisierungen mindestens 30 Minuten und muss auch mindestens eine Stunde gültig sein. Durch diese Einschränkung erhalten Sie mindestens 30 Minuten, um bei Problemen mit dem generierten Token einzugreifen.
>
>Wenn der Offset beispielsweise auf `1800` (30 Minuten) und das Zugriffstoken verfügt über eine `expires_in` von `2700` (45 Minuten), würde der Austausch fehlschlagen, da der daraus resultierende Unterschied weniger als 30 Minuten betragen würde.

Wenn Sie fertig sind, wählen Sie die Option **[!UICONTROL Geheime Daten erstellen]** aus, um die geheimen Daten zu speichern.

![Die [!UICONTROL Geheimnis erstellen] Tabulatorhervorhebung [!UICONTROL Geheimnis erstellen]](../../images/ui/event-forwarding/secrets/oauth-jwt-create-secret.png)

### [!UICONTROL Google OAuth 2] {#google-oauth2}

Um ein Geheimnis für Google OAuth 2 zu erstellen, wählen Sie aus der Dropdown-Liste **[!UICONTROL Typ]** die Option **[!UICONTROL Google OAuth 2]** aus. Wählen Sie unter **[!UICONTROL Bereiche]** die Google-APIs aus, für die Sie mithilfe dieses Geheimnisses Zugriff gewähren möchten. Die folgenden Produkte werden derzeit unterstützt:

* [Google Ads-API](https://developers.google.com/google-ads/api/docs/oauth/overview)
* [Pub/Sub-API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)

Klicken Sie abschließend auf **[!UICONTROL Geheimnis erstellen]**.

![Google OAuth 2-Geheimnis](../../images/ui/event-forwarding/secrets/google-oauth.png)

Ein Popup erscheint, das Sie darüber informiert, dass das Geheimnis manuell über Google autorisiert werden muss. Wählen Sie **[!UICONTROL Erstellen und autorisieren]** aus, um fortzufahren.

![Popup für Google-Autorisierung](../../images/ui/event-forwarding/secrets/google-authorization.png)

Es wird ein Dialogfeld angezeigt, in dem Sie die Anmeldeinformationen für Ihr Google-Konto eingeben können. Befolgen Sie die Anweisungen, um der Ereignisweiterleitung unter dem ausgewählten Bereich Zugriff auf Ihre Daten zu gewähren. Sobald der Autorisierungsprozess abgeschlossen ist, wird das Geheimnis erstellt.

>[!IMPORTANT]
>
>Falls für Ihre Organisation eine Richtlinie zur erneuten Authentifizierung für Google Cloud-Anwendungen festgelegt ist, werden die erstellten Geheimnisse nicht erfolgreich aktualisiert, wenn die Authentifizierung abgelaufen ist (je nach Richtlinienkonfiguration zwischen 1 und 24 Stunden).
>
>Um dieses Problem zu beheben, melden Sie sich bei der Google Admin Console an und navigieren Sie zur **[!DNL App access control]**-Seite, damit Sie die Ereignisweiterleitungs-App (Adobe Real-Time CDP-Ereignisweiterleitung) als [!DNL Trusted] markieren können. Weitere Informationen finden Sie in der Google-Dokumentation unter [Festlegen von Sitzungslängen für Google Cloud-Services](https://support.google.com/a/answer/9368756).

### [!UICONTROL [!DNL LinkedIn] OAuth 2] {#linkedin-oauth2}

So erstellen Sie eine [!DNL LinkedIn] OAuth 2-Geheimnis, wählen Sie **[!UICONTROL [!DNL LinkedIn]OAuth 2]** aus dem **[!UICONTROL Typ]** Dropdown. Wählen Sie als Nächstes **[!UICONTROL Geheimnis erstellen]**.

![Die [!UICONTROL Geheimnis erstellen] mit dem [!UICONTROL Typ] Feld markiert.](../../images/ui/event-forwarding/secrets/linkedin-oauth.png)

Ein Popup erscheint, das Sie darüber informiert, dass das Geheimnis manuell über autorisiert werden muss [!DNL LinkedIn]. Auswählen **[!UICONTROL Geheimnis erstellen und autorisieren mit[!DNL LinkedIn]]** , um fortzufahren.

![[!DNL LinkedIn] Popover-Markierung für Autorisierung [!UICONTROL Geheimnis erstellen und autorisieren mit [!DNL LinkedIn]].](../../images/ui/event-forwarding/secrets/linkedin-authorization.png)

Es wird ein Dialogfeld angezeigt, in dem Sie zur Eingabe Ihrer [!DNL LinkedIn] Anmeldedaten. Befolgen Sie die Anweisungen, um der Ereignisweiterleitung Zugriff auf Ihre Daten zu gewähren.

Sobald der Autorisierungsprozess abgeschlossen ist, kehren Sie zum **[!UICONTROL Geheimnisse]** -Tab, wo Sie Ihr neu erstelltes Geheimnis sehen können. Hier können Sie den Status des Geheimnisses und das Ablaufdatum sehen.

![Die [!UICONTROL Geheimnis] -Tab, der das neu erstellte Geheimnis hervorhebt.](../../images/ui/event-forwarding/secrets/linkedin-new-secret.png)

#### Erneutes Autorisieren eines [!UICONTROL [!DNL LinkedIn] OAuth 2] secret

>WICHTIG
>
>Sie müssen die Autorisierung mithilfe Ihrer [!DNL LinkedIn] alle 365 Tage. Wenn Sie die Autorisierung nicht rechtzeitig vornehmen, wird Ihr Geheimnis nicht aktualisiert und die Variable [!DNL LinkedIn] Konvertierungsanfragen schlagen fehl.

Drei Monate vor dem Geheimnis, für das eine erneute Autorisierung erforderlich ist, wird ein Popup angezeigt, wenn Sie auf einer Seite der Eigenschaft navigieren. Auswählen **[!UICONTROL Klicken Sie hier, um zu Ihren Geheimnissen zu gelangen.]**.

![Die [!UICONTROL Eigenschaftenübersicht] -Tab, der das geheime Popup zur erneuten Autorisierung hervorhebt.](../../images/ui/event-forwarding/secrets/linkedin-reauthorization-popup.png)

Sie werden zum [!UICONTROL Geheimnisse] Registerkarte. Die auf dieser Seite aufgelisteten Geheimnisse werden gefiltert, um nur die Geheimnisse anzuzeigen, die erneut autorisiert werden müssen. Auswählen **[!UICONTROL Authentifizierungspflicht]** für das Geheimnis, das Sie neu autorisieren müssen.

![Die [!UICONTROL Geheimnis] Tabulatorhervorhebung [!UICONTROL Authentifizierungspflicht]für die [!DNL LinkedIn] geheim.](../../images/ui/event-forwarding/secrets/linkedin-reauthorization.png)

Es wird ein Dialogfeld angezeigt, in dem Sie zur Eingabe Ihrer [!DNL LinkedIn] Anmeldedaten. Befolgen Sie die Anweisungen, um Ihr Geheimnis erneut zu autorisieren.

## Geheime Daten bearbeiten

Nachdem Sie geheime Daten für eine Eigenschaft erstellt haben, finden Sie sie im Abschnitt **[!UICONTROL Geheime Daten]** im Arbeitsbereich. Um die Details von vorhandenen geheimen Daten zu bearbeiten, wählen Sie den Namen der jeweiligen geheimen Daten aus der Liste aus.

![Geheime Daten zur Bearbeitung auswählen](../../images/ui/event-forwarding/secrets/edit-secret.png)

Im nächsten Bildschirm können Sie den Namen und die Anmeldeinformationen für die jeweiligen geheimen Daten ändern.

![Geheime Daten bearbeiten](../../images/ui/event-forwarding/secrets/edit-secret-config.png)

>[!NOTE]
>
>Wenn geheime Daten mit einer vorhandenen Umgebung verknüpft sind, können Sie die jeweiligen geheimen Daten nicht einer anderen Umgebung zuweisen. Wenn Sie dieselben Anmeldeinformationen in einer anderen Umgebung verwenden möchten, müssen Sie stattdessen [neue geheime Daten erstellen](#create). Die einzige Möglichkeit, die Umgebung von diesem Bildschirm aus neu zuzuweisen, besteht darin, die jeweiligen geheimen Daten nie zuvor einer Umgebung zugewiesen zu haben bzw. die Umgebung zu löschen, der die jeweiligen geheimen Daten zugewiesen waren.

### Austausch von geheimen Daten erneut versuchen

Sie können einen Austausch von geheimen Daten über den Bearbeitungsbildschirm erneut versuchen oder aktualisieren. Dieser Vorgang hängt vom Typ der zu bearbeitenden geheimen Daten ab:

| Typ von geheimen Daten | Protokoll erneut versuchen |
| --- | --- |
| [!UICONTROL Token] | Wählen Sie die Option **[!UICONTROL Geheime Daten austauschen]** aus, um den Austausch der geheimen Daten erneut zu versuchen. Dieses Steuerelement ist nur verfügbar, wenn eine Umgebung mit den jeweiligen geheimen Daten verknüpft ist. |
| [!UICONTROL HTTP] | Wenn keine Umgebung mit den jeweiligen geheimen Daten verknüpft ist, wählen Sie die Option **[!UICONTROL Geheime Daten austauschen]** aus, um die Berechtigung in base64 auszutauschen. Wenn eine Umgebung angehängt ist, wählen Sie die Option **[!UICONTROL Geheimnis austauschen und bereitstellen]** aus, um zu Base64 zu wechseln und das Geheimnis bereitzustellen. |
| [!UICONTROL OAuth 2] | Wählen Sie **[!UICONTROL Token erstellen]** aus, um die Anmeldeinformationen auszutauschen und ein Zugriffs-Token vom Authentifizierungsanbieter zurückzugeben. |

## Löschen von geheimen Daten

Um vorhandene geheime Daten im Arbeitsbereich **[!UICONTROL Geheime Daten]** zu löschen, aktivieren Sie zunächst das Kontrollkästchen neben dem Namen der jeweiligen geheimen Daten und wählen Sie anschließend die Option **[!UICONTROL Löschen]** aus.

![Geheime Daten löschen](../../images/ui/event-forwarding/secrets/delete.png)

## Verwenden von geheimen Daten bei der Ereignisweiterleitung

Um bei der Ereignisweiterleitung geheime Daten zu verwenden, müssen Sie zunächst ein [Datenelement](../managing-resources/data-elements.md) erstellen, das die geheimen Daten an sich referenziert. Nach dem Speichern des Datenelements können Sie dieses in die [Regeln](../managing-resources/rules.md) zur Ereignisweiterleitung einbeziehen und diese Regeln zu einer [Bibliothek](../publishing/libraries.md) hinzufügen, die wiederum als [Build](../publishing/builds.md) für die Adobe-Server bereitgestellt werden kann.

Wählen Sie beim Erstellen des Datenelements die **[!UICONTROL Core]**-Erweiterung und anschließend für den Datenelementtyp die Option **[!UICONTROL Geheime Daten]** aus. Das rechte Bedienfeld aktualisiert sich und bietet Dropdown-Steuerelemente zum Zuweisen von bis zu drei geheimen Daten zum Datenelement, und zwar für [!UICONTROL Entwicklung], [!UICONTROL Staging] und [!UICONTROL Produktion].

![Datenelement](../../images/ui/event-forwarding/secrets/data-element.png)

>[!NOTE]
>
>In den jeweiligen Dropdown-Listen werden nur geheime Daten angezeigt, die mit der Entwicklungs-, Staging- bzw. Produktionsumgebung verknüpft sind.

Indem Sie einem einzelnen Datenelement mehrere geheime Daten zuweisen und es in eine Regel einschließen, kann sich der Wert des Datenelements ändern, je nachdem, wo sich die übergeordnete Bibliothek im [Veröffentlichungsfluss](../publishing/publishing-flow.md) befindet.

![Datenelement mit verschiedenen geheimen Daten](../../images/ui/event-forwarding/secrets/multi-secret-data-element.png)

>[!NOTE]
>
>Beim Erstellen des Datenelements muss eine Entwicklungsumgebung zugewiesen werden. Geheime Daten für die Staging- und Produktionsumgebungen sind nicht erforderlich, aber Builds, die versuchen, zu diesen Umgebungen zu wechseln, funktionieren nicht, wenn für ihre Datenelemente des Typs „Geheime Daten“ keine geheimen Daten für die betreffende Umgebung ausgewählt wurden.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Geheimnisse in der Benutzeroberfläche verwaltet werden. Informationen zur Interaktion mit geheimen Daten mithilfe der Reactor-API finden Sie im [Endpunktleitfaden für geheime Daten](../../api/endpoints/secrets.md).
