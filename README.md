# 📚 SQL Data Types Cheatsheet

Comprehensive list of SQL data types, organized by category, with use cases, common mistakes, and tips.

## 🌟 1. Numeric Types

### **a. Integer Types**
| Type          | Description                        | Use Case                                   | Common Mistake                          |
|---------------|------------------------------------|------------------------------------------|---------------------------------------|
| `SMALLINT`    | 2-byte integer (Range: -32,768 to 32,767) | When saving **small numbers** like age or count. | Using it when values could exceed range. |
| `INTEGER`     | 4-byte integer (Range: -2 billion to 2 billion) | General-purpose numeric data. | Using it for IDs when `BIGINT` is needed. |
| `BIGINT`      | 8-byte integer (Huge range)         | Large values like **user IDs, large counters**. | Using `INTEGER` when future growth requires `BIGINT`. |
| `SERIAL`      | Auto-incrementing 4-byte integer.  | Auto-generated IDs. | Using without knowing it's just shorthand for `INTEGER` + `SEQUENCE`. |
| `BIGSERIAL`   | Auto-incrementing 8-byte integer.  | Auto-generated IDs for large tables. | Forgetting to use `BIGSERIAL` when IDs could exceed `SERIAL` range. |

### **b. Decimal & Floating Types**
| Type          | Description                        | Use Case                                   | Common Mistake                          |
|---------------|------------------------------------|------------------------------------------|---------------------------------------|
| `NUMERIC(p, s)` | Exact precision decimal.         | Financial data (**money, prices**).      | Using `FLOAT` for financial data (causes precision errors). |
| `DECIMAL(p, s)` | Alias for `NUMERIC`.             | Same as above.                           | Forgetting to specify precision and scale. |
| `REAL`        | 4-byte floating point.             | Scientific data, calculations requiring speed. | Using for financial data (rounding errors). |
| `DOUBLE PRECISION` | 8-byte floating point.         | When more precision than `REAL` is needed. | Assuming it's always exact (floating point inaccuracies). |

## 🌟 2. String Types
| Type          | Description                        | Use Case                                   | Common Mistake                          |
|---------------|------------------------------------|------------------------------------------|---------------------------------------|
| `CHAR(n)`     | Fixed-length string.              | Standardized IDs, codes (**ISO codes**). | Padding with spaces when shorter strings are inserted. |
| `VARCHAR(n)`  | Variable-length string.           | Usernames, names, descriptions.          | Forgetting to set an appropriate limit. |
| `TEXT`        | Unlimited length string.          | Large bodies of text (**comments, logs**). | Using `TEXT` when a length limit would be more efficient. |

## 🌟 3. Date & Time Types
| Type          | Description                        | Use Case                                   | Common Mistake                          |
|---------------|------------------------------------|------------------------------------------|---------------------------------------|
| `DATE`        | Stores date only (YYYY-MM-DD).    | Birth dates, deadlines.                  | Trying to store time with it. |
| `TIME`        | Stores time only (HH:MI:SS).      | Events that occur daily.                 | Not using `TIMESTAMP` when date is needed. |
| `TIMESTAMP`   | Stores date & time.               | Created/updated timestamps.              | Forgetting to use timezone-aware version (`TIMESTAMPTZ`). |
| `TIMESTAMPTZ` | Timestamp with timezone info.     | Events across different time zones.     | Using `TIMESTAMP` when dealing with users from various time zones. |
| `INTERVAL`    | Duration of time.                 | Time differences, age calculation.      | Mixing `INTERVAL` with regular `INT` or `NUMERIC`. |

## 🌟 4. Boolean Type
| Type          | Description                        | Use Case                                   | Common Mistake                          |
|---------------|------------------------------------|------------------------------------------|---------------------------------------|
| `BOOLEAN`     | Stores `TRUE`, `FALSE`, or `NULL`. | Flags, conditions, toggles (**is_active**). | Using `1/0` or `Y/N` instead of `BOOLEAN`. |

## 🌟 5. JSON & JSONB (PostgreSQL Specific)
| Type          | Description                        | Use Case                                   | Common Mistake                          |
|---------------|------------------------------------|------------------------------------------|---------------------------------------|
| `JSON`        | Stores JSON data (as text).       | Unstructured data, logs, metadata.       | Slow query performance, better use `JSONB` for indexing. |
| `JSONB`       | Binary JSON format, supports indexing. | Faster queries, filtering.             | Using `JSON` instead of `JSONB` for large datasets. |

## 🌟 6. Array Types (PostgreSQL Specific)
| Type          | Description                        | Use Case                                   | Common Mistake                          |
|---------------|------------------------------------|------------------------------------------|---------------------------------------|
| `ARRAY[]`     | Store multiple values of a type.  | Tags, lists of related items.           | Forgetting PostgreSQL supports arrays natively. |

## 🌟 7. Special Types
| Type          | Description                        | Use Case                                   | Common Mistake                          |
|---------------|------------------------------------|------------------------------------------|---------------------------------------|
| `UUID`        | Universally Unique Identifier.    | Globally unique IDs.                     | Using `VARCHAR` for IDs that should be UUIDs. |
| `CIDR`, `INET`| Network address types.            | IP addresses, subnets.                   | Using `TEXT` instead of these specialized types. |
| `MACADDR`     | MAC addresses.                    | Storing network device identifiers.     | Storing as `VARCHAR` instead of `MACADDR`. |

## 🌟 8. Geometry & Spatial Types (PostGIS)
| Type          | Description                        | Use Case                                   | Common Mistake                          |
|---------------|------------------------------------|------------------------------------------|---------------------------------------|
| `POINT`       | A point in a 2D space.            | Locations, coordinates.                  | Storing as `NUMERIC` or `TEXT` instead. |
| `LINE`, `POLYGON`, etc. | Geometrical shapes.      | Mapping, geospatial queries.             | Forgetting to install PostGIS. |

## 📌 Tips & Best Practices
- Always choose the **smallest data type** that will suit your needs. It saves space and improves performance.
- Use `NUMERIC` or `DECIMAL` for **money or precise calculations**, never `FLOAT` or `DOUBLE`.
- Prefer `UUID` over `SERIAL` or `BIGSERIAL` when you need **globally unique IDs** (especially in distributed systems).
- Use `JSONB` over `JSON` if you need to **query JSON data**.

Happy SQL-ing! 🚀

