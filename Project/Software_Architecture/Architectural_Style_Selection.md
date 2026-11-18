# Architectural Style Selection

## 1. Selected architectural style

3 Layer Architecture

## 2. Main characteristics

It has 3 hierarchical layers:
- User interface / presentation
- Middleware / application
- Database / data

It is a closed architecture, so each layer only calls the layer directly below it. The user interface never reaches the database, so the middleware handles the data requests between the user interface and the database.

## 3. Why it is appropriate for the project

This architecture is appropriate for BidBridge because this style is often used for websites and BidBridge is one. The browser is the user interface, the web server is the middleware and the database stores the data. It's also appropriate because the user interface and the database can be changed independently.

## 4. How it supports the identified design goals

**G01 Security:** The user interface never talks to the database. Every request goes through the middleware, which can check the user and the rules first.

**G02 Reliability:** The business rules and the data changes are done in the middleware, so payment and job status are handled in one place.

**G03 Availability:** The database is its own layer, so backup and recovery can be done on it without changing the other layers.

**G04 Performance:** The database layer can be improved without changing the other layers.

## 5. Advantages and limitations

**Advantages**
- The hierarchy keeps the system less complex.
- The closed architecture has low coupling, which is a benefit.
- The user interface and database can be changed on their own.

**Limitations**
- Closed architecture is less efficient because requests go through every layer.
- Each layer must only do its own job, otherwise the layers get mixed up and the middleware gets too big.
