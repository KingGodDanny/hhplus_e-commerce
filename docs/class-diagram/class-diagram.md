```mermaid
classDiagram
direction TB
class Users {
- Long user_id
- String name
- Timestamp created_at
- Timestamp updated_at
}

    class PointHistory {
	    -Long history_id
	    -Long point_id
	    -Int history_type
	    -Decimal amount
	    -Timestamp created_at
	    -Timestamp updated_at
        +getHistory()
        +createHistory()
        +updateHistory()
    }

    class Coupon {
	    -Long coupon_id
	    -String name
	    -Int coupon_stock
	    -Int coupon_state
	    -Float discount
	    -Timestamp created_at
	    -Timestamp updated_at
	    -Timestamp expired_at
        +getCoupon()
        +createCoupon()
        +updateCoupon()
    }

    class UserCoupon {
	    -Long user_coupon_id
	    -Long user_id
	    -Long coupon_id
	    -Int used_state
	    -Timestamp issued_at
	    -Timestamp used_at
        +getUserCoupon()
        +updateUserCoupon()
    }

    class Product {
	    -Long product_id
	    -String name
	    -Decimal price
	    -Int stock
	    -Int product_state
	    -Timestamp created_at
	    -Timestamp updated_at
        +updateProduct()
    }

    class Orders {
	    -Long order_id
	    -Long user_id
	    -Long total_price
	    -Long total_discount_rate
	    -Int order_state
	    -Int payment_state
	    -Timestamp created_at
	    -Timestamp updated_at
        +getOrder()
        +getOrderProduct()
        +getPopularProduct()
        +createOrder()
    }

    class OrderProduct {
	    -Long order_product_id
	    -Long order_id
	    -Long product_id
	    -Int product_quantity
	    -Decimal product_price
	    -Timestamp created_at
    }

    class Point {
	    Long point_id
	    -Long user_id
	    -Decimal amount
	    -Timestamp created_at
	    -Timestamp updated_at
        +charge()
        +use()
    }

    Users "1" --> "1" Point
    Point "1" --> "0..*" PointHistory
    Users "1" --> "0..*" UserCoupon
    Users "1" --> "0..*" Orders
    Coupon "1" --> "0..*" UserCoupon
    Orders "1" --> "0..*" UserCoupon
    Orders "1" --> "0..*" OrderProduct
    Product "1" --> "0..*" OrderProduct
