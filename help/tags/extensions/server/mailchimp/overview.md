---
title: Übersicht über die Mailchimp-Erweiterung
description: Verwenden Sie die Ereignisweiterleitung zu Trigger Mailchimp-E-Mails.
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
exl-id: a52870c4-10e6-45a0-a502-f48da3398f3f
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 6%

---

# Übersicht über die Ereignisweiterleitungs-Erweiterung &quot;Mailchimp&quot;

>[!NOTE]
>  
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=de).

Die Erweiterung &quot;Mailchimp [event forward](../../../ui/event-forwarding/overview.md)&quot;sendet Ereignisse an die Mailchimp Marketing-API, die E-Mails für Mailchimp-Marketingkampagnen, Journey oder Transaktionen Trigger.

In diesem Dokument wird beschrieben, wie Sie die Erweiterung einrichten und Regeln mithilfe der Aktion Ereignis hinzufügen konfigurieren.

## Voraussetzungen

In diesem Dokument wird davon ausgegangen, dass Sie mit den relevanten Mailchimp-Produkten vertraut sind, die von der -Erweiterung genutzt werden. Weitere Informationen finden Sie in der Hilfedokumentation zu Mailchimp für [campaigns](https://mailchimp.com/help/getting-started-with-campaigns/), [Journey](https://mailchimp.com/help/about-customer-journeys/) und [transaktionen](https://mailchimp.com/help/transactional/).

Für die Verwendung dieser Erweiterung ist ein Mailchimp-Konto erforderlich. Sie können sich für ein Konto [hier](https://login.mailchimp.com/signup/) anmelden. Notieren Sie sich im Dashboard des Mailchimp-Kontos die folgenden Werte, die in diesem Handbuch verwendet werden sollen:

- Ihr Mailchimp-Domänenpräfix
- Ihr API-Schlüssel
- Die Zielgruppen-ID
- Die standardmäßige E-Mail-Adresse &quot;from&quot;

Abhängig von Ihrem Mailchimp-Account-Plan haben Sie möglicherweise nur eingeschränkten Zugriff auf Mailchimp-Journey-Tools.

>[!TIP]
>  
>Wenn Sie Mailchimp-Automatisierungen wie Transaktions-E-Mails oder Journey verwenden, unterscheiden sich die Schritte und Bildschirme möglicherweise geringfügig von denen hier. Sie benötigen jedoch weiterhin dieselben Informationen, um diese Erweiterung wie oben beschrieben zu verwenden. Weitere Informationen zu den einzelnen Werten für Ihr bestimmtes Konto und Ihren Plan finden Sie im [Mailchimp Help Center](https://mailchimp.com/help/) .

### Domänenpräfix

Nach der Anmeldung bei Mailchimp und dem Landing in der Dashboard-Ansicht sollte die Adressleiste Ihres Browsers eine URL wie `https://us11.admin.mailchimp.com` oder nur `us11.admin.mailchimp.com` anzeigen. In diesem Beispiel ist das Präfix `us11` nur ein Platzhalter und Ihr Wert unterscheidet sich. Zeichnen Sie Ihre URL mit Ihrem Präfix für einen späteren Schritt auf.

### API-Schlüssel

Um den API-Schlüssel für Ihr Konto zu finden, wählen Sie Ihr Profilsymbol in der Benutzeroberfläche von Mailchimp und dann **Profil** aus. Sie sollten eine URL wie `https://us11.admin.mailchimp.com/account/profile/` sehen, aber mit dem Präfix **Ihr** anstelle von `us11`.

Wählen Sie **Extras** und dann **API-Schlüssel** aus:

![Menü &quot;Extras&quot;, Link mit API-Schlüsseln](../../../images/extensions/server/mailchimp/menu-API-keys.png)

Unter **Ihre API-Schlüssel** können Sie einen vorhandenen Schlüssel auswählen oder Sie können **Einen Schlüssel erstellen** auswählen, um einen neuen zu erstellen. Sie können einen neuen Schlüssel erstellen, der speziell mit dieser Erweiterung verwendet werden soll. Kopieren Sie den API-Schlüssel und speichern Sie ihn für einen späteren Schritt. Weitere Informationen finden Sie in der Mailchimp-Dokumentation zum [Generieren Ihres API-Schlüssels](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

### Zielgruppen-ID und Absenderadresse

Wählen Sie im linken Navigationsbereich **Zielgruppe** und dann **Zielgruppen-Dashboard** aus. Wählen Sie anschließend die Zielgruppe aus, die Sie mit dieser Erweiterung verwenden möchten. Weitere Informationen finden Sie im Dokument Mailchimp unter [Erstellen einer Audience](https://mailchimp.com/help/create-audience/) .

Wählen Sie bei erstellter und ausgewählter Zielgruppe das Dropdown-Menü **Zielgruppe verwalten** und danach **Einstellungen** aus. Auf diesem Bildschirm werden verschiedene Einstellungen für Ihre Zielgruppe angezeigt.

Am unteren Rand des Einstellungsbildschirms sollte `Unique id for audience [audience name]` angezeigt werden, wobei `[audience name]` der Name der tatsächlichen Zielgruppe ist. Kopieren Sie die Zielgruppen-ID und speichern Sie sie für einen späteren Schritt.

Wählen Sie **Zielgruppenname und Standardeinstellung** und bestätigen Sie, dass **Standardeinstellung von E-Mail-Adresse** den richtigen Wert für Ihre Kampagnen aufweist. Beachten Sie, dass die Zielgruppen-ID auch oben auf dieser Seite aufgeführt wird und der Wert ist, den Sie im letzten Schritt nach unten kopiert haben.

## Postimp-Automatisierung

Abhängig von Ihrem Mailchimp-Plan und der Verwendung von Transaktions-E-Mails, Journey oder anderen Mailchimp-Automatisierungen können Ihre spezifischen Journey-Einstellungen variieren.

>[!IMPORTANT]
>  
>Der Ereignisname, den Sie für den Trigger Ihrer Automatisierung oder Journey in Mailchimp ausgewählt haben, ist derselbe Ereignisname, den Sie mit dieser Erweiterung senden müssen. Notieren Sie den Ereignisnamen in Ihrer Mailchimp-Automatisierung und speichern Sie ihn für einen späteren Schritt.

## Installation und Konfiguration

In diesem Abschnitt werden die Schritte zum Installieren und Konfigurieren der Erweiterung aufgeführt. Um den Mailchimp-API-Schlüssel sicher zu speichern, müssen Sie die Ereignisweiterleitung [geheimnisse](../../../ui/event-forwarding/secrets.md) verwenden.

### Erstellen eines geheimen und Datenelements

Erstellen Sie in einer Ereignisweiterleitungseigenschaft [einen [!UICONTROL Token] secret](../../../ui/event-forwarding/secrets.md#token) mit dem Namen `Mailchimp API Key`.

Als Nächstes erstellen Sie mit der Erweiterung [!UICONTROL Core] ein Datenelement](../../../ui/managing-resources/data-elements.md#create-a-data-element) und mit dem Datenelementtyp [!UICONTROL Secret] , um auf das soeben erstellte Geheimnis `Mailchimp API Key` zu verweisen. [ Geben Sie `Mailchimp Token` als Datenelementnamen ein.

### Installieren und Konfigurieren der Erweiterung

Wählen Sie in derselben Ereignisweiterleitungseigenschaft **[!UICONTROL Erweiterungen],** und dann **[!UICONTROL Katalog]** aus, um die für die Installation verfügbaren Erweiterungen anzuzeigen. Suchen Sie von hier aus nach der Mailchimp-Erweiterung und wählen Sie **[!UICONTROL Installieren]**.

![Installieren der Mailchimp-Erweiterung](../../../images/extensions/server/mailchimp/install.png)

Der Konfigurationsbildschirm wird angezeigt. Geben Sie unter **[!UICONTROL Mailchimp Server Prefix Domain Name]** die Domäne ein, die Sie zuvor aus Ihrem Mailchimp-Konto kopiert haben, einschließlich des eindeutigen Domänenpräfixes.

>[!IMPORTANT]
>
>Schließen Sie in dieses Feld nicht `http://` oder `https://` ein.

![Erweiterungskonfiguration](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

Wählen Sie unter **[!UICONTROL Mailchimp-Token]** das Datenelementsymbol und danach das zuvor erstellte Datenelement `Mailchimp Token` aus. Wählen Sie **[!UICONTROL Speichern]** aus, um die Änderungen zu speichern.

Die Erweiterung wird jetzt installiert und für die Verwendung in Ihrer Eigenschaft konfiguriert.

## Datenerfassung

Bei Verwendung dieser Erweiterung in einer [Regel](../../../ui/managing-resources/rules.md) gibt es mehrere Datenwerte, die die Erweiterung mit jedem Ereignis an Mailchimp sendet. Bei einer typischen Implementierung können Sie die [Adobe Experience Platform Web SDK-Erweiterung](../../client/web-sdk/overview.md) so konfigurieren, dass diese Daten an [!DNL Platform Edge Network] gesendet werden, damit sie von der Erweiterung in der Ereignisweiterleitungseigenschaft verwendet werden können.

Die für diese Erweiterung erforderlichen Daten können vom Web SDK entweder als XDM-Daten (mit dem [`xdm`](/help/web-sdk/commands/sendevent/xdm.md) -Objekt) oder als Nicht-XDM-Daten (mit dem [`data`](/help/web-sdk/commands/sendevent/data.md) -Objekt) gesendet werden.

Wenn beispielsweise ein Kunde einen Kauf tätigt oder sich für ein Ereignis auf Ihrer Site registriert, können Sie eine Bestätigungs-E-Mail über Mailchimp mit dieser Erweiterung senden. Nachdem Sie die erforderlichen Informationen vom Web SDK an das Edge Network gesendet haben, wird die E-Mail von der Erweiterung mit Mailchimp Trigger.

![Konfiguration der Ereignisaktion hinzufügen](../../../images/extensions/server/mailchimp/action-configurations.png)

### Datenelemente

Der Screenshot im vorherigen Abschnitt zeigt die Daten, die Sie mit jedem Ereignis von dieser Erweiterung an Mailchimp senden können. Nachdem Sie das Web SDK für das Senden dieser Daten an das Edge Network konfiguriert haben, können Sie Datenelemente in der Ereignisweiterleitungseigenschaft erstellen, damit die Erweiterung auf diese Werte zugreifen kann.

Die nachstehende Tabelle enthält für jeden möglichen Wert detailliertere Informationen.

| Name | Beispielpfad | Typ | Beschreibung | Erforderlich | Beschränkungen |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> oder <br /> `arc.event.data._tenant.emailId` | Zeichenfolge | Die E-Mail-Adresse | **Ja** | Muss in der Mailchimp-Zielgruppe vorhanden sein |
| `listId` | `arc.event.xdm._tenant.listId`<br /> oder <br /> `arc.event.data._tenant.listid` | Zeichenfolge | Zielgruppen-ID | **Ja** | Muss mit einer vorhandenen Zielgruppen-ID übereinstimmen |
| `name` | `arc.event.xdm._tenant.name`<br /> oder <br /> `arc.event.data._tenant.name` | Zeichenfolge | Der Ereignisname | **Ja** | Länge von 2-30 Zeichen |
| `properties` | `arc.event.xdm._tenant.properties`<br /> oder <br /> `arc.event.data._tenant.properties` | Objekt | Eine optionale Liste der Eigenschaften im JSON-Format mit Details zum Ereignis | Nein |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> oder <br /> `arc.event.data._tenant.isSyncing` | Boolescher Wert | Mit `is_syncing` erstellte Ereignisse, die auf `true` **eingestellt sind, führen nicht zu Trigger-Automatisierungen** | Nein |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> oder `arc.event.data._tenant.occuredAt` | Zeichenfolge | Ein ISO 8601-Zeitstempel zum Zeitpunkt des Ereignisses | Nein |  |

{style="table-layout:auto"}

>[!IMPORTANT]
>  
>Die obigen Werte für den **Beispielpfad** sind nur Beispiele. Die in diesen Datenelementen referenzierten Feldnamen und [Pfade](../../../ui/event-forwarding/overview.md#data-element-path) können in Ihrer Eigenschaft unterschiedlich sein, je nachdem, wie Sie das Web SDK in den oben stehenden Schritten benannt und konfiguriert haben.

In Ihrer Ereignisweiterleitungseigenschaft können Sie für jedes der oben genannten Felder ein Datenelement erstellen. Nach der Erstellung können Sie auf die Datenelemente in der Aktion [!UICONTROL Ereignis hinzufügen] dieser Erweiterung verweisen.

![Konfiguration der Ereignisaktion hinzufügen](../../../images/extensions/server/mailchimp/action-configurations.png)

Sie können diese Erweiterung und die Aktion Ereignis hinzufügen für E-Mails von Trigger Mailchimp für Ihre Zielgruppen verwenden.

## Datenvalidierung

Wenn Sie mit Ereignisweiterleitungs-Erweiterungen arbeiten, ist der [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) sehr nützlich. Im Abschnitt Protokolle unter Edge-Protokolle können Sie die Anfragen sehen, die von Ihren Ereignisweiterleitungsregeln gestellt wurden, nachdem sie ausgelöst wurden. Die folgenden Screenshots zeigen, wie eine Anfrage von der Erweiterung an die Mailchimp-API gesendet wird.

![Adobe Experience Platform Debugger](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

Im Dashboard &quot;Mailchimp&quot;in der Ansicht &quot;Aktivitäts-Feed&quot;Ihrer Audience oder Audience-Mitglieder wird eine Liste der Ereignisse für diese Audience oder dieses Audience-Mitglied bereitgestellt. Dies sollte mit den von der Erweiterung gesendeten Ereignissen übereinstimmen und die gesendeten optionalen Daten zusammen mit der E-Mail oder Kampagne anzeigen, die sie erhalten haben. Weitere Informationen finden Sie in den Hilfshandbüchern [Mailchimp Automation](https://mailchimp.com/help/automation/) .
