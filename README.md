# Dates

Start by importing Foundation 
```
import Foundation
```

## 1a. Creating a specific Date
```
import Foundation

let calendar = Calendar.current
let dateComponents = DateComponents(calendar: calendar, year: 2050, month: 1, day: 15)
let date = calendar.date(from: dateComponents)!

print(date) // 2050-01-15 03:00:00 +0000
```

## 1b. Creating a Date "now"
```
import Foundation

let now: Date = Date()

print(now) // 2000-09-09 19:06:24 +0000
```

## 1c. Creating a Date from another, adding or subtracting values
```
import Foundation

let now: Date = Date()
let calendar = Calendar.current

let tomorrow: Date?  = calendar.date(byAdding: .day, value:  1, to: now)
let yesterday: Date? = calendar.date(byAdding: .day, value: -1, to: now)

print(now)       //          2000-09-09 19:08:10 +0000
print(tomorrow)  // Optional(2000-09-10 19:08:10 +0000)
print(yesterday) // Optional(2000-09-08 19:08:10 +0000)
```

## 2. Formatting a Date
```
import Foundation

let date = Date()

let dateFormatter = DateFormatter()
dateFormatter.locale = Locale(identifier: "pt_BR")
dateFormatter.dateFormat = "EEEE - dd/MMMM/yyyy"

// --------------------------------------------------
// dateFormatter.dateFormat = "yy"         //      08
// dateFormatter.dateFormat = "yyyy"       //    2008
// --------------------------------------------------
// dateFormatter.dateFormat = "M"          //       1
// dateFormatter.dateFormat = "MM"         //      01
// dateFormatter.dateFormat = "MMMM"       // January
// --------------------------------------------------
// dateFormatter.dateFormat = "d"          //       1
// dateFormatter.dateFormat = "dd"         //      01
// --------------------------------------------------
// dateFormatter.dateFormat = "EEEE"       //  Monday
// --------------------------------------------------
// dateFormatter.locale = Locale(identifier: "en_US")
// dateFormatter.locale = Locale(identifier: "pt_BR")
// --------------------------------------------------

let formattedDate = dateFormatter.string(from: date)

print(formattedDate) // quarta-feira - 09/setembro/2000
```

## 3. "Dismantling" a date
```
import Foundation

let date = Date()
let dateFormatter = DateFormatter()
dateFormatter.locale = Locale(identifier: "pt_BR")

dateFormatter.dateFormat = "EEEE"
let dayOfWeek: String = dateFormatter.string(from: date)

dateFormatter.dateFormat = "dd"
let dayOfTheMonthWith2Digits: String = dateFormatter.string(from: date)

dateFormatter.dateFormat = "MM"
let fullNameOfTheMonth: String = dateFormatter.string(from: date)

dateFormatter.dateFormat = "yyyy"
let year: String = dateFormatter.string(from: date)

dateFormatter.dateFormat = "h"
let hourFrom0To12: String = dateFormatter.string(from: date)

dateFormatter.dateFormat = "a"
let ampm: String = dateFormatter.string(from: date)

dateFormatter.dateFormat = "hh"
let hourFrom00To12: String = dateFormatter.string(from: date)

dateFormatter.dateFormat = "H"
let hourFrom0To23: String = dateFormatter.string(from: date)

dateFormatter.dateFormat = "HH"
let hourFrom00To23: String = dateFormatter.string(from: date)

dateFormatter.dateFormat = "m"
let minuteFrom0To59: String = dateFormatter.string(from: date)

dateFormatter.dateFormat = "mm"
let minuteFrom00To59: String = dateFormatter.string(from: date)

let txt = "Hoje é \(dayOfWeek), \(dayOfTheMonthWith2Digits)/\(fullNameOfTheMonth)/\(year). São \(hourFrom00To24):\(minuteFrom00To59)"

print(txt) // Hoje é quarta-feira, 09/09/2020. São 16:14
```

## 4. Extending Date
```
import Foundation

extension Date {
	
	enum LocaleIdentifier: String {
		case unitedStates = "en_US"
		case brazil       = "pt_BR"
	}
	
	enum DateFormat: String {
		case dayOfWeek                = "EEEE"
		case dayOfTheMonthWith2Digits = "dd"
		case monthFrom1To12           = "M"
		case monthFrom01To12          = "MM"
		case fullNameOfTheMonth       = "MMMM"
		case yearWith4Digits          = "yyyy"
		case hourFrom0To11            = "h"
		case ampm                     = "a"
		case hourFrom00To12           = "hh"
		case hourFrom0To23            = "H"
		case hourFrom00To23           = "HH"
		case minuteFrom0To59          = "m"
		case minuteFrom00To59         = "mm"
	}

	static func getFormattedDateComponentAsStringUsing(date: Date, localeIdentifier: LocaleIdentifier, andDateFormat dateFormat: DateFormat) -> String {
		let dateFormatter = DateFormatter()
		dateFormatter.locale = Locale(identifier: localeIdentifier.rawValue)
		dateFormatter.dateFormat = dateFormat.rawValue
		return dateFormatter.string(from: date)
	}
	
}

let someDate = Date()
let dayOfWeek                = Date.getFormattedDateComponentAsStringUsing(date: someDate, localeIdentifier: .brazil, andDateFormat: .dayOfWeek)
let dayOfTheMonthWith2Digits = Date.getFormattedDateComponentAsStringUsing(date: someDate, localeIdentifier: .brazil, andDateFormat: .dayOfTheMonthWith2Digits)
let monthFrom01To12          = Date.getFormattedDateComponentAsStringUsing(date: someDate, localeIdentifier: .brazil, andDateFormat: .monthFrom01To12)
let yearWith4Digits          = Date.getFormattedDateComponentAsStringUsing(date: someDate, localeIdentifier: .brazil, andDateFormat: .yearWith4Digits)

print("Hoje é \(dayOfWeek), \(dayOfTheMonthWith2Digits)/\(monthFrom01To12)/\(yearWith4Digits).") // Hoje é quarta-feira, 09/09/2020.

```
