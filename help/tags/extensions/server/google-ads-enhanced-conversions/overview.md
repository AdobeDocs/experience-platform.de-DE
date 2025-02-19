---
title: Google Ads Enhanced Conversions-Erweiterung
description: Erfahren Sie mehr über die Google Ads Enhanced Conversions-Erweiterung für die Ereignisweiterleitung in Adobe Experience Platform.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 0d98183838125fac66768b94bc1993bde9a374b5
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 1%

---

# [!DNL Google Ads] Enhanced Conversions-Erweiterung

Mit der [!DNL Google Ads]-API können Sie [erweiterten Konversionen](https://support.google.com/google-ads/answer/9888656) nutzen, indem Sie First-Party-Kundendaten in Form von Konversionsanpassungen senden. Google verwendet diese zusätzlichen Daten, um die Berichterstellung für Online-Konversionen aufgrund von Anzeigeninteraktionen zu verbessern.

Die [[!DNL Google Ads] Erweiterung für die Ereignisweiterleitung bei erweiterten Konvertierungen](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (früher als [!DNL Enhanced Conversions]-Erweiterung bezeichnet) bietet eine benutzerfreundliche Vorlage zur einfachen Implementierung erweiterter Konvertierungen für die [!DNL Google Ads]-API.

>[!IMPORTANT]
>
>Erweiterte Konvertierungen funktionieren nur für Konversionstypen, bei denen Kundendaten vorhanden sind, z. B. Abonnements, Anmeldungen und Käufe. Mindestens einer der folgenden Kundendaten muss verfügbar sein, da sie bei der [Konfiguration einer Konversionsaktion](#conversion-action-event-forwarding) für eine Ereignisweiterleitungsregel erforderlich sind:
>
>* E-Mail-Adresse (bevorzugt)
>* Name und Wohnadresse (Straße, Stadt, Bundesland/Region und Postleitzahl)
>* Telefonnummer (muss zusätzlich zu einer der beiden anderen oben genannten Informationen angegeben werden)

## Implementierungsübersicht

Erweiterte Konvertierungen nutzen die [!DNL Google Ads]-API, um Erstanbieterdaten zu einer Konvertierung hinzuzufügen, die auf einem Client-Gerät, normalerweise einer Website, stattgefunden hat. Dies bedeutet, dass es zwei Schritte zum Implementieren erweiterter Konvertierungen gibt:

1. Senden Sie eine Konvertierung vom Client.
1. Verwenden Sie die Ereignisweiterleitung, um zusätzliche First-Party-Daten zu senden, die die vom Client gesendeten Konversionsdaten verbessern.

>[!TIP]
>
>Um das Client-seitige Konversionsereignis mit den Erstanbieterdaten zu verknüpfen, die von der Ereignisweiterleitung gesendet werden, muss die `transaction_ID` in beiden Aufrufen identisch sein. Weitere Informationen dazu, wo dieser Wert für jeden Service angegeben werden muss, finden Sie in den Abschnitten zum Konfigurieren von Konversionsaktionen für [Tags](#conversion-action-tags) bzw[ &quot;](#conversion-action-event-forwarding)&quot;.

Da das Senden von Konversionsereignissen sowohl eine Client- als auch eine Server-seitige Implementierung umfasst, werden in diesem Dokument die erforderlichen Schritte zum Einrichten der Client-seitigen [[!DNL Google Global Site Tag] -Erweiterung (gtag](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) sowie die [!DNL Enhanced Conversions]-Erweiterung für die Ereignisweiterleitung behandelt.

Das folgende Video bietet eine Einführung in die [!DNL Enhanced Conversions]-Erweiterung und führt Sie auf einer allgemeinen Ebene durch die Implementierungsschritte:

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## Konvertierung mithilfe von Tags senden

Um ein Konversionsereignis von auf einer Website zu senden, muss [!DNL Google Global Site Tag] (gtag) bereitgestellt werden. Sie können dies mit Tags erreichen, indem Sie die [!DNL Google Global Site Tag]-Erweiterung (gtag) konfigurieren und installieren.

### Konfigurieren und Installieren der [!DNL Google Global Site Tag]

Navigieren Sie zur Benutzeroberfläche [!UICONTROL Datenerfassung] oder Experience Platform-Benutzeroberfläche und wählen Sie **[!UICONTROL linken Navigationsbereich]** Tags“ aus. Wählen Sie die Tag-Eigenschaft aus, auf der Sie die Erweiterung installieren möchten, und wählen Sie dann **[!UICONTROL Erweiterungen]** in der linken Navigationsleiste. Suchen Sie auf der **[!UICONTROL Katalog]** die Erweiterung [!UICONTROL Google Global Site Tag (gtag)] und wählen Sie **[!UICONTROL Installieren]** aus.

![Die Erweiterung [!UICONTROL Google Global Site Tag (gtag] wird unter der Ansicht [!UICONTROL Erweiterungen] in der Benutzeroberfläche [!UICONTROL Datenerfassung] ausgewählt.](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

Das Installationsdialogfeld wird angezeigt. Wählen Sie von hier **[!UICONTROL Konto hinzufügen]** und geben Sie die folgenden Werte an, wenn Sie dazu aufgefordert werden:

| Kontoeigenschaft | Beschreibung |
| --- | --- |
| Kontoname | Ein eindeutiger Name für das Konto. Dieser Name wird nur innerhalb der Tags-Benutzeroberfläche verwendet. |
| Konto-ID | Ihre [!DNL Google Ads]-Konto-ID. Melden Sie sich bei [!DNL Google Ads] an und navigieren Sie zu: **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. Die Zeichenfolge der Konto-ID befindet sich im Code-Snippet-Fenster, das mit `AW-` oder `d` beginnt. |
| Produkt | **[!UICONTROL Google Ads (AdWords)]**. |

{style="table-layout:auto"}

Klicken Sie abschließend auf **[!UICONTROL Konto hinzufügen]** und klicken Sie dann auf **[!UICONTROL Speichern]**.

### Hinzufügen einer Aktion zum Senden einer Konversion {#conversion-action-tags}

Nach der Installation der Erweiterung können Sie mit der Aufnahme von Konvertierungsaktionen in Ihre Tag-Regeln beginnen. Wählen Sie beim Erstellen oder Bearbeiten einer Regel, die auf die Konversion wartet, die Sie verbessern möchten, **[!UICONTROL Hinzufügen]** unter [!UICONTROL Aktionen]. Wählen Sie im nächsten Dialogfeld **[!UICONTROL Google Global Site Tag (gtag)]** aus der Dropdown-Liste [!UICONTROL Erweiterung] und wählen Sie dann **[!UICONTROL Ereignis senden]** unter [!UICONTROL Aktionstyp].

![Der [!UICONTROL Ereignis senden] Aktionstyp, der in der Aktionskonfigurationsansicht des Regelbearbeitungs-Workflows ausgewählt wird.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

Es werden zusätzliche Steuerelemente angezeigt, mit denen Sie das [!DNL gtag] konfigurieren können. Die folgenden Felder müssen mindestens ausgefüllt werden:

1. **[!UICONTROL Ereignisname (Aktion)]**: Geben Sie `conversion` als Wert ein.
1. Fügen Sie ein neues Feld hinzu, in dem der Schlüssel `transaction_id` ist und der Wert ein [Datenelement](../../../ui/managing-resources/data-elements.md) ist, das den Wert [Transaktions-ID](https://support.google.com/google-ads/answer/6386790) enthält.
1. **[!UICONTROL Konversionsbezeichnung]**: Geben Sie die entsprechende Konversionsbezeichnung aus Ihrem [!DNL Google Ads] ein. Um diesen Wert zu finden, melden Sie sich bei Google Ads an und navigieren Sie zu **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. Die Bezeichnung für die Konversion finden Sie unter [!DNL Instructions].

   >[!IMPORTANT]
   >
   >Stellen Sie sicher, dass erweiterte Konvertierungen aktiviert sind, während Sie sich im Bereich Tag-Setup Ihres [!DNL Google Ads]-Kontos befinden. Überprüfen und akzeptieren Sie dazu die Nutzungsbedingungen und wählen Sie dann **[!DNL Turn on enhanced conversions]** und **[!DNL API]** als Implementierungsmethode aus.

Nachdem Sie die Aktion konfiguriert haben, wählen Sie **[!UICONTROL Änderungen beibehalten]** aus, um die Aktion zur Regelkonfiguration hinzuzufügen. Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]** aus.

Veröffentlichen Sie abschließend einen neuen [Build](../../../ui/publishing/builds.md), um die Änderungen an der Bibliothek zu aktivieren.

## Senden von First-Party-Daten mithilfe der Ereignisweiterleitung

Sobald Sie Konversionsereignisse von der Client-Seite senden können, können Sie diese Konversionen mit der Erweiterung für die [!DNL Enhanced Conversions]-Ereignisweiterleitung verbessern.

### Erstellen eines Google OAuth 2-Geheimnisses und -Datenelements {#create-secret-data-element}

Bevor Sie die Erweiterung konfigurieren, müssen Sie ein Zugriffstoken in der Ereignisweiterleitung erstellen, um sich bei [!DNL Google Ads] API zu authentifizieren.

Ausführliche Anweisungen finden Sie im Handbuch [Erstellen von ](../../../ui/event-forwarding/secrets.md) für die Ereignisweiterleitung“. Stellen Sie sicher, dass Sie **[!UICONTROL Google OAuth 2]** als Geheimnistyp auswählen. Folgen Sie weiterhin den Anweisungen und wählen Sie auf Anforderung zur Auswahl eines Google-Kontoprofils das Konto aus, das Zugriff auf die Konversionsaktion hat, die Sie konfigurieren.

Nachdem die geheimen Daten erstellt wurden, [ Sie „Neues Datenelement erstellen](../../../ui/managing-resources/data-elements.md#create-a-data-element) und wählen Sie **[!UICONTROL Datenelementtyp]** Geheime Daten“ aus. Wählen Sie für jede Umgebung das entsprechende Google OAuth 2-Geheimnis aus und klicken Sie auf **[!UICONTROL In Bibliothek speichern]**.

### Konfigurieren und Installieren der [!DNL Enhanced Conversions] {#install-enhanced-conversions}

Suchen Sie die Erweiterung [!UICONTROL Google Ads Enhanced Conversions] im Ereignisweiterleitungskatalog und wählen Sie **[!UICONTROL Installieren]**.

![Die Erweiterung [!UICONTROL Google Ads Enhanced Conversions] wird in der Ansicht [!UICONTROL Erweiterungen] in der [!UICONTROL Datenerfassungs]-Benutzeroberfläche ausgewählt.](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

Um die Erweiterung zu konfigurieren, müssen Sie die beiden erforderlichen Felder ausfüllen:

1. **[!UICONTROL Kunden-ID]**: Die ID, die Ihr [!DNL Google Ads]-Konto eindeutig identifiziert. Um diesen Wert zu finden, melden Sie sich bei [!DNL Google Ads] an und navigieren Sie zu **[!DNL Help]** > **[!DNL Customer ID]**.
2. **[!UICONTROL Zugriffstoken-Datenelement]**: Wählen Sie das Datenelementsymbol (![Datenelementsymbol](/help/images/icons/database.png)) und dann das geheime Datenelement Google OAuth 2 aus, das Sie [im vorherigen Schritt konfiguriert](#create-secret-data-element) aus dem Menü.

Klicken Sie abschließend auf **[!UICONTROL Speichern]**, um die Erweiterung zu installieren.

### Hinzufügen [!UICONTROL  Aktion „Konvertierung senden] zu einer Regel {#conversion-action-event-forwarding}

Nachdem die Erweiterung installiert wurde, können Sie damit beginnen, [!UICONTROL Konversionsaktion senden] in Ihre Ereignisweiterleitungsregeln einzuschließen. Wählen Sie beim Erstellen oder Bearbeiten einer Regel, die auf die Konversion wartet, die Sie verbessern möchten, **[!UICONTROL Hinzufügen]** unter [!UICONTROL Aktionen]. Wählen Sie im nächsten Dialogfeld **[!UICONTROL Erweiterte Konvertierungen für Google Ads]** aus der Dropdown-Liste [!UICONTROL Erweiterung] und wählen Sie dann **[!UICONTROL Konversion senden]** unter [!UICONTROL Aktionstyp].

![Der [!UICONTROL Konvertierung senden] Aktionstyp, der in der Aktionskonfigurationsansicht des Regelbearbeitungs-Workflows ausgewählt wird.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

Im rechten Bereich werden neue Steuerelemente angezeigt, mit denen Sie die Konvertierung konfigurieren können. Die folgenden Felder müssen mindestens ausgefüllt werden:

**Konversionsinformationen**

| Eingabe | Beschreibung |
| --- | --- |
| Kunden-ID | Ihre [!DNL Google Ads] Kunden-ID. Standardmäßig wird die Kunden-ID verwendet, die Sie bei der [ der Erweiterung eingegeben ](#install-enhanced-conversions). |
| Konversions-ID oder Konversionskennzeichnung | Tracking-Werte, die bei der Einrichtung des Konversionstrackings von [!DNL Google Ads] abgerufen werden. Werte beginnen mit `AW-`.<br><br>Weitere Informationen zum Auffinden dieser Werte finden Sie in der [[!DNL Google Ads] Dokumentation](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| Transaction ID | Wählen Sie ein Datenelement mit demselben Transaktions-ID-Wert aus, der [ der Client-Seite ](#conversion-action-tags) der [!DNL Google Global Site Tag]-Erweiterung gesendet wird. |

**Benutzeridentifizierung**

* Mindestens eine der drei Benutzerkennung muss enthalten sein:
   * E-Mail
   * Telefonnummer
   * Vollständige Adresse

>[!TIP]
>
>Benutzeridentifizierungsdaten müssen gehasht werden, bevor sie an Google gesendet werden. Wenn die Daten beim Empfang der Ereignisweiterleitung nicht gehasht werden, wählen Sie den Umschalter **[!UICONTROL Normalisieren und Hash]** für ein bestimmtes Feld aus, um die Erweiterung anzuweisen, den Wert zu hashen.
>
>![Der Umschalter [!UICONTROL Normalisieren und Hash] ist für die Eingabe [!UICONTROL E-Mail] im Konfigurationsformular [!UICONTROL Konvertierung senden] aktiviert.](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

Wenn Sie fertig sind, wählen **[!UICONTROL Änderungen beibehalten]**, um die Aktion zur Regelkonfiguration hinzuzufügen. Wenn Sie mit der Regel zufrieden sind, wählen Sie **[!UICONTROL In Bibliothek speichern]** aus.

Veröffentlichen Sie abschließend eine neue Ereignisweiterleitung [Build](../../../ui/publishing/builds.md), um die Änderungen an der Bibliothek zu aktivieren.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Konversionsereignisse mithilfe der [!DNL Enhanced Conversions]-Erweiterung an [!DNL Google Ads] senden. Weitere Informationen zu den Funktionen für die Ereignisweiterleitung in Experience Platform finden Sie unter [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
