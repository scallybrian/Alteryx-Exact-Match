# Alteryx-Exact-Match
 Alteryx macro for non-fuzzy matching on pairs of keys

The *Exact Match* macro enables the user to join a dataset to itself based on multiple pairs of primary keys specified in the dataset.

[Use case - customer record data](https://www.notion.so/ad4f9efda24d440f8fcebb067e755547)

We have a customer dataset and we suspect that there is duplication. The same customer seems to appear in more than one record with varying levels of information:

- Sometimes the name and email matches (C001 & C002)
- Sometimes the name and phone number matches (C001 & C003)
- Sometimes the email and phone number matches (C001 & C004)

If two or more identifying fields match across two records, we can be fairly confident that the records refer to the same person.

We could bridge these records together by doing three separate joins on the different pairs of primary keys (name & email, name & phone number, email & phone number). The *Exact Match* macro allows these joins to be performed in a single tool. It subsequently identifies groups of IDs and outputs a mapping of the record IDs to a parent ID field.

### Using the macro

**Input data:** As shown in the example table above, all records that you want to join should be in one single table (akin to *Purge* mode in the *Fuzzy Matching* tool). The dataset should have an ID field and two or more primary keys that you want to match with.

**Macro interface:**

**Name of ID field:** This is the name of the ID field in your dataset.

**Specify two or more primary keys (comma-separated list):** A comma-separated list of the fields from your dataset that you wish to use as primary keys for the joins.

**[Optional] Specify mandatory primary keys for all joins (comma-separated list):** Enter any primary keys that must be included in all joins performed. In the below example, all joins must include the *Name* field as a primary key. A join on Name & Email and Name & Phone will be performed, but the join on Email & Phone will be omitted. Left blank

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1896439c-af23-463b-9c8d-2d66e49aed82/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1896439c-af23-463b-9c8d-2d66e49aed82/Untitled.png)

### Macro Outputs

**Joined (J):** This output returns all joined ID codes and the pair of primary keys that was used to successfully join them together. 

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3e83b76b-ca55-4e03-b6eb-b0c994c8cc9f/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3e83b76b-ca55-4e03-b6eb-b0c994c8cc9f/Untitled.png)

**Groups (G):** This output returns the original ID field and a Group ID field which identifies records that have been grouped together by the join procedures. If no group is identified for a record, the Group ID field will inherit the original ID.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/52968279-94a9-4a6b-9bca-311ef44edcfe/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/52968279-94a9-4a6b-9bca-311ef44edcfe/Untitled.png)
