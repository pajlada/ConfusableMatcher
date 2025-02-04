# ConfusableMatcher
Provides an `IndexOf` method for strings which uses string (key) to string (value) substring mapping.

See `Export.h` for C-like function exports

# Limitations

Due to limitations in `dense_hash_map`, key or value cannot start with `\x00` or `\x01`. These values are reserved as empty or deleted key/value placeholders.

# Example

```
std::vector<std::pair<std::string, std::string>> map; // This is a main string to string map
map.push_back(std::pair("A", "@")); // Map "A" to mean "@" when searching for a match
auto matcher = ConfusableMatcher(map); // This also adds default mappings such as "A" -> "A", "a" -> "A" or "0" -> "0" (specify false as second paramater to turn off)
matcher.AddMapping("8", "B", true); // Also map "8" to mean "B", mappings can be removed or added after creating a ConfusableMatcher
auto res = matcher.IndexOf(
    "@8", // Input string
    "AB", // What to search for
    { }, // Array of strings to ignore (skip) when searching
    true, // Whether to treat repeating substrings as matches which do not consume string we are searching for
    0 // Starting index
);
// res.first = 0 --- Index
// res.second = 2 --- Length
```
