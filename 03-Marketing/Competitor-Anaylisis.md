> Data retrived at January 2025

```plaintext
Company employees size nomenclature
A:    2 -    9
B:   10 -   49
C:   50 -  249
D:  250 -  999
E: 1000 - 9999

[network: followers](profile)
```

```dataviewjs
const data = await dv.io.csv("competitor-directory-jan2025.csv");

const normalizedData = data.map(row => {
  let newRow = {};
  for (let key in row) {
    const trimmedKey = key.trim();
    
    if (trimmedKey === "Services" || trimmedKey === "Target") {
      newRow[trimmedKey] = row[key].trim(); // Trim the value for these columns
    } else {
      newRow[trimmedKey] = row[key]; // Keep other columns as-is
    }
  }
  return newRow;
});

dv.table(
  ["Company", "Size", "Founded ", "Services/Target", "Website", "LinkedIn"],
  normalizedData.map(r => [
    r.Name,
    r.Size,
	r.Founded,
    r.Services + " " + r.Target,
    r.Website, 
    r.LinkedIn
  ])
);
```
