```mermaid
erDiagram
USERS ||--o| POINT: ""
POINT ||--|{ POINT_HISTORY: ""
USERS ||--o{ USER_COUPON: ""
USERS ||--o{ ORDERS: ""
COUPON ||--o{ USER_COUPON: ""
ORDERS }o--|| USER_COUPON: ""
ORDERS ||--|{ ORDER_PRODUCT: ""
PRODUCT ||--o{ ORDER_PRODUCT: ""


    USERS {
        LONG user_id PK "사용자 ID"
        VARCHAR name "이름"
        TIMESTAMP created_at "생성일시"
        TIMESTAMP updated_at "수정일시"
    }

    POINT {
        LONG point_id PK "잔고 ID"
        LONG user_id FK "사용자 ID"
        DECIMAL amount "잔고 금액"
        TIMESTAMP created_at "생성일시"
        TIMESTAMP updated_at "수정일시"
    }

    POINT_HISTORY {
        LONG history_id PK "이력 ID"
        LONG point_id FK "잔고 ID"
        INT history_type "이력 타입"
        DECIMAL amount "거래 금액"
        TIMESTAMP created_at "생성일시"
        TIMESTAMP updated_at "수정일시"
    }

    COUPON {
        LONG coupon_id PK "쿠폰 ID"
        VARCHAR name "이름"
        INT coupon_stock "수량"
        INT coupon_state "쿠폰 상태"
        FLOAT discount "할인율"
        TIMESTAMP created_at "생성일시"
        TIMESTAMP updated_at "수정일시"
        TIMESTAMP expired_at "만료일시"
    }

    USER_COUPON {
        LONG user_coupon_id PK "사용자 쿠폰 ID"
        LONG user_id FK "사용자 ID"
        LONG coupon_id FK "쿠폰 ID"
        INT used_state "사용 상태"
        TIMESTAMP issued_at "발급일시"
        TIMESTAMP used_at "사용일시"
    }

    PRODUCT {
        LONG product_id PK "상품 ID"
        VARCHAR name "이름"
        DECIMAL price "가격"
        INT stock "재고 수량"
        INT product_state "판매 상태"
        TIMESTAMP created_at "생성일시"
        TIMESTAMP updated_at "수정일시"
    }

    ORDERS {
        LONG order_id PK "주문 ID"
        LONG user_id FK "사용자 ID"
        LONG total_price "주문 총 금액"
        LONG total_discount_rate "총 할인율"
        int order_state "주문 상태"
        int payment_state "결제 상태"
        TIMESTAMP created_at "생성일시"
        TIMESTAMP updated_at "수정일시"
    }

    ORDER_PRODUCT {
        LONG order_product_id PK "주문 상품 ID"
        LONG order_id FK "주문 ID"
        LONG product_id FK "상품 ID"
        INT product_quantity "상품 개수"
        DECIMAL product_price "상품 금액"
        TIMESTAMP created_at "생성일시"
    }
