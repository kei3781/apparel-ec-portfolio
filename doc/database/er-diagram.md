erDiagram 
USERS ||--o{ ADDRESSES : has
USERS ||--o{ FAVORITES : has
USERS ||--|| CARTS : owns
USERS ||--o{ ORDERS : places

CATEGORIES ||--o{ PRODUCTS : contains

PRODUCTS ||--o{ PRODUCT_IMAGES : has
PRODUCTS ||--o{ PRODUCT_VARIANTS : has

SIZES ||--o{ PRODUCT_VARIANTS : uses
COLORS ||--o{ PRODUCT_VARIANTS : uses 

CARTS ||--o{ CART_ITEMS : contains

PRODUCT_VARIANTS ||--o{ CART_ITEMS : selected

ORDERS ||--o{ ORDER_ITEMS : contains 

PRODUCT_VARIANTS ||--o{ ORDER_ITEMS : ordered 

ORDERS ||--|| PAYMENTS : paid_by 

USERS { 
 bigint id PK 
 string name 
 string email 
 string password 
} 

ADDRESSES { 
  bigint id PK 
  bigint user_id FK 
  string postal_code 
  string prefecture 
  string city 
  string address1 
  string address2 
  string phone_number 
} 

CATEGORIES { 
  bigint id PK 
  string name 
  string slug 
} 

PRODUCTS { 
  bigint id PK 
  bigint category_id FK 
  string name 
  text description 
  integer price 
  boolean status 
} 

PRODUCT_IMAGES { 
  bigint id PK 
  bigint product_id FK 
  string image_path 
  integer sort_order 
} 

SIZES { 
  bigint id PK 
  string name 
} 

COLORS { 
  bigint id PK 
  string name 
  string code 
} 

PRODUCT_VARIANTS { 
  bigint id PK 
  bigint product_id FK 
  bigint size_id FK 
  bigint color_id FK 
  string sku 
  integer stock 
} 

FAVORITES { 
  bigint id PK 
  bigint user_id FK 
  bigint product_id FK 
} 

CARTS { 
  bigint id PK 
  bigint user_id FK 
} 

CART_ITEMS { 
  bigint id PK 
  bigint cart_id FK 
  bigint product_variant_id FK 
  integer quantity 
} 

ORDERS { 
  bigint id PK 
  bigint user_id FK 
  bigint address_id FK 
  integer total_price 
  string status 
} 

ORDER_ITEMS { 
  bigint id PK 
  bigint order_id FK 
  bigint product_variant_id FK
  integer price
  integer quantity 
} 

PAYMENTS { 
  bigint id PK 
  bigint order_id FK 
  string stripe_payment_intent_id 
  integer amount 
  string status 
  timestamp paid_at 
}