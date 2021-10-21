---
title: Ereignis-Weiterleitung von Geheimnissen
description: Erfahren Sie, wie Sie in der Benutzeroberfläche der Datenerfassung Geheimnisse konfigurieren, um die Authentifizierung an Endpunkten durchzuführen, die in den Eigenschaften der Ereignis-Weiterleitung verwendet werden.
source-git-commit: 43d593cd8adf5a29c3283a328c24b0994009222b
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 1%

---

# Geheimnisse für die Weiterleitung von Ereignissen

In der Ereignis-Weiterleitung ist ein geheimer Schlüssel eine Ressource, die eine Authentifizierungsberechtigung für ein anderes System darstellt und den sicheren Datenaustausch ermöglicht. Geheimnisse können nur in Ereignis-Weiterleitungseigenschaften erstellt werden.

Es gibt derzeit drei unterstützte geheime Typen:

| Geheimer Typ | Beschreibung |
| --- | --- |
| [!UICONTROL Token] | Eine einzelne Zeichenfolge aus Zeichen, die einen Authentifizierungstoken-Wert darstellt, der von beiden Systemen bekannt und verstanden wird. |
| [!UICONTROL HTTP] | Enthält zwei Zeichenfolgenattribute für einen Benutzernamen und ein Kennwort. |
| [!UICONTROL OAuth2] | Enthält mehrere Attribute zur Unterstützung der [OAuth2](https://datatracker.ietf.org/doc/html/rfc6749) Authentifizierungsspezifikation. Das System fragt Sie nach den erforderlichen Informationen und behandelt dann die Erneuerung dieser Token für Sie in einem bestimmten Intervall. Zurzeit nur die [Client-Anmeldedaten](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.4) Version von OAuth2 wird unterstützt. |

{style=&quot;table-layout:auto&quot;}

Dieses Handbuch bietet einen Überblick über die Konfiguration von Geheimnissen für eine Ereignis-Weiterleitung ([!UICONTROL Kante])-Eigenschaft in der Data Collection-Benutzeroberfläche.

>[!NOTE]
>
>Ausführliche Anleitungen zum Verwalten von Geheimnissen in der Reaktor-API, einschließlich Beispiel JSON der Struktur eines geheimen Geheims, finden Sie im [Leitfaden zur Geheimnis-API](../../api/guides/secrets.md).

## Voraussetzungen

In diesem Handbuch wird davon ausgegangen, dass Sie bereits mit der Verwaltung von Ressourcen für Tags und die Weiterleitung von Ereignissen in der Data Collection-Benutzeroberfläche vertraut sind, einschließlich der Erstellung eines Datenelements und einer Ereignis-Weiterleitungsregel. Siehe Leitfaden zu [Ressourcen verwalten](../managing-resources/overview.md) wenn Sie eine Einführung benötigen.

Sie sollten auch einen Überblick über den Veröffentlichungsfluss für Tags und Ereignis-Weiterleitung haben, einschließlich wie Sie einer Bibliothek Ressourcen hinzufügen und einen Build für Tests auf Ihrer Website installieren können. Siehe [Veröffentlichungsübersicht](../publishing/overview.md) für weitere Details.

## Geheimnis erstellen {#create}

Melden Sie sich bei der Data Collection-Benutzeroberfläche an und öffnen Sie die Ereignis-Weiterleitungseigenschaft, unter der Sie das Geheimnis hinzufügen möchten, um ein Geheimnis zu erstellen. Als Nächstes wählen Sie **[!UICONTROL Geheimnisse]** in der linken Navigation, gefolgt von **[!UICONTROL Neues Geheimnis erstellen]**.

![Neues Geheimnis erstellen](../../images/ui/event-forwarding/secrets/create-new-secret.png)

Im nächsten Bildschirm können Sie die Details des geheimen Bereichs konfigurieren. Damit ein Geheimnis durch die Weiterleitung von Ereignissen verwendet werden kann, muss es einer vorhandenen Umgebung zugewiesen werden. Wenn Sie noch keine Umgebung für Ihre Ereignis-Weiterleitungseigenschaft erstellt haben, finden Sie weitere Informationen im Handbuch unter [Umgebung](../publishing/environments.md) für Anleitungen zur Konfiguration dieser Komponenten, bevor Sie fortfahren.

>[!NOTE]
>
>Wenn Sie das Geheimnis noch erstellen und speichern möchten, bevor Sie es einer Umgebung hinzufügen, deaktivieren Sie die **[!UICONTROL Geheimnis an Umgebung anhängen]** umschalten, bevor Sie den Rest der Informationen ausfüllen. Beachten Sie, dass Sie es später einer Umgebung zuweisen müssen, wenn Sie das Geheimnis verwenden möchten.
>
>![Umgebung deaktivieren](../../images/ui/event-forwarding/secrets/env-disabled.png)

Unter **[!UICONTROL Zielgruppe Umgebung]** verwenden, wählen Sie im Dropdown-Menü die Umgebung aus, der Sie das Geheimnis zuweisen möchten. Unter **[!UICONTROL Geheimer Name]**, geben Sie einen Namen für das Geheimnis im Kontext der Umgebung. Dieser Name muss in allen Geheimnissen unter der Eigenschaft &quot;Ereignis-Weiterleitung&quot;eindeutig sein.

![Umgebung und Name](../../images/ui/event-forwarding/secrets/env-and-name.png)

Ein Geheimnis kann immer nur einer Umgebung zugewiesen werden, Sie können jedoch auf Wunsch mehreren Geheimnissen auf verschiedenen Umgebung die gleichen Anmeldedaten zuweisen. Auswählen **[!UICONTROL hinzufügen Umgebung]** um der Liste eine weitere Zeile hinzuzufügen.

![hinzufügen Umgebung](../../images/ui/event-forwarding/secrets/add-env.png)

Sie müssen für jede hinzugefügte Umgebung einen anderen eindeutigen Namen für das zugehörige Geheimnis angeben. Wenn Sie alle verfügbaren Umgebung ausschöpfen, **[!UICONTROL hinzufügen Umgebung]** Schaltfläche ist nicht verfügbar.

![hinzufügen Umgebung nicht verfügbar](../../images/ui/event-forwarding/secrets/add-env-greyed.png)

Von hier aus unterscheiden sich die Schritte zum Erstellen des Geheimtitels je nach Art des Geheimtitels, den Sie erstellen. Einzelheiten finden Sie in den folgenden Unterabschnitten:

* [[!UICONTROL Token]](#token)
* [[!UICONTROL HTTP]](#http)
* [[!UICONTROL OAuth2]](#oauth2)

### [!UICONTROL Token] {#token}

Um ein Tokengeheimnis zu erstellen, wählen Sie **[!UICONTROL Token]** von **[!UICONTROL Typ]** herunterladen. In **[!UICONTROL Token]** -Feld, das angezeigt wird, geben Sie die Berechtigungszeichenfolge an, die von dem System erkannt wird, für das Sie sich authentifizieren. Auswählen **[!UICONTROL Geheimnis erstellen]** um das Geheimnis zu speichern.

![Token-Geheimnis](../../images/ui/event-forwarding/secrets/token-secret.png)

### [!UICONTROL HTTP] {#http}

Um ein HTTP-Geheimnis zu erstellen, wählen Sie **[!UICONTROL Einfaches HTTP]** von **[!UICONTROL Typ]** herunterladen. Geben Sie in den unten stehenden Feldern einen Benutzernamen und ein Kennwort für die Anmeldedaten ein, bevor Sie **[!UICONTROL Geheimnis erstellen]** um das Geheimnis zu speichern.

>[!NOTE]
>
>Beim Speichern werden die Anmeldedaten mit der [&quot;Basic&quot;-HTTP-Authentifizierungsschema](https://www.rfc-editor.org/rfc/rfc7617.html).

![HTTP-Geheimfrage](../../images/ui/event-forwarding/secrets/http-secret.png)

### [!UICONTROL OAuth2] {#oauth2}

Um ein OAuth2-Geheimnis zu erstellen, wählen Sie **[!UICONTROL OAuth2]** von **[!UICONTROL Typ]** herunterladen. Geben Sie in den unten stehenden Feldern Ihre [[!UICONTROL Client-ID] und [!UICONTROL Kundengeheimnis]](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/)sowie [Autorisierungs-URL](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) für Ihre OAuth-Integration. Die [!UICONTROL Autorisierungs-URL] -Feld in der Data Collection-Benutzeroberfläche ist eine Verkettung zwischen dem Autorisierungsserver-Host und dem Tokenpfad.

![OAuth2-Geheimnis](../../images/ui/event-forwarding/secrets/oauth-secret-1.png)

Unter **[!UICONTROL Berechtigungsoptionen]** können Sie andere Berechtigungsoptionen wie z. B. `scope` und `audience` in Form von Schlüsselwertpaaren. Um weitere Schlüsselwertpaare hinzuzufügen, wählen Sie **[!UICONTROL hinzufügen]**.

![Berechtigungsoptionen](../../images/ui/event-forwarding/secrets/oauth-secret-2.png)

Schließlich können Sie die **[!UICONTROL Versatz aktualisieren]** Wert für das Geheimnis. Dies gibt die Anzahl der Sekunden vor dem Token-Ablaufdatum an, das das System automatisch aktualisiert. Die entsprechende Zeit in Stunden und Minuten wird rechts neben dem Feld angezeigt und wird während der Eingabe automatisch aktualisiert.

![Versatz aktualisieren](../../images/ui/event-forwarding/secrets/oauth-secret-3.png)

Wenn der Aktualisierungsabstand beispielsweise auf den Standardwert von `14400` (vier Stunden) und das Zugriffstoken hat eine `expires_in` Wert von `86400` (24 Stunden), aktualisiert das System das Geheimnis automatisch in 20 Stunden.

>[!IMPORTANT]
>
>Ein OAuth-Geheimnis erfordert mindestens vier Stunden zwischen Aktualisierungen und muss außerdem mindestens acht Stunden gültig sein. Diese Beschränkung gibt Ihnen mindestens vier Stunden Zeit, um zu intervenieren, wenn Probleme mit dem generierten Token auftreten.
>
>Wenn der Offset beispielsweise auf `28800` (acht Stunden) und das Zugriffstoken hat eine `expires_in` von `36000` (10 Stunden), würde der Austausch aufgrund der sich daraus ergebenden Differenz von weniger als vier Stunden scheitern.

Wählen Sie nach Beendigung **[!UICONTROL Geheimnis erstellen]** um das Geheimnis zu speichern.

![OAuth2-Versatz speichern](../../images/ui/event-forwarding/secrets/oauth-secret-4.png)

## Geheimnis bearbeiten

Nachdem Sie die Geheimnisse für eine Eigenschaft erstellt haben, finden Sie sie in der **[!UICONTROL Geheimnisse]** Arbeitsbereich. Um die Details eines vorhandenen geheimen Bereichs zu bearbeiten, wählen Sie den Namen aus der Liste aus.

![Zu bearbeitendes Geheimnis auswählen](../../images/ui/event-forwarding/secrets/edit-secret.png)

Im nächsten Bildschirm können Sie den Namen und die Anmeldedaten für das Geheimnis ändern.

![Geheimnis bearbeiten](../../images/ui/event-forwarding/secrets/edit-secret-config.png)

>[!NOTE]
>
>Wenn das Geheimnis einer vorhandenen Umgebung zugeordnet ist, können Sie das Geheimnis keiner anderen Umgebung zuweisen. Wenn Sie dieselben Anmeldedaten auf einer anderen Umgebung verwenden möchten, müssen Sie [ein neues Geheimnis erstellen](#create) statt. Die einzige Möglichkeit, die Umgebung aus diesem Bildschirm neu zuzuweisen, besteht darin, dass Sie das Geheimnis niemals zuvor einer Umgebung zugewiesen haben oder die Umgebung gelöscht haben, an die das Geheimnis angehängt wurde.

### Geheimaustausch erneut versuchen

Sie können einen geheimen Austausch über den Bearbeitungsbildschirm erneut versuchen oder aktualisieren. Dieser Vorgang variiert je nach dem zu bearbeitenden geheimen Typ:

| Geheimer Typ | Protokoll wiederholen |
| --- | --- |
| [!UICONTROL Token] | Auswählen **[!UICONTROL Geheimnis austauschen]** um den geheimen Austausch erneut zu versuchen. Dieses Steuerelement ist nur verfügbar, wenn dem Geheimnis eine Umgebung zugeordnet ist. |
| [!UICONTROL HTTP] | Wenn dem Geheimnis keine Umgebung zugeordnet ist, wählen Sie **[!UICONTROL Geheimnis austauschen]** um die Anmeldedaten in base64 zu tauschen. Wenn eine Umgebung angehängt ist, wählen Sie **[!UICONTROL Geheimnis austauschen und bereitstellen]** um auf base64 zu tauschen und das Geheimnis in Cloudfare bereitzustellen. |
| [!UICONTROL OAuth2] | Auswählen **[!UICONTROL Token generieren]** , um die Anmeldedaten auszutauschen und ein Zugriffstoken vom Authentifizierungsanbieter zurückzugeben. |

## Geheimnis löschen

So löschen Sie ein bestehendes Geheimnis in  **[!UICONTROL Geheimnisse]** im Arbeitsbereich das Kontrollkästchen neben dem Namen auswählen, bevor Sie **[!UICONTROL Löschen]**.

![Geheimnis löschen](../../images/ui/event-forwarding/secrets/delete.png)

## Geheimnisse in der Weiterleitung von Ereignissen verwenden

Um ein Geheimnis bei der Weiterleitung von Ereignissen zu verwenden, müssen Sie zunächst eine [Datenelement](../managing-resources/data-elements.md) die auf das Geheimnis selbst verweist. Nach dem Speichern des Datenelements können Sie es in die Ereignis-Weiterleitung einschließen [Regeln](../managing-resources/rules.md) und fügen diese Regeln zu [Bibliothek](../publishing/libraries.md), die wiederum auf den Servern der Adobe als [build](../publishing/builds.md).

Wählen Sie beim Erstellen des Datenelements die **[!UICONTROL Core]** Erweiterung, und wählen Sie **[!UICONTROL Geheimnis]** für den Datenelementtyp. Das rechte Bedienfeld aktualisiert und bietet Dropdown-Steuerelemente, mit denen dem Datenelement bis zu drei Geheimnisse zugewiesen werden können: eins für [!UICONTROL Entwicklung], [!UICONTROL Staging]und [!UICONTROL Produktion] bzw.

![Datenelement](../../images/ui/event-forwarding/secrets/data-element.png)

>[!NOTE]
>
>Für die jeweiligen Dropdown-Listen werden nur die mit den Entwicklungs-, Staging- und Produktions-Umgebung verbundenen Geheimnisse angezeigt.

Wenn einem einzelnen Datenelement mehrere Geheimnisse zugewiesen werden und es eine Regel enthält, kann sich der Wert des Datenelements ändern, je nachdem, wo sich die entsprechende Bibliothek in der [Veröffentlichungsfluss](../publishing/publishing-flow.md).

![Datenelement mit mehreren Geheimnissen](../../images/ui/event-forwarding/secrets/multi-secret-data-element.png)

>[!NOTE]
>
>Beim Erstellen des Datenelements muss eine Development-Umgebung zugewiesen werden. Geheimnisse für die Staging- und Produktions-Umgebung sind nicht erforderlich, aber Builds, die versuchen, an diese Umgebung Transition, schlagen fehl, wenn für ihre geheimen Datenelemente kein Geheimnis für die betreffende Umgebung ausgewählt wurde.

## Nächste Schritte

Dieses Handbuch behandelt die Verwaltung von Geheimnissen in der Benutzeroberfläche der Datenerfassung. Informationen zur Interaktion mit Geheimnissen mithilfe der Reactor-API finden Sie im [Secrets-Endpunkt-Leitfaden](../../api/endpoints/secrets.md).
