---
title: MailChimp-Erweiterung - Übersicht
description: Verwenden Sie die Ereignisweiterleitung an E-Mails von Trigger Mailchimp.
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
exl-id: a52870c4-10e6-45a0-a502-f48da3398f3f
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 6%

---

# Übersicht über die Mailchimp-Ereignisweiterleitungserweiterung

>[!NOTE]
>  
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=de).

Die Mailchimp-Erweiterung [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md) sendet Ereignisse an die Mailchimp Marketing-API, die E-Mails für Mailchimp-Marketingkampagnen, Journey-Trigger oder Transaktionen bereitstellen kann.

In diesem Dokument wird beschrieben, wie Sie die Erweiterung einrichten und Regeln mithilfe der Aktion Ereignis hinzufügen konfigurieren.

## Voraussetzungen

In diesem Dokument wird davon ausgegangen, dass Sie mit den relevanten Mailchimp-Produkten, die von der Erweiterung verwendet werden, vertraut sind. Weitere Informationen finden Sie in der Hilfedokumentation zu Mailchimp für [Kampagnen](https://mailchimp.com/help/getting-started-with-campaigns/), [Journey](https://mailchimp.com/help/about-customer-journeys/) und [Transaktionen](https://mailchimp.com/help/transactional/).

Für diese Erweiterung ist ein Mailchimp-Konto erforderlich. Sie können sich für ein Konto anmelden [hier](https://login.mailchimp.com/signup/). Notieren Sie sich im Dashboard des Mailchimp-Kontos die folgenden Werte für die Verwendung in diesem Handbuch:

- Ihr Mailchimp-Domain-Präfix
- Ihr API-Schlüssel
- Die Zielgruppen-ID
- Die standardmäßige „Von“-E-Mail-Adresse

Abhängig von Ihrem Mailchimp-Account-Plan haben Sie möglicherweise eingeschränkten Zugriff auf Mailchimp Customer Journey-Tools.

>[!TIP]
>  
>Wenn Sie Mailchimp-Automatisierungen wie Transaktions-E-Mails oder Kunden-Journeys verwenden, unterscheiden sich die Schritte und Bildschirme möglicherweise geringfügig von den hier aufgeführten. Sie benötigen jedoch dieselben Informationen, um diese Erweiterung wie oben beschrieben zu verwenden. Im [Mailchimp Help Center](https://mailchimp.com/help/) finden Sie Details zu den einzelnen Werten für Ihr spezifisches Konto und Ihren Plan.

### Domain-Präfix

Nach der Anmeldung bei Mailchimp und der Landung auf der Dashboard-Ansicht sollte die Adressleiste Ihres Browsers eine URL wie `https://us11.admin.mailchimp.com` oder nur `us11.admin.mailchimp.com` anzeigen. In diesem Beispiel ist das Präfix `us11` nur ein Platzhalter, und Ihr Wert unterscheidet sich. Notieren Sie sich Ihre URL mit Ihrem Präfix für einen späteren Schritt.

### API-Schlüssel

Um den API-Schlüssel für Ihr Konto zu finden, klicken Sie auf Ihr Profilsymbol in der Mailchimp-Benutzeroberfläche und wählen Sie dann **Profil**. Es sollte eine URL wie `https://us11.admin.mailchimp.com/account/profile/` mit dem Präfix **Ihr** anstelle von `us11` angezeigt werden.

Wählen Sie **Extras** und dann **API-Schlüssel**:

![Menü „Extras“, Link „API-Schlüssel“](../../../images/extensions/server/mailchimp/menu-API-keys.png)

Unter **Ihre API-Schlüssel** können Sie einen vorhandenen Schlüssel auswählen oder **Schlüssel erstellen** auswählen, um einen neuen zu erstellen. Sie können einen neuen Schlüssel erstellen, der speziell mit dieser Erweiterung verwendet werden soll. Kopieren Sie den API-Schlüssel und speichern Sie ihn für einen späteren Schritt. Weitere Informationen finden Sie in der Mailchimp-Dokumentation unter [Generieren Ihres API-Schlüssels](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

### Zielgruppen-ID und Absenderadresse

Wählen **Audience** im linken Navigationsbereich und dann **Audience-Dashboard** aus. Wählen Sie als Nächstes die Zielgruppe aus, die Sie mit dieser Erweiterung verwenden möchten. Weitere Informationen finden Sie im Mailchimp-Dokument unter [Erstellen einer Zielgruppe](https://mailchimp.com/help/create-audience/).

Nachdem Sie Ihre Audience erstellt und ausgewählt haben, wählen Sie das Dropdown-Menü **Zielgruppe verwalten** und wählen Sie **Einstellungen**. Auf diesem Bildschirm werden verschiedene Einstellungen für Ihre Zielgruppe angezeigt.

Unten im Bildschirm Einstellungen sollte `Unique id for audience [audience name]` angezeigt werden, wobei `[audience name]` der Name Ihrer tatsächlichen Audience ist. Kopieren Sie die Zielgruppen-ID und speichern Sie sie für einen späteren Schritt.

Wählen Sie **Zielgruppenname und Standardwerte** aus und bestätigen Sie, dass **Standardmäßige Absender-E-Mail** den richtigen Wert für Ihre Kampagnen hat. Beachten Sie, dass die Zielgruppen-ID ebenfalls oben auf dieser Seite aufgeführt ist und denselben Wert aufweist, den Sie im letzten Schritt nach unten kopiert haben.

## Mailchimp-Automatisierungen

Je nach Mailchimp-Plan und ob Sie Transaktions-E-Mails, Kunden-Journey oder andere Mailchimp-Automatisierungen verwenden, können Ihre spezifischen Journey-Einstellungen variieren.

>[!IMPORTANT]
>  
>Der Ereignisname, den Sie für den Trigger Ihrer Automatisierung oder Journey in Mailchimp ausgewählt haben, ist derselbe Ereignisname, den Sie mit dieser Erweiterung senden müssen. Notieren Sie sich den Ereignisnamen in Ihrer Mailchimp-Automatisierung und speichern Sie ihn für einen späteren Schritt.

## Installation und Konfiguration

In diesem Abschnitt werden die Schritte zur Installation und Konfiguration der Erweiterung aufgeführt. Um den Mailchimp-API-Schlüssel sicher zu speichern, müssen Sie die Ereignisweiterleitung ([) ](../../../ui/event-forwarding/secrets.md).

### Erstellen von geheimen Daten und Datenelementen

Erstellen Sie in einer Ereignisweiterleitungs-Eigenschaft [einen geheimen [!UICONTROL Token], ](../../../ui/event-forwarding/secrets.md#token). B. `Mailchimp API Key`.

Erstellen Sie [ein Datenelement](../../../ui/managing-resources/data-elements.md#create-a-data-element) mithilfe der [!UICONTROL Core]-Erweiterung und eines [!UICONTROL Secret] Datenelementtyps, um auf die soeben erstellten `Mailchimp API Key` zu verweisen. Geben Sie `Mailchimp Token` als Namen des Datenelements ein.

### Installieren und Konfigurieren der Erweiterung

Wählen Sie in derselben Ereignisweiterleitungs-Eigenschaft die Option **[!UICONTROL Extensions]** dann **[!UICONTROL Catalog]** aus, um die für die Installation verfügbaren Erweiterungen anzuzeigen. Suchen Sie von hier aus nach der Mailchimp-Erweiterung und wählen Sie **[!UICONTROL Install]** aus.

![Mailchimp-Erweiterung installieren](../../../images/extensions/server/mailchimp/install.png)

Der Konfigurationsbildschirm wird angezeigt. Geben Sie unter **[!UICONTROL Mailchimp Server Prefix Domain Name]** die Domain ein, die Sie zuvor aus Ihrem Mailchimp-Konto kopiert haben, einschließlich Ihres eindeutigen Domain-Präfixes.

>[!IMPORTANT]
>
>`http://` oder `https://` nicht in dieses Feld einschließen.

![Erweiterungskonfiguration](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

Klicken Sie unter **[!UICONTROL Mailchimp token]** auf das Symbol Datenelement und wählen Sie das `Mailchimp Token` Datenelement aus, das Sie zuvor erstellt haben. Wählen Sie **[!UICONTROL Save]** aus, um die Änderungen zu speichern.

Die Erweiterung ist jetzt installiert und für die Verwendung in Ihrer Eigenschaft konfiguriert.

## Datenerfassung

Bei Verwendung dieser Erweiterung in einer [Regel](../../../ui/managing-resources/rules.md) gibt es mehrere Datenwerte, die die Erweiterung mit jedem Ereignis an Mailchimp sendet. Für eine typische Implementierung können Sie die [Adobe Experience Platform Web SDK-Erweiterung](../../client/web-sdk/overview.md) so konfigurieren, dass diese Daten zur Verwendung durch die Erweiterung in der Ereignisweiterleitungs-Eigenschaft an [!DNL Experience Platform Edge Network] gesendet werden.

Die für diese Erweiterung erforderlichen Daten können von Web SDK entweder als XDM-Daten (unter Verwendung des [`xdm`](/help/collection/js/commands/sendevent/xdm.md)-Objekts) oder als Nicht-XDM-Daten (unter Verwendung des [`data`](/help/collection/js/commands/sendevent/data.md)-Objekts) gesendet werden.

Wenn ein Kunde beispielsweise einen Kauf tätigt oder sich für ein Ereignis auf Ihrer Website registriert, können Sie über Mailchimp mit dieser Erweiterung eine Bestätigungs-E-Mail senden. Nachdem Sie die erforderlichen Informationen von Web SDK an Edge Network gesendet haben, sendet die Erweiterung die E-Mail mit Mailchimp als Trigger.

![Konfiguration der Ereignisaktion hinzufügen](../../../images/extensions/server/mailchimp/action-configurations.png)

### Datenelemente

Der Screenshot im vorherigen Abschnitt zeigt die Daten, die Sie mit jedem Ereignis von dieser Erweiterung an Mailchimp senden können. Nachdem Sie Web SDK für das Senden dieser Daten an Edge Network konfiguriert haben, können Sie Datenelemente in der Ereignisweiterleitungseigenschaft erstellen, damit die Erweiterung auf diese Werte zugreifen kann.

Die nachstehende Tabelle enthält weitere Details zu jedem möglichen Wert.

| Name | Beispielpfad | Typ | Beschreibung | Erforderlich | Beschränkungen |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> oder<br /> `arc.event.data._tenant.emailId` | String | Die Adresse, die die E-Mail erhält | **Ja** | Muss in der Mailchimp-Zielgruppe vorhanden sein |
| `listId` | `arc.event.xdm._tenant.listId`<br /> oder<br /> `arc.event.data._tenant.listid` | String | Zielgruppen-ID | **Ja** | Muss mit einer vorhandenen Zielgruppen-ID übereinstimmen |
| `name` | `arc.event.xdm._tenant.name`<br /> oder<br /> `arc.event.data._tenant.name` | String | Der Ereignisname | **Ja** | 2-30 Zeichen lang |
| `properties` | `arc.event.xdm._tenant.properties`<br /> oder<br /> `arc.event.data._tenant.properties` | Objekt | Eine optionale Liste von Eigenschaften im JSON-Format mit Details zum Ereignis | Nein |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> oder<br /> `arc.event.data._tenant.isSyncing` | Boolescher Wert | Bei Ereignissen, die mit `is_syncing` festgelegt wurden`true` **werden** Trigger-Automatisierungen nicht unterstützt | Nein |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> oder `arc.event.data._tenant.occuredAt` | String | Ein ISO 8601-Zeitstempel, der angibt, wann das Ereignis aufgetreten ist | Nein |  |

{style="table-layout:auto"}

>[!IMPORTANT]
>  
>Die oben genannten **Beispielpfad**-Werte sind nur Beispiele. Die Feldnamen und [pfade](../../../ui/event-forwarding/overview.md#data-element-path) auf die in diesen Datenelementen verwiesen wird, können in Ihrer Eigenschaft unterschiedlich sein, je nachdem, wie Sie Web SDK in den obigen Schritten benannt und konfiguriert haben.

In der Ereignisweiterleitungs-Eigenschaft können Sie ein Datenelement für jedes der oben beschriebenen Felder erstellen. Nach der Erstellung können Sie in der [!UICONTROL Add Event] Aktion dieser Erweiterung auf die Datenelemente verweisen.

![Konfiguration der Ereignisaktion hinzufügen](../../../images/extensions/server/mailchimp/action-configurations.png)

Sie können jetzt diese Erweiterung und die Aktion Ereignis hinzufügen zu Trigger Mailchimp-E-Mails für Ihre Zielgruppen verwenden.

## Datenvalidierung

Beim Arbeiten mit Erweiterungen für die Ereignisweiterleitung ist die [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) sehr hilfreich. Im Abschnitt Protokolle unter Edge-Protokolle können Sie die Anfragen sehen, die von Ihren Ereignisweiterleitungsregeln nach deren Auslösung gestellt wurden. Die folgenden Screenshots zeigen, wie eine Anfrage an die Mailchimp-API von der Erweiterung gestellt wird.

![Adobe Experience Platform Debugger](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

Im Mailchimp-Dashboard wird in der Ansicht „Aktivitäts-Feed“ Ihrer Zielgruppe oder Ihres Zielgruppenmitglieds eine Liste der Ereignisse für diese Zielgruppe oder dieses Zielgruppenmitglied bereitgestellt. Diese sollte mit den von der Erweiterung gesendeten Ereignissen übereinstimmen und alle optionalen Daten anzeigen, die zusammen mit der E-Mail oder Kampagne gesendet wurden, die sie erhalten haben. Weitere Informationen finden Sie [Hilfeseiten zur Mailchimp](https://mailchimp.com/help/automation/)Automatisierung).
