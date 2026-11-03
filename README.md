# Quiz & Exam Platform (Full-stack & QA E2E Automation)

Nền tảng Tạo đề & Luyện thi Trắc nghiệm trực tuyến với cơ chế chấm điểm bảo mật phía Server (Server-side Grading) và bộ kiểm thử tự động End-to-End bằng **Java + Playwright**.

## 1. Kiến trúc & Công nghệ (Tech Stack)

- **Frontend:** React 18, TypeScript, Vite, Tailwind CSS, React Router v6.
- **Backend / Database (Serverless BaaS):** Supabase (PostgreSQL, GoTrue Auth, Row Level Security, PL/pgSQL RPC).
- **E2E Automation Testing:** Java 21, Maven, Playwright for Java (`1.48.0`), JUnit 5.
- **CI/CD:** GitHub Actions (Vercel Preview Deployment + Playwright Headless Runner + Trace Artifact).

## 2. Tính năng chính & Bảo mật

- **Phân quyền 3 vai trò (RBAC với RLS):**
  - **Student:** Xem danh sách đề công khai, làm bài thi có đếm ngược thời gian, nộp bài và xem lịch sử điểm số.
  - **Teacher:** Quản lý ngân hàng câu hỏi, tạo đề thi, xuất bản đề và xem thống kê kết quả của học sinh.
  - **Admin:** Quản lý tài khoản người dùng và phân quyền hệ thống.
- **Chống gian lận (Anti-Cheat Architecture):**
  - Học sinh không có quyền truy cập trực tiếp bảng `questions` chứa đáp án đúng (`correct_option_id`), chỉ được truy vấn qua `public_questions` view.
  - Toàn bộ logic chấm điểm và kiểm tra giới hạn thời gian làm bài được xử lý trong PostgreSQL Stored Procedure (`submit_exam` RPC với `SECURITY DEFINER`).

## 3. Cấu trúc thư mục (Monorepo)

```text
Quiz-Exam-Platform/
├── .github/workflows/       # CI/CD Pipelines & Supabase Keep-Alive Cron
├── supabase/                # SQL Migrations, RLS Policies, RPC & Seed Data
├── frontend/                # React + TypeScript + Vite SPA
├── e2e-tests/               # Java 21 + Playwright + JUnit 5 E2E Test Suite
├── AGENT_SPEC.md            # Tài liệu đặc tả kỹ thuật cho AI Coding Agent
└── README.md
