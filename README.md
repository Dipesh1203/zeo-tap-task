# Wrangler Enhancement: Byte Size and Time Duration Parsers

## 📘 Overview

This project enhances the **CDAP Wrangler** core library by introducing **native support for byte size (e.g., KB, MB, GB)** and **time duration units (e.g., ms, s, min)** within recipes. These enhancements simplify data transformations involving storage and time metrics, reducing multi-step recipes to single, clean operations.

---

## ✨ New Features Added

### ✅ 1. Grammar Enhancements (ANTLR)
- Introduced lexer rules: `BYTE_SIZE`, `TIME_DURATION`, and helper fragments `BYTE_UNIT`, `TIME_UNIT`.
- Modified parser to recognize byte size and time duration arguments.
- Location: `wrangler-core/src/main/antlr4/io/cdap/wrangler/parser/Directives.g4`

### ✅ 2. New Token Classes
- `ByteSize.java`: Parses and converts inputs like `10KB`, `5MB`, etc.
- `TimeDuration.java`: Parses `150ms`, `2.5s`, etc.
- These extend the `Token` class and include helper methods like `.getBytes()` and `.getMilliseconds()`.
- Location: `wrangler-api/src/main/java/io/cdap/wrangler/api/parser/`

### ✅ 3. Parser Integration
- Extended visit methods (e.g., `visitByteSizeArg`, `visitTimeDurationArg`) to return new token instances.
- Registered new token types in `TokenType`.

### ✅ 4. New Directive: `aggregate-stats`
- Performs aggregation (e.g., sum or average) across byte size and time columns.
- Supports optional arguments for unit conversion and aggregation type.
- Usage Example:

```wrangler
aggregate-stats :data_transfer_size :response_time total_size_mb total_time_sec
