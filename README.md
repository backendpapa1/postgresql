Here's your content transformed into a **cookbook-style SQL guide**, with each section as a *recipe* for a specific concept or skill.

---

# 🧑‍🍳 **SQL Beginner-to-Intermediate Cookbook**

## 📘 Table of Contents

1. [Referencing Tables](#referencing-tables)
2. [Using RETURNING](#using-returning)
3. [Multiple Inserts](#multiple-inserts)
4. [Updating Data](#updating-data)
5. [ON CONFLICT DO NOTHING](#on-conflict-do-nothing)
6. [String Concatenation (`||`)](#string-concatenation)
7. [Using `AS` for Aliases](#using-as-for-aliases)
8. [Ordering Data](#ordering-data)
9. [Ordering with NULLs](#ordering-with-nulls)
10. [DISTINCT Values](#distinct-values)
11. [Filtering with WHERE](#filtering-with-where)
12. [LIMIT and FETCH](#limit-and-fetch)
13. [IN and NOT IN](#in-and-not-in)
14. [BETWEEN and NOT BETWEEN](#between-and-not-between)
15. [Pattern Matching with LIKE and ILIKE](#pattern-matching)

---

## 📌 Referencing Tables

```sql
SELECT * FROM actors;
```

Use the table name directly in `FROM` to pull data from that table.

---

## 🔁 Using RETURNING

```sql
INSERT INTO actors (first_name, last_name)
VALUES ('John', 'Doe')
RETURNING id;
```

Returns the inserted row (or specific fields like `id`) immediately after insertion.

---

## 📥 Multiple Inserts

```sql
INSERT INTO genres (name)
VALUES ('Action'), ('Drama'), ('Comedy');
```

Insert multiple rows in one go.

---

## ✍️ Updating Data

```sql
UPDATE movies
SET movie_length = 120
WHERE id = 10;
```

---

## 🚫 ON CONFLICT DO NOTHING

```sql
INSERT INTO users (email)
VALUES ('john@example.com')
ON CONFLICT (email) DO NOTHING;
```

Avoids inserting duplicates based on a unique constraint.

---

## 🔗 String Concatenation (`||`)

```sql
SELECT first_name || ' ' || last_name AS full_name FROM actors;
```

---

## 🏷 Using `AS` for Aliases

```sql
SELECT 2 * 3 AS "multiply";
```

Aliases can name expressions or columns.

✅ `AS` is optional:

```sql
SELECT 2 * 3 "multiply";
```

---

## 📊 Ordering Data

### Using ORDER BY

```sql
SELECT 
  first_name,
  last_name,
  date_of_birth 
FROM actors
ORDER BY 
  1 ASC,  -- first_name
  3 DESC; -- date_of_birth
```

### With Alias

```sql
SELECT 
  first_name || ' ' || last_name AS full_name
FROM actors
ORDER BY full_name;
```

### With Function

```sql
SELECT first_name FROM actors
ORDER BY LENGTH(first_name);
```

---

## 📉 Ordering with NULLs

```sql
SELECT num FROM demo_sorting
ORDER BY num NULLS FIRST;

SELECT num FROM demo_sorting
ORDER BY num DESC NULLS FIRST;
```

---

## 🔍 DISTINCT Values

```sql
SELECT DISTINCT movie_lang FROM movies;
```

Combine for uniqueness:

```sql
SELECT DISTINCT movie_lang, director_id
FROM movies
ORDER BY 1;
```

---

## 🔎 Filtering with WHERE

### Comparison & Logical Operators

```sql
SELECT * FROM movies 
WHERE (movie_length < 100) AND (age_certificate = 'U')
ORDER BY release_date ASC;
```

```sql
SELECT DISTINCT * 
FROM movies 
WHERE (movie_length < 100) 
  OR (age_certificate = 'U' AND movie_lang = 'English') 
ORDER BY age_certificate ASC;
```

### ⚠️ Execution Order

`AND` is evaluated before `OR`. Use parentheses to clarify logic.

> ❗ Aliases can't be used in WHERE
> 🧠 SQL Order:
> **FROM → WHERE → SELECT → ORDER BY**

---

## 🔽 LIMIT and FETCH

### Using LIMIT

```sql
SELECT * FROM directors
WHERE nationality = 'American'
ORDER BY date_of_birth ASC
LIMIT 5;
```

### Using FETCH

```sql
SELECT * FROM movies
ORDER BY movie_length DESC
FETCH FIRST 5 ROWS ONLY;
```

### OFFSET with FETCH

```sql
SELECT * FROM movies
ORDER BY movie_length DESC
OFFSET 5 ROWS
FETCH NEXT 5 ROWS ONLY;
```

---

## ✅ IN and NOT IN

```sql
SELECT * FROM movies
WHERE movie_lang NOT IN ('English', 'Chinese');
```

---

## 🔢 BETWEEN and NOT BETWEEN

```sql
SELECT * FROM movies
WHERE movie_length NOT BETWEEN 100 AND 120
ORDER BY movie_length;
```

---

## 🧬 Pattern Matching with LIKE & ILIKE

### LIKE Examples

```sql
SELECT 'hello' LIKE 'hello';     -- true
SELECT 'hello' LIKE '%ell%';     -- true
SELECT 'hello' LIKE '__llo';     -- true
SELECT 'hello' LIKE '%ll_';      -- true
```

### LIKE with Table Data

```sql
SELECT * FROM actors
WHERE first_name LIKE 'A___' -- Names starting with A and 3 characters after
ORDER BY first_name ASC;
```

### ILIKE (Case-Insensitive)

```sql
SELECT * FROM actors
WHERE first_name ILIKE 'a%';
```

---

Let me know if you'd like this turned into a downloadable PDF or split into sections for a tutorial or learning module!
