### **MACHINE DIAGRAM - SƠ ĐỒ TRẠNG THÁI HỆ THỐNG**

```mermaid
stateDiagram-v2
    [*] --> SystemStartup
    
    SystemStartup --> SystemReady
    SystemStartup --> SystemError
    
    SystemError --> SystemRecovery
    SystemRecovery --> SystemReady
    SystemRecovery --> SystemError
    
    SystemReady --> UserAuthentication
    SystemReady --> ProductBrowsing
    SystemReady --> AdminAccess
    
    %% User Authentication States
    UserAuthentication --> UserRegistration
    UserAuthentication --> UserLogin
    UserAuthentication --> GuestAccess
    
    UserRegistration --> EmailVerification
    EmailVerification --> AccountActivated
    EmailVerification --> RegistrationFailed
    
    UserLogin --> LoginSuccess
    UserLogin --> LoginFailed
    LoginFailed --> UserLogin
    LoginFailed --> PasswordReset
    
    PasswordReset --> PasswordResetEmail
    PasswordResetEmail --> NewPasswordSet
    NewPasswordSet --> LoginSuccess
    
    AccountActivated --> LoginSuccess
    LoginSuccess --> UserDashboard
    GuestAccess --> ProductBrowsing
    
    %% Product Browsing States
    ProductBrowsing --> ProductSearch
    ProductBrowsing --> CategoryFilter
    ProductBrowsing --> CollectionView
    ProductBrowsing --> ProductDetail
    
    ProductSearch --> SearchResults
    SearchResults --> ProductDetail
    SearchResults --> ProductBrowsing
    
    CategoryFilter --> FilteredProducts
    FilteredProducts --> ProductDetail
    FilteredProducts --> ProductBrowsing
    
    CollectionView --> CollectionProducts
    CollectionProducts --> ProductDetail
    CollectionProducts --> ProductBrowsing
    
    ProductDetail --> AddToCart
    ProductDetail --> AddToWishlist
    ProductDetail --> WriteReview
    ProductDetail --> ProductBrowsing
    
    %% Shopping Cart States
    AddToCart --> CartUpdated
    CartUpdated --> CartManagement
    CartUpdated --> ProductDetail
    
    CartManagement --> UpdateQuantity
    CartManagement --> RemoveItem
    CartManagement --> CheckoutProcess
    CartManagement --> ProductBrowsing
    
    UpdateQuantity --> CartUpdated
    RemoveItem --> CartUpdated
    
    AddToWishlist --> WishlistUpdated
    WishlistUpdated --> WishlistManagement
    WishlistUpdated --> ProductDetail
    
    WishlistManagement --> MoveToCart
    WishlistManagement --> RemoveFromWishlist
    WishlistManagement --> ProductBrowsing
    
    MoveToCart --> CartUpdated
    RemoveFromWishlist --> WishlistUpdated
    
    %% Checkout Process States
    CheckoutProcess --> ShippingInfo
    ShippingInfo --> PaymentMethod
    PaymentMethod --> OrderReview
    OrderReview --> OrderConfirmation
    OrderReview --> ShippingInfo
    OrderReview --> PaymentMethod
    
    OrderConfirmation --> PaymentProcessing
    PaymentProcessing --> PaymentSuccess
    PaymentProcessing --> PaymentFailed
    
    PaymentFailed --> PaymentMethod
    PaymentFailed --> CheckoutProcess
    
    PaymentSuccess --> OrderCreated
    OrderCreated --> OrderProcessing
    OrderCreated --> InventoryReservation
    
    %% Order Processing States
    OrderProcessing --> InventoryCheck
    InventoryCheck --> StockAvailable
    InventoryCheck --> StockUnavailable
    
    StockUnavailable --> OrderCancelled
    StockAvailable --> OrderConfirmed
    
    OrderConfirmed --> WarehouseNotification
    WarehouseNotification --> OrderPicking
    OrderPicking --> OrderPacked
    OrderPacked --> OrderShipped
    
    OrderShipped --> InTransit
    InTransit --> OutForDelivery
    OutForDelivery --> Delivered
    
    Delivered --> OrderCompleted
    OrderCompleted --> ReviewProduct
    OrderCompleted --> OrderHistory
    
    OrderCancelled --> RefundProcessing
    RefundProcessing --> RefundCompleted
    
    %% Review States
    ReviewProduct --> ReviewSubmitted
    ReviewSubmitted --> ReviewModeration
    ReviewModeration --> ReviewApproved
    ReviewModeration --> ReviewRejected
    
    ReviewApproved --> ReviewPublished
    ReviewRejected --> ReviewResubmit
    ReviewResubmit --> ReviewSubmitted
    
    %% Admin States
    AdminAccess --> AdminDashboard
    AdminDashboard --> OrderManagement
    AdminDashboard --> ProductManagement
    AdminDashboard --> InventoryManagement
    AdminDashboard --> UserManagement
    AdminDashboard --> ReportGeneration
    
    OrderManagement --> OrderStatusUpdate
    OrderStatusUpdate --> OrderProcessing
    
    ProductManagement --> ProductUpdate
    ProductUpdate --> ProductPublished
    
    InventoryManagement --> StockUpdate
    StockUpdate --> InventoryUpdated
    
    UserManagement --> UserStatusUpdate
    UserStatusUpdate --> UserUpdated
    
    ReportGeneration --> ReportGenerated
    ReportGenerated --> AdminDashboard
    
    %% System Maintenance States
    SystemReady --> SystemMaintenance
    SystemMaintenance --> DatabaseBackup
    SystemMaintenance --> SystemUpdate
    SystemMaintenance --> SecurityAudit
    
    DatabaseBackup --> BackupCompleted
    SystemUpdate --> UpdateCompleted
    SecurityAudit --> AuditCompleted
    
    BackupCompleted --> SystemReady
    UpdateCompleted --> SystemReady
    AuditCompleted --> SystemReady
    
    %% Error Handling States
    SystemError --> ErrorLogging
    ErrorLogging --> ErrorNotification
    ErrorNotification --> SystemRecovery
    
    %% End States
    OrderCompleted --> [*]
    RefundCompleted --> [*]
    ReviewPublished --> [*]
    SystemReady --> [*]
```