User

- name
- sheet url
- clients

Client

- last_sync

Accounts (ABC)

- name
- fund_type : INTERNAL | EXTERNAL
- balance
- created
- updated
- archived

Internal Source extends (Accounts)

- type

External Source extends (Accounts)

- type
- parent

Transaction

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
