---
title: Google Ads Enhanced Conversions-Erweiterung
description: Erfahren Sie mehr über die Google Ads Enhanced Conversions-Erweiterung für die Ereignisweiterleitung in Adobe Experience Platform.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 1%

---

# [!DNL Google Ads] Erweiterte Erweiterung &quot;Conversions&quot;

Verwenden der [!DNL Google Ads] API, können Sie [erweiterte Konvertierungen](https://support.google.com/google-ads/answer/9888656) durch Übermittlung von Erstanbieter-Kundendaten in Form von Konversionsanpassungen. Google verwendet diese zusätzlichen Daten, um die Berichterstellung für Ihre Online-Konversionen zu verbessern, die durch Anzeigeninteraktionen gesteuert werden.

Die [[!DNL Google Ads] Erweiterte Erweiterung für die Konversions-Ereignisweiterleitung](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (zuvor als [!DNL Enhanced Conversions] Erweiterung) bietet eine benutzerfreundliche Vorlage zur einfachen Implementierung verbesserter Konvertierungen für die [!DNL Google Ads] API.

>[!IMPORTANT]
>
>Verbesserte Konversionen funktionieren nur bei Konversionstypen, bei denen Kundendaten vorhanden sind, z. B. Abonnements, Anmeldungen und Käufe. Eine oder mehrere der folgenden Kundendaten müssen verfügbar sein, da sie benötigt werden, wenn [Konfigurieren einer Konvertierungsaktion](#conversion-action-event-forwarding) für eine Ereignisweiterleitungsregel:
>
>* E-Mail-Adresse (empfohlen)
>* Name und Wohnadresse (Straße, Stadt, Bundesland/Region und Postleitzahl)
>* Telefonnummer (zusätzlich zu einem der beiden anderen oben genannten Informationen anzugeben)


## Implementierungsübersicht

Erweiterte Konvertierungen nutzen die [!DNL Google Ads] API zum Hinzufügen von Erstanbieterdaten zu einer Konvertierung, die auf einem Client-Gerät, normalerweise einer Website, stattgefunden hat. Dies bedeutet, dass es zwei Schritte gibt, um erweiterte Konvertierungen zu implementieren:

1. Senden Sie eine Konversion vom Client.
1. Verwenden Sie die Ereignisweiterleitung, um zusätzliche Erstanbieterdaten zu senden, die die vom Client gesendeten Konversionsdaten verbessern.

>[!TIP]
>
>Um das clientseitige Konversionsereignis mit den Erstanbieterdaten zu verknüpfen, die von der Ereignisweiterleitung gesendet werden, muss die `transaction_ID` muss in beiden Aufrufen identisch sein. Weitere Informationen dazu, wo dieser Wert für jeden Dienst bereitgestellt werden muss, finden Sie in den Abschnitten zum Konfigurieren von Konversionsaktionen für [tags](#conversion-action-tags) und [Ereignisweiterleitung](#conversion-action-event-forwarding)zurück.

Da das Senden von Konversionsereignissen sowohl eine Client- als auch eine Server-seitige Implementierung umfasst, werden in diesem Dokument die erforderlichen Schritte zum Einrichten der Client-seitigen [[!DNL Google Global Site Tag] (gtag)-Erweiterung](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) zusätzlich zu [!DNL Enhanced Conversions] Erweiterung für die Ereignisweiterleitung.

Das folgende Video bietet eine Einführung in die [!DNL Enhanced Conversions] Erweiterung und führt die Implementierungsschritte auf hoher Ebene durch:

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## Konvertierung mithilfe von Tags senden

So senden Sie ein Konversionsereignis von einer Website: [!DNL Google Global Site Tag] (gtag) bereitgestellt werden. Sie können dies mithilfe von Tags erreichen, indem Sie die [!DNL Google Global Site Tag] (gtag).

### Konfigurieren und installieren Sie die [!DNL Google Global Site Tag] Erweiterung

Navigieren Sie zum [!UICONTROL Datenerfassung] Benutzeroberfläche oder Experience Platform und wählen Sie **[!UICONTROL Tags]** in der linken Navigation. Wählen Sie die Tag-Eigenschaft aus, in der Sie die Erweiterung installieren möchten, und wählen Sie dann **[!UICONTROL Erweiterungen]** in der linken Navigation. Unter dem **[!UICONTROL Katalog]** Registerkarte, suchen Sie die [!UICONTROL Google Global Site Tag (gtag)] Erweiterung und wählen Sie **[!UICONTROL Installieren]**.

![Die [!UICONTROL Google Global Site Tag (gtag)] Erweiterung, die unter der [!UICONTROL Erweiterungen] Ansicht in der [!UICONTROL Datenerfassung] Benutzeroberfläche.](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

Das Installationsdialogfeld wird angezeigt. Wählen Sie von hier aus **[!UICONTROL Konto hinzufügen]** und geben Sie die folgenden Werte an, wenn Sie dazu aufgefordert werden:

| Kontoeigenschaft | Beschreibung |
| --- | --- |
| Kontoname | Ein eindeutiger Name für das Konto. Dieser Name wird nur in der Tags-Benutzeroberfläche verwendet. |
| Konto-ID | Ihre [!DNL Google Ads] Konto-ID. Um diesen Wert zu finden, melden Sie sich bei [!DNL Google Ads] und navigieren Sie zu: **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. Die Konto-ID-Zeichenfolge finden Sie im Code-Snippet-Fenster, das mit `AW-` oder `d`. |
| Produkt | Auswählen **[!UICONTROL Google Ads (AdWords)]**. |

{style=&quot;table-layout:auto&quot;}

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Konto hinzufügen]**, wählen Sie **[!UICONTROL Speichern]**.

### Hinzufügen einer Konvertierungsaktion zum Senden {#conversion-action-tags}

Nach der Installation der Erweiterung können Sie damit beginnen, Konversionsaktionen in Ihre Tag-Regeln aufzunehmen. Wählen Sie beim Erstellen oder Bearbeiten einer Regel, die die Konvertierung überwacht, die Sie erweitern möchten, die Option **[!UICONTROL Hinzufügen]** under [!UICONTROL Aktionen]. Wählen Sie im nächsten Dialogfeld **[!UICONTROL Google Global Site Tag (gtag)]** von [!UICONTROL Erweiterung] Dropdown-Liste und wählen Sie **[!UICONTROL Ereignis senden]** under [!UICONTROL Aktionstyp].

![Die [!UICONTROL Ereignis senden] Aktionstyp, der in der Aktionskonfigurationsansicht des Regelbearbeitungs-Workflows ausgewählt wird.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

Es werden zusätzliche Steuerelemente angezeigt, mit denen Sie die [!DNL gtag] -Ereignis. Es müssen mindestens die folgenden Felder ausgefüllt werden:

1. **[!UICONTROL Ereignisname (Aktion)]**: Eingabe `conversion` als Wert.
1. Fügen Sie ein neues Feld hinzu, in dem der Schlüssel `transaction_id` und der Wert ein [Datenelement](../../../ui/managing-resources/data-elements.md) , der [Transaktions-ID](https://support.google.com/google-ads/answer/6386790) -Wert.
1. **[!UICONTROL Konversionsbezeichnung]**: Geben Sie den entsprechenden Konversionstitel aus Ihrem [!DNL Google Ads] -Konto. Um diesen Wert zu finden, melden Sie sich bei Google Ads an und navigieren Sie zu **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. Die Konversionsbeschriftung finden Sie unter [!DNL Instructions].
   >[!IMPORTANT]
   >
   >Während Sie sich im Tag-Setup-Bereich Ihrer [!DNL Google Ads] müssen Sie sicherstellen, dass erweiterte Konvertierungen aktiviert sind. Überprüfen und akzeptieren Sie dazu die Nutzungsbedingungen und wählen Sie **[!DNL Turn on enhanced conversions]** und **[!DNL API]** als Implementierungsmethode.

Nachdem Sie die Aktion konfiguriert haben, wählen Sie **[!UICONTROL Änderungen beibehalten]** , um die Aktion zur Regelkonfiguration hinzuzufügen. Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]**.

Veröffentlichen Sie abschließend eine neue [build](../../../ui/publishing/builds.md) , um die Änderungen an der Bibliothek zu aktivieren.

## Senden von Erstanbieterdaten mit der Ereignisweiterleitung

Sobald Sie Konversionsereignisse vom Client senden können, können Sie diese Konversionen mithilfe der [!DNL Enhanced Conversions] Ereignisweiterleitungserweiterung.

### Google OAuth 2-Geheimnis und -Datenelement erstellen {#create-secret-data-element}

Bevor Sie die Erweiterung konfigurieren, müssen Sie in der Ereignisweiterleitung ein Zugriffstoken erstellen, um sich bei zu authentifizieren. [!DNL Google Ads] API.

Siehe Handbuch unter [Erstellen von Geheimnissen für die Ereignisweiterleitung](../../../ui/event-forwarding/secrets.md) für detaillierte Schritte. Stellen Sie sicher, dass Sie **[!UICONTROL Google OAuth 2]** als geheimen Typ. Folgen Sie weiterhin den Anweisungen. Wenn Sie aufgefordert werden, ein Google-Kontoprofil auszuwählen, wählen Sie das Konto aus, das Zugriff auf die von Ihnen konfigurierte Konvertierungsaktion hat.

Sobald der geheime Schlüssel erstellt wurde, [Neues Datenelement erstellen](../../../ui/managing-resources/data-elements.md#create-a-data-element) und wählen Sie **[!UICONTROL Geheimnis]** für den Datenelementtyp. Wählen Sie für jede Umgebung das entsprechende Google OAuth 2-Geheimnis aus und wählen Sie **[!UICONTROL In Bibliothek speichern]**.

### Konfigurieren und installieren Sie die [!DNL Enhanced Conversions] Erweiterung {#install-enhanced-conversions}

Suchen Sie die [!UICONTROL Erweiterte Konvertierungen von Google Ads] Erweiterung im Ereignisweiterleitungskatalog und wählen Sie **[!UICONTROL Installieren]**.

![Die [!UICONTROL Erweiterte Konvertierungen von Google Ads] Erweiterung, die unter der [!UICONTROL Erweiterungen] Ansicht in der [!UICONTROL Datenerfassung] Benutzeroberfläche.](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Um die Erweiterung zu konfigurieren, müssen Sie die beiden erforderlichen Felder ausfüllen:

1. **[!UICONTROL Kunden-ID]**: Die ID, die Ihre [!DNL Google Ads] -Konto. Um diesen Wert zu finden, melden Sie sich bei [!DNL Google Ads] und navigieren Sie zu **[!DNL Help]** > **[!DNL Customer ID]**.
1. **[!UICONTROL Zugreifen auf Token-Datenelement]**: Wählen Sie das Datenelementsymbol (![Datenelementsymbol](../../../images/extensions/server/google-ads-enhanced-conversions/data-element-icon.png)) und wählen Sie das geheime Google OAuth 2-Datenelement aus, das Sie verwenden [im vorherigen Schritt konfiguriert](#create-secret-data-element) aus dem Menü.

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Speichern]** , um die Erweiterung zu installieren.

### Hinzufügen einer [!UICONTROL Konvertierung senden] Aktion für eine Regel {#conversion-action-event-forwarding}

Nachdem die Erweiterung installiert wurde, können Sie beginnen, [!UICONTROL Konvertierung senden] Aktionen in Ihren Ereignisweiterleitungsregeln. Wählen Sie beim Erstellen oder Bearbeiten einer Regel, die die Konvertierung überwacht, die Sie erweitern möchten, die Option **[!UICONTROL Hinzufügen]** under [!UICONTROL Aktionen]. Wählen Sie im nächsten Dialogfeld **[!UICONTROL Erweiterte Konvertierungen von Google Ads]** von [!UICONTROL Erweiterung] Dropdown-Liste und wählen Sie **[!UICONTROL Konvertierung senden]** under [!UICONTROL Aktionstyp].

![Die [!UICONTROL Konvertierung senden] Aktionstyp, der in der Aktionskonfigurationsansicht des Regelbearbeitungs-Workflows ausgewählt wird.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

Im rechten Bereich werden neue Steuerelemente angezeigt, mit denen Sie Ihre Konvertierung konfigurieren können. Es müssen mindestens die folgenden Felder ausgefüllt werden:

**Konversionsinformationen**

| Eingabe | Beschreibung |
| --- | --- |
| Kundin bzw. Kunde ID | Ihre [!DNL Google Ads] Kunden-ID. Die Standardeinstellung ist die Kunden-ID, die Sie beim [Installieren der Erweiterung](#install-enhanced-conversions). |
| Konversions-ID oder Konversionsbezeichnung | Tracking-Werte aus [!DNL Google Ads] beim Einrichten des Konversions-Trackings. Werte beginnen mit `AW-`.<br><br>Weitere Informationen zum Auffinden dieser Werte finden Sie im Abschnitt [[!DNL Google Ads] Dokumentation](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| Transaction ID | Wählen Sie ein Datenelement aus, das denselben Transaktions-ID-Wert hat wie [von Client-Seite gesendet](#conversion-action-tags) mithilfe der [!DNL Google Global Site Tag] -Erweiterung. |

**Benutzeridentifizierung**

* Mindestens eine der drei Benutzer-IDs muss enthalten sein:
   * E-Mail
   * Telefonnummer
   * Vollständige Adresse

>[!TIP]
>
>Benutzeridentifizierungsdaten müssen gehasht werden, bevor sie an Google gesendet werden. Wenn die Daten nicht beim Empfang der Ereignisweiterleitung gehasht werden, wählen Sie die **[!UICONTROL Normalisieren und Hash]** ein-/ausschalten, um die Erweiterung anzuweisen, den Wert zu hash.
>
>![Die [!UICONTROL Normalisieren und Hash] Umschalten aktiviert für [!UICONTROL Email] -Eingabe innerhalb der [!UICONTROL Konvertierung senden] Aktionskonfigurationsformular.](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Änderungen beibehalten]** , um die Aktion zur Regelkonfiguration hinzuzufügen. Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]**.

Veröffentlichen Sie schließlich eine neue Ereignisweiterleitung [build](../../../ui/publishing/builds.md) , um die Änderungen an der Bibliothek zu aktivieren.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Konversionsereignisse an gesendet werden [!DNL Google Ads] mithilfe der [!DNL Enhanced Conversions] Ereignisweiterleitungserweiterung. Weiterführende Informationen zu Ereignisweiterleitungsfunktionen in Experience Platform finden Sie im Abschnitt [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
