# 🪐 Collection operations

참고 문서: [Kotlin-Collection operations overview](https://kotlinlang.org/docs/collection-operations.html)

## 컬렉션 타입별 사용 가능 함수 요약

### List - 거의 모든 함수 사용 가능

- 순서 보장, 중복 허용
- 인덱스 접근 가능

### Set - 순서 관련 함수 제외

- 중복 불가
- `slice`, `take`, `drop` 등 순서 의존 함수는 List로 변환 필요

### Map - 전용 함수들

- `mapKeys`, `mapValues`, `filterKeys`, `filterValues`
- 일반 컬렉션 함수는 `entries`, `keys`, `values`로 변환 필요

### Array - List와 거의 동일

- 고정 크기
- `toList()`로 변환해서 사용 권장

### Sequence - 지연 평가

- 모든 함수 사용 가능하지만 중간 연산은 지연됨
- `toList()`로 최종 평가

---

## 변환 함수

### map - 각 요소를 변환

```kotlin
val numbers = listOf(1, 2, 3)
val doubled = numbers.map { it * 2 }  // [2, 4, 6]

// 사용 가능: List, Set, Array, Sequence
```

### flatMap - 중첩 컬렉션을 평탄화

```kotlin
val nested = listOf(listOf(1, 2), listOf(3, 4))
val flat = nested.flatMap { it }  // [1, 2, 3, 4]

// 사용 가능: List, Set, Array, Sequence
```

### mapNotNull - null 제거하면서 변환

```kotlin
val strings = listOf("1", "a", "2")
val numbers = strings.mapNotNull { it.toIntOrNull() }  // [1, 2]

// 사용 가능: List, Set, Array, Sequence
```

### mapKeys / mapValues - Map 변환

```kotlin
val map = mapOf("a" to 1, "b" to 2)
val newKeys = map.mapKeys { (k, _) -> k.uppercase() }  // {"A": 1, "B": 2}
val newValues = map.mapValues { (_, v) -> v * 2 }  // {"a": 2, "b": 4}

// 사용 가능: Map만
```

---

## 필터 함수

### filter - 조건 만족하는 요소만

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val evens = numbers.filter { it % 2 == 0 }  // [2, 4]

// 사용 가능: List, Set, Array, Sequence
```

### filterNot - 조건 불만족하는 요소만

```kotlin
val odds = numbers.filterNot { it % 2 == 0 }  // [1, 3, 5]

// 사용 가능: List, Set, Array, Sequence
```

### filterNotNull - null 제거

```kotlin
val mixed = listOf(1, null, 2, null, 3)
val nonNull = mixed.filterNotNull()  // [1, 2, 3]

// 사용 가능: List, Set, Array, Sequence
```

### filterIsInstance - 특정 타입만

```kotlin
val mixed: List<Any> = listOf(1, "a", 2, "b")
val strings = mixed.filterIsInstance<String>()  // ["a", "b"]

// 사용 가능: List, Set, Array, Sequence
```

---

## 그룹화 함수

### groupBy - 길이로 그룹화

```kotlin
val words = listOf("a", "ab", "abc", "b")
val byLength = words.groupBy { it.length }
// {1: ["a", "b"], 2: ["ab"], 3: ["abc"]}

// 사용 가능: List, Set, Array, Sequence
```

### partition - 조건으로 2개로 분할

```kotlin
val (evens, odds) = numbers.partition { it % 2 == 0 }
// evens: [2, 4], odds: [1, 3, 5]

// 사용 가능: List, Set, Array, Sequence
```

---

## 정렬 함수

### sorted / sortedDescending - 오름차순/내림차순

```kotlin
val numbers = listOf(3, 1, 4, 1, 5)
val asc = numbers.sorted()  // [1, 1, 3, 4, 5]
val desc = numbers.sortedDescending()  // [5, 4, 3, 1, 1]

// 사용 가능: List, Set, Array, Sequence
```

### sortedBy / sortedByDescending - 특정 속성으로 정렬

```kotlin
val employees = listOf(...)
val byAge = employees.sortedBy { it.age }
val bySalary = employees.sortedByDescending { it.salary }

// 사용 가능: List, Set, Array, Sequence
```

---

## 추출 함수

### take / takeLast - 앞/뒤에서 n개

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val first3 = numbers.take(3)  // [1, 2, 3]
val last3 = numbers.takeLast(3)  // [3, 4, 5]

// 사용 가능: List, Array, Sequence
```

### drop / dropLast - 앞/뒤에서 n개 제거

```kotlin
val dropped = numbers.drop(2)  // [3, 4, 5]
val droppedLast = numbers.dropLast(2)  // [1, 2, 3]

// 사용 가능: List, Array, Sequence
```

### slice - 범위로 추출

```kotlin
val sliced = numbers.slice(1..3)  // [2, 3, 4]

// 사용 가능: List, Array
```

### distinct - 중복 제거

```kotlin
val duplicates = listOf(1, 2, 2, 3, 3, 3)
val unique = duplicates.distinct()  // [1, 2, 3]

// 사용 가능: List, Set, Array, Sequence
```

### distinctBy - 특정 속성으로 중복 제거

```kotlin
val employees = listOf(
    Employee("김철수", 28, "개발팀", 5500000),
    Employee("이영희", 32, "개발팀", 4800000)
)
val uniqueDepts = employees.distinctBy { it.department }
// 부서별로 첫 번째 직원만

// 사용 가능: List, Set, Array, Sequence
```

---

## 집계 함수

### sum / sumOf - 합계

```kotlin
val numbers = listOf(1, 2, 3, 4, 5)
val sum = numbers.sum()  // 15

val employees = listOf(...)
val totalSalary = employees.sumOf { it.salary }

// 사용 가능: List, Set, Array, Sequence
```

### average - 평균

```kotlin
val avg = numbers.average()  // 3.0

// 사용 가능: List, Set, Array, Sequence (숫자 타입만)
```

### count - 개수 세기

```kotlin
val count = numbers.count()  // 5
val evenCount = numbers.count { it % 2 == 0 }  // 2

// 사용 가능: List, Set, Array, Sequence
```

### maxOrNull / minOrNull - 최대/최소값

```kotlin
val max = numbers.maxOrNull()  // 5
val min = numbers.minOrNull()  // 1

// 사용 가능: List, Set, Array, Sequence
```

### maxByOrNull / minByOrNull - 특정 속성의 최대/최소

```kotlin
val highestPaid = employees.maxByOrNull { it.salary }
val youngest = employees.minByOrNull { it.age }

// 사용 가능: List, Set, Array, Sequence
```

---

## 검색 함수

### find / findLast - 첫/마지막 매칭 요소

```kotlin
val first = numbers.find { it > 3 }  // 4
val last = numbers.findLast { it > 3 }  // 5

// 사용 가능: List, Set, Array, Sequence
```

### first / last - 첫/마지막 요소

```kotlin
val first = numbers.first()  // 1
val last = numbers.last()  // 5
val firstEven = numbers.first { it % 2 == 0 }  // 2

// 사용 가능: List, Set, Array, Sequence
```

### firstOrNull / lastOrNull - null 안전 버전

```kotlin
val empty = emptyList<Int>()
val first = empty.firstOrNull()  // null

// 사용 가능: List, Set, Array, Sequence
```

### any / none / all - 조건 검사

```kotlin
val hasEven = numbers.any { it % 2 == 0 }  // true
val hasNegative = numbers.none { it < 0 }  // true
val allPositive = numbers.all { it > 0 }  // true

// 사용 가능: List, Set, Array, Sequence
```

### contains / containsAll - 포함 여부

```kotlin
val hasThree = numbers.contains(3)  // true
val hasAll = numbers.containsAll(listOf(1, 2, 3))  // true

// 사용 가능: List, Set, Array
```

---

## 결합 함수

### zip - 두 컬렉션 결합

```kotlin
val names = listOf("a", "b", "c")
val numbers = listOf(1, 2, 3)
val pairs = names.zip(numbers)  // [("a", 1), ("b", 2), ("c", 3)]

// 사용 가능: List, Array, Sequence
```

### associateWith / associateBy - Map으로 변환

```kotlin
val words = listOf("a", "ab", "abc")
val withLength = words.associateWith { it.length }
// {"a": 1, "ab": 2, "abc": 3}

val byLength = words.associateBy { it.length }
// {1: "a", 2: "ab", 3: "abc"}

// 사용 가능: List, Set, Array, Sequence
```

---

## 문자열 변환

### joinToString - 문자열로 결합

```kotlin
val joined = numbers.joinToString(", ")  // "1, 2, 3, 4, 5"
val custom = numbers.joinToString(
    separator = " | ",
    prefix = "[",
    postfix = "]"
)  // "[1 | 2 | 3 | 4 | 5]"

// 사용 가능: List, Set, Array, Sequence
```

---

## 다양한 구분자

### 단일 구분자

```kotlin
val csv = "1,2,3,4,5"
val numbers = csv.split(",")  // ["1", "2", "3", "4", "5"]
```

### 여러 구분자

```kotlin
val text = "apple,banana;cherry:grape"
val fruits = text.split(",", ";", ":")
// ["apple", "banana", "cherry", "grape"]
```

### 공백으로 분할

```kotlin
val sentence = "Hello World Kotlin"
val words = sentence.split(" ")  // ["Hello", "World", "Kotlin"]
```

### limit - 분할 횟수 제한

```kotlin
val text = "a,b,c,d,e"
val limited = text.split(",", limit = 3)
// ["a", "b", "c,d,e"]  // 2번만 분할
```

### ignoreCase - 대소문자 무시

```kotlin
val text = "appleXbananaXcherry"
val fruits = text.split("x", ignoreCase = true)
// ["apple", "banana", "cherry"]
```

---

## 실전 예제

```kotlin
// 부서별 평균 급여 (상위 2개 부서만)
val topDepartments = employees
    .groupBy { it.department }
    .mapValues { (_, emps) -> emps.map { it.salary }.average() }
    .toList()
    .sortedByDescending { (_, avg) -> avg }
    .take(2)

// 개발팀에서 30세 이상, 급여 상위 3명
val seniorDevs = employees
    .filter { it.department == "개발팀" }
    .filter { it.age >= 30 }
    .sortedByDescending { it.salary }
    .take(3)

// 부서별 인원수
val headcount = employees
    .groupBy { it.department }
    .mapValues { (_, emps) -> emps.count() }
```

```kotlin
package attendance.model

data class Employee(
    val name: String,
    val age: Int,
    val department: String,
    val salary: Int
) {
    init {
        require(name.isNotBlank()) { "이름은 비어있을 수 없습니다." }
        require(age > 0) { "나이는 0보다 커야합니다." }
        require(department.isNotBlank()) { "부서명은 비어있을 수 없습니다." }
        require(salary >= 0) { "급여는 음수일 수 없습니다." }
    }

    override fun toString(): String = "$name: $age, $department, $salary"
}
```

```kotlin
package attendance.model

object EmployeeStatistics {
    fun averageSalaryByDepartment(employees: List<Employee>): Map<String, Double> =
        employees
            .groupBy { it.department }
            .mapValues { (_, sa) -> sa.map { it.salary }.average() }

    fun employeeTop3(employees: List<Employee>): List<Employee> = employees.sortedByDescending { it.salary }.take(3)

    fun departmentTop3OnlySalaryInfo(employees: List<Employee>): Map<String, List<Int>> =
        employees.groupBy { it.department }
            .mapValues { (_, sa) -> sa.map { it.salary }.sortedByDescending { it }.take(3) }

    fun departmentTop3AllInfo(employees: List<Employee>): Map<String, List<Employee>> =
        employees.groupBy { it.department }
            .mapValues { (_, sa) -> sa.sortedByDescending { it.salary }.take(3) }

    fun developmentTeamOnly(employees: List<Employee>): List<Employee> =
        employees.filter { it.department == "개발팀" }
}
```