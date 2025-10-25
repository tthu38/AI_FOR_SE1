# 🎬 AI_FOR_SE1 — Movie Service Auto Test Generator

Dự án **AI_FOR_SE1** sử dụng trí tuệ nhân tạo để **phân tích và tự động sinh mã kiểm thử JUnit cho lớp MovieService**.  
Đây là đồ án thuộc môn **Software Engineering 1 (SE1)**, được phát triển nhằm minh họa quy trình tự động hóa kiểm thử trong phát triển phần mềm hiện đại.

---

## 🚀 Tổng quan chức năng

Các chức năng được phân tích trong MovieService:

| Function | Mô tả chính | Các trường hợp biên |
|-----------|-------------|--------------------|
| **createMovie(movie)** | Tạo mới một bộ phim | Tiêu đề trống, độ dài > 100 ký tự, duration ≤ 0, id trùng |
| **getMovieById(id)** | Lấy phim theo id | id không hợp lệ, không tồn tại |
| **updateMovie(id, updated)** | Cập nhật thông tin phim | id không hợp lệ, updated rỗng, không tồn tại |
| **deleteMovie(id)** | Xoá phim theo id | id không hợp lệ, không tồn tại |
| **getAllMovies()** | Lấy danh sách tất cả phim | Không có trường hợp biên |

> 📄 Nguồn: *MovieService_Analysis.txt*

---

## 🧪 Ma trận kiểm thử (Test Matrix)

Dưới đây là các nhóm test case được AI sinh tự động:

### 🔹 create(MovieRequest request)
| Category | Test Case | Input | Expected |
|-----------|------------|--------|-----------|
| Happy Path | Create valid movie | MovieRequest(title='Inception') | Movie saved with default poster |
| Edge Case | Missing title | MovieRequest(title='') | throws ValidationException |
| Error Scenario | Invalid request | MovieRequest(title=null) | throws ValidationException |

### 🔹 update(Integer id, MovieRequest request)
| Category | Test Case | Input | Expected |
|-----------|------------|--------|-----------|
| Happy Path | Update valid movie | MovieRequest(title='Inception', posterUrl='new-poster.jpg') | Movie updated with new poster |
| Edge Case | Missing title | MovieRequest(title='', posterUrl='new-poster.jpg') | throws ValidationException |
| Error Scenario | Invalid request | MovieRequest(title=null, posterUrl='new-poster.jpg') | throws ValidationException |

### 🔹 delete(Integer id)
| Category | Test Case | Input | Expected |
|-----------|------------|--------|-----------|
| Happy Path | Delete valid movie | id=1 | Movie deleted |
| Error Scenario | Invalid ID | id=null | throws RuntimeException |
| Error Scenario | Non-existent ID | id=999 | throws RuntimeException |

### 🔹 getById(Integer id)
| Category | Test Case | Input | Expected |
|-----------|------------|--------|-----------|
| Happy Path | Get valid movie | id=1 | MovieResponse with default poster |
| Error Scenario | Invalid ID | id=null | throws EntityNotFoundException |
| Error Scenario | Non-existent ID | id=999 | throws EntityNotFoundException |

### 🔹 getAll(String status)
| Category | Test Case | Input | Expected |
|-----------|------------|--------|-----------|
| Happy Path | Get all movies | status=null | List of MovieResponse |
| Edge Case | Get movies by status | status='Ended' | List of MovieResponse |
| Error Scenario | Invalid status | status=null | List of MovieResponse |

### 🔹 filterMovies(MovieFilterRequest request)
| Category | Test Case | Input | Expected |
|-----------|------------|--------|-----------|
| Happy Path | Filter valid movies | title='Inception' | List of MovieResponse |
| Edge Case | Filter by empty title | title='' | List of MovieResponse |
| Edge Case | Filter by null genre | genre=null | List of MovieResponse |

> 📄 Nguồn: *MovieService_TestMatrix.md*

---

## ⚙️ Công nghệ sử dụng
- **Java 21**
- **JUnit 5**, **Mockito**
- **OpenAI/Groq API** (đã ẩn key trong môi trường `.env`)
- **Maven** hoặc **Gradle**

---

## 💡 Cách chạy nhanh
```bash
javac -cp . prompt/*.java generated/*.java
java prompt.MovieAnalyze
