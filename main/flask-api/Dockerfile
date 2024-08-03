# 베이스 이미지로 Python 사용
FROM python:3.11-slim

# 작업 디렉토리 설정
WORKDIR /app

# 종속성 파일 복사
COPY requirements.txt ./

# 종속성 설치
RUN pip install --no-cache-dir -r requirements.txt

# 애플리케이션 코드 복사
COPY . .

# 포트 5000 노출
EXPOSE 5000

# Flask 애플리케이션 실행
CMD ["flask", "run", "--host=0.0.0.0", "--port=5000"]
