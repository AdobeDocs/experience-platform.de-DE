---
title: Stripe
description: Erfahren Sie, wie Sie Zahlungsdaten von Ihrem Stripe-Konto in Adobe Experience Platform aufnehmen
badge: Beta
exl-id: 191d217e-036d-491a-b7dd-abcad74625ba
source-git-commit: 62bcaa532cdec68a2f4f62e5784c35b91b7d5743
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 9%

---

# [!DNL Stripe]

>[!NOTE]
>
>Die [!DNL Stripe]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta[gekennzeichneten Quellen finden Sie ](../../home.md#terms-and-conditions) „Quellen - Übersicht“.

Tausende von Unternehmen aller Größenordnungen nutzen [!DNL Stripe] sowohl online als auch persönlich, um Zahlungen zu akzeptieren, neue Umsatzquellen zu erschließen und mithilfe von Adobe Experience Platform, Adobe Commerce und [!DNL Magento Open Source] global zu expandieren.

Verwenden Sie die [!DNL Stripe] in Experience Platform , um Daten aufzunehmen, die während des Kaufablaufs von Ihren Kunden erfasst werden. Verwenden Sie diese Daten nach der Aufnahme, um personalisierte Angebote zu erstellen und umfassendere geschäftliche Einblicke zu erschließen.

>[!TIP]
>
>Bei Fragen zur [!DNL Stripe] auf Experience Platform wenden Sie sich an [!DNL Stripe] unter adobe-Partnership<span>@stripe.com.

>[!BEGINSHADEBOX]

**Anwendungsbeispiel für die [!DNL Stripe]-Quelle**

Ihr Unternehmen ermöglicht es Kunden, Artikel in Ihrem Online-Shop zu kaufen mit der Option **jetzt kaufen** und **später bezahlen** (mit [!DNL Klarna], [!DNL Afterpay], [!DNL Affirm] oder [!DNL Zip]).

Verwenden Sie die [!DNL Stripe] Datenquelle, um die Verwendung von Optionen **Jetzt kaufen** und **Später bezahlen** zu analysieren und mit personalisierten Angeboten für diese Kunden zu experimentieren. Erwägen Sie zum Beispiel, Add-on-Artikel zu empfehlen, um die Anzahl der Artikel in ihrem Warenkorb vor dem Checkout zu erweitern.

>[!ENDSHADEBOX]

Lesen Sie das folgende Dokument, um Informationen darüber zu erhalten, wie Sie Ihr [!DNL Stripe]-Quellkonto einrichten, die erforderlichen Anmeldeinformationen abrufen und Ihre Schemata erstellen können.

## Voraussetzungen {#prerequisites}

In den folgenden Abschnitten finden Sie Informationen zur erforderlichen Einrichtung, die Sie vor dem Verbinden Ihres [!DNL Stripe]-Kontos mit Experience Platform durchführen müssen.

### Abrufen Ihres Zugriffs-Tokens

* Melden Sie sich mit Ihrer [!DNL Stripe] E[[!DNL Stripe] Mail-Adresse und Ihrem Passwort beim ](https://dashboard.stripe.com/login)Dashboard“ an.
* Wählen Sie im [!DNL Developers]-Dashboard **[!DNL API keys for developers]** aus.
* Wählen Sie auf **Registerkarte** API-Schlüssel“ die Option **[!DNL Reveal test key]** aus, um Ihr Zugriffs-Token anzuzeigen.
* Sie können dieses Token jetzt als Zugriffstoken verwenden, wenn Sie Ihr [!DNL Stripe]-Konto mit Experience Platform verbinden, entweder mithilfe der [!DNL Flow Service]-API oder der Experience Platform-Benutzeroberfläche.

### Sammeln erforderlicher Anmeldedaten

Um Ihr [!DNL Stripe]-Konto mit Experience Platform zu verbinden, müssen Sie Werte für die folgenden Authentifizierungsdaten angeben:

>[!BEGINTABS]

>[!TAB API]

Sie müssen die folgenden Anmeldeinformationen angeben, wenn Sie Ihr [!DNL Stripe]-Konto mit der [!DNL Flow Service]-API verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `accessToken` | Ihr [!DNL Stripe] OAuth 2-Authentifizierungstoken für aktualisierten Code. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID der [!DNL Stripe]. Diese ID lautet: `cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3`. |

>[!TAB UI]

Sie müssen die folgenden Anmeldeinformationen angeben, wenn Sie Ihr [!DNL Stripe]-Konto über die Experience Platform-Benutzeroberfläche verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Zugriffs-Token | Ihr [!DNL Stripe] OAuth 2-Authentifizierungstoken für aktualisierten Code. |

>[!ENDTABS]

Weitere Informationen zur Verwendung [!DNL Stripe] APIs finden Sie in der [[!DNL Stripe] Dokumentation zu API-Schlüsseln](https://docs.stripe.com/keys).

### Erstellen eines Experience-Datenmodell (XDM)-Schemas

Die [!DNL Stripe]-Quelle unterstützt die Aufnahme von Daten aus den folgenden Ressourcenpfaden:

* Kosten
* Abonnements
* Erstattungen
* Saldotransaktionen
* Kundinnen und Kunden
* Preise

Sie müssen ein XDM-Schema erstellen, um einen Datensatz zu beschreiben, in dem die Felder und Datentypen gespeichert werden können, die von [!DNL Stripe] an Experience Platform gesendet werden.

>[!BEGINTABS]

>[!TAB Kosten]

In [!DNL Stripe] stellen **Gebühren** Versuche dar, Geld in Ihre [!DNL Stripe] zu verschieben. Weitere Informationen zu bestimmten [[!DNL Stripe]  finden Sie ](https://docs.stripe.com/api/charges) API-Handbuch zu Gebühren .

+++Auswählen, um das Stripe-Ladeobjekt anzuzeigen

```json
{
  "id": "ch_3MmlLrLkdIwHu7ix0snN0B15",
  "object": "charge",
  "amount": 1099,
  "amount_captured": 1099,
  "amount_refunded": 0,
  "application": null,
  "application_fee": null,
  "application_fee_amount": null,
  "balance_transaction": "txn_3MmlLrLkdIwHu7ix0uke3Ezy",
  "billing_details": {
    "address": {
      "city": null,
      "country": null,
      "line1": null,
      "line2": null,
      "postal_code": null,
      "state": null
    },
    "email": null,
    "name": null,
    "phone": null
  },
  "calculated_statement_descriptor": "Stripe",
  "captured": true,
  "created": 1679090539,
  "currency": "usd",
  "customer": null,
  "description": null,
  "disputed": false,
  "failure_balance_transaction": null,
  "failure_code": null,
  "failure_message": null,
  "fraud_details": {},
  "invoice": null,
  "livemode": false,
  "metadata": {},
  "on_behalf_of": null,
  "outcome": {
    "network_status": "approved_by_network",
    "reason": null,
    "risk_level": "normal",
    "risk_score": 32,
    "seller_message": "Payment complete.",
    "type": "authorized"
  },
  "paid": true,
  "payment_intent": null,
  "payment_method": "card_1MmlLrLkdIwHu7ixIJwEWSNR",
  "payment_method_details": {
    "card": {
      "brand": "visa",
      "checks": {
        "address_line1_check": null,
        "address_postal_code_check": null,
        "cvc_check": null
      },
      "country": "US",
      "exp_month": 3,
      "exp_year": 2024,
      "fingerprint": "mToisGZ01V71BCos",
      "funding": "credit",
      "installments": null,
      "last4": "4242",
      "mandate": null,
      "network": "visa",
      "three_d_secure": null,
      "wallet": null
    },
    "type": "card"
  },
  "receipt_email": null,
  "receipt_number": null,
  "receipt_url": "https://pay.stripe.com/receipts/payment/CAcaFwoVYWNjdF8xTTJKVGtMa2RJd0h1N2l4KOvG06AGMgZfBXyr1aw6LBa9vaaSRWU96d8qBwz9z2J_CObiV_H2-e8RezSK_sw0KISesp4czsOUlVKY",
  "refunded": false,
  "review": null,
  "shipping": null,
  "source_transfer": null,
  "statement_descriptor": null,
  "statement_descriptor_suffix": null,
  "status": "succeeded",
  "transfer_data": null,
  "transfer_group": null
}
```

+++

>[!TAB Abonnements]

In [!DNL Stripe] können Sie **Abonnements** verwenden, um wiederkehrend eine Kundin oder einen Kunden zu berechnen. Weitere Informationen zu [[!DNL Stripe]  Abonnementattributen finden ](https://docs.stripe.com/api/subscriptions) im API-Handbuch Abonnements .

+++Auswählen, um das Stripe-Abonnementobjekt anzuzeigen

```json
{
  "id": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
  "object": "subscription",
  "application": null,
  "application_fee_percent": null,
  "automatic_tax": {
    "enabled": false,
    "liability": null
  },
  "billing_cycle_anchor": 1679609767,
  "billing_thresholds": null,
  "cancel_at": null,
  "cancel_at_period_end": false,
  "canceled_at": null,
  "cancellation_details": {
    "comment": null,
    "feedback": null,
    "reason": null
  },
  "collection_method": "charge_automatically",
  "created": 1679609767,
  "currency": "usd",
  "current_period_end": 1682288167,
  "current_period_start": 1679609767,
  "customer": "cus_Na6dX7aXxi11N4",
  "days_until_due": null,
  "default_payment_method": null,
  "default_source": null,
  "default_tax_rates": [],
  "description": null,
  "discount": null,
  "ended_at": null,
  "invoice_settings": {
    "issuer": {
      "type": "self"
    }
  },
  "items": {
    "object": "list",
    "data": [
      {
        "id": "si_Na6dzxczY5fwHx",
        "object": "subscription_item",
        "billing_thresholds": null,
        "created": 1679609768,
        "metadata": {},
        "plan": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "plan",
          "active": true,
          "aggregate_usage": null,
          "amount": 1000,
          "amount_decimal": "1000",
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "interval": "month",
          "interval_count": 1,
          "livemode": false,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "tiers_mode": null,
          "transform_usage": null,
          "trial_period_days": null,
          "usage_type": "licensed"
        },
        "price": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "price",
          "active": true,
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "custom_unit_amount": null,
          "livemode": false,
          "lookup_key": null,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "recurring": {
            "aggregate_usage": null,
            "interval": "month",
            "interval_count": 1,
            "trial_period_days": null,
            "usage_type": "licensed"
          },
          "tax_behavior": "unspecified",
          "tiers_mode": null,
          "transform_quantity": null,
          "type": "recurring",
          "unit_amount": 1000,
          "unit_amount_decimal": "1000"
        },
        "quantity": 1,
        "subscription": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
        "tax_rates": []
      }
    ],
    "has_more": false,
    "total_count": 1,
    "url": "/v1/subscription_items?subscription=sub_1MowQVLkdIwHu7ixeRlqHVzs"
  },
  "latest_invoice": "in_1MowQWLkdIwHu7ixuzkSPfKd",
  "livemode": false,
  "metadata": {},
  "next_pending_invoice_item_invoice": null,
  "on_behalf_of": null,
  "pause_collection": null,
  "payment_settings": {
    "payment_method_options": null,
    "payment_method_types": null,
    "save_default_payment_method": "off"
  },
  "pending_invoice_item_interval": null,
  "pending_setup_intent": null,
  "pending_update": null,
  "quantity": 1,
  "schedule": null,
  "start_date": 1679609767,
  "status": "active",
  "test_clock": null,
  "transfer_data": null,
  "trial_end": null,
  "trial_settings": {
    "end_behavior": {
      "missing_payment_method": "create_invoice"
    }
  },
  "trial_start": null
}
```

+++

>[!TAB Erstattungen]

In [!DNL Stripe] können Sie &quot;**&quot; verwenden** um eine zuvor erstellte Gebühr zurückzuerstatten. Lesen Sie das [[!DNL Stripe] API-Handbuch zu Rückerstattungen](https://docs.stripe.com/api/refunds) für weitere Informationen zu bestimmten Rückerstattungsattributen.

+++Auswählen, um das Stripe-Rückerstattungsobjekt anzuzeigen

```json
{
  "id": "re_1Nispe2eZvKYlo2Cd31jOCgZ",
  "object": "refund",
  "amount": 1000,
  "balance_transaction": "txn_1Nispe2eZvKYlo2CYezqFhEx",
  "charge": "ch_1NirD82eZvKYlo2CIvbtLWuY",
  "created": 1692942318,
  "currency": "usd",
  "destination_details": {
    "card": {
      "reference": "123456789012",
      "reference_status": "available",
      "reference_type": "acquirer_reference_number",
      "type": "refund"
    },
    "type": "card"
  },
  "metadata": {},
  "payment_intent": "pi_1GszsK2eZvKYlo2CfhZyoZLp",
  "reason": null,
  "receipt_number": null,
  "source_transfer_reversal": null,
  "status": "succeeded",
  "transfer_reversal": null
}
```

+++

>[!TAB Saldotransaktionen]

[!DNL Stripe] stellen **Saldotransaktionen** die Geldbewegung zwischen Ihren [!DNL Stripe] dar. Weitere [[!DNL Stripe]  zu bestimmten Saldotransaktionsattributen finden ](https://docs.stripe.com/api/balance_transactions) im API-Handbuch zu Saldotransaktionen .

+++Wählen Sie diese Option, um das Stripe-Saldo-Transaktionsobjekt anzuzeigen.

```json
{
  "id": "txn_1MiN3gLkdIwHu7ixxapQrznl",
  "object": "balance_transaction",
  "amount": -400,
  "available_on": 1678043844,
  "created": 1678043844,
  "currency": "usd",
  "description": null,
  "exchange_rate": null,
  "fee": 0,
  "fee_details": [],
  "net": -400,
  "reporting_category": "transfer",
  "source": "tr_1MiN3gLkdIwHu7ixNCZvFdgA",
  "status": "available",
  "type": "transfer"
}
```

+++

>[!TAB Kunden]

In [!DNL Stripe] repräsentieren **Kunden** einen bestimmten Kunden Ihres Unternehmens. Informationen zu bestimmten Kundenattributen finden Sie im [[!DNL Stripe] API-Handbuch für Kunden](https://docs.stripe.com/api/customers) für weitere Informationen zu bestimmten Kundenattributen.

+++Auswählen, um das Stripe-Kundenobjekt anzuzeigen

```json
{
  "id": "cus_NffrFeUfNV2Hib",
  "object": "customer",
  "address": null,
  "balance": 0,
  "created": 1680893993,
  "currency": null,
  "default_source": null,
  "delinquent": false,
  "description": null,
  "discount": null,
  "email": "jennyrosen@example.com",
  "invoice_prefix": "0759376C",
  "invoice_settings": {
    "custom_fields": null,
    "default_payment_method": null,
    "footer": null,
    "rendering_options": null
  },
  "livemode": false,
  "metadata": {},
  "name": "Jenny Rosen",
  "next_invoice_sequence": 1,
  "phone": null,
  "preferred_locales": [],
  "shipping": null,
  "tax_exempt": "none",
  "test_clock": null
}
```

+++

>[!TAB Preise]

[!DNL Stripe] stellen **Preise** die Stückkosten, die Währung und den optionalen Abrechnungszyklus sowohl für wiederkehrende als auch für einmalige Käufe von Produkten dar. Weitere Informationen zu [[!DNL Stripe]  Preisattributen finden ](https://docs.stripe.com/api/prices) im „API-Handbuch Preise“.

+++Auswählen, um das Stripe-Preisobjekt anzuzeigen

```json
{
  "id": "price_1MoBy5LkdIwHu7ixZhnattbh",
  "object": "price",
  "active": true,
  "billing_scheme": "per_unit",
  "created": 1679431181,
  "currency": "usd",
  "custom_unit_amount": null,
  "livemode": false,
  "lookup_key": null,
  "metadata": {},
  "nickname": null,
  "product": "prod_NZKdYqrwEYx6iK",
  "recurring": {
    "aggregate_usage": null,
    "interval": "month",
    "interval_count": 1,
    "trial_period_days": null,
    "usage_type": "licensed"
  },
  "tax_behavior": "unspecified",
  "tiers_mode": null,
  "transform_quantity": null,
  "type": "recurring",
  "unit_amount": 1000,
  "unit_amount_decimal": "1000"
}
```

+++

>[!ENDTABS]


### IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

### Konfigurieren von Berechtigungen auf Experience Platform

Sie müssen sowohl **[!UICONTROL Quellen anzeigen]** als auch **[!UICONTROL Quellen verwalten]** für Ihr Konto aktiviert haben, um Ihr [!DNL Stripe]-Konto mit Experience Platform zu verbinden. Wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten. Weitere Informationen finden Sie im [Handbuch zur Benutzeroberfläche der Zugriffssteuerung](../../../access-control/ui/overview.md).

## Nächste Schritte

Nachdem Sie die erforderliche Einrichtung abgeschlossen haben, können Sie fortfahren, eine Verbindung herzustellen und Ihre [!DNL Stripe] Daten auf Experience Platform aufzunehmen. Lesen Sie die folgenden Handbücher, um zu erfahren, wie Sie [!DNL Stripe] Zahlungsdaten mithilfe von APIs oder der Benutzeroberfläche auf Experience Platform aufnehmen:

* [Nehmen Sie Zahlungsdaten von Ihrem Stripe-Konto mithilfe der Flow Service-API auf Experience Platform auf](../../tutorials/api/create/payments/stripe.md).
* [Nehmen Sie Zahlungsdaten von Ihrem Stripe-Konto über die Benutzeroberfläche auf Experience Platform auf](../../tutorials/ui/create/payments/stripe.md).
