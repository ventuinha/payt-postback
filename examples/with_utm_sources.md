A parte importante está em link->sources

ele também aceita o parametro `src`

  

```json
{
  "integration_key": "a74cf3440b21998dc78c8f35c72f124e",
  "cart_id": "RW3NPR",
  "started_at": "2020-07-10 13:59:46",
  "updated_at": "2020-07-10 14:00:17",
  "seller_id": "AR6D4X",
  "test": false,
  "status": "paid",
  "type": "order",
  "tangible": true,
  "transaction_id": "R3NYZR",
  "shipping": {
    "price": 0,
    "status": "waiting_code",
    "service": "custom",
    "address": {
      "zipcode": "06763060",
      "street": "Rua Francisco Andugar Espinosa",
      "street_number": "999",
      "complement": "",
      "district": "Chácara Agrindus",
      "city": "Taboão da Serra",
      "estate": "SP",
      "country": "BR"
    }
  },
  "customer": {
    "name": "Solaire of Astoraz",
    "fake_email": false,
    "email": "test@payt.com",
    "doc": "67415765095",
    "phone": "+551199999999",
    "billing_address": {
      "zipcode": "06763060",
      "street": "Rua Francisco Andugar Espinosa",
      "street_number": "999",
      "complement": "",
      "district": "Chácara Agrindus",
      "city": "Taboão da Serra",
      "estate": "SP",
      "country": "BR"
    }
  },
  "product": {
    "code": "9RKD4M",
    "sku": "0001",
    "type": "physical",
    "name": "Shadowrun: Livro Básico 5ª Edição",
    "quantity": 1,
    "price": 15193
  },
  "link": {
    "title": "Shadowrun 5ª Edição",
    "url": "http://stonks.otm/f457c545a9ded88f18ecee47145a72c0",
    "sources": {
      "utm_source": "localhost",
      "utm_medium": "postback",
      "utm_campaign": "testing_sources",
      "utm_term": "local",
      "utm_content": "host"
    }
  },
  "transaction": {
    "created_at": "2020-07-10 14:00:17",
    "updated_at": "2020-07-10 14:00:17",
    "payment_method": "credit_card",
    "payment_status": "paid",
    "total_price": 15193,
    "quantity": 1,
    "modifiers": [],
    "installments": 1,
    "installment_price": 15193,
    "paid_at": "2020-07-10 14:00:17"
  }
}
```