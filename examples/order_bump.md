A estrutura dentro de `order_bumps.product` segue igual à `product` 
```json
{
  "integration_key": "a74cf3440b21998dc78c8f35c72f",
  "started_at": "2021-08-31 11:01:44",
  "updated_at": "2021-08-31 11:02:15",
  "seller_id": "######",
  "test": true,
  "status": "paid",
  "type": "order",
  "tangible": true,
  "transaction_id": "######",
  "cart_id": "######",
  "shipping": {
    "price": 0,
    "status": "waiting_code",
    "service": "custom",
    "address": {
      "zipcode": "06763060",
      "street": "Rua Francisco Andugar Espinosa",
      "street_number": "S/N",
      "complement": "",
      "district": "Chácara Agrindus",
      "city": "Taboão da Serra",
      "estate": "SP",
      "country": "BR"
    }
  },
  "customer": {
    "name": "Solaire of Astora",
    "fake_email": false,
    "email": "test@payt.com",
    "doc": "67415765095",
    "phone": "1199999999",
    "billing_address": {
      "zipcode": "06763060",
      "street": "Rua Francisco Andugar Espinosa",
      "street_number": "S/N",
      "complement": "",
      "district": "Chácara Agrindus",
      "city": "Taboão da Serra",
      "estate": "SP",
      "country": "BR"
    }
  },
  "product": {
    "code": "JLY9B4",
    "sku": "5da418756a44e",
    "type": "digital",
    "name": "Ebook",
    "quantity": 1,
    "price": 1500
  },
  "order_bumps": [
    {
      "code": "AR6D4X",
      "name": "OrderBump 1",
      "product": {
        "code": "JL8YXL",
        "sku": "2c0f51e2521a4",
        "type": "grouped",
        "name": "Grouped Orderbump Product",
        "quantity": 1,
        "price": 16000,
        "items": [
          {
            "code": "WRBB2R",
            "sku": "392b54b0d3378",
            "name": "Physical Book",
            "type": "physical",
            "quantity": 1,
            "price": 5000
          },
          {
            "code": "BRA8AR",
            "sku": "b884e71861b2b",
            "name": "Complementary Ebook",
            "type": "digital",
            "quantity": 1,
            "price": 11000
          }
        ]
      }
    }
  ],
  "link": {
    "title": "Checkout with OrderBump Example",
    "sources": [],
    "url": "https://payt.site/######"
  },
  "transaction": {
    "created_at": "2021-08-31 11:02:15",
    "updated_at": "2021-08-31 11:02:15",
    "payment_method": "credit_card",
    "payment_status": "paid",
    "total_price": 19936,
    "quantity": 1,
    "modifiers": [],
    "installments": 8,
    "installment_price": 2492,
    "paid_at": "2021-08-31 11:02:15"
  },
  "commission": [
    {
      "name": "PAYT TECNOLOGIA E EDUCACAO DIGITAL LTDA",
      "email": "contato@payt.com.br",
      "type": "platform",
      "amount": 3111
    },
    {
      "name": "LEGAL COMPANY NAME",
      "email": "company@payt.com.br",
      "type": "producer",
      "amount": 16825
    }
  ]
}
```
