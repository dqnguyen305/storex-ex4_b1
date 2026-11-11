# --- Giai đoạn 1: Build ứng dụng (Builder stage dùng Eclipse Temurin Java 17) ---
FROM eclipse-temurin:17-jdk AS builder
WORKDIR /app

# Copy các file cấu hình và source code gradle/maven
COPY . .

# Nếu dự án dùng Gradle Wrapper có sẵn trong thư mục demo:
RUN ./gradlew bootJar --no-daemon

# --- Giai đoạn 2: Đóng gói chạy production (Runtime stage) ---
FROM eclipse-temurin:17-jre
WORKDIR /app

# Copy file jar đã build sang container chạy (chỉnh sửa lại đường dẫn theo output của build gradle/maven)
COPY --from=builder /app/build/libs/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]