NoSQL, also referred to as “not only SQL”, “non-SQL”, is **an approach to [[database]] design that enables the storage and querying of data outside the traditional structures found in [[Relationsal Database ManagementSystem]]**

This will update one row to [[MongoDB]] and insert if not exists.

```python
from pymongo import MongoClient
db =  MongoClient(HOST,27017).collection_name
db.table_name.update_one({"_id":json["_id"]},{"$set":json},upsert=True)
```

~~~python
cursor=db.indeed_search_results_html.find({"field_name":equals})
for document in cursor:
	...
~~~