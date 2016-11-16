### Roman Numeral Converter

```javascript
function convertToRoman(num) {
    var roman = {
        1000:"M", 900:"CM", 500:"D", 400:"CD", 100:"C", 90:"XC",
        50:"L", 40:"XL", 10:"X", 9:"IX", 5:"V", 4:"IV", 1:"I"
    };
    var str =[];
    num.toString().split('').map(function(x, index, arr) {
        c = Math.pow(10, arr.length - index - 1);
        if (x == 9 || x == 4 || x == 5) {
          str[index] = roman[x * c];
        } else {
          var temp = [];
          var i = x;
          if (x > 5) {
            temp.push(roman[5 * c]);
            i = x - 5;
          }
          for (i; i > 0; i--)
            temp.push(roman[c]);
          str[index] = temp.join('');
      }
   });
   return str.join('');
}
```

### ReplaceString

```javascript
function replaceString(oldS, newS,fullS) {
  return fullS.split(oldS).join(newS);
}
```

### Greatest Common Divisor & Least Common Multiple
```javascript
function gcd(a, b) {
     if (b === 0) return a;
     return gcd(b, a % b);
}

function lcm(a,b){
     return a*b/gcd(a,b);
}
```
