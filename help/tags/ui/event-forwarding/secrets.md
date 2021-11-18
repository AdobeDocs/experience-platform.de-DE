---
title: Geheime Daten für die Ereignisweiterleitung
description: Erfahren Sie, wie Sie geheime Daten in der Datenerfassungs-Benutzeroberfläche konfigurieren, um sich bei Endpunkten zu authentifizieren, die in den Eigenschaften der Ereignisweiterleitung verwendet werden.
source-git-commit: 43d593cd8adf5a29c3283a328c24b0994009222b
workflow-type: ht
source-wordcount: '1445'
ht-degree: 100%

---

# Geheime Daten für die Ereignisweiterleitung

Bei der Ereignisweiterleitung sind geheime Daten eine Ressource, die eine Authentifizierungsberechtigung für ein anderes System darstellt und den sicheren Datenaustausch ermöglicht. Geheime Daten können nur in den Eigenschaften der Ereignisweiterleitung erstellt werden.

Derzeit werden drei Typen von geheimen Daten unterstützt:

| Typ von geheimen Daten | Beschreibung |
| --- | --- |
| [!UICONTROL Token] | Eine einzelne Zeichenfolge, die den Wert eines Authentifizierungs-Tokens darstellt, der von beiden Systemen verstanden wird. |
| [!UICONTROL HTTP] | Enthält zwei Zeichenfolgen-Attribute für einen Benutzernamen und ein Kennwort. |
| [!UICONTROL OAuth2] | Enthält mehrere Attribute zur Unterstützung der [OAuth2](https://datatracker.ietf.org/doc/html/rfc6749)-Authentifizierungsspezifikation. Das System fordert von Ihnen die erforderlichen Informationen an. Anschließend übernimmt es die Verlängerung dieser Token für Sie in einem bestimmten Intervall. Derzeit wird nur die OAuth2-Version mit [Client-Anmeldedaten](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.4) unterstützt. |

{style=&quot;table-layout:auto&quot;}

Dieses Handbuch bietet einen allgemeinen Überblick darüber, wie geheime Daten für eine [!UICONTROL Edge]-Eigenschaft zur Ereignisweiterleitung in der Datenerfassungs-Benutzeroberfläche konfiguriert werden.

>[!NOTE]
>
>Ausführliche Anleitungen zum Verwalten von geheimen Daten in der Reactor-API, einschließlich einer Beispiel-JSON zur Struktur der geheimen Daten, finden Sie im [API-Handbuch für geheime Daten](../../api/guides/secrets.md).

## Voraussetzungen

In diesem Handbuch wird davon ausgegangen, dass Sie bereits mit der Verwaltung von Ressourcen für Tags und mit der Ereignisweiterleitung in der Datenerfassungs-Benutzeroberfläche vertraut sind, einschließlich der Erstellung eines Datenelements und einer Ereignisweiterleitungsregel. Wenn Sie eine Einführung benötigen, finden Sie weitere Informationen im Handbuch unter [Verwalten von Ressourcen](../managing-resources/overview.md).

Außerdem sollten Sie über ein grundlegendes Verständnis des Veröffentlichungsflusses im Hinblick auf Tags und Ereignisweiterleitung verfügen, einschließlich der Möglichkeit, Ressourcen zu einer Bibliothek hinzuzufügen und einen Build zum Testen auf Ihrer Website zu installieren. Weitere Informationen finden Sie in der [Publishing-Übersicht](../publishing/overview.md).

## Erstellen geheimer Daten {#create}

Um geheime Daten zu erstellen, melden Sie sich bei der Datenerfassungs-Benutzeroberfläche an und öffnen Sie die Ereignisweiterleitungseigenschaft, unter der Sie die geheimen Daten hinzufügen möchten. Wählen Sie anschließend im linken Navigationsbereich zunächst **[!UICONTROL Geheime Daten]** und dann **[!UICONTROL Neue geheime Daten erstellen]** aus.

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
* [[!UICONTROL OAuth2]](#oauth2)

### [!UICONTROL Token] {#token}

Um geheime Daten vom Typ „Token“ zu erstellen, wählen Sie in der Dropdown-Liste **[!UICONTROL Typ]** die Option **[!UICONTROL Token]** aus. Geben Sie im nun erscheinenden Feld **[!UICONTROL Token]** die Zeichenfolge zur Anmeldung an, die vom System erkannt wird, für das Sie sich authentifizieren. Wählen Sie **[!UICONTROL Geheime Daten erstellen]** aus, um die geheimen Daten zu speichern.

![Geheime Daten vom Typ „Token“](../../images/ui/event-forwarding/secrets/token-secret.png)

### [!UICONTROL HTTP] {#http}

Um geheime Daten vom Typ „HTTP“ zu erstellen, wählen Sie in der Dropdown-Liste **[!UICONTROL Typ]** die Option **[!UICONTROL Einfaches HTTP]** aus. Geben Sie in den unten angezeigten Feldern einen Benutzernamen und ein Kennwort zur Anmeldung ein, bevor Sie die Option **[!UICONTROL Geheime Daten erstellen]** auswählen, um die jeweiligen geheimen Daten zu speichern.

>[!NOTE]
>
>Nach dem Speichern werden die Anmeldedaten mit dem [Grundlegenden HTTP-Authentifizierungsschema](https://www.rfc-editor.org/rfc/rfc7617.html) verschlüsselt.

![Geheime Daten vom Typ „HTTP“](../../images/ui/event-forwarding/secrets/http-secret.png)

### [!UICONTROL OAuth2] {#oauth2}

Um geheime Daten vom Typ „OAuth2“ zu erstellen, wählen Sie aus der Dropdown-Liste **[!UICONTROL Typ]** die Option **[!UICONTROL OAuth2]** aus. Geben Sie in den unten angezeigten Feldern Ihre [[!UICONTROL Client-ID] und [!UICONTROL Ihre geheimen Client-Daten]](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/) sowie die [Autorisierungs-URL](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) für Ihre OAuth-Integration ein. Das Feld [!UICONTROL Autorisierungs-URL] in der Datenerfassungs-Benutzeroberfläche ist eine Verkettung zwischen dem Autorisierungs-Server-Host und dem Token-Pfad.

![Geheime Daten vom Typ „OAuth2“](../../images/ui/event-forwarding/secrets/oauth-secret-1.png)

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

![OAuth2-Versatz speichern](../../images/ui/event-forwarding/secrets/oauth-secret-4.png)

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
| [!UICONTROL HTTP] | Wenn keine Umgebung mit den jeweiligen geheimen Daten verknüpft ist, wählen Sie die Option **[!UICONTROL Geheime Daten austauschen]** aus, um die Berechtigung in base64 auszutauschen. Wenn eine Umgebung angehängt ist, wählen Sie die Option **[!UICONTROL Geheime Daten austauschen und bereitstellen]** aus, um auf base64 auszutauschen und die geheimen Daten für Cloudfare bereitzustellen. |
| [!UICONTROL OAuth2] | Wählen Sie **[!UICONTROL Token erstellen]** aus, um die Anmeldeinformationen auszutauschen und ein Zugriffs-Token vom Authentifizierungsanbieter zurückzugeben. |

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

In diesem Handbuch wurde beschrieben, wie geheime Daten in der Datenerfassungs-Benutzeroberfläche verwaltet werden. Informationen zur Interaktion mit geheimen Daten mithilfe der Reactor-API finden Sie im [Endpunktleitfaden für geheime Daten](../../api/endpoints/secrets.md).
