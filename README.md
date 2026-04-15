[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574122&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** thaitd11022004@gmail.com
**Name:** Trương Đức Thái
**Date:** April 15, 2026

---

## Mô tả

Bài lab này giới thiệu **Data Pipeline & Data Observability** - hai khái niệm cốt lõi trong data engineering:

1. **Data Pipeline (ETL)**: Xây dựng quy trình Validate → Transform → Load để xử lý dữ liệu bẩn, loại bỏ invalid records, và lưu clean data.

2. **Data Observability**: Giám sát và phân tích tác động của dữ liệu bẩn (garbage data) lên AI Agent, chứng minh nguyên lý "garbage in, garbage out".

Đã hoàn thành cả **solution.py** (ETL Pipeline) và **agent_simulation.py** (Stress Test), so sánh kết quả Agent với clean data vs garbage data.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas pytest 
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
python generate_garbage.py    # Tạo garbage_data.csv với dữ liệu bẩn
python agent_simulation.py    # Chạy agent với cả 2 bộ data (clean vs garbage)
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Kết quả

### ETL Pipeline (solution.py)
- **Validation summary**: 3 records kept, 2 dropped
- **Errors found**: 
  - ID 3: Price <= 0
  - ID 4: Missing Category
- **Output**: `processed_data.csv` với 3 valid records

### Agent Simulation Results
| Scenario | Agent Response | Status |
|----------|---|---|
| **Clean Data** | "Best choice is Laptop at $1200" | ✅ Chính xác |
| **Garbage Data** | "Best choice is Nuclear Reactor at $999999" | ❌ Sai do dữ liệu bẩn |

**Nhận xét**: Agent có trả lời hợp lý khi dữ liệu clean, nhưng bị đánh lừa hoàn toàn bởi dữ liệu bẩn → **Data Quality > Prompt Quality**
