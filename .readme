# regular expressions

Created By: Atul Verma
Last Edited: Jun 17, 2020 12:17 AM

```python
import re
re.search(pattern,string) #return match object if found else return none

#convert list to a series to do vectorised pattern matching
#eg. a = ["hello","my"] a = pd.Series(a)
#a.str.contains(pattern)

```

`[]` is a set 

![regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled.png](regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled.png)

# Quantifiers

![regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%201.png](regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%201.png)

![regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%202.png](regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%202.png)

![regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%203.png](regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%203.png)

![regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%204.png](regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%204.png)

```python
pattern = "\[\w+\]"
tag_titles = titles[titles.str.contains(pattern)]#for selecting [video],[pdf],etc
pattern = r"\[(\w+)\]"
tag_freq = titles.str.extract(pattern).value_counts()
```

`r""` here means raw string which will not interpret any special sequence such as \b ,\n etc

## capture groups

![regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%205.png](regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%205.png)

```python
pattern = r"(\[\w+\])"
tag_5_matches = tag_5.str.extract(pattern)
print(tag_5_matches)
```

## Negative character classes

pattern = r"\b[Cc]\b[^.+]"

![regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%206.png](regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%206.png)

## using word boundry

```python
pattern_2 = r"\bJava\b"

m2 = re.search(pattern_2, string)
print(m2)

pattern = r"(\b[Jj]ava\b)"
java_titles = titles[titles.str.contains(pattern)]
```

### Beginning anchor and the end anchor, which represent the start and the end of the string, respectfully.

![regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%207.png](regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%207.png)

```python
start_pattern = r"^\[\w+\]"
end_pattern = r"\[\w+\]$"
beginning_count = titles.str.contains(start_pattern).sum()
ending_count = titles.str.contains(end_pattern).sum()
```

### Flags in regular expersions

use flags = `re.IGNORECASE` or `re.I` for ignoring case senstivity while matching pattern

```python
email_tests.str.contains(r"email",flags=re.I)
import re

email_tests = pd.Series(['email', 'Email', 'e Mail', 'e mail', 'E-mail',
              'e-mail', 'eMail', 'E-Mail', 'EMAIL', 'emails', 'Emails',
              'E-Mails'])
pattern = r"\be[\-\s]?mails?\b"
email_mentions = titles.str.contains(pattern,flags = re.I ).sum()
```

```python
hn_sql = hn[hn['title'].str.contains(r"\w+SQL", flags=re.I)].copy()
hn_sql['flavor'] = hn_sql.title.str.extract(r"(\w+SQL)",flags = re.I)
hn_sql['flavor'] = hn_sql['flavor'].str.lower()
sql_pivot = hn_sql.pivot_table(index = "flavor",values = "num_comments")
```

![regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%208.png](regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%208.png)

### Lookarounds

![regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%209.png](regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%209.png)

```python
pattern = r"(?<!Series\s)\b[Cc]\b(?![\+\.])"
c_mentions = titles.str.contains(pattern).sum()
'''
Match instances of C or c where they are not preceded or followed by another wordcharacter.
From the match above:
Exclude instances where it is followed by a . or + character, without removing instances where the match occurs at the end of the string.
Exclude instances where the word 'Series' immediately precedes the match.
'''
```

## backreferences

![regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%2010.png](regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%2010.png)

![regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%2011.png](regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%2011.png)

```python
pattern = r"\b(\w+)\s\1\b"
repeated_words = titles[titles.str.contains(pattern)]# for repeated words eg Flexbox Cheatsheet Cheatsheet
```

### substituting values

```python
re.sub(pattern, repl, string, flags=0)
string = "aBcDEfGHIj"

print(re.sub(r"[A-Z]", "-", string))
#op a-c--f---j

Series.str.replace(pat, repl, flags=0)

pattern = r"https?://([\w\-\.]+)"
test_urls_clean = test_urls.str.extract(pattern,flags = re.I) #for extracting domains
```

### Multiple capture groups

```python
pattern = r"(https?)://([\w\-\.]+)/?(.*)"
test_url_parts = test_urls.str.extract(pattern,flags = re.I)
```

### Named capture groups

![regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%2012.png](regular%20expressions%2098750e09600241399b78f64b7de6e7a0/Untitled%2012.png)

```python
pattern = r"(?P<protocol>https?)://(?P<domain>[\w\.\-]+)/?(?P<path>.*)"
url_parts = hn['url'].str.extract(pattern,flags = re.I)
```