### **DATABASE TABLES - CÁC BẢNG DỮ LIỆU CHÍNH**

#### **A. USER MANAGEMENT TABLES**

**users**
| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| user_id | VARCHAR(36) | PRIMARY KEY | Unique user identifier |
| email | VARCHAR(255) | UNIQUE, NOT NULL | User email address |
| password_hash | VARCHAR(255) | NOT NULL | Hashed password |
| full_name | VARCHAR(255) | NOT NULL | User full name |
| phone | VARCHAR(20) | | User phone number |
| date_of_birth | DATE | | User birth date |
| gender | ENUM('M','F','O') | | User gender |
| created_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Account creation time |
| is_active | BOOLEAN | DEFAULT TRUE | Account status |
| role | ENUM('CUSTOMER','ADMIN','STAFF') | DEFAULT 'CUSTOMER' | User role |
| avatar_url | VARCHAR(500) | | Profile image URL |

**user_profiles**
| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| profile_id | VARCHAR(36) | PRIMARY KEY | Profile identifier |
| user_id | VARCHAR(36) | FOREIGN KEY, NOT NULL | Reference to users |
| first_name | VARCHAR(100) | | First name |
| last_name | VARCHAR(100) | | Last name |
| phone | VARCHAR(20) | | Phone number |
| avatar_url | VARCHAR(500) | | Profile image |
| date_of_birth | DATE | | Birth date |
| gender | ENUM('M','F','O') | | Gender |
| preferences | JSON | | User preferences |
| updated_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP ON UPDATE | Last update time |

**user_addresses**
| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| address_id | VARCHAR(36) | PRIMARY KEY | Address identifier |
| user_id | VARCHAR(36) | FOREIGN KEY, NOT NULL | Reference to users |
| full_name | VARCHAR(255) | NOT NULL | Recipient name |
| phone | VARCHAR(20) | NOT NULL | Contact phone |
| address | TEXT | NOT NULL | Street address |
| city | VARCHAR(100) | NOT NULL | City name |
| district | VARCHAR(100) | NOT NULL | District name |
| ward | VARCHAR(100) | NOT NULL | Ward name |
| postal_code | VARCHAR(10) | | Postal code |
| is_default | BOOLEAN | DEFAULT FALSE | Default address flag |
| created_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Creation time |

#### **B. PRODUCT MANAGEMENT TABLES**

**products**
| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| product_id | VARCHAR(36) | PRIMARY KEY | Product identifier |
| name | VARCHAR(255) | NOT NULL | Product name |
| description | TEXT | | Product description |
| brand | VARCHAR(100) | | Brand name |
| category_id | VARCHAR(36) | FOREIGN KEY | Reference to categories |
| subcategory | VARCHAR(100) | | Subcategory name |
| price | DECIMAL(10,2) | NOT NULL | Base price |
| sale_price | DECIMAL(10,2) | | Sale price |
| status | ENUM('ACTIVE','INACTIVE','DRAFT') | DEFAULT 'DRAFT' | Product status |
| created_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Creation time |
| updated_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP ON UPDATE | Last update |
| created_by | VARCHAR(36) | FOREIGN KEY | Creator user ID |
| seo_title | VARCHAR(255) | | SEO title |
| seo_description | TEXT | | SEO description |
| meta_keywords | TEXT | | Meta keywords |

**product_variants**
| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| variant_id | VARCHAR(36) | PRIMARY KEY | Variant identifier |
| product_id | VARCHAR(36) | FOREIGN KEY, NOT NULL | Reference to products |
| size | VARCHAR(20) | | Size (S, M, L, XL, etc.) |
| color | VARCHAR(50) | | Color name |
| material | VARCHAR(100) | | Material type |
| sku | VARCHAR(100) | UNIQUE | Stock keeping unit |
| price | DECIMAL(10,2) | | Variant price |
| stock | INTEGER | DEFAULT 0 | Stock quantity |
| status | ENUM('ACTIVE','INACTIVE') | DEFAULT 'ACTIVE' | Variant status |
| image_url | VARCHAR(500) | | Variant image |
| created_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Creation time |

**product_images**
| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| image_id | VARCHAR(36) | PRIMARY KEY | Image identifier |
| product_id | VARCHAR(36) | FOREIGN KEY, NOT NULL | Reference to products |
| variant_id | VARCHAR(36) | FOREIGN KEY | Reference to variants |
| image_url | VARCHAR(500) | NOT NULL | Image URL |
| alt_text | VARCHAR(255) | | Alt text for accessibility |
| sort_order | INTEGER | DEFAULT 0 | Display order |
| is_primary | BOOLEAN | DEFAULT FALSE | Primary image flag |
| image_type | ENUM('MAIN','GALLERY','THUMBNAIL') | DEFAULT 'GALLERY' | Image type |
| created_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Creation time |

**categories**
| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| category_id | VARCHAR(36) | PRIMARY KEY | Category identifier |
| name | VARCHAR(255) | NOT NULL | Category name |
| description | TEXT | | Category description |
| parent_id | VARCHAR(36) | FOREIGN KEY | Parent category |
| slug | VARCHAR(255) | UNIQUE | URL slug |
| image_url | VARCHAR(500) | | Category image |
| sort_order | INTEGER | DEFAULT 0 | Display order |
| is_active | BOOLEAN | DEFAULT TRUE | Active status |
| created_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Creation time |

#### **C. SHOPPING & ORDER TABLES**

