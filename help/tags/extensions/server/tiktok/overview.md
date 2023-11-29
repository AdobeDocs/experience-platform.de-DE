---
title: Integration der Adobe TikTok Web Events API
description: Mit dieser Adobe Experience Platform-Web-Events-API können Sie Website-Interaktionen direkt mit TikTok teilen.
last-substantial-update: 2023-09-26T00:00:00Z
source-git-commit: d8b7006ade1dc82fdd79b7ed744c021bc304bca7
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 5%

---

# [!DNL TikTok] Übersicht über die Web Events API-Erweiterung

Die [!DNL TikTok] Ereignis-API ist sicher [Edge Network Server-API](/help/server-api/overview.md) -Benutzeroberfläche, über die Sie Informationen für [!DNL TikTok] direkt über Benutzeraktionen auf Ihren Websites. Sie können die Ereignisweiterleitungsregeln nutzen, um Daten aus dem [!DNL Adobe Experience Platform Edge Network] nach [!DNL TikTok] durch Verwendung von [!DNL TikTok] Web Events API-Erweiterung.

## Voraussetzungen für [!DNL TikTok] {#prerequisites}

So konfigurieren Sie die [!DNL TikTok] Web-Events-API zur Verwendung der [!DNL TikTok] Ereignis-API erstellen, müssen Sie eine [!DNL TikTok] Pixelcode und Zugriffstoken.

