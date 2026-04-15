# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600328
**Name:** Trương Đức Thái
**Date:** April 15, 2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | "Best choice is Laptop at $1200" | 9/10 | Reasonable recommendation from valid data |
| Garbage Data (`garbage_data.csv`) | "Best choice is Nuclear Reactor at $999999" | 1/10 | Completely incorrect due to poisoned data |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Garbage data gây ra các vấn đề sau:

1. **Duplicate IDs & Data Inconsistency**: Dữ liệu garbage chứa nhiều duplicate IDs và dữ liệu mâu thuẫn, làm agent nhầm lẫn khi so sánh sản phẩm.

2. **Outlier Prices**: Giá "Nuclear Reactor $999999" là outlier cực kỳ lớn, khiến agent nghĩ đó là sản phẩm có giá trị cao nhất. Agent áp dụng logic MAX price mà không kiểm tra tính hợp lý.

3. **Missing & Invalid Data Types**: Các field Category bị missing hoặc NULL values khiến agent không thể xác thực dữ liệu trước khi xử lý.

4. **Logic Giả Định Sai**: Agent chỉ dựa trên dữ liệu input mà không có validation. Nó không biết "Nuclear Reactor" là fake data, nên tin tưởng và trả lời sai.

5. **Tác Động Trực Tiếp**: Garbage data không bị filter (vì generate_garbage.py bypass ETL validation), nên 100% độc hại dữ liệu đầu vào = 100% sai lệch output.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** – **ĐỒNG Ý hoàn toàn**

Dù prompt của agent có tốt cỡ nào, nếu dữ liệu input là rác thì output cũng là rác ("garbage in, garbage out"). 

Thử nghiệm này chứng minh:
- **Clean data (3 records)** → Agent trả lời hợp lý: "Laptop $1200"
- **Garbage data (5 records + fake)** → Agent trả lời vô lý: "Nuclear Reactor $999999"

**Kết luận**: Data quality là nền tảng. Không có dữ liệu tốt, không có AI tốt. ETL Pipeline với validation, error handling rất quan trọng.
