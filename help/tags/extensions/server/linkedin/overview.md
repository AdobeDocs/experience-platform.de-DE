---
title: LinkedIn Conversions API Event Forwarding-Erweiterung
description: Mit dieser Adobe Experience Platform-Ereignisweiterleitungserweiterung können Sie die Leistung Ihrer LinkedIn-Marketingkampagne messen.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 411e7b77-081e-4139-ba34-04468e519ea5
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 4%

---

# [!DNL LinkedIn]-Konversions-API-Erweiterung

[[!DNL LinkedIn Conversions API]](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api) ist ein Konversions-Tracking-Tool, das eine direkte Verbindung zwischen Marketingdaten von einem Advertiser-Server und [!DNL LinkedIn]. Dadurch können Advertiser die Effektivität ihrer [!DNL LinkedIn] Marketing-Kampagnen unabhängig vom Ort der Konversion verwenden und diese Informationen nutzen, um die Kampagnenoptimierung zu fördern. Die [!DNL LinkedIn Conversions API] Die -Erweiterung kann die Leistung steigern und die Kosten pro Aktion senken, indem sie die Attribution vollständig, die Datenzuverlässigkeit verbessert und die Bereitstellung optimiert.

## Voraussetzungen {#prerequisites}

Sie müssen eine Konversionsregel in Ihrer [!DNL LinkedIn] Kampagnenanzeigenkonto. [!DNL Adobe] empfiehlt, &quot;CAPI&quot;am Anfang des Konversationsregelnamens einzufügen, um ihn von anderen Konversionsregeltypen abzuheben, die Sie möglicherweise konfiguriert haben.

### Erstellen eines Geheimnisses und eines Datenelements

Erstellen Sie eine neue [!DNL LinkedIn] [Ereignisweiterleitungsgeheimnis](../../../ui/event-forwarding/secrets.md) und geben Sie ihm einen eindeutigen Namen, der das authentifizierende Mitglied angibt. Dies wird verwendet, um die Verbindung zu Ihrem Konto zu authentifizieren, während der Wert sicher bleibt.

Als Nächstes [Datenelement erstellen](../../../ui/managing-resources/data-elements.md#create-a-data-element) mithilfe der [!UICONTROL Core] Erweiterung und [!UICONTROL Geheimnis] Datenelementtyp zum Referenzieren der `LinkedIn` geheim, das Sie gerade erstellt haben.

## Installieren und konfigurieren Sie die [!DNL LinkedIn] Erweiterung {#install}

So installieren Sie die Erweiterung: [Erstellen einer Ereignisweiterleitungs-Eigenschaft](../../../ui/event-forwarding/overview.md#properties) oder wählen Sie eine vorhandene Eigenschaft aus, die bearbeitet werden soll.

Wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation aus. Im **[!UICONTROL Katalog]** auswählen, wählen Sie die **[!UICONTROL LinkedIn]** Erweiterung und wählen Sie **[!UICONTROL Installieren]**.

![Der Erweiterungskatalog, der die [!DNL LinkedIn] Erweiterungskartenmarkierung.](../../../images/extensions/server/linkedin/install-extension.png)

Geben Sie im nächsten Bildschirm den zuvor erstellten Datenelementschlüssel in das Feld `Access Token` -Feld. Das Datenelement-Geheimnis enthält Ihre [!DNL LinkedIn] OAuth 2-Token. Wählen Sie **[!UICONTROL Speichern]**, wenn Sie fertig sind.

![Die [!DNL LinkedIn] Erweiterungskonfigurationsseite mit [!UICONTROL Zugriffstoken] und [!UICONTROL Speichern] hervorgehoben.](../../../images/extensions/server/linkedin/configure-extension.png)

## Erstellen Sie eine [!DNL Send Conversion] Regel {#tracking-rule}

Sobald alle Ihre Datenelemente eingerichtet sind, können Sie mit der Erstellung von Ereignisweiterleitungsregeln beginnen, die bestimmen, wann und wie Ihre Ereignisse an gesendet werden [!DNL LinkedIn].

Neue Ereignisweiterleitung erstellen [Regel](../../../ui/managing-resources/rules.md) in Ihrer Ereignisweiterleitungseigenschaft. under **[!UICONTROL Aktionen]**, fügen Sie eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL LinkedIn]**. Wählen Sie als Nächstes **[!UICONTROL Web-Konversion senden]** für die **[!UICONTROL Aktionstyp]**.

![Die Ansicht &quot;Eigenschaftsregeln für die Ereignisweiterleitung&quot;mit den Feldern, die zum Hinzufügen einer Aktionskonfiguration für Ereignisweiterleitungsregeln erforderlich sind, hervorgehoben.](../../../images/extensions/server/linkedin/linkedin-event-action.png)

Nach der Auswahl scheinen zusätzliche Steuerelemente das Ereignis weiter zu konfigurieren. Auswählen **[!UICONTROL Änderungen beibehalten]** , um die Regel zu speichern.

**[!UICONTROL Benutzerdaten]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL E-Mail] | E-Mail-Adresse des Kontakts, der mit dem Konversionsereignis verbunden ist. Der E-Mail-Wert wird durch den Erweiterungscode in SHA256 kodiert, es sei denn, der angegebene Wert ist bereits eine SHA256-Zeichenfolge. |
| [!UICONTROL LinkedIn-UUID zur Verfolgung von Erstanbieteranzeigen] | Dies ist eine Erstanbieter-Cookie-ID. Werbetreibende müssen das erweiterte Konversions-Tracking aktivieren von [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag) , um Erstanbieter-Cookies zu aktivieren, die einen Klick-ID-Parameter anhängen `li_fat_id` zu den Klick-URLs. |
| [!UICONTROL Kundeninformationsdaten] | Dieses Feld enthält ein JSON-Objekt mit zusätzlichen Attributen, die zusammen mit der Nachricht gesendet werden.<br><br>Unter dem **[!UICONTROL Roh]** können Sie das JSON-Objekt direkt in das bereitgestellte Textfeld einfügen oder das Datenelementsymbol (![Datensatzsymbol](../../../images/extensions/server/aws/data-element-icon.png)), um aus einer Liste vorhandener Datenelemente zur Darstellung der Daten auszuwählen.<br><br>Sie können auch die **[!UICONTROL JSON-Schlüssel-Wert-Paare-Editor]** Option zum manuellen Hinzufügen jedes Schlüssel-Wert-Paares über einen UI-Editor. Jeder Wert kann durch eine Roheingabe dargestellt werden oder stattdessen kann ein Datenelement ausgewählt werden. Die zulässigen Schlüsselwerte sind: `firstName`, `lastName`, `companyName`, `title` und `country`. |

