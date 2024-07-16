---
title: Google Ads Enhanced Conversions-Erweiterung
description: Erfahren Sie mehr über die Google Ads Enhanced Conversions-Erweiterung für die Ereignisweiterleitung in Adobe Experience Platform.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 1%

---

# [!DNL Google Ads] Erweiterung der erweiterten Konvertierungen

Mithilfe der [!DNL Google Ads] -API können Sie [erweiterte Konversionen](https://support.google.com/google-ads/answer/9888656) nutzen, indem Sie Erstanbieter-Kundendaten in Form von Konversionsanpassungen senden. Google verwendet diese zusätzlichen Daten, um die Berichterstellung für Ihre Online-Konversionen zu verbessern, die durch Anzeigeninteraktionen gesteuert werden.

Die Erweiterung [[!DNL Google Ads] Erweiterte Konversions-Ereignisweiterleitungserweiterung](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (zuvor als Erweiterung [!DNL Enhanced Conversions] bezeichnet) bietet eine benutzerfreundliche Vorlage, mit der Sie erweiterte Konversionen für die API [!DNL Google Ads] einfach implementieren können.

>[!IMPORTANT]
>
>Verbesserte Konversionen funktionieren nur bei Konversionstypen, bei denen Kundendaten vorhanden sind, z. B. Abonnements, Anmeldungen und Käufe. Eine oder mehrere der folgenden Kundendaten müssen verfügbar sein, da sie beim [Konfigurieren einer Konversionsaktion](#conversion-action-event-forwarding) für eine Ereignisweiterleitungsregel erforderlich sind:
>
>* E-Mail-Adresse (empfohlen)
>* Name und Wohnadresse (Straße, Stadt, Bundesland/Region und Postleitzahl)
>* Telefonnummer (zusätzlich zu einem der beiden anderen oben genannten Informationen anzugeben)

## Implementierungsübersicht

Erweiterte Konvertierungen nutzen die [!DNL Google Ads] -API, um Erstanbieterdaten zu einer Konvertierung hinzuzufügen, die auf einem Client-Gerät, normalerweise einer Website, stattgefunden hat. Dies bedeutet, dass es zwei Schritte gibt, um erweiterte Konvertierungen zu implementieren:

1. Senden Sie eine Konversion vom Client.
1. Verwenden Sie die Ereignisweiterleitung, um zusätzliche Erstanbieterdaten zu senden, die die vom Client gesendeten Konversionsdaten verbessern.

>[!TIP]
>
>Um das clientseitige Konversionsereignis mit den Erstanbieterdaten zu verknüpfen, die von der Ereignisweiterleitung gesendet werden, muss &quot;`transaction_ID`&quot;in beiden Aufrufen identisch sein. Weitere Informationen dazu, wo dieser Wert für jeden Dienst angegeben werden muss, finden Sie in den Abschnitten zum Konfigurieren von Konversionsaktionen für [Tags](#conversion-action-tags) und [Ereignisweiterleitung](#conversion-action-event-forwarding).

Da das Senden von Konversionsereignissen sowohl eine Client- als auch eine Server-seitige Implementierung umfasst, werden in diesem Dokument die erforderlichen Schritte zum Einrichten der clientseitigen [[!DNL Google Global Site Tag] (gtag)-Erweiterung](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) zusätzlich zur [!DNL Enhanced Conversions] -Erweiterung für die Ereignisweiterleitung behandelt.

Das folgende Video bietet eine Einführung in die Erweiterung [!DNL Enhanced Conversions] und führt die Implementierungsschritte auf hoher Ebene durch:

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## Konvertierung mithilfe von Tags senden

Um ein Konversionsereignis von auf einer Website zu senden, muss [!DNL Google Global Site Tag] (gtag) bereitgestellt werden. Sie können dies mithilfe von Tags erreichen, indem Sie die Erweiterung [!DNL Google Global Site Tag] (gtag) konfigurieren und installieren.

### Konfigurieren und Installieren der [!DNL Google Global Site Tag] -Erweiterung

Navigieren Sie zur Benutzeroberfläche von [!UICONTROL Datenerfassung] oder Experience Platform und wählen Sie im linken Navigationsbereich **[!UICONTROL Tags]** aus. Wählen Sie die Tag-Eigenschaft aus, in der Sie die Erweiterung installieren möchten, und wählen Sie dann im linken Navigationsbereich **[!UICONTROL Erweiterungen]** aus. Suchen Sie auf der Registerkarte **[!UICONTROL Katalog]** die Erweiterung [!UICONTROL Google Global Site Tag (gtag)] und wählen Sie die Option **[!UICONTROL Installieren]** aus.

![Die Erweiterung [!UICONTROL Google Global Site Tag (gtag)], die unter der Ansicht [!UICONTROL Erweiterungen] in der Benutzeroberfläche [!UICONTROL Datenerfassung] ausgewählt wird.](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

Das Installationsdialogfeld wird angezeigt. Wählen Sie hier **[!UICONTROL Konto hinzufügen]** aus und geben Sie die folgenden Werte ein, wenn Sie dazu aufgefordert werden:

| Kontoeigenschaft | Beschreibung |
| --- | --- |
| Kontoname | Ein eindeutiger Name für das Konto. Dieser Name wird nur in der Tags-Benutzeroberfläche verwendet. |
| Konto-ID | Ihre [!DNL Google Ads] -Konto-ID. Um diesen Wert zu finden, melden Sie sich bei [!DNL Google Ads] an und navigieren Sie zu: **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. Die Konto-ID-Zeichenfolge finden Sie im Codeausschnitt-Fenster, das mit `AW-` oder `d` beginnt. |
| Produkt | Wählen Sie **[!UICONTROL Google Ads (AdWords)]** aus. |

{style="table-layout:auto"}

Wählen Sie abschließend **[!UICONTROL Konto hinzufügen]** und dann **[!UICONTROL Speichern]** aus.

### Hinzufügen einer Konvertierungsaktion für einen Versand {#conversion-action-tags}

Nach der Installation der Erweiterung können Sie damit beginnen, Konversionsaktionen in Ihre Tag-Regeln aufzunehmen. Wählen Sie beim Erstellen oder Bearbeiten einer Regel, die die Konvertierung überwacht, die Sie erweitern möchten, **[!UICONTROL Hinzufügen]** unter [!UICONTROL Aktionen] aus. Wählen Sie im nächsten Dialogfeld **[!UICONTROL Google Global Site Tag (gtag)]** aus dem Dropdown-Menü [!UICONTROL Erweiterung] und dann **[!UICONTROL Ereignis senden]** unter [!UICONTROL Aktionstyp].

![Der Aktionstyp [!UICONTROL Ereignis senden] , der in der Aktionskonfigurationsansicht des Regelbearbeitungs-Workflows ausgewählt wird.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

Es werden zusätzliche Steuerelemente angezeigt, mit denen Sie das [!DNL gtag] -Ereignis konfigurieren können. Es müssen mindestens die folgenden Felder ausgefüllt werden:

1. **[!UICONTROL Ereignisname (Aktion)]**: Geben Sie `conversion` als Wert ein.
1. Fügen Sie ein neues Feld hinzu, wobei der Schlüssel `transaction_id` und der Wert ein [Datenelement](../../../ui/managing-resources/data-elements.md) ist, das den Wert [Transaktions-ID](https://support.google.com/google-ads/answer/6386790) enthält.
1. **[!UICONTROL Konversionsbezeichnung]**: Geben Sie den entsprechenden Konversionstitel aus Ihrem [!DNL Google Ads]-Konto ein. Um diesen Wert zu finden, melden Sie sich bei Google Ads an und navigieren Sie zu **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. Die Konversionsbeschriftung finden Sie unter [!DNL Instructions].
   >[!IMPORTANT]
   >
   >Stellen Sie sicher, dass erweiterte Konvertierungen aktiviert sind, während Sie sich im Bereich für die Tag-Einrichtung Ihres [!DNL Google Ads]-Kontos befinden. Überprüfen und akzeptieren Sie dazu die Nutzungsbedingungen und wählen Sie dann **[!DNL Turn on enhanced conversions]** und **[!DNL API]** als Implementierungsmethode aus.

Nachdem Sie die Aktion konfiguriert haben, wählen Sie **[!UICONTROL Änderungen beibehalten]** aus, um die Aktion zur Regelkonfiguration hinzuzufügen. Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]** aus.

Veröffentlichen Sie abschließend einen neuen [Build](../../../ui/publishing/builds.md) , um die Änderungen an der Bibliothek zu aktivieren.

## Senden von Erstanbieterdaten mit der Ereignisweiterleitung

Sobald Sie Konversionsereignisse Client-seitig senden können, können Sie diese Konversionen mithilfe der Erweiterung [!DNL Enhanced Conversions] Ereignisweiterleitung verbessern.

### Google OAuth 2-Geheimnis und -Datenelement erstellen {#create-secret-data-element}

Bevor Sie die Erweiterung konfigurieren, müssen Sie in der Ereignisweiterleitung ein Zugriffstoken erstellen, um sich bei der [!DNL Google Ads] -API zu authentifizieren.

Detaillierte Schritte finden Sie im Handbuch zu [Erstellen von Geheimnissen für die Ereignisweiterleitung](../../../ui/event-forwarding/secrets.md) . Stellen Sie sicher, dass Sie **[!UICONTROL Google OAuth 2]** als geheimen Typ auswählen. Folgen Sie weiterhin den Anweisungen. Wenn Sie aufgefordert werden, ein Google-Kontoprofil auszuwählen, wählen Sie das Konto aus, das Zugriff auf die von Ihnen konfigurierte Konvertierungsaktion hat.

Nachdem der geheime Schlüssel erstellt wurde, erstellen [ein neues Datenelement](../../../ui/managing-resources/data-elements.md#create-a-data-element) und wählen Sie **[!UICONTROL Geheimnis]** für den Datenelementtyp aus. Wählen Sie für jede Umgebung das entsprechende Google OAuth 2-Geheimnis aus und wählen Sie **[!UICONTROL In Bibliothek speichern]** aus.

### Konfigurieren und Installieren der [!DNL Enhanced Conversions] -Erweiterung {#install-enhanced-conversions}

Suchen Sie die Erweiterung [!UICONTROL Google Ads Enhanced Conversions] im Ereignisweiterleitungskatalog und wählen Sie **[!UICONTROL Installieren]** aus.

![ Die Erweiterung [!UICONTROL Google Ads Enhanced Conversions] , die unter der Ansicht [!UICONTROL Erweiterungen] in der Benutzeroberfläche [!UICONTROL Datenerfassung] ausgewählt ist.](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Um die Erweiterung zu konfigurieren, müssen Sie die beiden erforderlichen Felder ausfüllen:

1. **[!UICONTROL Kunden-ID]**: Die ID, mit der Ihr [!DNL Google Ads]-Konto eindeutig identifiziert wird. Um diesen Wert zu finden, melden Sie sich bei [!DNL Google Ads] an und navigieren Sie zu **[!DNL Help]** > **[!DNL Customer ID]**.
1. **[!UICONTROL Auf Token-Datenelement zugreifen]**: Wählen Sie das Datenelementsymbol (![Datenelementsymbol](../../../images/extensions/server/google-ads-enhanced-conversions/data-element-icon.png)) und wählen Sie das geheime Datenelement Google OAuth 2 aus, das Sie im vorherigen Schritt [ konfiguriert haben.](#create-secret-data-element)

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Speichern]** aus, um die Erweiterung zu installieren.

### Hinzufügen einer Aktion [!UICONTROL Konvertierung senden] zu einer Regel {#conversion-action-event-forwarding}

Nachdem die Erweiterung installiert wurde, können Sie beginnen, [!UICONTROL Konversionsaktionen senden] in Ihre Ereignisweiterleitungsregeln aufzunehmen. Wählen Sie beim Erstellen oder Bearbeiten einer Regel, die die Konvertierung überwacht, die Sie erweitern möchten, **[!UICONTROL Hinzufügen]** unter [!UICONTROL Aktionen] aus. Wählen Sie im nächsten Dialogfeld **[!UICONTROL Google Ads Enhanced Conversions]** aus dem Dropdown-Menü [!UICONTROL Extension] und dann **[!UICONTROL Send Conversion]** unter [!UICONTROL Aktionstyp].

![Der Aktionstyp [!UICONTROL Konversion senden] , der in der Aktionskonfigurationsansicht des Regelbearbeitungs-Workflows ausgewählt wird.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

Im rechten Bereich werden neue Steuerelemente angezeigt, mit denen Sie Ihre Konvertierung konfigurieren können. Es müssen mindestens die folgenden Felder ausgefüllt werden:

**Konversionsinformationen**

| Eingabe | Beschreibung |
| --- | --- |
| Kunden-ID | Ihre [!DNL Google Ads] Kunden-ID. Die Standardeinstellung ist die Kunden-ID, die Sie beim [Installieren der Erweiterung](#install-enhanced-conversions) eingegeben haben. |
| Konversions-ID oder Konversionsbezeichnung | Tracking-Werte, die beim Einrichten des Konversions-Trackings von [!DNL Google Ads] abgerufen wurden. Werte beginnen mit `AW-`.<br><br>Weitere Informationen zum Auffinden dieser Werte finden Sie in der [[!DNL Google Ads] Dokumentation](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| Transaction ID | Wählen Sie ein Datenelement aus, das denselben Transaktions-ID-Wert wie [aufweist, der von der Clientseite ](#conversion-action-tags) mit der Erweiterung [!DNL Google Global Site Tag] gesendet wurde. |

**Benutzeridentifizierung**

* Mindestens eine der drei Benutzer-IDs muss enthalten sein:
   * E-Mail
   * Telefonnummer
   * Vollständige Adresse

>[!TIP]
>
>Benutzeridentifizierungsdaten müssen gehasht werden, bevor sie an Google gesendet werden. Wenn die Daten nicht gehasht werden, wenn die Ereignisweiterleitung sie erhält, wählen Sie den Umschalter **[!UICONTROL Normalisieren und Hash]** für ein bestimmtes Feld aus, um die Erweiterung anzuweisen, den Wert zu hash.
>
>![ Der Umschalter [!UICONTROL Normalisieren und Hash] ist für die Eingabe [!UICONTROL E-Mail] im Konfigurationsformular für die Aktion [!UICONTROL Konversion senden] aktiviert.](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

Wählen Sie nach Abschluss **[!UICONTROL Änderungen beibehalten]** aus, um die Aktion zur Regelkonfiguration hinzuzufügen. Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]** aus.

Veröffentlichen Sie abschließend eine neue Ereignisweiterleitung [build](../../../ui/publishing/builds.md) , um die Änderungen an der Bibliothek zu aktivieren.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Konversionsereignisse mithilfe der Ereignisweiterleitungs-Erweiterung [!DNL Enhanced Conversions] an [!DNL Google Ads] gesendet werden. Weiterführende Informationen zu Ereignisweiterleitungsfunktionen in Experience Platform finden Sie in der [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
