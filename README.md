# javascript_human_readable_bytes_size
[JavaScript] Human Readable Bytes Size Formatter - No Loops!

```javascript
function human_readable_bytes_size(bytes, decimals, sap) {
  decimals = "number" === typeof decimals ? decimals : 2;
  sap = "string" === typeof sap ? sap : "";

  var 
    size = ['B', 'kB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB']
  , factor = Math.floor(  (String(bytes).length - 1) / 3  )
  ;
  
  bytes = bytes / Math.pow(1024, factor);  //calc
  bytes = Math.floor(bytes * Math.pow(10, decimals)) / Math.pow(10, decimals);  //round digits
  
   
  return String(bytes) + sap + size[factor];
}
```


```javascript
human_readable_bytes_size(29)
//"29B"
human_readable_bytes_size(29000000000000000)
//"25.75PB"
human_readable_bytes_size(2900000000000)
//"2.63TB"
human_readable_bytes_size(290000000000)
//"270.08GB"
human_readable_bytes_size(290000000000,5)
//"270.08354GB"
human_readable_bytes_size(290000000000,5,"---")
//"270.08354---GB"
```

<hr/>

if you want to put comma every 3 digits,
making things more readable,
use the following regular-expression-replace:

```javascript
bytes = String(bytes);
bytes.replace(/(\d)(?=(\d{3})+$)/g, "$1,");
```

if you only want to add comma to the fraction part (after the `.`)
use this instead:

```javascript
bytes = String(bytes).split(".");
bytes[0] = bytes[0].replace(/(\d)(?=(\d{3})+$)/g, "$1,");
bytes = bytes.join(".");
```
