# Reflection — Lab 19

**Tên:** Trần Anh Tú
**Mã học viên:** 2A202600291
**Cohort:** Track 2
**Path đã chạy:** docker

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trên golden set 50 queries:
- **`exact`** (15 queries): BM25 = Hybrid = 96.7%. BM25 đã đủ mạnh khi query dùng đúng từ kỹ thuật có trong corpus. Hybrid không thua nhưng cũng không thêm giá trị.
- **`paraphrase`** (15 queries): Cả 3 mode đều thấp (~24–33%) do model `bge-small-en` được train tiếng Anh, kém trên tiếng Việt thuần. Hybrid = 32% thắng nhẹ so với BM25 = 33% (xấp xỉ bằng nhau).
- **`mixed`** (20 queries): Hybrid thắng rõ 100% vs Semantic 98.5% vs Keyword 97.0%.

**Khi KHÔNG nên dùng Hybrid:**
1. **Corpus nhỏ, query luôn exact-match**: BM25 đủ, thêm vector chỉ tăng độ trễ.
2. **Latency-critical (<1ms)**: Hybrid cần chạy 2 retriever + RRF fusion, đắt hơn pure BM25 3–10×.
3. **Corpus thuần kỹ thuật với từ khóa chuẩn**: Ví dụ code search bằng function/class name, BM25 chính xác hơn.

---

## Điều ngạc nhiên nhất khi làm lab này

Python 3.14 trên Windows thiếu MSVC Redistributable khiến cả `onnxruntime` và `torch` đều lỗi DLL — phải cài MSVC VC++ Redistributable trước khi bất kỳ ML library nào chạy được. Sau khi cài, mọi thứ hoạt động ngay.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
