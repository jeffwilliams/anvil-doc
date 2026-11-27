# How to Ignore Case in Searches

To do a case-insensitive search, use a regular expression containing the case-insensitive flag. For example, to search for "drove downtown in the rain" case insensitively, type:

```
/(?i)drove downtown in the rain/
```

Select it, then ++right-button++. Regular expressions in Anvil use the Go regexp package's [syntax](https://pkg.go.dev/regexp/syntax).
