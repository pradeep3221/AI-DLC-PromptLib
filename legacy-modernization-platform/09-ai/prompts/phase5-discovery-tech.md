# Phase 5 (P5): Domain Discovery — Technology-Specific Extraction

> Technology-specific business rules extraction prompts for JS/TS, Java, Python, PHP,
> iOS/Swift, Salesforce Apex, Ruby, WebForms, Angular, and PowerShell codebases.

**⚠️ AI GUARDRAILS APPLY**: All prompts in this phase MUST follow the AI Guardrails defined in [ORCHESTRATION-PROMPT.md](ORCHESTRATION-PROMPT.md#ai-guardrails-anti-hallucination-rules). Apply the Confidence Level Framework to every extracted rule.

---

## Document Information

| Property | Value |
|----------|-------|
| **Document Version** | 4.0.0 |
| **Last Updated** | March 2026 |
| **Status** | Active |
| **Part Of** | Comprehensive Prompt Library |

### Related Documents

| Document | Description |
|----------|-------------|
| [PROMPT-INDEX.md](PROMPT-INDEX.md) | Quick reference catalog |
| [phase4-discovery-core.md](phase4-discovery-core.md) | Core domain discovery (P4.1–P4.7) |
| [phase6-discovery-legacy.md](phase6-discovery-legacy.md) | Legacy deep extraction (P6.1–P6.12) |
| [ORCHESTRATION-PROMPT.md](ORCHESTRATION-PROMPT.md) | Execution workflow & guardrails |

---

## Table of Contents

- [P5.1 JavaScript/TypeScript Business Rules](#p51-javascripttypescript-business-rules)
- [P5.2 Java Business Rules Extraction](#p52-java-business-rules-extraction)
- [P5.3 Python Business Rules Extraction](#p53-python-business-rules-extraction)
- [P5.4 PHP Business Rules Extraction](#p54-php-business-rules-extraction)
- [P5.5 iOS/Swift Business Rules Extraction](#p55-iosswift-business-rules-extraction)
- [P5.6 Salesforce Apex Extraction](#p56-salesforce-apex-extraction)
- [P5.7 Ruby Business Rules Extraction](#p57-ruby-business-rules-extraction)
- [P5.8 WebForms Business Rules Extraction](#p58-webforms-business-rules-extraction)
- [P5.9 Angular Business Rules Extraction](#p59-angular-business-rules-extraction)
- [P5.10 PowerShell Business Rules Extraction](#p510-powershell-business-rules-extraction)

---

## P5.1 JavaScript/TypeScript Business Rules

```
**Goal**: Extract business rules embedded in JS/TS frontend and Node.js backend code

**Scan Patterns**:

1. **Frontend Validation** (React/Vue/Angular):
   - Form validation schemas (Yup, Zod, Joi)
   - Component-level validation in onChange/onBlur handlers
   - Custom hooks with business logic (useCalculation, useEligibility)
   - Redux/Vuex/NgRx actions with business logic in reducers

2. **Backend Logic** (Node.js/Express/NestJS):
   - Middleware with authorization/validation rules
   - Service classes with business methods
   - Route handlers with inline business logic
   - Utility functions (calculateTotal, validateOrder)

3. **Shared Logic**:
   - Shared validation libraries
   - Constants files with business thresholds
   - Enum-like objects defining statuses/types

**Extract Per Rule**:

| File | Function/Method | Rule Description | Confidence | Evidence |
|------|-----------------|------------------|------------|----------|

**Key Patterns to Find**:
```javascript
// Validation rules
if (amount > MAX_ORDER_LIMIT) { ... }
const schema = z.object({ email: z.string().email(), age: z.number().min(18) })

// State transitions
if (order.status === 'pending' && canApprove(user)) { order.status = 'approved' }

// Calculations
const total = items.reduce((sum, i) => sum + i.price * i.qty, 0) * (1 - discount)

// Authorization
if (!user.roles.includes('admin') && order.amount > 10000) { throw new ForbiddenError() }
```

**Output**: /docs/domain/js-ts-business-rules.md
```

---

## P5.2 Java Business Rules Extraction

```
**Goal**: Extract business rules from Java codebases (Spring Boot, Jakarta EE, legacy J2EE)

**Scan Patterns**:

1. **Service Layer**:
   - @Service classes with business methods
   - @Transactional methods (transaction boundaries = business operations)
   - Custom exceptions (BusinessRuleViolationException, etc.)

2. **Validation**:
   - @Valid / @Validated annotations
   - Custom ConstraintValidator implementations
   - Manual validation in service methods

3. **Domain Model**:
   - Entity classes with business methods (not just getters/setters)
   - Value objects with validation in constructors
   - Enums with behavior (strategy pattern via enum)

4. **Integration**:
   - @Scheduled methods (cron jobs)
   - @JmsListener / @KafkaListener message handlers
   - REST clients calling external services

**Key Patterns**:
```java
// Business validation
@Service
public class OrderService {
    public void placeOrder(Order order) {
        if (order.getTotal() > customer.getCreditLimit())
            throw new CreditLimitExceededException();
    }
}

// State machine
public enum OrderStatus {
    DRAFT { public boolean canTransitionTo(OrderStatus next) { return next == SUBMITTED; } },
    SUBMITTED { ... }
}

// Specification pattern
public class EligibleForDiscountSpec implements Specification<Customer> {
    public boolean isSatisfiedBy(Customer c) {
        return c.getOrderCount() > 10 && c.getAccountAge() > Duration.ofDays(365);
    }
}
```

**Extract Per Rule**:

| Class | Method | Rule Description | Pattern | Confidence | Evidence |
|-------|--------|------------------|---------|------------|----------|

**Output**: /docs/domain/java-business-rules.md
```

---

## P5.3 Python Business Rules Extraction

```
**Goal**: Extract business rules from Python codebases (Django, Flask, FastAPI, scripts)

**Scan Patterns**:

1. **Django**:
   - Model validators (clean(), validate_*)
   - ModelForm clean methods
   - Signals (post_save, pre_delete) with business logic
   - Custom managers with business queries
   - Admin actions with business logic

2. **Flask/FastAPI**:
   - Route handlers with business logic
   - Marshmallow/Pydantic schemas with validators
   - Service modules with business functions

3. **Business Logic**:
   - Functions with calculate_*, validate_*, check_*, is_eligible_*
   - Decorator-based permissions
   - Celery tasks with business processing

**Key Patterns**:
```python
# Django model validation
class Order(models.Model):
    def clean(self):
        if self.total > self.customer.credit_limit:
            raise ValidationError("Exceeds credit limit")

# Calculation
def calculate_shipping(weight, destination, expedited=False):
    base_rate = RATES[destination]
    if weight > HEAVY_THRESHOLD:
        base_rate *= HEAVY_MULTIPLIER
    if expedited:
        base_rate *= EXPEDITED_FACTOR
    return base_rate

# State transition
ALLOWED_TRANSITIONS = {
    'draft': ['submitted'],
    'submitted': ['approved', 'rejected'],
    'approved': ['shipped'],
}
```

**Extract Per Rule**:

| Module | Function/Class | Rule Description | Confidence | Evidence |
|--------|----------------|------------------|------------|----------|

**Output**: /docs/domain/python-business-rules.md
```

---

## P5.4 PHP Business Rules Extraction

```
**Goal**: Extract business rules from PHP codebases (Laravel, Symfony, WordPress, legacy)

**Scan Patterns**:

1. **Laravel**:
   - Form Request classes (rules(), authorize())
   - Eloquent model events (creating, updating, deleting)
   - Gate/Policy definitions (authorization rules)
   - Middleware with business logic
   - Scheduled commands (console kernel)

2. **Symfony**:
   - Constraint validators
   - Voter classes
   - EventSubscriber with business logic

3. **Legacy PHP**:
   - Global functions with business logic
   - Include/require chains
   - Session-based state management
   - Direct SQL with business rules in WHERE clauses

**Key Patterns**:
```php
// Laravel Form Request
public function rules() {
    return [
        'amount' => 'required|numeric|min:0|max:' . config('business.max_order'),
        'status' => 'in:draft,submitted,approved',
    ];
}

// Policy
public function update(User $user, Order $order) {
    return $user->id === $order->user_id && $order->status === 'draft';
}

// Legacy business logic
function calculateDiscount($customer, $total) {
    if ($customer['loyalty_years'] > 5 && $total > 1000) {
        return $total * 0.15;
    }
    return $total * 0.05;
}
```

**Extract Per Rule**:

| File | Class/Function | Rule Description | Confidence | Evidence |
|------|----------------|------------------|------------|----------|

**Output**: /docs/domain/php-business-rules.md
```

---

## P5.5 iOS/Swift Business Rules Extraction

```
**Goal**: Extract business rules from iOS/Swift codebases

**Scan Patterns**:

1. **ViewModels / Presenters**:
   - Validation logic in view models
   - Business calculations before API calls
   - State management with business rules

2. **Managers / Services**:
   - *Manager.swift, *Service.swift files
   - Business logic in completion handlers
   - Offline rules (what to do when network unavailable)

3. **Core Data**:
   - NSManagedObject subclasses with validation
   - Fetch request predicates with business filters
   - Derived attributes

**Key Patterns**:
```swift
// Validation
func validateOrder(_ order: Order) -> [ValidationError] {
    var errors: [ValidationError] = []
    if order.total > customer.creditLimit {
        errors.append(.creditLimitExceeded)
    }
    if order.items.isEmpty {
        errors.append(.emptyOrder)
    }
    return errors
}

// State machine
enum OrderState {
    case draft, submitted, approved, shipped
    
    var allowedTransitions: [OrderState] {
        switch self {
        case .draft: return [.submitted]
        case .submitted: return [.approved, .draft]
        // ...
        }
    }
}
```

**Extract Per Rule**:

| File | Class/Method | Rule Description | Confidence | Evidence |
|------|-------------|------------------|------------|----------|

**Output**: /docs/domain/ios-swift-business-rules.md
```

---

## P5.6 Salesforce Apex Extraction

```
**Goal**: Extract business rules from Salesforce Apex codebases

**Scan Patterns**:

1. **Trigger Handlers**:
   - Before/after insert, update, delete triggers
   - Business rules in trigger handler classes
   - Cross-object validations

2. **Apex Classes**:
   - *Service.cls, *Handler.cls, *Helper.cls
   - @AuraEnabled methods (Lightning component backend)
   - Batch Apex execute() methods
   - Scheduled Apex execute() methods

3. **Validation Rules / Formulas**:
   - Formula fields with business calculations
   - Validation rules (metadata)
   - Process Builder / Flow definitions

4. **SOQL with Business Logic**:
   - Queries with complex WHERE clauses
   - Aggregate queries for business metrics

**Key Patterns**:
```apex
// Trigger validation
trigger OrderTrigger on Order__c (before insert, before update) {
    for (Order__c ord : Trigger.new) {
        if (ord.Total__c > ord.Account__r.Credit_Limit__c) {
            ord.addError('Exceeds credit limit');
        }
    }
}

// Service class
public class OrderService {
    public static void applyDiscount(List<Order__c> orders) {
        for (Order__c ord : orders) {
            if (ord.Customer_Tier__c == 'Gold' && ord.Total__c > 1000) {
                ord.Discount__c = 0.15;
            }
        }
    }
}
```

**Extract Per Rule**:

| File | Class/Method | Rule Description | Object | Confidence | Evidence |
|------|-------------|------------------|--------|------------|----------|

**Output**: /docs/domain/apex-business-rules.md
```

---

## P5.7 Ruby Business Rules Extraction

```
**Goal**: Extract business rules from Ruby codebases (Rails, Sinatra, scripts)

**Scan Patterns**:

1. **Rails Models**:
   - ActiveRecord validations (validates, validate)
   - Callbacks (before_save, after_create, etc.)
   - Scopes with business logic
   - Custom validation methods

2. **Service Objects**:
   - app/services/*_service.rb
   - PORO classes with call/perform/execute methods
   - Interactors / Use cases

3. **Controllers**:
   - before_action with authorization
   - Strong parameters (business field rules)
   - Custom actions with business logic

4. **Background Jobs**:
   - Sidekiq/ActiveJob workers
   - Scheduled jobs (whenever, clockwork)

**Key Patterns**:
```ruby
# Model validations
class Order < ApplicationRecord
  validates :total, numericality: { greater_than: 0 }
  validate :credit_limit_check
  
  private
  
  def credit_limit_check
    if total > customer.credit_limit
      errors.add(:total, "exceeds credit limit")
    end
  end
end

# Service object
class CalculateShippingService
  def call(order)
    base_rate = ShippingRate.for(order.destination)
    base_rate *= 1.5 if order.weight > HEAVY_THRESHOLD
    base_rate *= 2.0 if order.expedited?
    base_rate
  end
end
```

**Extract Per Rule**:

| File | Class/Method | Rule Description | Confidence | Evidence |
|------|-------------|------------------|------------|----------|

**Output**: /docs/domain/ruby-business-rules.md
```

---

## P5.8 WebForms Business Rules Extraction

```
**Goal**: Extract business rules deeply embedded in ASP.NET WebForms code-behind

**Why Special Treatment**: WebForms tightly couples UI with business logic, making extraction
particularly challenging. Business rules hide in event handlers, ViewState manipulations,
and page lifecycle methods.

**Scan Patterns**:

1. **Page Lifecycle Events**:
   - Page_Load / Page_Init with business logic
   - Page_PreRender with calculated display values
   - IsPostBack branches with different logic

2. **Control Event Handlers**:
   - Button_Click with business operations
   - GridView_RowCommand with row-level business logic
   - DropDownList_SelectedIndexChanged with cascading rules

3. **Validation**:
   - CustomValidator ServerValidate methods
   - Code-behind validation before save
   - JavaScript validation rules (if business-critical)

4. **Data Binding**:
   - ObjectDataSource / SqlDataSource with inline SQL
   - DataBound events with business transformations
   - Repeater/ListView ItemDataBound with conditional rendering

**Key Patterns**:
```csharp
// Button handler with business logic
protected void btnSubmit_Click(object sender, EventArgs e)
{
    decimal total = CalculateOrderTotal();
    if (total > GetCustomerCreditLimit(Session["CustomerID"]))
    {
        lblError.Text = "Credit limit exceeded";
        return;
    }
    // Process order...
}

// Page_Load with business initialization
protected void Page_Load(object sender, EventArgs e)
{
    if (!IsPostBack)
    {
        if (User.IsInRole("Manager"))
            pnlApproval.Visible = true;
        
        LoadPendingOrders(DateTime.Now.AddDays(-30));
    }
}

// GridView with business logic
protected void gvOrders_RowCommand(object sender, GridViewCommandEventArgs e)
{
    if (e.CommandName == "Approve")
    {
        int orderId = Convert.ToInt32(e.CommandArgument);
        ApproveOrder(orderId, User.Identity.Name);
    }
}
```

**Extract Per Page**:

| Page (*.aspx) | Event Handler | Business Rule | Confidence | Extract To |
|----------------|---------------|---------------|------------|------------|
| Orders.aspx | btnSubmit_Click | Credit limit check | HIGH | OrderValidator |
| Orders.aspx | Page_Load | Manager-only approval panel | MEDIUM | Authorization policy |

**Output**: /docs/domain/webforms-business-rules.md

**⚠️ Warning**: WebForms often has business logic spread across:
- Code-behind (.aspx.cs / .aspx.vb)
- Custom controls (.ascx.cs)
- App_Code/ folder
- Global.asax
All must be scanned together for complete extraction.
```

---

## P5.9 Angular Business Rules Extraction

```
**Goal**: Extract business rules from Angular codebases (AngularJS and Angular 2+)

**Scan Patterns**:

1. **Angular 2+ (TypeScript)**:
   - Component methods with business calculations
   - Custom validators (sync and async)
   - Guards (canActivate, canDeactivate) with business rules
   - Interceptors with business logic (e.g., token refresh rules)
   - NgRx effects/reducers with business state management
   - Pipes with business transformations

2. **AngularJS (JavaScript)**:
   - Controller $scope methods
   - Service/Factory business logic
   - Directive link functions with validation
   - Filter functions with business transformations

**Key Patterns**:
```typescript
// Custom validator
export function creditLimitValidator(customerService: CustomerService): AsyncValidatorFn {
  return (control: AbstractControl): Observable<ValidationErrors | null> => {
    return customerService.getCreditLimit().pipe(
      map(limit => control.value > limit ? { creditExceeded: true } : null)
    );
  };
}

// Guard with business logic
canActivate(route: ActivatedRouteSnapshot): boolean {
  const order = this.orderService.getCurrent();
  if (order.status !== 'draft') {
    this.router.navigate(['/orders', order.id, 'view']);
    return false;
  }
  return true;
}

// NgRx reducer with business state
on(OrderActions.applyDiscount, (state, { discount }) => {
  if (state.customerTier === 'Gold' && discount > 0.2) {
    return { ...state, discount: 0.2 }; // Cap at 20% for Gold
  }
  return { ...state, discount };
})
```

**Extract Per Rule**:

| File | Component/Service | Rule Description | Confidence | Evidence |
|------|-------------------|------------------|------------|----------|

**Output**: /docs/domain/angular-business-rules.md
```

---

## P5.10 PowerShell Business Rules Extraction

```
**Goal**: Extract business rules from PowerShell scripts and modules

**Why This Matters**: PowerShell scripts often contain critical business automation that
runs as scheduled tasks, deployment scripts, or data processing pipelines. These rules
are frequently undocumented and critical.

**Scan Patterns**:

1. **Scheduled Scripts**:
   - Data import/export with business transformations
   - Report generation with business calculations
   - Cleanup scripts with business retention rules
   - Monitoring scripts with business thresholds

2. **Admin Automation**:
   - User provisioning with business role assignments
   - Permission management with business authorization rules
   - Configuration scripts with business parameters

3. **Data Processing**:
   - CSV/Excel import with business validation
   - API integration scripts
   - Database maintenance with business-aware retention

**Key Patterns**:
```powershell
# Business threshold
$InactiveThresholdDays = 90
$accounts = Get-ADUser -Filter {LastLogonDate -lt $cutoffDate}
foreach ($account in $accounts) {
    if ($account.Department -ne "Executive") {
        Disable-ADAccount $account
        # Business rule: Executives are exempt from auto-disable
    }
}

# Data validation
function Validate-ImportData {
    param([PSObject[]]$Records)
    foreach ($record in $Records) {
        if ($record.Amount -gt 50000) {
            Write-Warning "High value transaction requires approval: $($record.ID)"
            $record | Export-Csv -Path $ApprovalQueue -Append
        }
    }
}

# Business calculation
function Calculate-Commission {
    param($SalesAmount, $Tier)
    switch ($Tier) {
        "Bronze" { return $SalesAmount * 0.05 }
        "Silver" { return $SalesAmount * 0.08 }
        "Gold"   { return $SalesAmount * 0.12 }
        default  { return $SalesAmount * 0.03 }
    }
}
```

**Extract Per Script**:

| Script | Function | Rule Description | Schedule | Confidence | Evidence |
|--------|----------|-----------------|----------|------------|----------|

**Migration Targets**:

| Current Form | Recommended Target |
|--------------|--------------------|
| Scheduled PS script | Azure Function (Timer) or .NET Worker |
| Manual admin script | API endpoint + UI |
| Data processing | Azure Data Factory or .NET service |
| Monitoring | Application Insights alerts |

**Output**: /docs/domain/powershell-business-rules.md
```
