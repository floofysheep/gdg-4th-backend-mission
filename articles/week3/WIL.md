# 3주차 WIL
## 1. JavaDoc
Java에서 코드에 주석으로 API 문서를 생성하는 도구이다. Java 표준 도구 중 하나이며, 주로 클래스, 메서드, 필드에 설명을 추가하여 HTML 형식의 문서를 자동 생성한다. 

대부분의 IDE에 JavaDoc이 내장되어 있어 설치가 따로 필요하지는 않다.

JavaDoc의 기본 문법은 다음과 같다.
```java
/**
 * [요약 설명]  ← 한 줄 요약 (한 문장으로 시작)
 * [상세 설명]  ← 선택 사항, 여러 줄 가능
 *
 * @태그 설명    ← 여러 개 사용 가능
 */

```

📌 **자주 사용하는 태그**

| 태그                        | 설명                    |
| ------------------------- | --------------------- |
| **`@author`**                 | 작성자 이름                |
| **`@version`**                | 버전 정보                 |
| **`@param`**                  | 메서드의 매개변수 설명          |
| **`@return` **                | 메서드의 반환값 설명           |
| **`@throws`** 또는 **`@exception`** | 발생할 수 있는 예외 설명        |
| **`@see`**                    | 관련 클래스, 메서드, 문서 등을 참조 |
| **`@since`**                  | 처음 등장한 버전             |
| **`@deprecated` **            | 더 이상 사용되지 않음을 표시      |
| **`{@link ClassName}`**       | 해당 클래스에 대한 링크 생성      |
| **`{@code 코드}`**              | 코드 블록을 인라인으로 표시       |


