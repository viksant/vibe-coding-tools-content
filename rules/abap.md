---
title: "ABAP Cursor Guidelines"
description: "You are an expert in ABAP programming, SAP development, and enterprise software architecture."
category: "rules"
tags: ["ABAP", "SAP", "Enterprise Software"]
tech_stack: ["ABAP", "SAP NetWeaver"]
---

You are an expert in ABAP programming, SAP development, and enterprise software architecture.

### Code Style and Structure
- **Write Clean, Readable Code**: Ensure your code is straightforward and comprehensible. Use descriptive names for variables, methods, and classes.
- **Modular Programming**: Implement function modules, methods, and classes to develop modular and reusable code.
- **Separation of Concerns**: Distinguish between business logic, database operations, and user interface code.
- **Object-Oriented ABAP**: Favor object-oriented programming (OOP) principles when applicable, utilizing classes and interfaces.

### Naming Conventions
- **Variables**: Use lowercase with type prefixes (e.g., `lv_count` for local variables, `gv_total` for global variables).
- **Methods and Functions**: Use uppercase verb-noun combinations (e.g., `GET_CUSTOMER_DATA`, `CALCULATE_TOTAL`).
- **Classes**: Use uppercase for class names, prefixed with `ZCL_` for custom classes (e.g., `ZCL_CUSTOMER_MANAGER`).
- **Interfaces**: Use uppercase for interface names, prefixed with `ZIF_` (e.g., `ZIF_PRINTABLE`).

### ABAP Syntax and Features
- **Use Modern ABAP**: Take advantage of newer ABAP features such as inline declarations, string templates, and functional methods when available.
- **Avoid Obsolete Statements**: Substitute outdated statements (like `MOVE`) with modern alternatives (like assignment operators).
- **Use ABAP SQL**: Prefer ABAP SQL syntax (e.g., `SELECT ... INTO TABLE @DATA(lt_result)`) over native SQL for enhanced performance and readability.
- **Exception Handling**: Implement class-based exception handling using `TRY ... CATCH ... ENDTRY` for effective error management.

### Performance Optimization
- **Optimize Database Access**: Reduce database calls, utilize appropriate indexes, and retrieve only necessary fields.
- **Use Internal Tables Efficiently**: Select the right internal table types (STANDARD, SORTED, HASHED) based on the specific use case.
- **Avoid SELECT ***: Always specify the required fields in `SELECT` statements to minimize data transfer.
- **Parallel Processing**: Employ parallel processing techniques such as asynchronous RFC calls or parallel cursor processing for handling large data operations.

### UI Development
- **Separation of UI Logic**: Keep UI logic distinct from business logic, ideally in separate includes or classes.
- **Consistent UI Design**: Adhere to SAP UI guidelines to ensure a uniform user experience across applications.
- **Screen Painter Optimization**: Enhance screen painter layouts for performance, particularly for complex screens.

### Best Practices
- **Follow SAP Naming Conventions**: Comply with SAP's naming conventions for custom objects (using the `Z*` or `Y*` namespace).
- **Code Documentation**: Utilize ABAP Doc for inline documentation of classes, methods, and intricate logic.
- **Unit Testing**: Implement unit tests using the ABAP Unit Test framework for critical business logic.
- **Version Control**: Use SAP's version control system or integrate with external systems like Git.
- **Code Inspector**: Regularly run Code Inspector checks to ensure code quality and adherence to best practices.
- **Performance Analysis**: Utilize SQL trace and runtime analysis tools to identify and address performance bottlenecks.
- **SAP NetWeaver**: Leverage SAP NetWeaver features for scalability, security, and integration with both SAP and non-SAP systems.