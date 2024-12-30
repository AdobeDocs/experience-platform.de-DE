---
title: LinkedIn Conversions-API, Ereignisweiterleitungs-Erweiterung
description: Mit dieser Adobe Experience Platform-Ereignisweiterleitungserweiterung können Sie die Leistung Ihrer LinkedIn-Marketing-Kampagne messen.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 411e7b77-081e-4139-ba34-04468e519ea5
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 3%

---

# [!DNL LinkedIn]-Konversions-API-Erweiterung

[[!DNL LinkedIn Conversions API]](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api) ist ein Konversionsverfolgungs-Tool, das eine direkte Verbindung zwischen Marketing-Daten vom Server eines Werbetreibenden und [!DNL LinkedIn] herstellt. Dadurch können Werbetreibende die Effektivität ihrer [!DNL LinkedIn] Marketing-Kampagnen unabhängig vom Ort der Konversion bewerten und diese Informationen zur Kampagnenoptimierung nutzen. Die [!DNL LinkedIn Conversions API]-Erweiterung kann durch eine vollständigere Attribution, eine verbesserte Datenzuverlässigkeit und eine optimierte Bereitstellung dazu beitragen, die Leistung zu steigern und die Kosten pro Aktion zu senken.

## Voraussetzungen {#prerequisites}

