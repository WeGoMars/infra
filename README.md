# infra

프로젝트 디렉터리 구조 
project-root/
├── docker-compose.yml
├── nginx/
│   └── default.conf
├── nestjs/
│   └── Dockerfile
├── nextjs/
│   └── Dockerfile
├── flask/
│   └── Dockerfile
└── .env



#.yaml 파일 작성

version: '3.8'

services:
  mysql:
    image: mysql:8
    container_name: mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: app_db
      MYSQL_USER: app_user
      MYSQL_PASSWORD: app_pass
    volumes:
      - mysql_data:/var/lib/mysql
    networks:
      - backend

  nestjs:
    build: ./nestjs
    container_name: nestjs
    restart: always
    depends_on:
      - mysql
    networks:
      - backend

  flask:
    build: ./flask
    container_name: flask
    restart: always
    depends_on:
      - mysql
    networks:
      - backend

  nextjs:
    build: ./nextjs
    container_name: nextjs
    restart: always
    networks:
      - backend

  nginx:
    image: nginx:latest
    container_name: nginx
    ports:
      - "80:80"
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf
    depends_on:
      - nestjs
      - flask
      - nextjs
    networks:
      - backend

volumes:
  mysql_data:

networks:
  backend:
    driver: bridge