**shopping_carts**
| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| cart_id | VARCHAR(36) | PRIMARY KEY | Cart identifier |
| user_id | VARCHAR(36) | FOREIGN KEY, NOT NULL | Reference to users |
| created_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Creation time |
| updated_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP ON UPDATE | Last update |
| total_amount | DECIMAL(10,2) | DEFAULT 0.00 | Total cart amount |
| total_items | INTEGER | DEFAULT 0 | Total items count |

**cart_items**
| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| item_id | VARCHAR(36) | PRIMARY KEY | Item identifier |
| cart_id | VARCHAR(36) | FOREIGN KEY, NOT NULL | Reference to cart |
| product_id | VARCHAR(36) | FOREIGN KEY, NOT NULL | Reference to products |
| variant_id | VARCHAR(36) | FOREIGN KEY | Reference to variants |
| quantity | INTEGER | NOT NULL, DEFAULT 1 | Item quantity |
| unit_price | DECIMAL(10,2) | NOT NULL | Unit price |
| total_price | DECIMAL(10,2) | NOT NULL | Total price |
| added_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Added time |

**orders**
| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| order_id | VARCHAR(36) | PRIMARY KEY | Order identifier |
| user_id | VARCHAR(36) | FOREIGN KEY, NOT NULL | Reference to users |
| order_number | VARCHAR(50) | UNIQUE, NOT NULL | Order number |
| status | ENUM('PENDING','CONFIRMED','PROCESSING','SHIPPED','DELIVERED','CANCELLED') | DEFAULT 'PENDING' | Order status |
| subtotal | DECIMAL(10,2) | NOT NULL | Subtotal amount |
| shipping_fee | DECIMAL(10,2) | DEFAULT 0.00 | Shipping fee |
| tax | DECIMAL(10,2) | DEFAULT 0.00 | Tax amount |
| total_amount | DECIMAL(10,2) | NOT NULL | Total amount |
| payment_method | VARCHAR(50) | | Payment method |
| payment_status | ENUM('PENDING','PAID','FAILED','REFUNDED') | DEFAULT 'PENDING' | Payment status |
| order_date | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Order date |
| delivery_date | TIMESTAMP | | Expected delivery |
| notes | TEXT | | Order notes |
| created_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Creation time |

**order_items**
| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| item_id | VARCHAR(36) | PRIMARY KEY | Item identifier |
| order_id | VARCHAR(36) | FOREIGN KEY, NOT NULL | Reference to orders |
| product_id | VARCHAR(36) | FOREIGN KEY, NOT NULL | Reference to products |
| variant_id | VARCHAR(36) | FOREIGN KEY | Reference to variants |
| product_name | VARCHAR(255) | NOT NULL | Product name at time of order |
| variant_name | VARCHAR(255) | | Variant details |
| quantity | INTEGER | NOT NULL | Quantity ordered |
| unit_price | DECIMAL(10,2) | NOT NULL | Unit price at time of order |
| total_price | DECIMAL(10,2) | NOT NULL | Total price |
| status | ENUM('PENDING','CONFIRMED','SHIPPED','DELIVERED','CANCELLED') | DEFAULT 'PENDING' | Item status |
| created_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Creation time |

#### **D. INVENTORY MANAGEMENT TABLES**

**inventory**
| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| inventory_id | VARCHAR(36) | PRIMARY KEY | Inventory identifier |
| product_id | VARCHAR(36) | FOREIGN KEY, NOT NULL | Reference to products |
| variant_id | VARCHAR(36) | FOREIGN KEY | Reference to variants |
| warehouse_id | VARCHAR(36) | FOREIGN KEY, NOT NULL | Reference to warehouses |
| current_stock | INTEGER | DEFAULT 0 | Current stock level |
| reserved_stock | INTEGER | DEFAULT 0 | Reserved stock |
| available_stock | INTEGER | GENERATED ALWAYS AS (current_stock - reserved_stock) | Available stock |
| minimum_stock | INTEGER | DEFAULT 0 | Minimum stock level |
| maximum_stock | INTEGER | DEFAULT 999999 | Maximum stock level |
| last_updated | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP ON UPDATE | Last update time |

**warehouses**
| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| warehouse_id | VARCHAR(36) | PRIMARY KEY | Warehouse identifier |
| name | VARCHAR(255) | NOT NULL | Warehouse name |
| address | TEXT | NOT NULL | Warehouse address |
| city | VARCHAR(100) | NOT NULL | City |
| phone | VARCHAR(20) | | Contact phone |
| manager | VARCHAR(255) | | Manager name |
| is_active | BOOLEAN | DEFAULT TRUE | Active status |
| created_at | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Creation time |

**stock_transactions**
| Column | Data Type | Constraints | Description |
|--------|-----------|-------------|-------------|
| transaction_id | VARCHAR(36) | PRIMARY KEY | Transaction identifier |
| product_id | VARCHAR(36) | FOREIGN KEY, NOT NULL | Reference to products |
| variant_id | VARCHAR(36) | FOREIGN KEY | Reference to variants |
| warehouse_id | VARCHAR(36) | FOREIGN KEY, NOT NULL | Reference to warehouses |
| type | ENUM('IN','OUT','ADJUSTMENT','TRANSFER') | NOT NULL | Transaction type |
| quantity | INTEGER | NOT NULL | Quantity change |
| reason | TEXT | | Transaction reason |
| reference | VARCHAR(100) | | Reference number |
| transaction_date | TIMESTAMP | DEFAULT CURRENT_TIMESTAMP | Transaction date |
| created_by | VARCHAR(36) | FOREIGN KEY | Creator user ID |