Sie müssen [Konversionsregel erstellen](https://www.linkedin.com/help/lms/answer/a1657171) in Ihrem [!DNL LinkedIn Campaign Manager] Konto. [!DNL Adobe] empfiehlt, am Anfang des Namens der Konversationsregel „CAPI“ einzufügen, um sie von anderen Konversionsregeltypen zu unterscheiden, die Sie möglicherweise konfiguriert haben.

### Erstellen von geheimen Daten und eines Datenelements

Erstellen Sie ein neues [!DNL LinkedIn][Ereignisweiterleitungsgeheimnis](../../../ui/event-forwarding/secrets.md) und geben Sie ihm einen eindeutigen Namen, der das authentifizierende Mitglied angibt. Dies wird verwendet, um die Verbindung zu Ihrem Konto zu authentifizieren und dabei den Wert sicher zu halten.

Als Nächstes erstellen [ mithilfe ](../../../ui/managing-resources/data-elements.md#create-a-data-element) Erweiterung [!UICONTROL Core] und eines Datenelementtyps [!UICONTROL Secret] ein Datenelement, das auf das soeben erstellte `LinkedIn` verweist.

## Installieren und Konfigurieren der [!DNL LinkedIn] {#install}

Um die Erweiterung zu installieren[ erstellen Sie eine Ereignisweiterleitungseigenschaft ](../../../ui/event-forwarding/overview.md#properties) wählen Sie eine vorhandene Eigenschaft aus, die Sie bearbeiten möchten.

Wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation aus. Wählen Sie auf **[!UICONTROL Registerkarte]** Katalog“ die Erweiterung **[!UICONTROL LinkedIn]** und dann **[!UICONTROL Installieren]** aus.

![Der Erweiterungskatalog mit der [!DNL LinkedIn] Erweiterungskarte, in der install hervorgehoben ist.](../../../images/extensions/server/linkedin/install-extension.png)

Geben Sie im nächsten Bildschirm das zuvor erstellte Datenelementgeheimnis in das Feld `Access Token` ein. Das Datenelementgeheimnis enthält Ihr [!DNL LinkedIn] OAuth 2-Token. Wählen Sie **[!UICONTROL Speichern]**, wenn Sie fertig sind.

![Die Seite Konfiguration der [!DNL LinkedIn]-Erweiterung mit dem [!UICONTROL Zugriffstoken]-Feld und [!UICONTROL Speichern] hervorgehoben.](../../../images/extensions/server/linkedin/configure-extension.png)

## Erstellen einer [!DNL Send Conversion] Regel {#tracking-rule}

Nachdem alle Datenelemente eingerichtet wurden, können Sie mit der Erstellung von Ereignisweiterleitungsregeln beginnen, die bestimmen, wann und wie Ihre Ereignisse an [!DNL LinkedIn] gesendet werden.

Erstellen Sie eine neue [ (Regel](../../../ui/managing-resources/rules.md) in Ihrer Ereignisweiterleitungseigenschaft. Fügen **[!UICONTROL unter „Aktionen]** eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL LinkedIn]** fest. Wählen Sie als Nächstes **[!UICONTROL Konvertierung senden]** für den **[!UICONTROL Aktionstyp]**.

![Die Ansicht mit den Eigenschaftsregeln für die Ereignisweiterleitung mit den Feldern, die zum Hinzufügen einer Regelkonfiguration für die Ereignisweiterleitung erforderlich sind, ist hervorgehoben.](../../../images/extensions/server/linkedin/linkedin-event-action.png)

Nach der Auswahl erscheinen zusätzliche Steuerelemente, um das Ereignis weiter zu konfigurieren. Wählen **[!UICONTROL Änderungen beibehalten]**, um die Regel zu speichern.

**[!UICONTROL Benutzerdaten]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL E-Mail] | E-Mail-Adresse des Kontakts, der mit dem Konversionsereignis verknüpft ist. Der E-Mail-Wert wird vom Erweiterungs-Code in SHA256 codiert, es sei denn, der angegebene Wert ist bereits eine SHA256-Zeichenfolge. |
| [!UICONTROL LinkedIn-First-Party-Anzeigen-Tracking-UUID] | Dies ist eine Erstanbieter-Cookie-ID. Werbetreibende müssen das erweiterte Konversions-Tracking von [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag) aktivieren, um Erstanbieter-Cookies zu aktivieren, die einen Klick-ID-Parameter `li_fat_id` an die Klick-URLs anhängen. |
| [!UICONTROL Kundeninformationsdaten] | Dieses Feld enthält ein JSON-Objekt mit zusätzlichen Attributen, die zusammen mit der Nachricht gesendet werden.<br><br>Unter der Option **[!UICONTROL Raw]** können Sie das JSON-Objekt direkt in das bereitgestellte Textfeld einfügen oder Sie können das Datenelementsymbol (![Datensatzsymbol](/help/images/icons/database.png)) auswählen, um aus einer Liste vorhandener Datenelemente zur Darstellung der Daten auszuwählen.<br><br>Sie können auch die Option **[!UICONTROL JSON-Schlüssel-Wert-Paare-Editor]** verwenden, um jedes Schlüssel-Wert-Paar manuell über einen Benutzeroberflächen-Editor hinzuzufügen. Jeder Wert kann durch eine Roheingabe dargestellt werden oder stattdessen kann ein Datenelement ausgewählt werden. Die akzeptierten Schlüsselwerte sind: `firstName`, `lastName`, `companyName`, `title` und `country`. |

{style="table-layout:auto"}

![Der [!DNL User Data] Abschnitt mit Beispieldaten, die in die Felder eingegeben werden.](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL Konversionsdaten]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Konversion] | Die ID der in [LinkedIn Campaign Manager](https://www.linkedin.com/help/lms/answer/a1657171) erstellten Konversionsregel. Wählen Sie die Konversionsregel aus, um die ID abzurufen, und kopieren Sie dann die ID wie `/conversions/<id>` aus der Browser-URL (z. B. `/campaignmanager/accounts/508111232/conversions/15588877`). |
| [!UICONTROL Konvertierungszeit] | Jeder Zeitstempel in Millisekunden, bei dem das Konversionsereignis aufgetreten ist. <br><br> Hinweis: Wenn Ihre Quelle den Konvertierungszeitstempel in Sekunden aufzeichnet, fügen Sie am Ende bitte 000 ein, um ihn in Millisekunden zu transformieren. |
| [!UICONTROL Währung] | Währungscode im ISO-Format. |
| [!UICONTROL Betrag] | Wert der Konvertierung in einer Dezimalzeichenfolge (z. B. „100.05„). |
| [!UICONTROL Ereignis-ID] | Die eindeutige ID, die von Werbetreibenden generiert wird, um jedes Ereignis anzugeben. Dies ist ein optionales Feld, das für die [Deduplizierung“ ](https://learn.microsoft.com/en-us/linkedin/marketing/conversions/deduplication?view=li-lms-2024-02) wird. |

{style="table-layout:auto"}

![Der [!DNL Conversion Data] Abschnitt mit Beispieldaten in den Feldern.](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL Konfigurationsüberschreibungen]**

>HINWEIS
>
>Das Feld [!UICONTROL Konfigurationsüberschreibungen] ermöglicht es Benutzenden, für jede Regel ein anderes [!DNL LinkedIn]-Zugriffstoken festzulegen, sodass jede Regel ein Zugriffstoken verwenden kann, das möglicherweise Zugriff auf verschiedene [!DNL LinkedIn]-Werbekonten hat.

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Zugriffstoken] | Das [!DNL LinkedIn] Zugriffstoken. |

![Der [!DNL Configuration Overrides] Abschnitt mit Beispieldateneingabe in das Feld.](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Daten mithilfe der Erweiterung für die [!DNL LinkedIn Conversions API]-Ereignisweiterleitung an [!DNL LinkedIn] senden. Weitere Informationen zu den Ereignisweiterleitungsfunktionen in [!DNL Adobe Experience Platform] finden Sie unter [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).

Weitere Informationen zum Debuggen Ihrer Implementierung mit dem Experience Platform-Debugger und dem Überwachungs-Tool für die Ereignisweiterleitung finden Sie unter [Adobe Experience Platform Debugger - Übersicht](../../../../debugger/home.md) und [Überwachen von Aktivitäten in der Ereignisweiterleitung](../../../ui/event-forwarding/monitoring.md).
