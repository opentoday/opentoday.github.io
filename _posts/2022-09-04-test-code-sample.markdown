# try-catch

```typescript
function isValid(date: Date) {
    return Object.prototype.toString.call(date) === '[object Date]'
        && !Number.isNaN(date.getTime())
}

function parse(birthday: string): Date {
    let date = new Date(birthday)
    if (!isValid(date)) {
        throw new RangeError('Enter a date in the form YYYY/MM/DD')
    }
    return date
}

let date = parse('2002/01/01')
if (date) {
    console.info('Date is', date.toISOString())
} else {
    console.error('Error parsing date for some reason')
}
```