{style="table-layout:auto"}

![Die [!DNL User Data] -Abschnitt mit Beispieldaten in die Felder.](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL Konversionsdaten]**

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Konversion] | Die ID der Konversionsregel, die in [LinkedIn Campaign Manager](https://www.linkedin.com/help/lms/answer/a1657171) oder [!DNL LinkedIn Campaign Manager]. |
| [!UICONTROL Konvertierungszeit] | Jeder Zeitstempel in Millisekunden, bei dem das Konversionsereignis eingetreten ist. <br><br> Hinweis: Wenn Ihre Quelle den Konvertierungszeitstempel in Sekunden aufzeichnet, fügen Sie am Ende 000 ein, um ihn in Millisekunden umzuwandeln. |
| [!UICONTROL Währung] | Währungscode im ISO-Format. |
| [!UICONTROL Stärke] | Wert der Konvertierung in Dezimalzeichenfolge (z. B. &quot;100.05&quot;). |
| [!UICONTROL Ereignis-ID] | Die eindeutige ID, die von Werbetreibenden zur Angabe jedes Ereignisses generiert wurde. Dies ist ein optionales Feld, das zur Deduplizierung verwendet wird. |

{style="table-layout:auto"}

![Die [!DNL Conversion Data] -Abschnitt mit Beispieldaten in den Feldern.](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL Konfigurationsüberschreibungen]**

>HINWEIS
>
>Die [!UICONTROL Konfigurationsüberschreibungen] kann ein Benutzer eine andere [!DNL LinkedIn] Zugriffstoken für jede Regel, sodass jede Regel ein Zugriffstoken verwendet, das Zugriff auf verschiedene [!DNL LinkedIn] Anzeigenkonten.

| Eingabe | Beschreibung |
| --- | --- |
| [!UICONTROL Zugriffs-Token] | Die [!DNL LinkedIn] Zugriffstoken. |

![Die [!DNL Configuration Overrides] -Abschnitt mit Beispieldateneingaben im Feld.](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Daten an [!DNL LinkedIn] mithilfe der [!DNL LinkedIn Conversions API] Ereignisweiterleitungserweiterung. Weitere Informationen zu den Ereignisweiterleitungsfunktionen finden Sie unter [!DNL Adobe Experience Platform], siehe [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
