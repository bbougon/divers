# mock manuel d'une classe et instanciation:

```javascript
import {ChronoUnit, convert, ZonedDateTime} from "@js-joda/core";

export class DateTimeProvider {

    constructor() {
    }

    startMonth = () => {
        return new Date(new Date().getFullYear(), new Date().getMonth(), 1);
    };

    endMonth = () => {
        return new Date(new Date().getFullYear(), new Date().getMonth() + 1, 0, 23, 59, 59);
    };

    now = () => {
        return new Date();
    }
    
    add = (amount, unit) => {
    }
}

export default DateTimeProvider;
```

```javascript
describe('Date time provider', function () {

    const provider = () => {
        return class extends DateTimeProvider {
            now = () => {
                return new Date(2020, 9, 10, 14, 12, 26);
            }
        }
    };
    
    let dateProvider;

    beforeEach(() => {
        dateProvider = provider();
    });

    it('should add the expected amount of unit', () => {
        let provider = new dateProvider.prototype.constructor();

        let date = provider.add(1, "hours");

        expect(date).toEqual(new Date(2020, 9, 10, 15, 12, 26));
    });
})
```
