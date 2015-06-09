# money.js

JavaScript version of Sebastian Bergmann's [Money](https://github.com/sebastianbergmann/money).

## Usage Examples

#### Creating a Money object and accessing its monetary value

```javascript
// Create Money object that represents 1 EUR
var m = new Money(100, new Currency('EUR'));

// Access the Money object's monetary value
console.log(m.getAmount());

// Access the Money object's monetary value converted to its base units
console.log(m.getConvertedAmount());
```

The code above produces the output shown below:

    100
    
    1.00

#### Creating a Money object from a string value

```javascript
// Create Money object that represents 12.34 EUR
var m = Money.fromString('12.34', new Currency('EUR'));

// Access the Money object's monetary value
console.log(m.getAmount());
```

The code above produces the output shown below:

    1234

#### Basic arithmetic using Money objects

```javascript
// Create two Money objects that represent 1 EUR and 2 EUR, respectively
var a = new Money(100, new Currency('EUR')),
    b = new Money(200, new Currency('EUR')),
    c;

// Negate a Money object
c = a.negate();
console.log(c.getAmount());

// Calculate the sum of two Money objects
c = a.add(b);
console.log(c.getAmount());

// Calculate the difference of two Money objects
c = b.subtract(a);
console.log(c.getAmount());

// Multiply a Money object with a factor
c = a.multiply(2);
console.log(c.getAmount());
```

The code above produces the output shown below:

    -100
    300
    100
    200

#### Comparing Money objects

```javascript
// Create two Money objects that represent 1 EUR and 2 EUR, respectively
var a = new Money(100, new Currency('EUR')),
    b = new Money(200, new Currency('EUR'));

console.log(a.lessThan(b));
console.log(a.greaterThan(b));

console.log(b.lessThan(a));
console.log(b.greaterThan(a));

console.log(a.compareTo(b));
console.log(a.compareTo(a));
console.log(b.compareTo(a));
```

The code above produces the output shown below:

    true
    false
    false
    true
    -1
    0
    1

The `compareTo()` method returns an integer less than, equal to, or greater than
zero if the value of one `Money` object is considered to be respectively less
than, equal to, or greater than that of another `Money` object.

#### Allocate the monetary value represented by a Money object among N targets

```javascript
// Create a Money object that represents 0,99 EUR
var a = new Money(99, new Currency('EUR'));

var t = a.allocateToTargets(10);
for (var i = 0; i < t.length; i++) {
    console.log(t[i].getAmount());
}
```

The code above produces the output shown below:

    10
    10
    10
    10
    10
    10
    10
    10
    10
    9

#### Allocate the monetary value represented by a Money object using a list of ratios

```javascript
// Create a Money object that represents 0,05 EUR
var a = new Money(5, new Currency('EUR'));

var t = a.allocateByRatios([3, 7]);
for (var i = 0; i < t.length; i++) {
    console.log(t[i].getAmount());
}
```

The code above produces the output shown below:

    2
    3

#### Extract a percentage (and a subtotal) from the monetary value represented by a Money object

```javascript
// Create a Money object that represents 100,00 EUR
var original = new Money(10000, new Currency('EUR'));

// Extract 21% (and the corresponding subtotal)
var extract = original.extractPercentage(21);

console.log(original.getAmount());
console.log(extract.subtotal.getAmount());
console.log(extract.percentage.getAmount());
```

The code above produces the output shown below:

    10000
    8264
    1736

Please note that this extracts the percentage out of a monetary value where the
percentage is already included. If you want to get the percentage of the
monetary value you should use multiplication (`multiply(0.21)`, for instance,
to calculate 21% of a monetary value represented by a Money object) instead.