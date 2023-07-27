Salesforce ORM

```python
from typing import Annotated

from salesforce_orm import SalesforceModel, Field, generate_permission_set
from salesforce_orm.standard_objects import Account, Contact


class Invoice(SalesforceModel):
    __salesforce_object_name__ = "Invoice__c"

    db_id: Annotated[str, Field("DB_Id__c", external_id=True)]
    amount: Annotated[int, Field("Amount__c")]


invoice = Invoice(db_id="123", amount=100)
invoice.upsert(invoice.db_id)
print(invoice.id)


generate_permission_set([Account, Contact, Invoice]).to_file(
    "Integration_User.permissionset-meta.xml"
)
```
