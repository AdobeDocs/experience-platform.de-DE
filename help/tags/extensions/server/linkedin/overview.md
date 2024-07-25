---
title: LinkedIn Conversions API Event Forwarding-Erweiterung
description: Mit dieser Adobe Experience Platform-Ereignisweiterleitungserweiterung können Sie die Leistung Ihrer LinkedIn-Marketingkampagne messen.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 411e7b77-081e-4139-ba34-04468e519ea5
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 3%

---

# [!DNL LinkedIn]-Konversions-API-Erweiterung

[[!DNL LinkedIn Conversions API]](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api) ist ein Konversions-Tracking-Tool, das eine direkte Verbindung zwischen den Marketingdaten eines Advertiser-Servers und [!DNL LinkedIn] herstellt. Dadurch können Werbetreibende die Effektivität ihrer [!DNL LinkedIn]-Marketing-Kampagnen unabhängig vom Ort der Konversion bewerten und diese Informationen nutzen, um die Kampagnenoptimierung zu fördern. Die [!DNL LinkedIn Conversions API] -Erweiterung kann die Leistung steigern und die Kosten pro Aktion senken, indem sie die Attribution vollständig, die Datenzuverlässigkeit verbessert und die Bereitstellung optimiert.

## Voraussetzungen {#prerequisites}

Sie müssen [eine Konversionsregel ](https://www.linkedin.com/help/lms/answer/a1657171) in Ihrem [!DNL LinkedIn Campaign Manager]-Konto erstellen. [!DNL Adobe] empfiehlt, &quot;CAPI&quot;am Anfang des Namens der Konversationsregel einzubeziehen, um sie von anderen Konversionsregeltypen abzuheben, die Sie möglicherweise konfiguriert haben.

### Erstellen eines Geheimnisses und eines Datenelements

Erstellen Sie ein neues [!DNL LinkedIn] [Ereignisweiterleitungsgeheimnis](../../../ui/event-forwarding/secrets.md) und geben Sie ihm einen eindeutigen Namen, der das authentifizierende Mitglied angibt. Dies wird verwendet, um die Verbindung zu Ihrem Konto zu authentifizieren, während der Wert sicher bleibt.

Als Nächstes erstellen Sie mit der Erweiterung [!UICONTROL Core] ein Datenelement](../../../ui/managing-resources/data-elements.md#create-a-data-element) und mit dem Datenelementtyp [!UICONTROL Secret] , um auf das soeben erstellte Geheimnis `LinkedIn` zu verweisen.[

## Installieren und Konfigurieren der [!DNL LinkedIn] -Erweiterung {#install}

Um die Erweiterung zu installieren, erstellen Sie [eine Ereignisweiterleitungs-Eigenschaft](../../../ui/event-forwarding/overview.md#properties) oder wählen Sie eine vorhandene Eigenschaft aus, die bearbeitet werden soll.

Wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation aus. Wählen Sie auf der Registerkarte **[!UICONTROL Katalog]** die Erweiterung **[!UICONTROL LinkedIn]** und dann **[!UICONTROL Installieren]** aus.

![Der Erweiterungskatalog, der die Installation der Erweiterungskarte [!DNL LinkedIn] hervorhebt.](../../../images/extensions/server/linkedin/install-extension.png)

Geben Sie im nächsten Bildschirm im Feld `Access Token` den zuvor erstellten Datenelementschlüssel ein. Das Datenelement-Geheimnis enthält Ihr [!DNL LinkedIn] OAuth 2-Token. Wählen Sie **[!UICONTROL Speichern]**, wenn Sie fertig sind.

![Die Konfigurationsseite der Erweiterung [!DNL LinkedIn] mit dem Feld [!UICONTROL Zugriffstoken] und dem Feld [!UICONTROL Speichern], hervorgehoben.](../../../images/extensions/server/linkedin/configure-extension.png)

## Erstellen einer [!DNL Send Conversion] -Regel {#tracking-rule}

Sobald alle Ihre Datenelemente eingerichtet sind, können Sie mit der Erstellung von Ereignisweiterleitungsregeln beginnen, die bestimmen, wann und wie Ihre Ereignisse an [!DNL LinkedIn] gesendet werden.

Erstellen Sie in Ihrer Ereignisweiterleitungseigenschaft eine neue Ereignisweiterleitungsregel [Regel](../../../ui/managing-resources/rules.md). Fügen Sie unter **[!UICONTROL Aktionen]** eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL LinkedIn]** fest. Wählen Sie als Nächstes **[!UICONTROL Konversion senden]** für den **[!UICONTROL Aktionstyp]** aus.

![Die Ansicht &quot;Eigenschaftsregeln für die Ereignisweiterleitung&quot;mit den Feldern, die zum Hinzufügen einer Aktionskonfiguration für die Ereignisweiterleitung erforderlich sind, hervorgehoben.](../../../images/extensions/server/linkedin/linkedin-event-action.png)

Nach der Auswahl scheinen zusätzliche Steuerelemente das Ereignis weiter zu konfigurieren. Wählen Sie **[!UICONTROL Änderungen beibehalten]** aus, um die Regel zu speichern.

**[!UICONTROL Benutzerdaten]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL E-Mail] | E-Mail-Adresse des Kontakts, der mit dem Konversionsereignis verbunden ist. Der E-Mail-Wert wird durch den Erweiterungscode in SHA256 kodiert, es sei denn, der angegebene Wert ist bereits eine SHA256-Zeichenfolge. |
| [!UICONTROL LinkedIn First Party Ads Tracking UUID] | Dies ist eine Erstanbieter-Cookie-ID. Werbetreibende müssen das erweiterte Konversions-Tracking von [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag) aktivieren, um Erstanbieter-Cookies zu aktivieren, die einen Klick-ID-Parameter `li_fat_id` an die Klick-URLs anhängen. |
| [!UICONTROL Daten zu Kundeninformationen] | Dieses Feld enthält ein JSON-Objekt mit zusätzlichen Attributen, die zusammen mit der Nachricht gesendet werden.<br><br>Unter der Option **[!UICONTROL Raw]** können Sie das JSON-Objekt direkt in das bereitgestellte Textfeld einfügen. Alternativ können Sie das Datenelementsymbol (![Datensatzsymbol](/help/images/icons/database.png)) auswählen, das aus einer Liste vorhandener Datenelemente ausgewählt werden soll, um die Daten darzustellen.<br><br>Sie können auch die Option **[!UICONTROL JSON Key-Value Paares Editor]** verwenden, um jedes Schlüssel-Wert-Paar manuell über einen UI-Editor hinzuzufügen. Jeder Wert kann durch eine Roheingabe dargestellt werden oder stattdessen kann ein Datenelement ausgewählt werden. Die zulässigen Schlüsselwerte sind: `firstName`, `lastName`, `companyName`, `title` und `country`. |

