# Phase 4 (P4): Domain Discovery — Core Prompts

> Core domain discovery prompts for multi-technology scanning, service contract analysis,
> VB.NET extraction, WPF analysis, console/worker analysis, and stored procedure deep extraction.

**⚠️ AI GUARDRAILS APPLY**: All prompts in this phase MUST follow the AI Guardrails defined in [ORCHESTRATION-PROMPT.md](ORCHESTRATION-PROMPT.md#ai-guardrails-anti-hallucination-rules). Key rules:
- **Business rules require confidence levels** with defined criteria (see Confidence Framework)
- **Include evidence** (file path, line numbers, code snippets) for every extracted rule
- **Flag uncertain rules** for human validation — do not present assumptions as facts
- **Cross-reference with tests/docs** to validate extracted rules

### UNCERTAIN Flag — When to Use

| Scenario | Example | Action Required |
|----------|---------|-----------------|
| Cannot distinguish business rule from technical code | Error handling that might encode business policy | Flag for SME review |
| Logic appears in multiple places with variations | Same calculation done differently in 2 files | Flag for clarification |
| Naming suggests business rule but logic unclear | `ValidateSpecialCase()` with complex nested IFs | Flag for documentation |
| Rule seems important but no documentation exists | Complex CASE statement with magic numbers | Flag for business analyst |
| Conflicting implementations found | SP does X, code does Y for same operation | Flag as conflict |

**UNCERTAIN rules MUST NOT be migrated without explicit human sign-off.**

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
| [phase1-inventory.md](phase1-inventory.md) | Prerequisite: Inventory & assessment |
| [phase3-architecture-scoring.md](phase3-architecture-scoring.md) | Feeds into: Scoring & triangulation |
| [phase5-discovery-tech.md](phase5-discovery-tech.md) | Technology-specific extraction (P5.1–P5.10) |
| [phase6-discovery-legacy.md](phase6-discovery-legacy.md) | Legacy deep extraction (P6.1–P6.12) |
| [ORCHESTRATION-PROMPT.md](ORCHESTRATION-PROMPT.md) | Execution workflow & guardrails |

---

## Table of Contents

- [P4.1 Multi-Technology Domain Scan](#p41-multi-technology-domain-scan)
- [P4.2 Service Contract Analysis (WCF/ASMX)](#p42-service-contract-analysis-wcfasmx)
- [P4.3 VB.NET Business Rules Extraction](#p43-vbnet-business-rules-extraction)
- [P4.4 WPF ViewModel Analysis](#p44-wpf-viewmodel-analysis)
- [P4.5 Console/Worker Service Analysis](#p45-consoleworker-service-analysis)
- [P4.6 Stored Procedure Deep Business Rules Extraction](#p46-stored-procedure-deep-business-rules-extraction)
- [P4.7 Identify SP Caller Technologies](#p47-identify-sp-caller-technologies)

---

## P4.1 Multi-Technology Domain Scan

```
**Goal**: Discover domain concepts across ALL technology types in the codebase

**Prerequisite**: P1.1 Component Inventory (know what techs exist)

**Scan by Technology**:

1. **ASP.NET WebForms** (*.aspx.cs, *.aspx.vb):
   - Page_Load business logic
   - Button click handlers
   - GridView data binding
   - User control interactions

2. **WCF Services** (*.svc, *Service.cs):
   - [ServiceContract] interfaces
   - [DataContract] classes
   - [OperationContract] methods
   - [FaultContract] definitions

3. **WPF Applications** (*.xaml.cs, *ViewModel.cs):
   - ICommand implementations
   - INotifyPropertyChanged properties
   - Converters with business logic
   - Validation rules

4. **Console/Worker** (Program.cs, *Worker.cs):
   - Main method logic
   - Command handlers
   - Scheduled task logic
   - Background processing

5. **VB.NET** (*.vb):
   - Module-level functions
   - Class methods
   - Business rule Sub/Functions

6. **Stored Procedures** (*.sql):
   - Procedures with IF/CASE logic
   - Triggers
   - Computed columns
   - Views with joins

7. **ASP.NET MVC / Web API** (*Controller.cs):
   - Action methods with business logic
   - Filters with business rules
   - Model validation attributes

8. **Entity Framework** (*Context.cs, *Configuration.cs):
   - SaveChanges overrides
   - Query filters
   - Computed columns
   - Seeded data

**Output**: /docs/domain/entity-candidates.md

**Per Domain Concept**:
| Name | Source Files | Technology | Code Snippet | Confidence |
|------|-------------|------------|--------------|------------|

**Feeds Into**:
- P1.4 Domain Model
- P3.3 Triangulation
```

---

## P4.2 Service Contract Analysis (WCF/ASMX)

```
**Goal**: Extract domain concepts from service contracts

**Scan**:
- [ServiceContract] interfaces
- [DataContract] classes
- [OperationContract] methods
- WSDL files if available

**Extract**:

1. **Operations → Commands/Queries**:
| Operation | HTTP Verb | Command/Query Name | Domain |
|-----------|-----------|-------------------|--------|
| CreateOrder | POST | CreateOrderCommand | Orders |
| GetOrder | GET | GetOrderQuery | Orders |
| UpdateStatus | PUT | UpdateStatusCommand | Orders |

2. **Data Contracts → DTOs/Entities**:
| DataContract | Properties | Maps To Entity | Domain |
|--------------|------------|----------------|--------|
| OrderDTO | Id, Date, Items | Order | Orders |

3. **Fault Contracts → Error Handling**:
| FaultContract | Condition | API Response | Business Rule? |
|---------------|-----------|--------------|:--------------:|
| ValidationFault | Invalid input | 400 Bad Request | No (technical) |
| CreditExceededFault | Over limit | 422 Unprocessable | Yes |

**Output**: /docs/domain/service-analysis.md
```

---

## P4.3 VB.NET Business Rules Extraction

```
**Goal**: Identify domain logic in VB.NET codebases

**What We Extract** (Business Rules include):
- **Validation Logic**: Data constraints, required fields, range checks, format validation
- **Calculation Formulas**: Pricing, discounts, totals, taxes, commissions, derived values
- **State-Transition Rules**: Status changes, workflow progression, lifecycle management
- **Conditional Business Logic**: Type-specific behavior, eligibility rules, authorization checks
- **Cross-Entity Rules**: Credit limits, inventory constraints, referential business rules

**Scan Patterns**:
```vb
' Business rule patterns to find:
Public Function Calculate*(...)
Public Sub Validate*(...)
If ... Then ... ElseIf (complex conditionals)
Select Case (switch statements)
Module *Rules
Module *Calculations
Class *Process
Class *Manager
```

**Extract**:
1. **Functions with Business Logic**: Calculations, validations, transitions, transformations
2. **Module-Level Constants**: Magic numbers → Named constants, Status codes → Enums

**Output**: /docs/domain/vb-business-logic.md

**Format**:
| Module/Class | Method | Business Rule | Confidence | Migrate To |
|--------------|--------|---------------|------------|------------|
| OrderModule | CalculateTotal | Sum + Tax + Discount | HIGH — has unit test | OrderDomainService |
| CustomerModule | ValidateCredit | Credit limit check | MEDIUM — clear logic, no test | CustomerValidator |

**⚠️ AI GUARDRAIL**: Apply confidence criteria from the Confidence Level Framework to ALL rules.
For each extracted rule, include:
- Confidence level (HIGH/MEDIUM/LOW/UNCERTAIN)
- Evidence (file path, line numbers, code snippet)
- Validation action if confidence < HIGH
```

---

## P4.4 WPF ViewModel Analysis

```
**Goal**: Extract domain logic from WPF ViewModels

**Scan**:
- *ViewModel.cs files
- ICommand implementations
- Property setters with logic
- IDataErrorInfo / INotifyDataErrorInfo implementations

**Identify**:

1. **Commands → API Operations**:
| Command | CanExecute Logic | Execute Logic | API Endpoint |
|---------|------------------|---------------|--------------|
| SaveCommand | IsValid && !IsBusy | Save to DB | POST /orders |

2. **Validation → FluentValidation**:
| Property | Validation Rule | FluentValidation Equivalent |
|----------|-----------------|----------------------------|
| Email | Regex pattern | RuleFor(x => x.Email).EmailAddress() |

3. **Computed Properties → Domain Logic**:
| Property | Calculation | Move To |
|----------|-------------|---------|
| TotalPrice | Sum(Items.Price) | Order.CalculateTotal() |

**Output**: /docs/domain/wpf-viewmodel-analysis.md
```

---

## P4.5 Console/Worker Service Analysis

```
**Goal**: Extract domain logic from background processes

**Scan**:
- Program.cs / Main() methods
- *Worker.cs / *Service.cs files
- *Job.cs / *Task.cs files
- Scheduled task configurations

**Identify**:

1. **Job Types**:
| Job | Schedule | Input | Output | Domain |
|-----|----------|-------|--------|--------|
| OrderSync | Hourly | DB Query | API Call | Orders |
| ReportGen | Daily | Multiple DBs | Email | Reporting |

2. **Processing Logic**:
- Batch processing patterns
- Retry/error handling
- Idempotency requirements
- Transaction boundaries

3. **Migration Target**:
| Current | Recommended Target |
|---------|-------------------|
| Console + Task Scheduler | Azure Function (Timer) |
| Windows Service | Worker Service (.NET 8) |
| SSIS Package | Azure Data Factory |

**Output**: /docs/domain/background-process-analysis.md
```

---

## P4.6 Stored Procedure Deep Business Rules Extraction

```
**Goal**: Systematically extract ALL business rules from stored procedures

**Why This Is Critical**: Business rules often hide in stored procedures regardless of 
which technology (WebForms, WCF, WPF, Console, VB.NET) calls them. This prompt ensures 
complete extraction.

**What We Extract**:
- **Validation Logic**: Data constraints, required fields, range checks, format validation
- **Calculation Formulas**: Pricing, discounts, totals, taxes, commissions, derived values
- **State-Transition Rules**: Status changes, workflow progression, lifecycle management
- **Conditional Business Logic**: Type-specific behavior, eligibility rules, authorization checks
- **Cross-Entity Rules**: Credit limits, inventory constraints, referential business rules

**Scan All SP Files** (*.sql):

1. **Identify Business Logic Patterns**:

| Pattern | Example | Extraction Target |
|---------|---------|-------------------|
| Validation | IF @amount < 0 RAISERROR... | FluentValidation rule |
| Conditional Insert/Update | IF NOT EXISTS (SELECT...) | Handler pre-check |
| Status Transitions | IF @old_status = 'A' AND @new_status = 'B' | Domain Service |
| Calculations | SET @total = @qty * @price * (1 - @discount) | Entity method or Service |
| Cross-table Rules | IF (SELECT credit FROM Customer) < @amount | Domain Service |
| Date Logic | IF @date < GETDATE() - 30 | Domain Service |
| Conditional Branching | IF @type = 'A' ... ELSE IF @type = 'B' | Strategy pattern |
| Error Handling | IF @@ERROR <> 0 OR @@ROWCOUNT = 0 | Exception handling |
| Audit/Logging | INSERT INTO AuditLog... | Middleware or Service |
| Sequence Generation | SELECT @next = MAX(seq) + 1 | Domain Service |

2. **Per-SP Documentation**:

```markdown
## SP: {sp_name}

### Called By
| Technology | File | Method |
|------------|------|--------|

### Business Rules Found
| Line # | Rule Description | Code Snippet | Confidence | Move To |
|--------|------------------|--------------|------------|---------|

### Parameters Analysis
| Parameter | Usage | Business Rule? |
|-----------|-------|:--------------:|

### Dependencies
- Tables: {list}
- Other SPs: {list}
- Functions: {list}
```

3. **Extraction Mapping**:

| SP Name | Rule | Target Layer | Target File | Method Name |
|---------|------|--------------|-------------|-------------|

**Output**: /docs/data/sp-business-logic-extraction.md

**Constraints**:
- Document EVERY business rule, no matter how small
- Include line numbers for traceability
- Note ALL callers (any technology) — cross-ref with Prompt P4.7
- Flag rules that span multiple SPs (need coordination)

**⚠️ AI GUARDRAIL: Confidence Level Requirements**

Every extracted rule MUST include confidence level:

| Confidence | Criteria | Evidence Required | Action |
|------------|----------|-------------------|--------|
| **HIGH** | Has code comment, unit test, or matches documented requirements | Comment, test path, or doc ref | ✅ Can proceed |
| **MEDIUM** | Clear from code logic but no docs/tests | Code snippet with line numbers | ⚠️ Flag for review |
| **LOW** | Inferred from naming or spread across files | Multiple refs, inference explanation | ❌ Must have human validation |
| **UNCERTAIN** | Cannot determine if business or technical | Code + ambiguity explanation | ❌ Must have human sign-off |

**Required Output Per Rule**:

```markdown
### Rule: [Descriptive Name]

**Confidence**: [HIGH/MEDIUM/LOW/UNCERTAIN]
**Justification**: [Why this confidence level]

**Evidence**:
- File: path/to/file.sql
- Lines: 45–52
- Code:
  ```sql
  IF (SELECT CreditLimit FROM Customer WHERE ID = @CustomerID) < @OrderTotal
  BEGIN
      RAISERROR('Credit limit exceeded', 16, 1)
      RETURN
  END
  ```

**Supporting Evidence** (for HIGH):
- [ ] Code comment found: [quote]
- [ ] Unit test exists: [path]
- [ ] Requirements doc: [reference]

**Validation Required** (for MEDIUM/LOW/UNCERTAIN):
- [ ] Confirm with: [Team/Person]
- [ ] Add test case: [scenario]
- [ ] Document in: [ADR or doc]

**Migration Target**: OrderValidator.ValidateCreditLimit()
```

**Mandatory Cross-Reference Step**:

After extraction, search for existing tests and docs:

| Rule | Test Search Pattern | Found? | Test File |
|------|---------------------|:------:|-----------|

| Rule | Doc Search | Found? | Location |
|------|------------|:------:|----------|

Then update confidence levels based on findings.
```

---

## P4.7 Identify SP Caller Technologies

```
**Goal**: Map which technologies call each stored procedure

**Why This Matters**: A single SP may be called by WebForms, WCF, Console apps, etc.
ALL callers must be updated when migrating business logic out of SPs.

**Scan For SP Calls**:

1. **C# Patterns**:
```csharp
// ADO.NET
SqlCommand cmd = new SqlCommand("usp_CreateOrder", conn);
cmd.CommandType = CommandType.StoredProcedure;

// EF Core
context.Database.ExecuteSqlRaw("EXEC usp_CreateOrder @p0, @p1", ...);

// Dapper
connection.Execute("usp_CreateOrder", new { ... }, commandType: CommandType.StoredProcedure);
```

2. **VB.NET Patterns**:
```vb
Dim cmd As New SqlCommand("usp_CreateOrder", conn)
cmd.CommandType = CommandType.StoredProcedure
```

3. **Config Patterns**:
```xml
<!-- app.config / web.config -->
<add key="CreateOrderSP" value="usp_CreateOrder"/>
```

4. **Other SP Calls (SQL)**:
```sql
EXEC usp_ValidateCustomer @CustomerID
```

**Output**: /docs/data/sp-caller-map.md

**Format**:

| SP Name | C# Callers | VB.NET Callers | SQL Callers | Config Refs | Total |
|---------|------------|----------------|-------------|-------------|-------|
| usp_CreateOrder | OrderService.cs:45, WebForm.aspx.cs:120 | | usp_ProcessBatch:78 | | 3 |

**Migration Impact**:

| SP Name | Callers Count | Migration Complexity | Strategy |
|---------|:-------------:|:--------------------:|----------|
| usp_CreateOrder | 5 | 🔴 High | Create API endpoint, update all callers |
| usp_GetReport | 1 | 🟢 Low | Inline into calling service |
```
