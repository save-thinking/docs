# Storage framework

Contents:

* [Summary](#summary)
  * [Issue](#issue)
  * [Decision](#decision)
  * [Status](#status)
* [Details](#details)
  * [Assumptions](#assumptions)
  * [Constraints](#constraints)
  * [Positions](#positions)
  * [Argument](#argument)
* [Related](#related)
  * [Related decisions](#related-decisions)
  * [Related requirements](#related-requirements)
* [Notes](#notes)


## Summary


### Issue

We want to use a client-side storage for our web application:

  * We want our application to be a local-first.

  * Since our application stores sensitive financial data, we wanted some storage which is secure.

    


### Decision

Decided on IndexedDB.


### Status

Decided on IndexedDB against other alternatives.

## Details


### Assumptions

We want our storage to be persistent.

We want our data to be structured and transactional as we are dealing with financial data.



### Constraints

IndexedDB has limited storage limits and limited browser compatibility. 



### Positions

We considered the following options for storage: IndexedDB, localStorage and SQLite. 

localStrorage allows only key-value pair storage structure.

Example with localStorage:

```js
localStorage.setItem('myKey', 'myValue');
const value = localStorage.getItem('myKey');
localStorage.removeItem('myKey');
```

Since we handle sensitive user information, localStorage is not the best approach for us. It is also limited to 5MB across all major browsers.


IndexedDB allows low-level API for client-side storage of significant amounts of structured data, including files/blobs.

Example with IndexedDB:

```js
const dbName = "the_name";

const request = indexedDB.open(dbName, 2);

request.onerror = (event) => {
  // Handle errors.
};
request.onupgradeneeded = (event) => {
  const db = event.target.result;

  // Create an objectStore to hold information about our customers. We're
  // going to use "ssn" as our key path because it's guaranteed to be
  // unique - or at least that's what I was told during the kickoff meeting.
  const objectStore = db.createObjectStore("customers", { keyPath: "ssn" });

  // Create an index to search customers by name. We may have duplicates
  // so we can't use a unique index.
  objectStore.createIndex("name", "name", { unique: false });

  // Create an index to search customers by email. We want to ensure that
  // no two customers have the same email, so use a unique index.
  objectStore.createIndex("email", "email", { unique: true });

  // Use transaction oncomplete to make sure the objectStore creation is
  // finished before adding data into it.
  objectStore.transaction.oncomplete = (event) => {
    // Store values in the newly created objectStore.
    const customerObjectStore = db.transaction("customers", "readwrite").objectStore("customers");
    customerData.forEach((customer) => {
      customerObjectStore.add(customer);
    });
  };
};

```

SQLite is zero-configuration, transactional SQL database engine. Given the type of data that we are managing for our application, a transactional and relational database would be a good approach.

``` sql
CREATE TABLE Account(
   AaccountId VARCHAR PRIMARY KEY,
   Name NVARCHAR
);
```

### Argument

Given the scope of our current application and other constraints, IndexedDB serves our usecase. We decided to use IndexedDB with the possibility of using SQLite in future.



## Related


### Related decisions

The storage framework we choose may affect testability and design.


### Related requirements

We want to store sensitive transatctional data without compromising on the performance.


## Notes

References - https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Using_IndexedDB