{style="table-layout:auto"}

![Der Abschnitt [!DNL User Data], der Beispieldaten in die Felder eingibt.](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL Konversionsdaten]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Konversion] | Die Kennung der Konversionsregel, die im [LinkedIn Campaign Manager](https://www.linkedin.com/help/lms/answer/a1657171) erstellt wurde. Wählen Sie die Konversionsregel aus, um die ID abzurufen, und kopieren Sie dann die ID aus der Browser-URL (z. B. `/campaignmanager/accounts/508111232/conversions/15588877`) in den Wert `/conversions/<id>`. |
| [!UICONTROL Konvertierungszeit] | Jeder Zeitstempel in Millisekunden, bei dem das Konversionsereignis eingetreten ist. <br><br> Hinweis: Wenn Ihre Quelle den Konvertierungszeitstempel in Sekunden aufzeichnet, fügen Sie am Ende bitte 000 ein, um ihn in Millisekunden umzuwandeln. |
| [!UICONTROL Währung] | Währungscode im ISO-Format. |
| [!UICONTROL Betrag] | Wert der Konvertierung in Dezimalzeichenfolge (z. B. &quot;100.05&quot;). |
| [!UICONTROL Ereignis-ID] | Die eindeutige ID, die von Werbetreibenden zur Angabe jedes Ereignisses generiert wurde. Dies ist ein optionales Feld und wird für die [Deduplizierung](https://learn.microsoft.com/en-us/linkedin/marketing/conversions/deduplication?view=li-lms-2024-02) verwendet. |

{style="table-layout:auto"}

![Der Abschnitt [!DNL Conversion Data], der Beispieldaten in den Feldern anzeigt.](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL Konfigurationsüberschreibungen]**

>NOTE
>
>Das Feld [!UICONTROL Konfigurationsüberschreibungen] ermöglicht es einem Benutzer, für jede Regel ein anderes [!DNL LinkedIn] -Zugriffstoken festzulegen, sodass jede Regel ein Zugriffstoken verwendet, das Zugriff auf verschiedene [!DNL LinkedIn] -Anzeigenkonten haben kann.

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Zugriffs-Token] | Das Zugriffs-Token [!DNL LinkedIn]. |

![Der Abschnitt [!DNL Configuration Overrides], der Beispieldateneingaben im Feld anzeigt.](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Daten mit der Ereignisweiterleitungs-Erweiterung [!DNL LinkedIn Conversions API] an [!DNL LinkedIn] gesendet werden. Weitere Informationen zu den Ereignisweiterleitungsfunktionen in [!DNL Adobe Experience Platform] finden Sie in der [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).

Weitere Informationen zum Debugging Ihrer Implementierung mithilfe des Experience Platform Debugger- und Ereignisweiterleitungs-Überwachungstools finden Sie in der [Adobe Experience Platform Debugger-Übersicht](../../../../debugger/home.md) und in der [Überwachung der Aktivitäten in der Ereignisweiterleitung](../../../ui/event-forwarding/monitoring.md).
