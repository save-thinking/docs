User

- name
- sheet url
- clients

Client

- last_sync

Accounts (ABC)

- name
- fund_type : INTERNAL | EXTERNAL
- archived

Internal Source extends (Accounts)

- type
- balance
- created
- updated

External Source extends (Accounts)

- type
- parent

Transaction
- type : INCOME | EXPENSE | TRANSFER
- created
- updated
- note
- source_fund_id fk
- destination_fund_id fk
- amount
- currency
- tag_id fk

Tag

- name
