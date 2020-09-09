# Dates

Start by importing Foundation 
```
import Foundation
```

## 1a. Creating a specific Date
```
let calendar = Calendar.current
let dateComponents = DateComponents(calendar: calendar, year: 2050, month: 1, day: 15)
let customDate = calendar.date(from: dateComponents)!
```

## 1b. Creating a Date "now"
```
let now: Date = Date()
```

## 1c. Creating a Date from another, adding or subtracting values
```
let tomorrow: Date?  = calendar.date(byAdding: .day, value:  1, to: now)
let yesterday: Date? = calendar.date(byAdding: .day, value: -1, to: now)
```

## 2. Formatting a Date
```
let dateFormatter = DateFormatter()
dateFormatter.locale = Locale(identifier: "pt_BR")
dateFormatter.dateFormat = "EEEE - dd/MMMM/yyyy" // quarta-feira - 09/setembro/2020

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
```

## 3. Creating a String from a Date
```
Criando uma String a partir de uma data:
let formattedDate = dateFormatter.string(from: date)
print(formattedDate)

## 4. "Dismantling" a date
```
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
let hourFrom0To24: String = dateFormatter.string(from: date)

dateFormatter.dateFormat = "HH"
let hourFrom00To24: String = dateFormatter.string(from: date)

dateFormatter.dateFormat = "m"
let minuteFrom0To59: String = dateFormatter.string(from: date)

dateFormatter.dateFormat = "mm"
let minuteFrom00To59: String = dateFormatter.string(from: date)

let txt = "Hoje é \(dayOfWeek), \(dayOfTheMonthWith2Digits)/\(fullNameOfTheMonth)/\(year). São \(hourFrom00To24):\(minuteFrom00To59)"
print(txt)

## 5. Extending Date
```
extension Date {
	
	enum DateFormat: String {
		case dayOfWeek                = "EEEE"
		case dayOfTheMonthWith2Digits = "dd"
		case fullNameOfTheMonth       = "MM"
		case year                     = "yyyy"
		case hourFrom0To12            = "h"
		case ampm                     = "a"
		case hourFrom00To12           = "hh"
		case hourFrom0To24            = "H"
		case hourFrom00To24           = "HH"
		case minuteFrom0To59          = "m"
		case minuteFrom00To59         = "mm"
	}
	
	static func getFormattedDateComponentAsStringUsing(date: Date, andDateFormat dateFormat: DateFormat) -> String {
		dateFormatter.dateFormat = dateFormat.rawValue
		return dateFormatter.string(from: date)
	}
	
}

let someDate = Date()
let _hourFrom00To24 = Date.getFormattedDateComponentAsStringUsing(date: someDate, andDateFormat: .hourFrom00To24)
print(_hourFrom00To24)

```
