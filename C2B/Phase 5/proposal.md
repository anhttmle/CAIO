# 1. Dự án phát triển from scratch
```mermaid

flowchart LR
    A[(Cobol Repo)] --> B["Restructure AI<br/>(Specs Gen)"]
    B --> C[(Cobol Specs)]
    C --> D["Restructure AI<br/>(Specs Migration)"]
    D --> E[(Java Specs)]
    E --> F[Backlog]

    E --> tester["Tester"]

    tester --> G[("Java<br/>Test case")]
    G --> H[Code deploy]
    H --> I[Test result]
    I --> F

    F --> J["Dev Team<br/>or<br/>Coding Agent"]
    J --> K[("Java Repo)")]
    K --> H

    %% Optional visual alignment helpers
    classDef db fill:#f8f8f8,stroke:#999,stroke-width:1px;
    class A,C,E,G,K db;

```

### Luồng chính (Cobol → Java)
- **Cobol Repo** → **Restructure AI (Specs Gen)**: Source code Cobol ban đầu được đưa vào AI để tạo đặc tả (Specs Gen).
- **Restructure AI (Specs Gen)** → **Cobol Specs**: AI sinh ra tài liệu đặc tả từ code Cobol.
- **Cobol Specs** → **Restructure AI (Specs Migration)**: AI tiếp tục chuyển đổi đặc tả Cobol sang đặc tả Java (Specs Migration).
- **Restructure AI (Specs Migration)** → **Java Specs**: Kết quả là bộ đặc tả cho hệ thống Java.
- **Java Specs** → **Backlog**: Các Java specs được đưa vào backlog để thực thi.

### Nhánh kiểm thử
- **Java Specs** → **Tester**: Tester sử dụng Java specs để viết test.
- **Tester** → **Java Test case**: Sinh ra các test case cho Java.
- **Java Test case** → **Code deploy**: Test case được deploy cùng code.
- **Code deploy** → **Test result**: Chạy test và thu kết quả.
- **Test result** → **Backlog**: Kết quả test (fail/pass, bug) quay lại backlog để xử lý tiếp.

### Nhánh phát triển
- **Backlog** → **Dev Team / Coding Agent**: Backlog được xử lý bởi dev hoặc AI coding agent.
- **Dev Team / Coding Agent** → **Java Repo**: Code Java được implement và commit vào repo.
- **Java Repo** → **Code deploy**: Code mới được deploy để chạy test.

# 2. Dự án đang migration

```mermaid

flowchart LR
  Dev[/"Dev Team<br/>or<br/>Coding Agent"/]

  %% Cobol path (top)
  CobolRepo[(Cobol Repo)]
  RespecGen1["Restructure AI<br/>(Specs Gen)"]
  CobolSpecs[(Cobol Specs)]
  RespecDiffTop["Restructure AI<br/>(Specs Diff)"]
  Backlog[/"Backlog"/]

  CobolRepo -->|generate| RespecGen1
  RespecGen1 -->|reviewer| CobolSpecs
  CobolSpecs --> RespecDiffTop
  RespecDiffTop --> Backlog
  CobolSpecs -. reviewer .-> Backlog

  %% Java path (middle)
  JavaRepo_old[("Java Repo<br/>1.0.0")]
  RespecGen2["Restructure AI<br/>(Specs Gen)"]
  JavaSpecs_old[("Java Specs<br/>1.0.0")]
  RespecDiffMid["Restructure AI<br/>(Specs Diff)"]
  JavaSpecs_new[("Java Specs<br/>1.1.0")]

  Dev --> JavaRepo_old
  JavaRepo_old -->|generate| RespecGen2
  RespecGen2 -->|reviewer| JavaSpecs_old
  JavaSpecs_old --> RespecDiffMid
  RespecDiffMid --> JavaSpecs_new
  RespecDiffMid -. reviewer .-> JavaSpecs_new

  %% Source diff path (bottom)
  JavaRepo_new[("Java Repo<br/>1.1.0")]
  SourceDiff[/"Source Diff"/]
  SrcRespecDiff["Restructure AI<br/>(Specs Diff)"]

  Dev --> JavaRepo_new
  JavaRepo_old -->|source code| SourceDiff
  JavaRepo_new -->|source code| SourceDiff
  SourceDiff --> SrcRespecDiff
  SrcRespecDiff --> JavaSpecs_new
  SrcRespecDiff -. reviewer .-> JavaSpecs_new

  %% Connections to backlog and reviewers
  JavaSpecs_old --> RespecDiffTop
  RespecDiffTop -->|reviewer| Backlog
  JavaSpecs_new --> RespecDiffTop

  Backlog --> Dev

  %% visual classes
  classDef repo fill:#f8f8f8,stroke:#999,stroke-width:1px;
  classDef ai fill:#fff2cc,stroke:#c79a00,stroke-width:1px;
  classDef specs fill:#e6d0f5,stroke:#8c5ca3,stroke-width:1px;
  classDef actor fill:#ffffff,stroke:#222,stroke-width:1px;

  class CobolRepo,JavaRepo_old,JavaRepo_new repo;
  class RespecGen1,RespecGen2,RespecDiffTop,RespecDiffMid,SrcRespecDiff ai;
  class CobolSpecs,JavaSpecs_old,JavaSpecs_new specs;

```
