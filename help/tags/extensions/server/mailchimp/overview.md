---
title: Übersicht über die Mailchimp-Erweiterung
description: Verwenden Sie die Ereignisweiterleitung zu Trigger Mailchimp-E-Mails.
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
exl-id: a52870c4-10e6-45a0-a502-f48da3398f3f
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 7%

---

# Übersicht über die Ereignisweiterleitungs-Erweiterung &quot;Mailchimp&quot;

>[!NOTE]
>  
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=de).

Der Mailchimp [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) sendet Ereignisse an die Mailchimp Marketing-API, die E-Mails für Mailchimp-Marketingkampagnen, Journey oder Transaktionen per Trigger verschicken kann.

In diesem Dokument wird beschrieben, wie Sie die Erweiterung einrichten und Regeln mithilfe der Aktion Ereignis hinzufügen konfigurieren.

## Voraussetzungen

In diesem Dokument wird davon ausgegangen, dass Sie mit den relevanten Mailchimp-Produkten vertraut sind, die von der -Erweiterung genutzt werden. Weitere Informationen finden Sie in der Mailchimp-Hilfedokumentation für [Kampagnen](https://mailchimp.com/help/getting-started-with-campaigns/), [Journey](https://mailchimp.com/help/about-customer-journeys/)und [Transaktionen](https://mailchimp.com/help/transactional/).

Für die Verwendung dieser Erweiterung ist ein Mailchimp-Konto erforderlich. Sie können sich für ein Konto anmelden [here](https://login.mailchimp.com/signup/). Notieren Sie sich im Dashboard des Mailchimp-Kontos die folgenden Werte, die in diesem Handbuch verwendet werden sollen:

- Ihr Mailchimp-Domänenpräfix
- Ihr API-Schlüssel
- Die Zielgruppen-ID
- Die standardmäßige E-Mail-Adresse &quot;from&quot;

Abhängig von Ihrem Mailchimp-Account-Plan haben Sie möglicherweise nur eingeschränkten Zugriff auf Mailchimp-Journey-Tools.

>[!TIP]
>  
>Wenn Sie Mailchimp-Automatisierungen wie Transaktions-E-Mails oder Journey verwenden, unterscheiden sich die Schritte und Bildschirme möglicherweise geringfügig von denen hier. Sie benötigen jedoch weiterhin dieselben Informationen, um diese Erweiterung wie oben beschrieben zu verwenden. Siehe [Hilfecenter für Mailchimp](https://mailchimp.com/help/) für Details zu jedem dieser Werte für Ihr spezifisches Konto und Ihren Plan.

### Domänenpräfix

Nach der Anmeldung bei Mailchimp und dem Landing in der Dashboard-Ansicht sollte die Adressleiste Ihres Browsers eine URL wie `https://us11.admin.mailchimp.com` oder `us11.admin.mailchimp.com`. In diesem Beispiel wird das Präfix `us11` ist nur ein Platzhalter und Ihr Wert wird anders sein. Zeichnen Sie Ihre URL mit Ihrem Präfix für einen späteren Schritt auf.

### API-Schlüssel

Um den API-Schlüssel für Ihr Konto zu finden, wählen Sie Ihr Profilsymbol in der Benutzeroberfläche von Mailchimp aus und klicken Sie dann auf **Profil**. Sie sollten eine URL wie `https://us11.admin.mailchimp.com/account/profile/` aber mit **Ihre** Präfix anstelle von `us11`.

Auswählen **Extras**, dann **API-Schlüssel**:

![Extras-Menü, API-Schlüssel-Link](../../../images/extensions/server/mailchimp/menu-API-keys.png)

under **Ihre API-Schlüssel** können Sie einen vorhandenen Schlüssel auswählen oder **Erstellen eines Schlüssels** , um eine neue zu erstellen. Sie können einen neuen Schlüssel erstellen, der speziell mit dieser Erweiterung verwendet werden soll. Kopieren Sie den API-Schlüssel und speichern Sie ihn für einen späteren Schritt. Weitere Informationen finden Sie in der Mailchimp-Dokumentation zum [API-Schlüssel generieren](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

### Zielgruppen-ID und Absenderadresse

Auswählen **Zielgruppe** in der linken Navigation und **Zielgruppen-Dashboard**. Wählen Sie anschließend die Zielgruppe aus, die Sie mit dieser Erweiterung verwenden möchten. Weitere Informationen finden Sie im Dokument Mailchimp unter [Erstellen einer Zielgruppe](https://mailchimp.com/help/create-audience/).

Wählen Sie bei der Erstellung und Auswahl der Audience die **Zielgruppe verwalten** Dropdown und wählen Sie **Einstellungen**. Auf diesem Bildschirm werden verschiedene Einstellungen für Ihre Zielgruppe angezeigt.

Am unteren Rand des Einstellungsbildschirms sollte Folgendes angezeigt werden: `Unique id for audience [audience name]` where `[audience name]` ist der Name Ihrer tatsächlichen Zielgruppe. Kopieren Sie die Zielgruppen-ID und speichern Sie sie für einen späteren Schritt.

Auswählen **Zielgruppenname und Standardwerte** und bestätigen Sie, dass **Standard von E-Mail-Adresse** hat den richtigen Wert für Ihre Kampagnen. Beachten Sie, dass die Zielgruppen-ID auch oben auf dieser Seite aufgeführt wird und der Wert ist, den Sie im letzten Schritt nach unten kopiert haben.

## Postimp-Automatisierung

Abhängig von Ihrem Mailchimp-Plan und der Verwendung von Transaktions-E-Mails, Journey oder anderen Mailchimp-Automatisierungen können Ihre spezifischen Journey-Einstellungen variieren.

>[!IMPORTANT]
>  
>Der Ereignisname, den Sie für den Trigger Ihrer Automatisierung oder Journey in Mailchimp ausgewählt haben, ist derselbe Ereignisname, den Sie mit dieser Erweiterung senden müssen. Notieren Sie den Ereignisnamen in Ihrer Mailchimp-Automatisierung und speichern Sie ihn für einen späteren Schritt.

## Installation und Konfiguration

In diesem Abschnitt werden die Schritte zum Installieren und Konfigurieren der Erweiterung aufgeführt. Um den Mailchimp-API-Schlüssel sicher zu speichern, müssen Sie die Ereignisweiterleitung verwenden [Geheimnisse](../../../ui/event-forwarding/secrets.md).

### Erstellen eines geheimen und Datenelements

In einer Ereignisweiterleitungseigenschaft [Erstellen Sie eine [!UICONTROL Token] secret](../../../ui/event-forwarding/secrets.md#token) aufgerufen `Mailchimp API Key`.

Als Nächstes [Datenelement erstellen](../../../ui/managing-resources/data-elements.md#create-a-data-element) mithilfe der [!UICONTROL Core] Erweiterung und [!UICONTROL Geheimnis] Datenelementtyp zum Referenzieren der `Mailchimp API Key` geheim, das Sie gerade erstellt haben. Eingabe `Mailchimp Token` als Datenelementname.

### Installieren und Konfigurieren der Erweiterung

Wählen Sie in derselben Ereignisweiterleitungseigenschaft die Option **[!UICONTROL Erweiterungen],** then **[!UICONTROL Katalog]** , um die für die Installation verfügbaren Erweiterungen anzuzeigen. Suchen Sie von hier aus nach der Mailchimp-Erweiterung und wählen Sie **[!UICONTROL Installieren]**.

![Installieren der Mailchimp-Erweiterung](../../../images/extensions/server/mailchimp/install.png)

Der Konfigurationsbildschirm wird angezeigt. under **[!UICONTROL Mailchimp Server Prefix Domain Name]** Geben Sie die Domäne ein, die Sie zuvor aus Ihrem Mailchimp-Konto kopiert haben, einschließlich Ihres eindeutigen Domänenpräfixes.

>[!IMPORTANT]
>
>Nicht einschließen `http://` oder `https://` in dieses Feld ein.

![Erweiterungskonfiguration](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

under **[!UICONTROL Mailchimp-Token]**, wählen Sie das Datenelementsymbol aus und wählen Sie die `Mailchimp Token` -Datenelement, das Sie zuvor erstellt haben. Auswählen **[!UICONTROL Speichern]** , um die Änderungen zu speichern.

Die Erweiterung wird jetzt installiert und für die Verwendung in Ihrer Eigenschaft konfiguriert.

## Datenerfassung

Wenn Sie diese Erweiterung in einer [Regel](../../../ui/managing-resources/rules.md), gibt es mehrere Datenwerte, die die Erweiterung mit jedem Ereignis an Mailchimp sendet. Für eine typische Implementierung können Sie die [Adobe Experience Platform Web SDK-Erweiterung](../../client/sdk/overview.md) senden Sie diese Daten an [!DNL Platform Edge Network] für die Verwendung durch die Erweiterung in der Ereignisweiterleitungseigenschaft.

Die für diese Erweiterung erforderlichen Daten können vom Web SDK entweder als XDM-Daten oder als Nicht-XDM-Daten gesendet werden. Weitere Informationen finden Sie in der Dokumentation . [Senden von XDM-Daten](../../../../edge/fundamentals/tracking-events.md#sending-non-xdm-data).

Wenn beispielsweise ein Kunde einen Kauf tätigt oder sich für ein Ereignis auf Ihrer Site registriert, können Sie eine Bestätigungs-E-Mail über Mailchimp mit dieser Erweiterung senden. Nachdem Sie die erforderlichen Informationen vom Web SDK an das Edge-Netzwerk gesendet haben, wird die E-Mail von der Erweiterung mit Mailchimp Trigger.

![Konfiguration der Ereignisaktion hinzufügen](../../../images/extensions/server/mailchimp/action-configurations.png)

### Datenelemente

Der Screenshot im vorherigen Abschnitt zeigt die Daten, die Sie mit jedem Ereignis von dieser Erweiterung an Mailchimp senden können. Nachdem Sie das Web SDK so konfiguriert haben, dass diese Daten an das Edge-Netzwerk gesendet werden, können Sie Datenelemente in der Ereignisweiterleitungseigenschaft erstellen, damit die Erweiterung auf diese Werte zugreifen kann.

Die nachstehende Tabelle enthält weitere Details zu den einzelnen Werten.

| Name | Beispielpfad | Typ | Beschreibung | Erforderlich | Beschränkungen |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> oder<br /> `arc.event.data._tenant.emailId` | Zeichenfolge | Die E-Mail-Adresse | **Ja** | Muss in der Mailchimp-Zielgruppe vorhanden sein |
| `listId` | `arc.event.xdm._tenant.listId`<br /> oder<br /> `arc.event.data._tenant.listid` | Zeichenfolge | Zielgruppen-ID | **Ja** | Muss mit einer vorhandenen Zielgruppen-ID übereinstimmen |
| `name` | `arc.event.xdm._tenant.name`<br /> oder<br /> `arc.event.data._tenant.name` | Zeichenfolge | Der Ereignisname | **Ja** | Länge von 2-30 Zeichen |
| `properties` | `arc.event.xdm._tenant.properties`<br /> oder<br /> `arc.event.data._tenant.properties` | Objekt | Eine optionale Liste der Eigenschaften im JSON-Format mit Details zum Ereignis | Nein |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> oder<br /> `arc.event.data._tenant.isSyncing` | boolean | Mit `is_syncing` auf `true` **nicht** Automatisierung von Triggern | Nein |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> oder `arc.event.data._tenant.occuredAt` | Zeichenfolge | Ein ISO 8601-Zeitstempel zum Zeitpunkt des Ereignisses | Nein |  |

{style=&quot;table-layout:auto&quot;}

>[!IMPORTANT]
>  
>Die **Beispielpfad** -Werte sind nur Beispiele. Die Feldnamen und [Pfade](../../../ui/event-forwarding/overview.md#data-element-path) auf die in diesen Datenelementen verwiesen wird, kann in Ihrer Eigenschaft unterschiedlich sein, je nachdem, wie Sie das Web SDK in den oben genannten Schritten benannt und konfiguriert haben.

In Ihrer Ereignisweiterleitungseigenschaft können Sie für jedes der oben genannten Felder ein Datenelement erstellen. Nach der Erstellung können Sie die Datenelemente im [!UICONTROL Ereignis hinzufügen] Aktion dieser Erweiterung.

![Konfiguration der Ereignisaktion hinzufügen](../../../images/extensions/server/mailchimp/action-configurations.png)

Sie können diese Erweiterung und die Aktion Ereignis hinzufügen für E-Mails von Trigger Mailchimp für Ihre Zielgruppen verwenden.

## Datenvalidierung

Wenn Sie mit Erweiterungen für die Ereignisweiterleitung arbeiten, wird die [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) ist sehr nützlich. Im Abschnitt Protokolle unter Edge-Protokolle können Sie die Anforderungen sehen, die von Ihren Ereignisweiterleitungsregeln gestellt wurden, nachdem sie ausgelöst wurden. Die folgenden Screenshots zeigen, wie eine Anfrage von der Erweiterung an die Mailchimp-API gesendet wird.

![Adobe Experience Platform Debugger](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

Im Dashboard &quot;Mailchimp&quot;in der Ansicht &quot;Aktivitäts-Feed&quot;Ihrer Audience oder Audience-Mitglieder wird eine Liste der Ereignisse für diese Audience oder dieses Audience-Mitglied bereitgestellt. Dies sollte mit den von der Erweiterung gesendeten Ereignissen übereinstimmen und die gesendeten optionalen Daten zusammen mit der E-Mail oder Kampagne anzeigen, die sie erhalten haben. Siehe [Hilfeleitlinien zur Postimpfautomatisierung](https://mailchimp.com/help/automation/) für weitere Details.
