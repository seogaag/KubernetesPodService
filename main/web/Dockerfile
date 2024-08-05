# 단계 1: 빌드 단계
FROM node:18 AS build

# 작업 디렉토리 설정
WORKDIR /app

# 환경 변수 설정
ENV NODE_OPTIONS=--openssl-legacy-provider

# package.json 파일 복사
COPY package*.json ./

# 종속성 설치
RUN npm install

# 전체 소스 코드 복사
COPY . .

# 애플리케이션 빌드
RUN npm run build
CMD [ "npm", "start" ]

# 빌드 폴더 확인
# RUN ls -la /app/build

# # 단계 2: Nginx를 사용하여 정적 파일 서빙
FROM nginx:alpine

# WORKDIR /app

# Nginx 설정 및 파일 복사
COPY --from=build /app/build /usr/share/nginx/html

# COPY nginx.conf /etc/nginx/nginx.conf/

# 포트 80 노출
EXPOSE 80

# # Nginx 실행/
CMD ["nginx", "-g", "daemon off;"]
