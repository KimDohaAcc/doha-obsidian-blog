---
{"dg-publish":true,"permalink":"/공부/SW/BO(Business Object)/","dgPassFrontmatter":true}
---


비지니스 로직을 처리하는 객체

주로 비지니스 규칙 구현, 데이터 처리, 연산 수행에 사용된다
BO는 비지니스 도메인에서의 객체를 나타내며 비지니스 규칙을 캡슐화하고 적용하는 데 사용한다

```java
public class OrderBO {
    public boolean placeOrder(Order order) {
        // 주문 유효성 검사 및 처리 로직
        if (order.isValid()) {
            // 주문 데이터베이스에 저장 및 기타 비즈니스 로직 처리
            // ...
            return true;
        } else {
            return false;
        }
    }

    public boolean cancelOrder(Order order) {
        // 주문 취소 처리 로직
        // ...
        return true;
    }

    public double calculateTotalPrice(Order order) {
        // 주문에 대한 총 가격 계산 로직
        double totalPrice = 0.0;
        // ...
        return totalPrice;
    }
}

```