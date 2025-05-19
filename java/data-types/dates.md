# Old ways
Before _Java 8_ `java.util.Date` and `java.util.Calendar` were used which is thread safe and easy to use, also time-zone logic included.
# Java 8
## Basics
`java.time` package.
Immutable types.

* `LocalDate` such as _2025-05-15_,
* `LocalTime` such as _22:31:00_,
* `LocalDateTime` such as _2025-05-15 22:31:00_.

```java
LocalDate.now();
LocalDate.of(2025, 5, 15);
LocalDate.of(2025, Month.MAY, 15);
// invalid, runtime exception
LocalDate.of(2025, 13, 15);

LocalTime.now();
LocalTime.of(22,35,0,0);

LocalDateTime.now();
LocalDateTime.of(2025,5,15,22,31,0,0);
LocalDateTime.of(LocalDate.now(), LocalTime.now());
```

* `MonthDay` is a combination of month and day of month,
* `YearMonth` is representing a combination of year and month,
* `Year` object represents a year.

```java
MonthDay.of(5,15).atYear(2025);
YearMonth.now().atDay(135);
```
## Zone
* `ZonedDateTime` represents a date and time with time zone,
* `ZoneId` used to convert between an `Instant` and a `LocalDateTime`, either a fixed offset or a geographical region,
* `Instant` represents a specific point in _UTC_ (Coordinated Universal Time) on the timeline.

| Feature | `Instant` | `ZonedDateTime` |
|--|--|--|
| Time zone aware | N (always _UTC_) | Y (has zone info) |
| Suitable for storage | Y | Not ideal (may be irrelevant later) |
| Suitable for display | Not directly | Y |
| Use in scheduling | Not recommended | Preffered |
| Lightweight | Y | N |

```java
ZonedDateTime zDT = Instant.now().atZone(ZoneId.of("Europe/Budapest"));
Instant instant = zDT.toInstant();
```

**Store as `Instant`, display as `ZoneDateTime`**.
## Clock
Abstract class that provided access to `Instant`, date, and time using time zone. Usage is optional and allows alternate clocks.

System factory methods (`.now()`) rely on `System.currentTimeMilis()`.

```java
Clock.systemDefaultZone();
Clock.systemUTC();
clock.instant();

Clock.offset(clock, Duration.ofHours(10));
```
## Comparing
* `compareTo`
* `isAfter`
* `isBefore`
* `isEqual`
## Formatting
`Java.time.format`
* `DateTimeFormatter`

### Common letters for patterns
| Symbol | Represents |  |
|--|--|--|
| `Y` | year of era | `yyyy` -> 2025, `yy` -> 25 |
| `D` | Day of the year | 1-366 |
| `d` | Day of month | 1-31 |
| `M` | Month of year | `M` -> 5, `MM` -> 05, `MMM` -> Apr, `MMMM` -> April |
| `h` | Clock hour am/pm | 1-12 |
| `H` | Hour of day | 0-23 |
| `m` | Minutes of hour | 0-59 |
| `s` | Seconds of minute | 0-59 |
| `z` | Time zone name | The word represnting the time zone |
| `Z` | Zone offset | Representing the offset |

```java
DateTimeFormatter.ofPattern("dd-MMMM-yyyy").format(lDT);
DateTimeFormatter.ofLocalizedDateTime(FormatStyle.MEDIUM).format(lDT);
```
## Period
Represents an amount of  time in days, months, and years.

```java
Period.of(1,1,1);
Period.ofDays(100);
period = Period.between(lD1, lD2);
```
## Duration
Represents an amount of time in seconds or nanoseconds. 

```java
Duration.of(1, ChronoUnit.DAYS);
Duration.ofHours(10);
Duration.between(lT1.lT2);
```
## Coverting from legacy
1. Convert `java.util.Date` to `Instant`.
2. Convert `Instant` to `LocalDate(Time)` or `ZonedDateTime`.

```java
date.toInstant().atZone(ZoneId.systemDefault()).toLocalDateTime();
```

1. Convert `java.util.Calendar` to `Instant`.
2. Get the `ZoneId`from the `Calendar`.
3. Covert `Instant` to `LocalDate(Time)` or `ZonedDateTime` using the `ZoneID`.

```java
Calendar.getInstance().toInstant().atZone(ZoneId.systemDefault()).toLocalDateTime();
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTAzMzM5ODYxNF19
-->