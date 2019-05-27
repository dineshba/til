#### Partial Index in DB

We can have partial index on table based on the value

#### Examle and usecase:
Let take the Payments table

|id | user_id | amount  | date      | is_settled   |
|---|:---:    |:---:    |:---:      |:---:           |
|  1|   1     |  100    |2017/10/01 | true         |
|  2|   1     |  200    |2017/10/02 | true         |
|  3|   1     |  300    |2017/10/03 | false        |

Mostly we will query for **not settled payments**. In this case we can a partial index query for non-settled payments

```psql
CREATE INDEX payments_index ON payments (id)
    WHERE is_settled is NOT TRUE;
```

This will **increase the performance of non settled payments** which is our use case 