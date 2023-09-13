#  Do the following docker and sql related tasks.

- Use this dataset: https://raw.githubusercontent.com/erkansirin78/datasets/master/retail_db/customers.csv
```console 

## 1. 
- Create a docker-compose.yaml file that creates mysql and postgresql containers.

## 2. 
- Create (on both mysql and postgresql) **dataops** db and **dataops_user** user. Grant `dataops_user`with full permissions on `dataops` database.

## 3. 
- Create a table in `dataops` db then insert first 5 rows of dataset to **customer** table.

## 4. 
- Update customerId 3 customerLName Smith as Fox.

## 5. 
- Delete customerId 5 (Robert Hudson).

## 6. 
- SELECT customerFName, customerStreet,customerCity,customerState,customerZipcode where the customerFName is Marry.
