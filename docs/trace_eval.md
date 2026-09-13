# 📊 BÁO CÁO THU HOẠCH NGHIỆM THU BÀI LAB 3 (BƯỚC 3 — SUBMISSION ARTIFACT)

> **Họ và Tên Học viên:** Ngô Minh Thu  
> **Mã Sinh Viên / Mã Học viên:** 2A202602679 
> **Chủ đề Lựa chọn:** *Trợ lý Học vụ & Tra cứu Lịch thi VinUni:* Tra cứu điểm GPA, lịch thi và đặt lịch tư vấn học vụ với Cố vấn.

---

## 1. BẢNG CHẤM ĐIỂM AGENTIC FIT SCORING MATRIX (ĐÁNH GIÁ CHỦ ĐỀ)

| Tiêu chí Đánh giá | Mức độ (1 - 5) | Giải trình chi tiết lý do chọn điểm |
| :--- | :---: | :--- |
| **1. Multi-step Reasoning** | 3/ 5 | Khi sinh viên yêu cầu đặt lịch tư vấn thì cần phải xác định lịch học và làm việc của cả sinh viên và cố vấn để xếp và đự lịch phù hợp. |
| **2. Tool Interaction** | 5/ 5 | Hệ thống cần kết nối với cơ sở dữ liệu điểm và lịch của sinh viên và cố cấn, cần sử dụng function calling hoặc MCP Server để lựa chọn và gọi đúng công cụ theo yêu cầu của sinh viên. |
| **3. Dynamic Decision** | 4/ 5 | Hệ thống cần kiểm tra lịch của cố vấn có cùng với lịch sinh viên mong muốn, nếu không khải tìm thời gian khác không trùng với lịch học tập của sinh viên. |
| **4. Long Horizon Goal** | 4/ 5 | Hệ thống cần duy trì mục tiêu đặt lịch tư vấn học vụ trong suốt quá trình xử lý,xác nhận, kiểm tra lịch tùng, lịch phù hợp, mong muốn của sinh viên để đảm bảo rằng sinh viên nhận được gợi ý phù hợp về lịch học. |
| **TỔNG ĐIỂM AGENTIC FIT** | 16/ 20** | *Nếu tổng điểm > 12/20: Bài toán rất phù hợp triển khai Agentic System.* |

---

## 2. TRÍCH XUẤT KẾT QUẢ WATERFALL TRACE LOG (SAU KHI CHẠY TEST SUITE TRÊN API THẬT)

> ⚠️ **YÊU CẦU NGHIỆM THU:** Mở tệp `.env` điền `GEMINI_API_KEY` (hoặc `OPENAI_API_KEY`) để kết nối LLM thật trước khi thực thi `python src/app.py --all`. Bài nộp chỉ dùng Mock Offline Provider sẽ không đạt điểm nghiệm thực tế.

Dán 1 đoạn trích xuất log tiêu biểu từ file `docs/trace_waterfall.json` sinh ra từ phản hồi LLM API thật:

```json
[
  {
    "step": 1,
    "query": "Hãy tra cứu thông tin học vụ của sinh viên SV2026001, sau đó đặt lịch hẹn với cố vấn học tập được ghi trong hồ sơ vào 14:00 ngày 15/09/2026.",
    "action_type": "TOOL_EXECUTION",
    "thought": "Gemini quyết định gọi công cụ 'academic_query' với tham số: {\"student_id\": \"SV2026001\"}",
    "tool_name": "academic_query",
    "arguments": {
      "student_id": "SV2026001"
    },
    "observation": {
      "status": "SUCCESS",
      "student_id": "SV2026001",
      "data": {
        "full_name": "Nguyễn Văn An",
        "class": "AI-K4",
        "gpa": 3.85,
        "email": "an.nv@vinuni.edu.vn",
        "status": "Đang học",
        "advisor": "PGS.TS Nguyễn Văn A"
      }
    },
    "latency_ms": 3215.61
  },
  {
    "step": 2,
    "query": "Hãy tra cứu thông tin học vụ của sinh viên SV2026001, sau đó đặt lịch hẹn với cố vấn học tập được ghi trong hồ sơ vào 14:00 ngày 15/09/2026.",
    "action_type": "TOOL_EXECUTION",
    "thought": "Gemini quyết định gọi công cụ 'schedule_appointment' với tham số: {\"student_id\": \"SV2026001\", \"advisor_name\": \"PGS.TS Nguyễn Văn A\", \"datetime_str\": \"14:00 15/09/2026\"}",
    "tool_name": "schedule_appointment",
    "arguments": {
      "student_id": "SV2026001",
      "advisor_name": "PGS.TS Nguyễn Văn A",
      "datetime_str": "14:00 15/09/2026"
    },
    "observation": {
      "status": "SUCCESS",
      "booking_id": "BK-SV2026001-99",
      "student_id": "SV2026001",
      "datetime": "14:00 15/09/2026",
      "advisor": "PGS.TS Nguyễn Văn A",
      "message": "Đặt lịch thành công cho sinh viên SV2026001 với PGS.TS Nguyễn Văn A vào lúc 14:00 15/09/2026."
    },
    "latency_ms": 2872.41
  },
  {
    "step": 3,
    "query": "Hãy tra cứu thông tin học vụ của sinh viên SV2026001, sau đó đặt lịch hẹn với cố vấn học tập được ghi trong hồ sơ vào 14:00 ngày 15/09/2026.",
    "action_type": "FINAL_ANSWER",
    "thought": "Gemini phản hồi trực tiếp bằng văn bản (không cần gọi công cụ).",
    "output": "Thông tin học vụ của sinh viên SV2026001:\n*   **Họ và tên:** Nguyễn Văn An\n*   **Lớp:** AI-K4\n*   **GPA:** 3.85\n*   **Email:** an.nv@vinuni.edu.vn\n*   **Trạng thái:** Đang học\n*   **Cố vấn học tập:** PGS.TS Nguyễn Văn A\n\nLịch hẹn tư vấn với PGS.TS Nguyễn Văn A vào lúc 14:00 ngày 15/09/2026 đã được đặt thành công. Mã đặt lịch của bạn là BK-SV2026001-99.",
    "latency_ms": 6336.11
  }
]
```

---

## 3. TỔNG KẾT KẾT QUẢ NGHIỆM THU & NỘP BÀI

- [x] Đã điền API Key thật trong `.env` và xác nhận Agent chạy mượt mà trên LLM API thật (Gemini/OpenAI).
- **Tổng số Test Cases đã chạy thành công:** 5 / 5 test cases.
- **Số lượt gọi Tool qua MCP Server chính xác:** 2 lượt.
- **Kết quả đẩy Repo nộp bài:** [x] Đã Commit và Push mã nguồn thành công lên GitHub cá nhân.

---

