# 使用node.js來建置
FROM node:18 AS bulid

WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install

COPY . ./
RUN npm run build

# 2. 使用 Nginx 來提供靜態檔案
FROM nginx:alpine

# 設定 Nginx 伺服器的靜態檔案路徑
COPY --from=build /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]


#先用 node:18 安裝 npm 套件並建置 Vue
#再用 nginx:alpine 部署靜態檔案，減少容器體積