Sie müssen über gültige [!DNL TikTok] für Geschäftskonten, um eine [!DNL TikTok] Pixel unter Verwendung der Partner-Einrichtung. Navigieren Sie zu [[!DNL TikTok] für die Registrierungsseite für Unternehmen](https://www.tiktok.com/business/en-US/solutions/business-account) , um sich zu registrieren und ein Konto zu erstellen, falls Sie noch kein Konto haben.

Sie müssen bei Ihrem Geschäftskonto angemeldet sein, um [!DNL TikTok] Pixel bei der Partnereinrichtung. Gehen Sie dazu wie folgt vor:

1. Navigieren Sie zum **[!UICONTROL Assets]** Registerkarte und wählen Sie **[!UICONTROL Ereignis]**.
2. Wählen Sie unter &quot;Web Events&quot;die Option **[!UICONTROL Verwalten]**.
3. Auswählen **[!UICONTROL Webereignisse einrichten]**.
4. Auswählen **[!UICONTROL Partnereinrichtung]** als Verbindungsmethode.

Siehe [Erste Schritte mit Pixel](https://ads.tiktok.com/help/article/get-started-pixel) Anleitung für weitere Informationen zum Einrichten der [!DNL TikTok] Pixel.

Sie können ein Zugriffstoken generieren, sobald das Pixel erfolgreich erstellt wurde. Navigieren Sie dazu zum Pixel und wählen Sie die **[!UICONTROL Einstellungen]** Registerkarte. Wählen Sie unter &quot;Events API&quot; **[!UICONTROL Zugriffstoken generieren]**.

Siehe [[!DNL TikTok] Erste Schritte](https://business-api.tiktok.com/portal/docs?id=1739584855420929) für weitere Informationen zum Einrichten des Pixel-Codes und Zugriffs-Tokens.

## Installieren und konfigurieren Sie die [!DNL TikTok] Web Events API-Erweiterung {#install}

Um die Erweiterung zu installieren, wählen Sie **[!UICONTROL Erweiterungen]** in der linken Navigation. Im **[!UICONTROL Katalog]** auswählen, wählen Sie die **[!UICONTROL TikTok Web Events API-Erweiterung]** und wählen Sie **[!UICONTROL Installieren]**.

![Der Erweiterungskatalog, der die [!DNL TikTok] Erweiterungskartenmarkierung.](../../../images/extensions/server/tiktok/install-extension.png)

Geben Sie im nächsten Bildschirm die folgenden Konfigurationswerte ein, die Sie zuvor aus [!DNL TikTok] Anzeigen-Manager:

* **[!UICONTROL Pixelcode]**
* **[!UICONTROL Zugriffs-Token]**

Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![[!DNL TikTok] Konfigurationsbildschirm für [!DNL TikTok] Web-Events-API-Erweiterung.](../../../images/extensions/server/tiktok/configure.png)

## Konfigurieren einer Ereignisweiterleitungsregel {#config-rule}

Sobald alle Ihre Datenelemente eingerichtet sind, können Sie mit der Erstellung von Ereignisweiterleitungsregeln beginnen, die bestimmen, wann und wie Ihre Ereignisse an gesendet werden [!DNL TikTok].

Erstellen Sie eine neue [Regel](../../../ui/managing-resources/rules.md) in Ihrer Ereignisweiterleitungseigenschaft. under **[!UICONTROL Aktionen]**, fügen Sie eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL TikTok Web Events API-Erweiterung]**. So senden Sie Edge Network-Ereignisse an [!DNL TikTok], legen Sie die **[!UICONTROL Aktionstyp]** nach **[!UICONTROL TikTok Web Events API-Ereignis senden].**

![Die [!UICONTROL TikTok Web Events API-Ereignis senden] Aktionstyp, der für eine [!DNL TikTok] in der Datenerfassungs-Benutzeroberfläche.](../../../images/extensions/server/tiktok/select-action.png)

Nach der Auswahl scheinen zusätzliche Steuerelemente das Ereignis weiter zu konfigurieren, wie unten beschrieben. Wählen Sie nach Abschluss **[!UICONTROL Änderungen beibehalten]** , um die Regel zu speichern.

**[!UICONTROL Web-Ereignisse und -Parameter]**

Web-Ereignisse und -Parameter enthalten allgemeine Informationen zum Ereignis. Standardereignisse werden in allen [!DNL TikTok] Integrations-Tools und können für die Berichterstellung , die Optimierung für Konversionen und die Erstellung von Zielgruppen verwendet werden.

| Eingabe | Beschreibung |
| --- | --- |
| Ereignisname | Der Name des Ereignisses. Dies sind Aktionen mit vordefinierten Namen, die von [!DNL TikTok] und ist ein erforderliches Feld. Siehe Abschnitt [[!DNL TikTok] Marketing-API](https://business-api.tiktok.com/portal/docs?id=1741601162187777) Dokumentation finden Sie weitere Informationen zu unterstützten Ereignissen. |
| Ereigniszeit | Datum/Uhrzeit als Zeichenfolge in ISO 8601 oder in yyy-MM-dd&#39;T&#39;HH:mm:Format ss:SSSZ . Dies ist ein erforderliches Feld. |
| Ereignis-ID | Die eindeutige ID, die von Advertisern zur Angabe jedes Ereignisses generiert wurde. Dies ist ein optionales Feld, das zur Deduplizierung verwendet wird. |

{style="table-layout:auto"}

![Die [!DNL Web Events and Parameters] -Abschnitt mit Beispieldaten in die Felder.](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL Benutzerkontextparameter]**

Benutzerkontextparameter enthalten Kundeninformationen, mit denen Webbesucherereignisse mit [!DNL TikTok] Benutzer. Durch die Einbeziehung mehrerer Typen von übereinstimmenden Daten können Sie die Genauigkeit von Targeting- und Optimierungsmodellen erhöhen.

| Eingabe | Beschreibung |
| --- | --- |
| IP-Adresse | Öffentliche IP-Adresse des Browsers ohne Hash. IPv4- und IPv6-Adressen werden unterstützt. Sowohl die vollständige als auch die komprimierte Form von IPv6-Adressen werden erkannt. |
| Benutzeragent | Der Benutzeragent ohne Hash vom Gerät des Benutzers. |
| E-Mail | E-Mail-Adresse des Kontakts, der mit dem Konversionsereignis verbunden ist. |
| Telefon | Die Telefonnummer muss das Format E164 aufweisen [+][Ländercode].[Bereichscode][local phone number] vor dem Hashing. |
| Cookie-ID | Wenn Sie das Pixel SDK verwenden, wird automatisch eine eindeutige Kennung im `_ttp` Cookie, wenn Cookies aktiviert sind. Die `_ttp` -Wert extrahiert und für dieses Feld verwendet werden. |
| Externe ID | Jede eindeutige Kennung wie Benutzer-IDs, externe Cookie-IDs usw. muss mit SHA256 gehasht werden. |
| TikTok-Klick-ID | Die `ttclid` , die bei jeder Auswahl einer Werbung auf der Landingpage zur URL der Landingpage hinzugefügt wird [!DNL TikTok]. |
| „Seiten-URL“ | Die Seiten-URL zum Zeitpunkt des Ereignisses. |
| Seiten-Referrer-URL | Die URL der verweisenden Seite. |

{style="table-layout:auto"}

![Die [!DNL User Context Parameters] -Abschnitt mit Beispieldaten in die Felder.](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL Eigenschaftenparameter]**

Verwenden Sie die Eigenschaftenparameter, um zusätzliche unterstützte Eigenschaften zu konfigurieren.

| Eingabe | Beschreibung |
| --- | --- |
| Preis | Die Kosten eines einzelnen Artikels. |
| Menge | Die Anzahl der Artikel, die im Ereignis gekauft werden. Hierbei muss es sich um eine positive Zahl größer als 0 handeln. |
| Content-Typ | Ein Wert von `product` oder `product_group` muss der Objekteigenschaft content_type zugewiesen sein, je nachdem, wie Sie Ihren Daten-Feed bei der Einrichtung Ihres Produktkatalogs konfigurieren. |
| Inhalts-ID | Eine eindeutige Kennung des Produktelements. |
| Inhaltskategorie | Kategorie der Seite/des Produkts. |
| Inhaltsname | Name der Seite/des Produkts. |
| Währung | Die Währung der Artikel, die im Ereignis gekauft werden. Dies wird in ISO-4217 ausgedrückt. |
| Wert | Der Gesamtpreis der Bestellung. Dieser Wert entspricht dem Preis * der Menge. |
| Beschreibung | Eine Beschreibung des Elements oder der Seite. |
| Abfrage | Die Textzeichenfolge, die zum Nachschlagen eines Produkts verwendet wurde. |
| Status | Der Status einer Bestellung, eines Artikels oder eines Dienstes. Beispiel: &quot;gesendet&quot;. |

{style="table-layout:auto"}

![Die [!DNL Properties Parameters] -Abschnitt mit Beispieldaten in die Felder.](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## Ereignis-Deduplizierung {#deduplication}

[!DNL TikTok] Pixel müssen für die Deduplizierung eingerichtet werden, wenn Sie beide [!DNL TikTok] Pixel-SDK und die [!DNL TikTok] Web-Events-API-Erweiterung zum Senden derselben Ereignisse an [!DNL TikTok].

Eine Deduplizierung ist nicht erforderlich, wenn vom Client und vom Server unterschiedliche Ereignistypen gesendet werden, die sich nicht überschneiden. Um sicherzustellen, dass Ihre Berichterstellung nicht negativ beeinflusst wird, müssen Sie sicherstellen, dass jedes einzelne Ereignis, das von der [!DNL TikTok] Pixel-SDK und die [!DNL TikTok] Web-Events-API-Erweiterung wird dedupliziert.

Stellen Sie beim Senden freigegebener Ereignisse sicher, dass jedes Ereignis eine Pixel-ID, Ereignis-ID und einen Namen enthält. Duplizierte Ereignisse, die innerhalb von fünf Minuten aufeinander folgen, werden zusammengeführt. Wenn das Datenfeld beim ersten Ereignis fehlte, wird es mit dem nachfolgenden Ereignis kombiniert. Alle doppelten Ereignisse, die innerhalb von 48 Stunden empfangen wurden, werden entfernt.

Siehe [!DNL TikTok] Dokumentation zu [Ereignisdeduplizierung](https://ads.tiktok.com/help/article/event-deduplication) Weitere Informationen zu diesem Prozess.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie serverseitige Ereignisdaten an senden [!DNL TikTok] mithilfe der [!DNL TikTok] Web-Events-API-Erweiterung. Weitere Informationen zu den Ereignisweiterleitungsfunktionen finden Sie unter [!DNL Adobe Experience Platform], siehe [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