### ✅ **적용**
1주차 때 만든 쇼핑몰 프로젝트에 javaDoc을 적용해보았다. 다음은 그 중 search 메소드에 대한 코드이다.
```java
/**
     * 상품 이름으로 재고를 조회합니다.
     * @param name 검색할 상품 이름
     * @return 상품 정보
     */
    @Operation(summary = "상품 조회", description = "상품 이름으로 재고를 조회합니다.")
    @GetMapping("/search")
    public Item search(@RequestParam String name) {
        return consumerService.findItem(name);
    }
```
위 주석을 삽입하였을 때, IntelliJ에서 마우스를 올리면 다음과 같은 설명을 확인해볼 수 있다.
![](https://velog.velcdn.com/images/sheep_/post/1b3c579d-a94d-4d65-8587-561be571fb4b/image.png)

javaDoc을 사용하면 코드의 목적과 사용 방법을 명확하게 알 수 있어 코드의 이해가 편해지고 이에 따라 협업 시에 유용한 도구로 사용될 것 같다는 생각이 든다. 
```
/**
**/
```
처음에 봤을 때 위 주석 처리에 오타가 나서 *의 하나가 다른 줄로 가있다고 생각했는데 내가 틀리게 생각한 거였다. 직접 적용하여 보니까 일반 주석보다 더 유용하다고 생각된다...

## 2. Swagger
RESTful API를 명세화하고 문서화하는 표준 프레임워크이다. API의 구조, 입출력, 경로 등을 JSON 또는 YAML 형식으로 문서화하며, 자동으로 인터랙티브한 웹 UI 문서를 생성한다.

📌 **spring에서 자주 쓰이는 Swagger 어노테이션**

| 어노테이션          | 설명                |
| -------------- | ----------------- |
| **`@Operation`**   | 특정 API 메서드에 대한 설명 |
| **`@Parameter`**   | 파라미터 설명           |
| **`@Schema`**      | 객체 속성 설명 (DTO 등)  |
| **`@Tag`**         | API 그룹화           |
| **`@ApiResponse`** | 응답 설명             |

### ✅ **적용**
javaDoc을 적용한 코드에 swagger까지 적용해보겠다.
```java
/**
     * 상품 이름으로 재고를 조회합니다.
     * @param name 검색할 상품 이름
     * @return 상품 정보
     */
    @Operation(summary = "상품 조회", description = "상품 이름으로 재고를 조회합니다.")
    @GetMapping("/search")
    public Item search(@RequestParam String name) {
        return consumerService.findItem(name);
    }
```

swagger 사용을 위해서는 의존성 목록에 아래 코드를 추가해줘야한다.
```java
implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.0.2'
```
swagger 또한 협업 시 유용한 도구라는 것을 알 수 있다. 하지만 아직 사용 방법에 대해서는 조금은 익숙하지 않은 듯한 느낌이다. ~~자동으로 API 문서를 생성해준다고 하는데 확인을 못하고 있다. (확인해보기...)~~
## 3. ORM(Object-Relation Mapping)
**ORM**은 객체지향 프로그래밍 언어의 객체를 관계형 데이터베이스의 테이블과 자동으로 매핑해주는 기술이다. 이에 SQL을 직접 작성하지 않고도 DB와 상호작용할 수 있게 도와준다. Java에서 대표적으로 사용하는 이러한 도구는 **Hibernate**이다.

장점으로는, SQL을 직접 작성하지 않아도 되므로 개발 속도가 빨라 생산성이 향상될 수 있다. 또한 특정 DBMS(Database Management System)에 종속되어 있지 않아 다른 DB로의 교체가 비교적 쉽다. 

단점으로는, 복잡합 Query의 경우 직접 작성하기 어렵다. 또한 자동으로 생성한 SQL을 직접 확인하기 어려워 디버깅 과정에서 어려움을 겪을 수 있다.



## 4. 영속성 컨텍스트(Persistence Context)
영속성 컨텍스트는 엔티티(Entity)를 영구 저장하는 환경이라는 의미를 가진다. 이는 JPA의 핵심으로 엔티티를 추적하고 변경을 자동 반영하게 해주는 캐시 역할을 한다.

Entitiy의 4가지의 생명주기에 대해서도 알아보자. 

1️⃣ **비영속**
영속성 컨텍스트와 관계가 없는 상태로 아직 DB와 연결되지 않은 상태이다.

2️⃣ **영속**
영속성 컨텍스트에서 관리 중인 상태로 DB에 저장된 상태이다.

3️⃣ **준영속**
영속 상태였으나, 더 이상 영속성 컨텍스트에서 관리되지 않는 상태이다.

4️⃣ **삭제**
삭제 대상이 되어 DB에서 삭제가 될 예정인 상태이다.

### **✅ 적용** 
이제 Hibernate가 save() 메소드를 호출할 때 작용 방식에 대해 살펴보자.
save()를 호출하면 Hibernate는 다음과 같이 동작한다.
```java
itemRepository.save(item);
```
- item이 새로운 객체이면 → INSERT INTO item ... 쿼리를 생성해서 실행

- item이 이미 DB에 있는 ID를 가진 객체이면 → UPDATE item ... 쿼리를 생성해서 실행
즉, save() 하나로 상황에 따라 insert 또는 update가 자동으로 발생하게 된다.

다음으로는 @Transactional을 적용하여 변경 감지(Dirty Checking)에 대해 알아보려고 한다. **변경 감지(Dirty Checking)**란, 영속성 컨텍스트가 관리하는 객체들이 등록, 변경, 수정, 삭제가 되었을때 DB에 반영되도록 하는 것이다.

```java
@Transactional
public void addStock(String name, int count) {
    Item item = itemRepository.findByName(name)
                 .orElseThrow(() -> new IllegalArgumentException("상품 없음"));

    item.setStock(item.getStock() + count); // 여기서 변경 발생

    // save() 없어도 실제 DB에 UPDATE 쿼리 나감
}

```
이때 `@Transactional`로 트랜잭션 열림 → `item`은 영속 상태 → 변경 감지 → 커밋 시 UPDATE 과정으로 작동된다.

## 추가.
### JPA(Java Persistence API)
자바에서 객체를 데이터베이스에 저장하고 관리하기 위한 인터페이스와 기능을 제공하는 API이다. 

그 구조는 다음과 같다.
```
JPA (인터페이스)
 └─ Hibernate (구현체, 가장 널리 쓰임)
      └─ Spring Data JPA (스프링이 편하게 사용할 수 있도록 감싼 라이브러리)

```

>**JPA** = 자바 객체 <-> DB 자동 매핑 도와주는 ORM 기술 (인터페이스 명세)
**Hibernate** = JPA의 대표 구현체
**Spring Data JPA** = 스프링 환경에서 JPA를 더 편하게 쓰도록 도와주는 라이브러리


### 🌟 마치며
javaDoc과 swagger를 실제 프로젝트에 적용해보았는데 `@param`, `@return`과 `@Operation` 태그만 사용해봐서, 다른 태그들도 이용해서 그 기능들을 조금 더 심층적으로 알아가야겠다. 'ORM은 객체와 테이블을 자동으로 매핑해주는 기술로 그 과정 중간에 영속성 컨텍스트가 관여하고 있다.' 이 개념 자체는 추상적으로 다가와서 실제 적용 과정을 통해 아주 조금은 이해를 한 것 같다. Entity의 4가지 생명주기 중 준영속에 대해서는 조금 더 학습이 필요한 듯하다. 

1주차 쇼핑몰 프로젝트에서 기능별로 클래스를 나누고 재작성해보았다. 또한 해당 메소드에 적절한 javaDoc과 swagger를 적용해보았다. 적절한 어노테이션 적용이나 코드 작성에 아직은 어려움을 느낀다. 시험이 끝나면 좋은 코드 구현을 위한 학습에 많은 시간을 투자해야겠다.

