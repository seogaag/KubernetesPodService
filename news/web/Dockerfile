# 단계 1: 빌드 단계
FROM node:18-alpine AS build

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

# 빌드 폴더 확인
# RUN ls -la /app/build

# 단계 2: Nginx를 사용하여 정적 파일 서빙
FROM nginx:alpine

WORKDIR /app

# # Nginx 설정 및 파일 복사
# COPY --from=build /app/build /usr/share/nginx/html
# # RUN rm 
# # COPY nginx.conf /etc/nginx/nginx.conf

# # # 기본 Nginx 설정 파일 제거
# # RUN rm /etc/nginx/conf.d/default.conf

# COPY --from=build /app .
# RUN rm -r /usr/share/nginx/html
# RUN mv build/ /usr/share/nginx/html
# RUN mv nginx.conf /etc/nginx/conf.d
# RUN rm /etc/nginx/conf.d/default.conf

# 빌드된 파일을 Nginx의 디폴트 HTML 디렉토리로 복사
COPY --from=build /app/build /usr/share/nginx/html

# 사용자 정의 Nginx 설정 파일 복사
COPY nginx.conf /etc/nginx/nginx.conf

# 포트 80 노출
EXPOSE 80

# Nginx 실행
CMD ["nginx", "-g", "daemon off;"]
