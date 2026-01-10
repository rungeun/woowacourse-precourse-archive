# 🪐 Time

## 날짜 생성

```kotlin
import java.time.LocalDate

// 특정 날짜
val date = LocalDate.of(2026, 1, 10)  // 2026년 1월 10일

// 오늘
val today = LocalDate.now()
```

## 날짜 정보 추출

```kotlin
val year = date.year           // 2026
val month = date.monthValue    // 1
val day = date.dayOfMonth      // 10
val dayOfWeek = date.dayOfWeek // SATURDAY
```

## 날짜 계산

```kotlin
val nextDay = date.plusDays(1)      // 하루 후 2026-01-11
val nextWeek = date.plusWeeks(1)    // 일주일 후
val nextMonth = date.plusMonths(1)  // 한달 후
val yesterday = date.minusDays(1)   // 하루 전
```

## 요일 비교

```kotlin
import java.time.DayOfWeek

val isSaturday = date.dayOfWeek == DayOfWeek.SATURDAY // 토요일인가
val isWeekend = date.dayOfWeek == DayOfWeek.SATURDAY ||
        date.dayOfWeek == DayOfWeek.SUNDAY // 주말인가
```

## 해당 월의 마지막 날

```kotlin
val lastDay = date.lengthOfMonth()  // 28, 29, 30, 31
```

## 날짜 비교

```kotlin
val isBefore = date.isBefore(today) // today의 전 날은 date인가
val isAfter = date.isAfter(today) // today의 다음 날은 date인가
val isEqual = date.isEqual(today) // today와 date가 같은 날인가
```

## 시간 포함 (LocalDateTime)

```kotlin
import java.time.LocalDateTime

val dateTime = LocalDateTime.of(2026, 1, 10, 14, 30, 0)  // 2026-01-10T14:30
val now = LocalDateTime.now() // 나노초 포함 현재 시간 2026-01-09T10:41:02.012821500
val now2 = LocalDateTime.now().withNano(0) // 현재 시간 초까지 표시  2026-01-09T10:42:36
val now3 = LocalDateTime.now()
    .withSecond(0)
    .withNano(0)    // 현재 시간 분까지 표시 2026-01-09T10:44

val hour = dateTime.hour        // 14
val minute = dateTime.minute    // 30
val second = dateTime.second    // 0
```

## LocalDate ↔ LocalDateTime 변환

```kotlin
// LocalDate → LocalDateTime
val dateTime = date.atTime(14, 30)           // date에 14:30:00추가 (2026-01-10T14:30)
val startOfDay = date.atStartOfDay()         // date에 00:00:00추가 (2026-01-10T00:00)

// LocalDateTime → LocalDate
val dateOnly = dateTime.toLocalDate()        // 시간 제거 2026-01-10
```

## 시간만 다루기 (LocalTime)

```kotlin
import java.time.LocalTime

val time = LocalTime.of(14, 30, 0)     // 14:30
val time2 = LocalTime.of(14, 30, 10)     // 14:30:10
val nowTime = LocalTime.now()           // 10:51:12.708352700

val hourOnly = time.hour               // 14
val minuteOnly = time.minute           // 30
```

## 날짜 포맷팅

```kotlin
import java.time.format.DateTimeFormatter

val formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd")
val formatted = date.format(formatter)  // 2026-01-10

val formatter2 = DateTimeFormatter.ofPattern("<<yyyy>>MM<<dd>>")
val formatted2 = date.format(formatter2)  // <<2026>>01<<10>>

// 파싱 (문자열 -> LocalDate)
val parsed = LocalDate.parse("2026-01-10", formatter) //2026-01-10
```

## 날짜 범위 순회

```kotlin
val start = LocalDate.of(2026, 1, 10)
val end = LocalDate.of(2026, 1, 15)

var current = start
while (!current.isAfter(end)) {
    println(current)
    current = current.plusDays(1)
}
/*
2026-01-10
2026-01-11
2026-01-12
2026-01-13
2026-01-14
2026-01-15
 */
```

## 기간 계산 (Period, Duration)

```kotlin
import java.time.Period
import java.time.Duration

val start = LocalDate.of(2026, 1, 10)
val end = LocalDate.of(2026, 1, 15)

// 날짜 간 차이
val period = Period.between(start, end)
val days = period.days      // 5
val months = period.months // 0

// 시간 간 차이 (LocalDateTime)
val start1 = LocalDateTime.of(2026, 1, 10, 15, 10)
val end1 = LocalDateTime.of(2026, 1, 10, 16, 22)

val duration = Duration.between(start1, end1)
val hours = duration.toHours()      // 1
val minutes = duration.toMinutes()  // 72
```

## 특정 요일로 이동

```kotlin
import java.time.temporal.TemporalAdjusters
import java.time.DayOfWeek

// 다음 월요일
val nextMonday = date.with(TemporalAdjusters.next(DayOfWeek.MONDAY))    // 2026-01-12

// 이번 달 첫째 날
val firstDayOfMonth = date.with(TemporalAdjusters.firstDayOfMonth())    // 2026-01-01

// 이번 달 마지막 날
val lastDayOfMonth = date.with(TemporalAdjusters.lastDayOfMonth())      // 2026-01-31
```

## 윤년 확인

```kotlin
val isLeapYear = date.isLeapYear    // false
```

## Instant (타임스탬프)

```kotlin
import java.time.Instant

val instant = Instant.now()              // 현재 UTC 타임스탬프    2026-01-09T02:08:27.298852400Z
val epochSeconds = instant.epochSecond   // Unix timestamp      1767924507
```

## 날짜 차이 계산 (ChronoUnit)

```kotlin
import java.time.temporal.ChronoUnit

val daysBetween = ChronoUnit.DAYS.between(start, end)       // 5
val monthsBetween = ChronoUnit.MONTHS.between(start, end)   // 0
```

